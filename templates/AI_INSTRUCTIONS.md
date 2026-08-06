# Reusable AI Development Instructions

This file is a generalized starting point for a repository-level AI instruction file such as `CLAUDE.md`, `AGENTS.md`, or another tool-specific equivalent.

The most important lesson is not the exact wording. It is that stable development rules should live in the repository rather than being recopied into every prompt.

---

## Prime directive

**Simpler is better.**

Prefer the smallest solution that fully satisfies the requirement, remains testable, and preserves reasonable future options.

Do not add abstractions, feature flags, frameworks, files, or parallel systems unless the change genuinely requires them.

## Before creating anything new

Search the repository for an existing implementation, helper, component, workflow, document, or architectural pattern that can be extended.

Before proposing a new path, answer:

1. What existing capability is closest to this requirement?
2. Why can it not be extended safely?
3. Would the new implementation duplicate logic, data, tests, documentation, or maintenance?

**Do not create a parallel system merely because it is easier to solve the immediate task in isolation.**

## Scope

- Implement the smallest complete, testable slice.
- Do not silently expand scope.
- Do not retrofit unrelated legacy code unless it is directly affected, inexpensive to fix, or blocks correct use.
- Keep changes atomic when partial implementation would create an unsafe or misleading state.

## Plan before implementation

For meaningful work, first provide a brief plan covering:

- problem being solved;
- proposed scope;
- existing systems likely to be reused;
- key files or components affected;
- observable acceptance criteria;
- tests and documentation likely required;
- risks or architectural decisions.

## Issues are the source of planned work

Use GitHub issues or the repository's equivalent tracker as the canonical source of approved engineering work.

Do not create duplicate issue drafts in documentation folders unless a long-lived specification or architecture artifact is genuinely required.

Acceptance criteria must be observable and testable. Prefer Given/When/Then or clear pass/fail language.

Do not invent missing requirements. Ask when the missing information is critical; record non-blocking uncertainty explicitly.

## Evidence, not confidence

Do not report that a change “looks good” or “should work” as proof of completion.

Provide evidence proportional to risk, such as:

- targeted regression tests;
- boundary and failure-case tests;
- full relevant test-suite results;
- build, lint, or type-check results;
- before/after output;
- manual verification steps;
- confirmation that acceptance criteria were met.

Every discovered defect should become a regression test when practical.

## Fail safely

When required data, configuration, continuity, permissions, or assumptions are invalid, prefer an explicit failure or omission over silently generating misleading output.

For production behavior, answer:

1. How can this fail?
2. How will the failure be detected?
3. What prevents partial or duplicate execution?
4. How can the system recover?

## Documentation is part of the change

For every meaningful change, evaluate whether to update:

- architecture documentation;
- decision records;
- operating runbooks;
- data dictionaries or contracts;
- developer instructions;
- examples and templates;
- session or continuity notes;
- documentation indexes or registries.

Update the canonical document rather than creating another document that competes with it.

## Separate data from presentation

Reusable business logic should produce structured values rather than completed user-facing prose whenever practical.

Keep presentation, locale, formatting, and channel-specific rendering at the boundary. This reduces duplication and preserves accessibility, localization, and multi-channel options.

## Security and privacy

- Never expose or log secrets.
- Log only the minimum useful identifiers, counts, and status information.
- Respect access controls rather than bypassing them for convenience.
- Treat production data changes, destructive operations, and permission changes as high-risk work requiring explicit scope and verification.

## Commits and pull requests

Keep commits focused and descriptions factual.

A pull request should explain:

- what changed;
- why it changed;
- what existing capability was reused or why a new path was necessary;
- how it was tested;
- what documentation changed;
- remaining risks or follow-up work.

## Session continuity

At the beginning of work, read the repository overview, current-session notes, architecture principles, and role instructions relevant to the task.

At the end, ensure that durable decisions and unresolved work are stored in the repository—not only in the AI conversation.
