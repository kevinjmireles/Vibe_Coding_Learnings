# Core Prompts

These prompts are intentionally short. The repository should contain the durable rules; the prompt should identify the role and current assignment.

Replace bracketed placeholders with the relevant issue, pull request, or document.

## Builder

```text
Read the repository's AI instructions and Builder role guide. Implement [ISSUE OR TASK] exactly as scoped. Reuse existing systems before creating anything new. Add appropriate tests and documentation, run the required checks, and report the evidence, risks, and any unresolved questions. Do not merge.
```

## Reviewer

```text
Read the repository's AI instructions and Reviewer role guide. Review [PULL REQUEST] against the issue, actual code, tests, documentation, and architecture. Form your assessment independently before relying on the Builder's summary. Apply the parallel-path and duplication gates. Report only meaningful findings, a quality grade, confidence, and whether the pull request is ready to merge. Do not modify or merge unless explicitly asked.
```

## Reviewer after fixes

```text
Re-review [PULL REQUEST]. Verify each prior finding against the current code and tests, check for regressions introduced by the fixes, and state clearly whether it is ready to merge. Do not repeat resolved findings except to confirm resolution.
```

## Documentation Steward

```text
Read the Steward role guide. Review [MERGED CHANGE OR PULL REQUEST] for documentation drift. Verify that architecture, contracts, runbooks, examples, indexes, and continuity notes still reflect the code. Update only documentation that is genuinely affected, and do not create a competing canonical document.
```

## Architecture Steward

```text
Read the architecture principles and Architecture Steward role guide. Assess [FEATURE, DESIGN, OR CHANGE] for duplication, parallel paths, scalability, security, accessibility, localization, data provenance, migration cost, and long-term platform impact. Distinguish what must be built now, designed for now, watched, or ignored. Recommend the simplest path that preserves important future options.
```

## Issue drafting

```text
Turn this request into a GitHub issue. First identify the problem, proposed scope, existing systems to reuse, key files or components, observable acceptance criteria, tests, documentation impact, risks, exclusions, and open questions. Do not create the issue until the proposed scope is approved.
```

## Bug investigation

```text
Investigate [BUG]. Reproduce or establish evidence first. Identify the root cause rather than applying successive speculative fixes. Check for the same failure pattern elsewhere. Propose the smallest complete correction, regression tests, and any operational or documentation follow-up. Do not claim resolution without evidence.
```

## Audit before refactoring

```text
Audit [SYSTEM OR PATTERN] before changing it. Inventory every implementation, variation, dependency, test, consumer, and canonical document. Identify true defects separately from inconsistencies and design opportunities. Recommend a sequenced plan that establishes the shared contract before migrating individual implementations.
```

## Mobile handoff

```text
Document the current state in the repository so another model or device can continue without this conversation. Record completed work, decisions, evidence, unresolved questions, exact next steps, relevant branches or pull requests, and links to canonical documents. Minimize information that must be copied from chat.
```

## Why these prompts are short

Long prompts became difficult to maintain, especially across multiple AI products and mobile devices. Moving the rules into version-controlled files made prompts smaller, reduced copy-and-paste, and ensured that different models worked from the same operating instructions.
