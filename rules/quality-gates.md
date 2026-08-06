# Quality Gates

These gates turn recurring failure patterns into repeatable checks. The strongest gates are enforced by GitHub rather than left as reminders.

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

Use GitHub to enforce the workflow where possible:

- PR templates require key testing, documentation, and review information;
- automated PR-quality checks verify required fields or checklist state;
- CI runs tests, linting, builds, and other objective validation;
- branch protection requires designated status checks to pass;
- unresolved required checks prevent merge;
- review requirements can require approval before merge;
- merge permissions remain with the authorized human.

A checklist reminds. A required check prevents an incomplete merge.

## 11. Merge gate

A change is ready to merge when:

- acceptance criteria are met;
- meaningful review findings are resolved or explicitly accepted;
- required GitHub and CI checks pass;
- documentation is current;
- no unresolved duplication or architecture concern remains;
- the Reviewer states clearly that it is ready;
- the authorized human agrees with the outcome.

> **The best process is one you cannot accidentally skip.**

See [Every Manual Step Eventually Belongs in GitHub](../docs/011-every-manual-step-eventually-belongs-in-github.md).