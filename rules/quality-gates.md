# Quality Gates

These gates turn recurring failure patterns into repeatable checks. The strongest gates are enforced by GitHub rather than left as reminders.

## 1. Problem gate

Before implementation:

- Is the actual problem stated clearly?
- Is the user or operational impact understood?
- Are acceptance criteria observable?
- Is important information missing?
- Is this one coherent change or several unrelated requests?

### 1.1 Problem validation gate

A clearly stated problem can still be rare, harmless, already mitigated, or unsolved by the proposed design — and a correctly stated one can still be lost across the many PRs that implement it. For any initiative larger than a bug fix, answer these **in writing, with numbers**, presented so a decision is possible in seconds.

**Order and format, every time:**

1. One sentence: what is this.
2. The founding number this traces back to, if one exists (quote the originating issue), or state that none exists yet.
3. One literal comparison line, same units as the founding number:
   `today: <X>/<unit> → after: <Y>/<unit> (confidence: measured | estimated | unknown)`
4. Cost — PRs, money, new operational surface.
5. The ask: **approve** / **clarify: <question>** / **not now**. No other response is valid on escalated work (see Tiering below).

Business units throughout (recipients, minutes, dollars), never internal parameters, above this line. Full technical detail belongs below a divider, unlimited in length, for the builder and reviewer — the approver should never need to read it to decide.

**The underlying content, unconditional regardless of presentation:**

- **Has it actually happened?** Link the incident, log, or user report. If it has not happened yet, say so explicitly rather than leaving it implied.
- **Probability × impact.** How often at current scale, and what is the blast radius when it occurs?
- **Show the arithmetic — this is the comparison line above, not optional, not conditional on the change being labeled "performance."** Current capacity, proposed capacity, and required capacity, same units, side by side. If the proposal is slower or smaller than what it replaces, the design is wrong regardless of its elegance. A prior draft of this gate demoted this to something an author could skip by not flagging their own work as scale-related; it is never skippable.
- **State the scale target as a number.** "Required capacity" means the documented design target, not today's volume. Building ahead of current need is often correct; building without a written target is what produces both over- and under-engineering. If no target exists, establishing one is the first task.
- **What did the roadmap already say?** If an existing architecture or roadmap document already classified this capability as deferred with a trigger, state whether the trigger has fired. Overriding a prior deliberate deferral requires justifying the override, not just the work.
- **What is the cheapest thing that would work?** Price at least one config-only, one provider-native, and one do-nothing option, and explain why each is insufficient.
- **What new failure surface does this create?** New environment variables, operational states, triage paths, scheduled jobs, paid dependencies, and runbook pages are recurring costs paid by everyone who touches the system later.
- **Where is the real probable breakage?** If this failure mode is unlikely, name the likely one. Redirection is often this gate's most valuable output.

**Tiering — two levels, not more:**

- **Routine** (bug fix, copy change, dependency bump, added test): one line, what and why. Nothing above applies.
- **Everything else:** the full gate applies.

**Escalate immediately, no judgment required, if any of these are true** — and if none are true at authoring time but any become true later, escalate then:

- More than one PR. **This is a standing obligation, not a one-time check:** any PR beyond the first in a multi-PR initiative must restate the today → after comparison against the *founding issue's own number* before it can be approved. A campaign that starts as one PR and grows must re-run this the moment it grows, not retroactively.
- New recurring cost.
- New external dependency.
- New always-on component (cron, worker, queue).
- Can't be undone by a revert (data migration, provider switch).
- Touches send, signup, or ingest.

**Confidence tags — three, not more:** measured / estimated / unknown. On escalated work, `unknown` or a stale `estimated` on the today→after comparison blocks sign-off until it is measured or explicitly accepted in writing. A tag that changes nothing when it says `unknown` is decoration, not a control.

> Rigor about execution is not validation of purpose. A meticulous plan can still build the wrong thing — and a correctly validated plan can still drift once implementation spans many PRs, unless the founding number travels with the work.

See [Do the Math Before You Build](../docs/024-do-the-math-before-you-build.md) and [Re-Check the Number You Already Wrote Down](../docs/025-recheck-the-number-you-already-wrote-down.md).

## 2. Reuse and duplication gate

Before creating a new component, helper, workflow, table, document, or service:

- What existing capability is closest?
- Can it be extended without distorting its purpose?
- Would a new path duplicate behavior, data, tests, documentation, or maintenance?
- If a new path is necessary, is the reason documented?
- Is there a migration or deprecation plan for the old path?

> Before creating anything new, prove that the existing system cannot be extended safely.

## 3. Scope gate

- Is this the smallest complete testable slice?
- Does partial implementation create risk or misleading behavior?
- Has unrelated cleanup been added?
- Are future enhancements clearly separated from current requirements?

## 4. Architecture gate

For substantial changes:

- Does this conflict with a documented architectural principle?
- Does it create future migration work?
- Is it the simplest design that preserves important long-term options?
- Does it introduce a second source of truth?
- Does it keep data, business logic, and presentation appropriately separated?
- Have accessibility, localization, security, provenance, and scale been considered in proportion to the change?

## 5. Failure-mode gate

- What happens when required data is missing or stale?
- What happens when execution is interrupted?
- Can retries create duplicates?
- Is partial success recorded clearly?
- Are failures observable?
- Is there a recovery path?
- Does the system fail closed when producing output would be misleading or unsafe?

## 6. Test gate

- Is the requested behavior tested?
- Is the original defect reproduced by a regression test?
- Are meaningful boundaries and invalid inputs covered?
- Do the tests validate behavior rather than implementation trivia?
- Were relevant existing suites run?
- Could the tests pass while the user-visible behavior is still wrong?

## 7. Parallel-path review gate

The Reviewer should ask:

- Is the implementation correct?
- Is there a materially simpler or more reusable path?
- Did the Builder solve only the visible symptom?
- Does the same failure pattern exist elsewhere?
- Would an experienced maintainer choose this approach after seeing the whole system?

Correct code can still be the wrong implementation path.

## 8. Documentation gate

Documentation is a core Builder responsibility, not a separate after-the-fact task.

- Did this change alter architecture, contracts, operations, terminology, data, or workflow?
- Was the canonical document updated?
- Was a competing document accidentally created?
- Do examples and templates still match the real behavior?
- Can another person or AI continue without the current chat?

The Reviewer verifies documentation impact. The Architecture Steward checks long-term consistency when shared systems or architectural principles change.

## 9. Pull-request truth gate

Before merge, the PR description should match the final implementation—not the original plan.

Verify:

- summary is current;
- files and behavior described are accurate;
- tests listed were actually run;
- Builder self-grade is present;
- independent Reviewer grade and confidence are present;
- review findings and fixes are documented when useful;
- documentation checklist reflects reality;
- known limitations are explicit.

## 10. Enforced GitHub gate

Important requirements should not depend solely on someone remembering them.

GitHub provides several layers that can turn written expectations into enforceable workflow:

- **Issue and PR templates** make required structure visible.
- **GitHub Actions** can inspect issue or PR content and fail when required sections, fields, labels, evidence, or metadata are missing.
- **CI workflows** run objective validation such as tests, type checking, linting, builds, migrations, or consistency checks.
- **Required status checks and branch protection** prevent merge while designated checks are failing or incomplete.
- **Review requirements** can require approval before merge.
- **Merge permissions** keep the final decision with the authorized human.

For issues, Actions can verify that an implementation-ready issue has the required problem statement, acceptance criteria, labels, or other project-specific fields before downstream work relies on it.

For pull requests, Actions can verify that required evidence is present—for example testing, documentation impact, known limitations, Builder self-grade, or Reviewer fields—rather than merely trusting that the template was completed correctly.

This creates a progression:

**lesson → rule → template → automated check → required gate**

A checklist reminds. An Action verifies. A required status check can stop an incomplete merge.

Automation should enforce observable minimums, not pretend to replace judgment. A workflow can confirm that a documentation section exists; it cannot determine that the documentation is thoughtful or correct. Human and independent AI review still matter.

See [GitHub Actions Turn Rules into Guardrails](../docs/014-github-actions-turn-rules-into-guardrails.md).

## 11. Merge gate

A change is ready to merge when:

- acceptance criteria are met;
- meaningful review findings are resolved or explicitly accepted;
- required GitHub and CI checks pass;
- documentation is current;
- no unresolved duplication or architecture concern remains;
- the Reviewer states clearly that it is ready;
- the authorized human agrees with the outcome, using §1.1's required response format (**approve** / **clarify: <question>** / **not now**) on any escalated work.

> **The best process is one you cannot accidentally skip.**

See [Every Manual Step Eventually Belongs in GitHub](../docs/011-every-manual-step-eventually-belongs-in-github.md).