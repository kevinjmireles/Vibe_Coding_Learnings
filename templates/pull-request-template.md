# Pull Request Template

```markdown
The issue owns deep problem validation. This PR carries the decision brief and any required re-check against the founding number — link to the issue; do not duplicate its full validation here unless this PR itself changes the problem.

**Tier:** Routine (one line, skip below) / Escalated (full gate applies)

## What is this

One sentence, plain language.

## Founding number

Quote the number this traces back to (from the issue that started this initiative), with a link to that issue — or state that none exists.

**If this is PR 2 or later in a multi-PR initiative:** restate Today → after against the *founding issue's own number*, not just this PR's local scope. This is required, not optional, every time — that is where drift across a campaign hides.

**If this PR changes the problem, target, scope, assumptions, or cost enough that the founding issue's validation is no longer accurate:** update the founding issue (or record an explicit superseding decision there) before restating the new founding number here. Don't let the PR quietly drift from the issue instead.

## Today → after

```
today: <X>/<unit> → after: <Y>/<unit>  (confidence: measured | estimated | unknown)
```

Business units, not internal parameters. If `after` is worse than `today` or than the founding number, that is the finding.

## Ask

**approve** / **clarify: <question>** / **not now**

## Summary

- What changed?
- Why was the change needed?

## Issue

Closes #[issue number]

## Existing capability reused

What existing system, component, helper, workflow, or contract was extended?

If a new path was created, why could the existing system not be extended safely?

## Implementation

Describe the final implementation—not the original plan if the plan changed.

## Test plan

- [ ] Targeted regression tests
- [ ] Boundary or failure-case tests where relevant
- [ ] Relevant existing test suite
- [ ] Build, lint, type-check, or manual validation where relevant

List the actual commands or checks run and their results.

## Documentation

- [ ] Architecture or contract documentation checked
- [ ] Runbooks or operational guidance checked
- [ ] Examples and templates checked
- [ ] Session or continuity notes checked
- [ ] Documentation index or registry checked

Explain each update or state why no change was required.

## Failure and recovery behavior

How does the change behave when required data, configuration, permissions, or external services are unavailable? Can retries or partial execution create duplicates?

## Risks and limitations

What remains uncertain, intentionally deferred, or dependent on follow-up work?

## Builder self-assessment

**Grade:** A / B / C / D / F

**Justification:**

## Reviewer assessment

**Grade:** A / B / C / D / F

**Confidence:** High / Medium / Low

**Ready to merge:** Yes / No

**Justification:**
```

## Grading guide

- **A** — Complete, clear, appropriately scoped, well-tested, documented, and no meaningful reviewer correction required.
- **B** — Solid and mergeable after limited reviewer findings or corrections.
- **C** — Significant issues were found; substantial revision was required before merge.
- **D** — Major correctness, architecture, testing, or documentation failures.
- **F** — Unsafe, fundamentally incorrect, or unrelated to the approved requirement.

The grade is not a performance score. It records how much meaningful correction was required and helps identify recurring process weaknesses.
