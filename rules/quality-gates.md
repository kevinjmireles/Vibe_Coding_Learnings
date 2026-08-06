# Quality Gates

These gates turn recurring failure patterns into repeatable questions. They are most useful when applied at issue drafting, implementation, review, and merge—not only at the end.

## 1. Problem gate

Before implementation:

- Is the actual problem stated clearly?
- Is the user or operational impact understood?
- Are acceptance criteria observable?
- Is important information missing?
- Is this one coherent change or several unrelated requests?

## 2. Reuse and duplication gate

Before creating a new component, helper, workflow, table, document, or service:

- What existing capability is closest?
- Can it be extended without distorting its purpose?
- Would a new path duplicate behavior, data, tests, documentation, or maintenance?
- If a new path is necessary, is the reason documented?
- Is there a migration or deprecation plan for the old path?

A useful default rule:

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

- Did this change alter architecture, contracts, operations, terminology, data, or workflow?
- Was the canonical document updated?
- Was a competing document accidentally created?
- Do examples and templates still match the real behavior?
- Can another person or AI continue without the current chat?

## 9. Pull-request truth gate

Before merge, the PR description should match the final implementation—not the original plan.

Verify:

- summary is current;
- files and behavior described are accurate;
- tests listed were actually run;
- review findings and fixes are documented when useful;
- known limitations are explicit;
- checklist items reflect reality.

## 10. Merge gate

A change is ready to merge when:

- acceptance criteria are met;
- meaningful review findings are resolved or explicitly accepted;
- relevant checks pass;
- documentation is current;
- no unresolved duplication or architecture concern remains;
- the Reviewer states clearly that it is ready;
- the authorized human agrees with the outcome.
