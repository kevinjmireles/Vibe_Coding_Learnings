# Issue Template

Use this template to turn an idea, defect, or improvement into a bounded unit of work that another person or AI can execute without reconstructing the entire conversation.

```markdown
# [Clear problem-focused title]

## Problem

What is broken, missing, inconsistent, risky, or unnecessarily difficult?

## Impact

Who or what is affected, and why does it matter?

## Evidence

Include screenshots, logs, examples, affected files, links, or reproduction steps when available.

## Problem validation

Required for anything larger than a bug fix. See [Do the Math Before You Build](../docs/024-do-the-math-before-you-build.md).

- **Has it happened?** Incident, log, or report — or an explicit "not observed yet."
- **Probability × impact:** how often at current scale, and how bad each time.
- **Arithmetic:** current capacity / proposed capacity / required capacity, same units, side by side.
- **Prior classification:** what the roadmap or architecture docs already decided about this capability, and whether its trigger has fired.
- **Cheapest alternatives considered:** config-only, provider-native, and do-nothing — each priced and rejected with a reason.
- **New failure surface introduced:** env vars, operational states, scheduled jobs, paid dependencies, triage paths.

## Existing systems to reuse

Identify the closest existing component, helper, workflow, contract, document, or architecture. Explain whether it should be extended.

## Proposed scope

Describe the smallest complete change that solves the problem.

## Acceptance criteria

- Given ..., when ..., then ...
- [Observable pass/fail condition]
- [Required failure or boundary behavior]
- [Required test or documentation outcome]

## Tests

Describe the regression, boundary, failure-case, integration, or manual validation expected.

## Documentation impact

List canonical documents, contracts, runbooks, examples, or indexes that may require updates. Use `None` only after checking.

## Risks or architectural decisions

Call out duplication risk, migration impact, security, accessibility, localization, data integrity, scale, or operational concerns.

## Out of scope

List related work intentionally excluded.

## Questions

Record non-blocking uncertainty without inventing answers.
```

## Drafting rules

- State the problem before prescribing the implementation.
- Make acceptance criteria observable and testable.
- Identify existing systems before authorizing a new one.
- Keep work together when partial delivery would be unsafe.
- Split unrelated improvements rather than hiding them in one issue.
- Do not use the issue as a substitute for a long-lived architecture document when a durable design decision is required.
