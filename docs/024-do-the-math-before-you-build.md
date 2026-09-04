# Do the Math Before You Build

> **A rigorous plan for an unvalidated problem is still waste. Before building, size the problem — probability and impact — and prove with arithmetic that the proposed solution's real capacity intersects the real need. A correctly sized problem is not then done: without something structural forcing the founding number to travel forward, it can be built past within a single day of fast, careful, well-reviewed iteration.**

We spent a significant amount of effort building a durable, crash-safe, lease-fenced, retry-capable email delivery queue.

It worked. It was well-tested. It had migrations, real-PostgreSQL concurrency tests, an operator runbook, a fail-closed kill switch, an activation cutoff guard, and a carefully sequenced rollout plan with six phases and roughly twenty acceptance criteria.

Then someone asked a simple question:

> How long would this take to send 100,000 emails?

**Fourteen days.**

Nobody had done that arithmetic. Not in the issue. Not in any of the pull requests. Not in the review.

## Failure pattern: solving an unvalidated problem, unusably

Two distinct failures stacked on top of each other. Either one alone is expensive. Together they produce work that cannot be salvaged by tuning.

### Failure 1: the problem was never sized

The system was built to solve "a large send could fail partway through and leave inconsistent state."

That is a real failure mode. But nobody asked how *probable* it was, or how *impactful*, at the scale the product actually operates at. Had we asked, the answer was already written down in our own repository:

> "the platform's current single-Supabase-project, single-send-worker, synchronous `/api/send/execute` design is explicitly designed to handle this comfortably"

And more specifically, the roadmap had already classified this exact capability:

> **N-parallel-worker send execution (replacing single synchronous `/api/send/execute` run)** — Category: **Watch**. Trigger: ceilings "actually hit by real cohort sizes such that a single run can't complete in an acceptable window. **Not yet observed.**"

The guardrail existed. It was specific, it named this exact work, it set an explicit trigger, and it recorded that the trigger had not fired.

Nobody opened the file.

That is a different and more painful failure than not knowing. The analysis had already been done by our own past selves, and the work proceeded anyway because no step in the process forced anyone to go look.

### Failure 2: the solution's capacity never intersected the need

The delivery queue processed **one job per scheduler tick, 25 recipients per tick, on a 5-minute cadence.**

That is the arithmetic nobody ran:

| | Throughput |
|---|---|
| New durable queue | 25 per 5 min = **5/min** = 7,200/day |
| Existing synchronous path it replaced | 10 concurrent provider calls ≈ **1,200–3,000/min** |

The replacement was **roughly 250–600× slower than the code it was meant to supersede.**

At that rate, 20,000 recipients takes about three days and 100,000 takes about two weeks. Meanwhile the "primitive" synchronous path it was displacing would have done 10,000 in a handful of minutes.

So the new system was simultaneously:

- **unnecessary** at the volumes the product actually sends (where the old path finishes in seconds), and
- **unusable** at the volumes that would have justified building it.

There was no volume at which it was the right tool. It was a sledgehammer that was also too small to kill the fly.

## Why this happens with AI

The plan *looked* rigorous. That was the trap.

It had phases, acceptance criteria, rollback sequences, evidence requirements, explicit non-goals, and a STOP/REVIEW gate. Every individual element was thoughtful. A reviewer skimming it would come away impressed.

But **rigor about execution is not the same as validation of purpose.** A document can be meticulous about *how* to build the wrong thing.

AI makes this failure much easier to reach:

- Ask an agent to plan a durable queue and it will produce an excellent durable queue plan. It will not spontaneously ask whether you need a queue.
- Agents are strongly biased toward the framing in the prompt. "Make the send pipeline durable" is accepted as a premise, not examined as a hypothesis.
- The cost of *producing* elaborate plans has collapsed, so plan length no longer signals that anyone thought hard about necessity. It used to take a week to write a six-phase rollout plan, and that week was itself a forcing function.
- Nobody's arithmetic gets checked, because the plan contains numbers (batch size 25, lease 120s, retry ×5) that *look* like quantitative reasoning. Parameters are not projections.

The specific tell, in hindsight: the plan contained an SLA table for 25, 100, 250, and 500 recipients. Those numbers were never reconciled against what the business actually needed to send. The table made the plan feel quantified while quietly defining the problem down to whatever the chosen design happened to handle.

## The workarounds nobody priced

Before building a queue, the cheap options should have been costed and rejected explicitly. None of them were considered:

1. **Change two environment variables.** The sync path's recipient cap and parallelism were already configurable. Raising them was a config change with zero code.
2. **Use the provider's batching.** The email provider accepts up to 1,000 recipients in a single API call. The entire architecture was built on the unexamined premise of one email per API call per row — a premise that, once questioned, removes most of the pressure that justified the queue.
3. **Re-run the failed send.** The system *already* deduplicated on a sent-only identity key. A partially-completed send could simply be run again; already-sent recipients would be skipped automatically. The core disaster scenario the queue was built to prevent already had a safe, zero-code answer.

Option 3 is the one that stings. The cheapest mitigation was already built, already tested, and already documented — and the durable queue's own design documents referenced it as an invariant to preserve, without anyone noticing it made the queue largely unnecessary at current scale.

## The other shape of this: mechanism disproportionate to frequency

The same failure appears without any throughput math, whenever a mechanism's complexity is wildly out of proportion to how often the thing it watches actually changes.

We reviewed a plan with elaborate change-detection logic for county boundaries.

County boundaries do change — Connecticut's county-equivalents were reorganized recently, and Alaska occasionally redraws census areas. So the correct answer is not "never check." But the *frequency* is roughly annual at the very most, driven by scheduled Census releases, not continuous drift.

Continuous detection machinery for an annual, pre-announced, externally-scheduled event is the wrong mechanism. Checking at data-ingest time, or once a year against the published release, gets essentially all of the value for essentially none of the complexity.

> **Match the mechanism's cadence to the phenomenon's cadence. Continuous monitoring of a phenomenon that changes annually is not thoroughness — it's cost with no marginal detection benefit.**

## A correctly sized problem can still decay within a single day of rapid iteration

Failure 1 and Failure 2 above describe a problem that was never sized. This is a different, more unsettling case: the problem *was* sized correctly, on day one, in writing — and still got lost, not over months, but within a single day of continuous, careful, well-reviewed work.

Issue #473, opened in late July, proposed replacing synchronous email delivery with a durable queue. It stated a clean, quantified, non-self-serving trigger:

> "The transition should happen before normal sends exceed roughly 100 recipients or routinely take more than 10–15 seconds."

That's a legitimate usability threshold, not a number invented to justify a predetermined design. Nothing about this issue was the failure. Its stated goal was explicit that the whole point of the redesign was decoupling the HTTP response from total delivery time — it never promised the new system would also finish in 10–15 seconds. So the founding number wasn't a completion-time SLA for the new system; it was the reason synchronous delivery had to go. Worth being precise about that distinction, since getting it wrong is exactly the kind of imprecision this lesson exists to catch.

What #473 also never did — and this is the actual gap — was set *any* completion-time target for the system that replaced it. That's Failure 1 and Failure 2 again, in miniature: no target means no way to check the design against it.

Five weeks later, on September 1st, implementation began. PR #833 (03:13–07:12 that morning) built the executor: 25 recipients claimed per scheduler tick. Its own "Known limitations" section said, correctly and in writing:

> "Scheduler cadence is daily due to the Vercel Hobby plan; sub-daily cron is a real requirement to revisit before/at authored cutover."

Over the following day, four more real decisions were made on exactly this question — scheduler cadence — recorded across five comments on issue #845: a decision to use a free external cron-ping service instead of paying for Vercel Pro; an independent review that found five findings against that plan (three blockers — secret storage, rotation, a liveness check that doesn't actually prove the scheduler fired — plus two smaller corrections); an owner decision reversing course to Vercel Pro instead, reasoning explicitly about future traffic growth; and a final reversal back to the daily Hobby-plan cadence to keep the app deployable, deferring the Pro/5-minute switch to "a tiny follow-up PR."

This was not neglect. Four real decisions, in about a day, each substantive. What none of them did — what nothing in the process made anyone do — was reopen #473 and ask: even at the best cadence being discussed, does 25 recipients per 5 minutes (≈30 minutes to drain 100 recipients) actually solve the problem #473 described, for a system meant to replace one that used to handle 100 recipients synchronously in 10–15 seconds? The founding number was never in the room for any of those conversations, despite everyone in the room caring, correctly, about exactly the topic that number would have settled.

### Why rapid, engaged iteration is not protection against this

The instinct is to assume this kind of drift needs time and neglect — weeks passing, people forgetting, priorities shifting elsewhere. This evidence says otherwise. This is [lesson 023](023-process-as-product.md)'s claim made concrete: *AI changes the velocity of technical debt, not its economics.* A founding requirement can now be built past, reviewed repeatedly, and left behind, inside about a day of attentive work — because velocity increased, but nothing about *what travels forward between iterations* changed to match it.

Each of those exchanges was reviewed on its own terms and passed. None was ever asked to reopen the issue that started the whole effort and do one line of arithmetic against it. That is not a diligence problem. It is a structural one: nothing in the process carries a founding number from the issue that stated it into the artifacts that have to satisfy it, no matter how fast or how careful the intervening work is.

### Making the founding number travel with the work

**Every issue or PR states its founding number up front**, before any other content, as one literal comparison line in the same units as that number:

```
today: <X>/<unit> → after: <Y>/<unit>  (confidence: measured | estimated | unknown)
```

Business units — recipients, minutes, dollars — never internal parameters, above this line. If `after` is worse than `today` or than the founding number, that's the finding, and it belongs here, not three thousand words into a "known limitations" section.

**The founding number must be the earliest one, not the most recent one.** #845 introduced its own "initial target SLA" as though setting a fresh baseline, rather than being forced to reconcile against #473's actual number. Citing "no founding number exists" or silently starting a new one when an earlier requirement for the same capability already exists is not acceptable — say "earliest found: none located" if that's true, but don't let a later document quietly become the new ground zero.

**Growth past one PR is a standing obligation to re-run the comparison, not a one-time check.** Nobody declares a fifteen-PR campaign, or a five-round evening, on the first exchange. So: any work beyond the first PR in a multi-part initiative must restate the today → after line against the *founding* issue's own number before it can be approved — every time, not once. Run against this exact case:

```
today (target, per #473): 100 recipients in ≤15s
after (best cadence discussed): 100 recipients in ~30min  (confidence: estimated)
```

Disqualifying on sight, and it requires no new judgment — both numbers were already written down; this only requires putting them next to each other.

**Confidence tags — three, not more — with a real consequence.** `measured` / `estimated` / `unknown`. On any work escalated past routine, `unknown` or a stale `estimated` on the today→after line blocks sign-off until it's measured or explicitly accepted in writing. A tag that changes nothing when it says `unknown` is decoration.

**The only valid response to escalated work is one of three:** `approve` / `clarify: <question>` / `not now`. Not silence, not a default. Choosing from three options isn't an admission that the detail was too much to follow — it's simply how a decision gets made, every time, so it's never accidental.

A near-miss while writing this section is itself worth recording: an early draft demoted the "show the arithmetic" rule below into something an author could skip by not labeling their own work "performance-related." That's the same shape of failure as the durable queue itself, one level removed — a load-bearing check made quietly optional by how the work gets framed. It was caught before anything was committed, by a review built specifically not to trust the draft's own framing. That's the argument for why this has to be structural: even a document about the failure, written immediately after diagnosing it, tried to make the same move.

## The process introduced: a Problem Validation Gate

The existing [Problem gate](../rules/quality-gates.md) asked whether the problem was *stated clearly*. That is necessary and insufficient. A clearly stated problem can still be rare, harmless, already mitigated, or unsolved by the proposed design.

Before any initiative larger than a bug fix, answer these — **in writing, in the issue, with numbers**:

### 1. What actually breaks, and has it broken?

Has this failed in production? How many times? Link the incident, log, or user report.

If the honest answer is "it hasn't happened yet," say so explicitly. That is not disqualifying — but it must be *stated*, because it changes everything downstream.

### 2. Probability × impact

How often would this occur at current scale, and what is the blast radius when it does?

A daily occurrence that annoys one admin and an annual occurrence that corrupts customer data warrant completely different investments. Write down both numbers, even as rough estimates.

### 3. Show the arithmetic

Not parameters. **Projections.**

- What throughput/latency/volume does the current system achieve?
- What will the proposed system achieve, computed from its actual parameters?
- What does the business actually need?

All three numbers, in the same units, in the same table. If the new system's number is worse than the current system's, the design is wrong regardless of how elegant it is.

This one question would have caught our failure in about ninety seconds.

**"Required capacity" means the design target, not today's volume.** This is the distinction that makes the difference between prudent preparation and waste.

Building ahead of current need is often correct. A product that intends to go from 100 subscribers to 100,000 should not architect for 100 — discovering at launch that the delivery path needs a rewrite is exactly the expensive outcome this gate exists to prevent.

But "prepare for scale" only works if the target is written down as a number and the design is checked against *it*. Our failure was not preparing for scale. It was building a specific implementation whose throughput nobody ever compared to the scale target — a target that, we later realized, had never been stated anywhere at all.

Had the issue said "must reach 100,000 recipients without a rewrite," the chosen design (25 recipients per 5-minute tick) would have been rejected immediately, and the actual bottleneck — one provider API call per recipient, when the provider accepts 1,000 per call — would have been obvious on day one.

> **An unstated scale target is the root cause hiding behind most over- and under-engineering. Write the number down, then check the design against the number.**

Note also what this reveals about *which* work was wasted. The durable persistence layer — job and recipient state, lease fencing, retry tracking, dedupe — was the right foundation, because at the target scale a send genuinely cannot complete inside one request. The defect was isolated to the dispatch layer. Sizing the problem correctly does not always mean building less; sometimes it means building the same substrate with completely different parameters.

### 4. What did the roadmap already say?

Check the existing architecture and roadmap documents for this exact capability *before* planning it. If a prior decision classified it as deferred, with a trigger, then the only valid first question is: **has the trigger fired?**

If it has not fired, the burden is to justify overriding a past deliberate decision — not merely to justify the new work on its own merits.

### 5. What is the cheapest thing that would work?

List at least one config-only, one provider-native, and one do-nothing option. Price each. Explain why each is insufficient.

"We didn't think of one" is not an answer; it is a signal to stop and think of one.

### 6. What new failure surface does this create?

New env vars, new operational states, new triage paths, new scheduled jobs, new paid dependencies, new runbook pages, new things that can silently stop working.

Complexity is a recurring cost paid by every future engineer and agent touching the system. Name it before accepting it.

### 7. Where is the *real* probable breakage?

If this failure mode is unlikely, what is the likely one? Is the effort being spent where the actual risk is?

The most valuable output of this gate is often redirection rather than rejection.

## Making it enforceable

A checklist reminds; an Action verifies. Following the progression in [GitHub Actions Turn Rules into Guardrails](014-github-actions-turn-rules-into-guardrails.md):

**lesson → rule → template → automated check → required gate**

- Add these questions to the issue template, so the structure is visible.
- Require the throughput/capacity table for any issue touching delivery, ingestion, or scheduled processing.
- Have CI fail an implementation-ready issue that lacks the evidence and arithmetic sections.
- Require a link to the relevant roadmap classification, so bypassing a prior "Watch" decision is a conscious act rather than an oversight.
- Require every PR beyond the first in a multi-part initiative to restate the today→after comparison against the founding issue's own number, not just its own local scope.
- Require `approve` / `clarify: <question>` / `not now` as the only valid response on escalated work — no other response is accepted.

The goal is not bureaucracy. It is to make it *impossible to accidentally skip* the ninety seconds of arithmetic that would have prevented weeks of work.

## Reusable takeaway

> **A plan's rigor tells you nothing about whether the problem is real. Only evidence does — and only arithmetic tells you whether your solution actually solves it.**

Four questions, asked before any significant build — and re-asked at every step after — would have prevented every failure described here:

1. **How often does this actually happen, and how bad is it when it does?**
2. **What do the numbers say — current capacity, proposed capacity, and required capacity at the stated design target, side by side?**
3. **What is the cheapest thing that would work, and why isn't it enough?**
4. **Does the founding number still hold, right now, at this step — not just at the start?**

If you cannot answer the first three with specifics, you are not ready to build. You are ready to investigate.

If you cannot answer the fourth, correctly stating the problem once was not enough — velocity, not neglect, is what carries a real requirement out of view, and only something structural, not memory or good intentions, carries it back.

And when your own repository has already answered the question — go read it first.
