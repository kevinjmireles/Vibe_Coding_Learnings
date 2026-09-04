# Re-Check the Number You Already Wrote Down

> **A correctly quantified requirement, stated once at the start of an initiative, decays across every PR that follows unless something forces it back into view. The fix is not asking better questions on day one — we already did that. It's making the founding number impossible to lose.**

We got something right, then lost it, and didn't notice for roughly fifteen pull requests.

## The evidence

Issue #473, opened in July, proposed replacing synchronous email delivery with a durable queue. It stated a clean, quantified, non-self-serving trigger for why:

> "The transition should happen before normal sends exceed roughly **100 recipients or routinely take more than 10–15 seconds**."

That is exactly the kind of number a good requirement should have. It wasn't invented to justify a predetermined design — it described an actual usability threshold. Nothing about this issue was the failure.

The first implementation PR (#833) built the executor: a bounded batch of 25 recipients, claimed once per scheduler invocation. Its own "Known limitations" section said, in writing:

> "Scheduler cadence is daily due to the Vercel Hobby plan; **sub-daily cron is a real requirement to revisit before/at authored cutover.**"

That's a correct, honest, carried-forward flag. It was in the very first PR of the campaign.

Nine PRs later, issue #845 designed the activation plan and wrote an explicit service-level target:

> "100 recipients should normally drain within roughly **30 minutes** at default claim size and 5-minute cadence."

Thirty minutes. Not the 10–15 seconds the entire initiative existed to guarantee. **Somewhere between 120 and 180 times slower than the founding requirement** — and that's the *best case*, assuming the 5-minute cadence in that plan was actually running, which it wasn't; production stayed on the daily cadence #833 flagged, making the real number closer to a full day.

Nobody computed that ratio. Not in #833, which correctly named the gap. Not in #845, which built a detailed rollout plan on top of it. Not in any of the PRs between them. The number every one of those PRs needed to check against was sitting in the founding issue the entire time.

## Failure pattern: the requirement was correct, and got orphaned anyway

This is a different failure than "the problem was never sized" (see [Do the Math Before You Build](024-do-the-math-before-you-build.md), which covers not sizing the problem at all). Here, the problem *was* sized, correctly, in writing, before anything was built. The failure is structural: nothing in the process carries a founding number forward from the issue that stated it into the ten-plus PRs that had to satisfy it.

Each PR was reviewed against its own acceptance criteria. Each PR passed. Nobody's job, on any single PR, was to re-open the original issue and check the arithmetic — so nobody did, even though one PR *explicitly flagged that this exact check was owed* and still didn't run it.

This is worse than a one-time oversight. It shows that flagging a gap in prose is not the same as making it checkable. "A real requirement to revisit" is a sentence a person can read, nod at, and carry forward as a vague intention. It is not a number anyone can compare against, so it never got compared.

## Why density made this easy to miss

Every one of those PRs was thorough. Multi-thousand-word bodies, acceptance criteria, test plans, documentation checklists, self-grades. That thoroughness is real and it is also exactly what let the drift hide.

- **Review happens per-PR, not per-campaign.** A reviewer (human or AI) evaluates whether *this* PR does what *this* PR claims. Nobody's frame includes "does this still serve the issue that started the whole thing," because that issue is three weeks and nine PRs in the past.
- **A "known limitation" is prose, and prose doesn't demand action.** #833 discharged its obligation to be honest the moment it wrote the sentence. Nothing forced that sentence to resurface as a question at the next relevant decision point.
- **Volume reads as diligence.** A PR with a documentation checklist, a risk review, and a self-grade looks like a PR that has been thought through. Whether it was checked against the *original number* is a completely different question that polish does not answer.
- **AI produces this volume at zero marginal cost**, so it no longer signals that anyone spent the time. The approver — the one person positioned to ask "wait, does this still make sense against what we set out to do" — has the least ability to hold fifteen PRs of context in their head, and the most reason to trust that the process already checked it.

## The fix: make the founding number travel with the work, not the memory of it

Two changes, added to the existing problem-validation gate (§1.1) rather than as a new layer — this content already lives there, in "show the arithmetic"; what was missing is presentation and a trigger to *re-run it*.

### 1. Present it so a decision is possible in seconds, not minutes

Every issue or PR opens with, in this order:

- **One sentence: what is this.**
- **The founding number**, if one exists (from the issue that started the initiative), or a note that none exists yet.
- **The comparison**, as one literal line, same units as the founding number:

  ```
  today: <X>/<unit> → after: <Y>/<unit>  (confidence: measured | estimated | unknown)
  ```

  If `Y` is worse than `X`, that is not a detail — it is the finding, and it belongs on line one, not in a "known limitations" section three thousand words later.
- **The cost** — PRs, money, new operational surface.
- **The ask**, in one of exactly three forms: **approve** / **clarify: <question>** / **not now**.

Business units throughout — recipients, minutes, dollars — never batch size or lease seconds above the fold. Full technical detail stays available below a divider, for the builder and reviewer; the approver never has to read it to decide.

### 2. Force the re-check when a campaign grows

The single most useful thing in this repository's existing gate is not a question — it's a set of conditions that require no judgment to evaluate: does this touch send/signup/ingest, does it add an always-on component, is it irreversible, does it exceed one PR. Any one of those is enough to escalate to full scrutiny.

The one that failed here is "more than one PR" — because nobody declares a fifteen-PR campaign on PR one. So it becomes a standing obligation instead of a one-time check:

> **Any PR beyond the first in a multi-PR initiative must restate the today → after line against the founding issue's own number before it can be approved.**

That line, run at PR #845 using #473's actual number, reads:

```
today (target, per #473): 100 recipients in ≤15s
after (this plan):        100 recipients in ~30min  (confidence: estimated)
```

That comparison is disqualifying on sight. It requires no new judgment — the founding number and the proposed number are both already written down; this only requires putting them in the same place.

### 3. Confidence tags, and a consequence for the honest ones

Three levels — **measured**, **estimated**, **unknown** — not more; a fourth (*guess* vs *estimated*) asks for a distinction nobody applies consistently.

The tag is not decoration: on any escalated work, `unknown` or a stale `estimated` on the today→after line blocks sign-off until it is measured or explicitly accepted in writing. Otherwise the tag is a confession that changes nothing, precisely at the moment it matters most.

### 4. Replace silent approval with a forced choice

The only valid responses to escalated work are **approve**, **clarify: <question>**, or **not now**. Not a checkbox, not silence read as agreement. Choosing from three options is not an admission that you couldn't follow the detail — it is simply how you respond, every time, so the moment of decision is always visible and never accidental.

## Even this lesson almost repeated the pattern

While drafting the first version of this material, an earlier proposal quietly turned §1.1's existing, unconditional rule — *"if the proposal is slower or smaller than what it replaces, the design is wrong"* — into something an author could opt out of by not checking a box labeled "performance." An independent review caught it before anything was committed. The same failure this lesson describes — a load-bearing requirement demoted to something easy to skip — nearly happened again, one draft later, while writing the fix for it. That is the strongest available argument for why this has to be structural rather than a matter of remembering to be careful.

## Reusable takeaway

> **Stating the requirement correctly once is necessary and not sufficient. Build the thing that makes it impossible to lose across every PR that follows — not a better question, a number that travels with the work and a trigger that forces it back into view.**

Three mechanisms, in order of leverage:

1. **The founding number goes in the brief of every subsequent PR**, in the same units, not just the founding issue.
2. **Growth past one PR obligates a re-check** against that number — not a new judgment call, just a comparison of two numbers already on record.
3. **The approver chooses from three options, every time** — approve, clarify, or not now — so a decision is always a decision, never a default.
