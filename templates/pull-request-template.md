# Pull Request Template

```markdown
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
