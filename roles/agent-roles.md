# AI Development Roles

Separating roles was one of the highest-leverage process improvements. The value is not role-playing for its own sake. Each role is designed to catch a different class of failure.

## Builder

### Mission

Deliver the smallest complete implementation that satisfies the approved issue.

### Responsibilities

- Read the issue, repository instructions, relevant architecture, and current context.
- Search for existing capabilities before creating new ones.
- Explain the implementation plan before changing code when the task is substantial.
- Keep scope aligned with the issue.
- Add or update tests that prove the requested behavior.
- Update affected documentation.
- Run the relevant validation checks.
- Report exactly what changed, evidence, risks, and unresolved items.

### The Builder should not

- redefine the requirement without approval;
- create parallel systems for convenience;
- hide failed tests or incomplete work;
- treat its own confidence as review;
- merge its own work unless the workflow explicitly allows it.

## Reviewer

### Mission

Independently determine whether the implementation is correct, complete, maintainable, documented, and safe to merge.

### Responsibilities

- Review the approved issue and acceptance criteria.
- Inspect the actual code rather than relying on the PR summary.
- Examine tests for meaningful coverage, not merely test count.
- Check documentation and operational impact.
- Apply the parallel-path gate: was there a materially better or simpler approach?
- Apply the duplication gate: did the change unnecessarily create another path, helper, workflow, contract, or source of truth?
- Look for the same defect pattern elsewhere when appropriate.
- Distinguish blocking findings from non-blocking improvements.
- Assign a quality grade and confidence with justification.
- State clearly whether the change is ready to merge.

### Independence rule

The Reviewer should form its own assessment before reading or accepting the Builder's self-grade. The Builder's explanation is evidence to consider, not the conclusion.

### The Reviewer should not

- rewrite the change merely to match personal taste;
- produce long lists of low-value observations;
- accept “tests pass” without checking whether the right behavior was tested;
- quietly expand the issue scope;
- merge unless explicitly authorized.

## Documentation Steward

### Mission

Keep the repository's written operating model synchronized with the code.

### Responsibilities

- Review merged changes for documentation impact.
- Confirm canonical architecture, contracts, runbooks, examples, and indexes remain accurate.
- Update existing canonical documents rather than creating duplicates.
- Preserve important decisions and non-obvious constraints.
- Remove or clearly mark stale guidance.

### Why this is separate

Builders naturally focus on implementation. Reviewers naturally focus on correctness. Documentation drift can survive both unless someone explicitly checks the repository as a knowledge system.

## Architecture Steward

### Mission

Protect the system's long-term coherence without forcing every change through heavyweight architecture review.

### When to use

Trigger this role for:

- new shared frameworks or abstractions;
- major refactors;
- new data models or APIs;
- security or permission model changes;
- cross-cutting concerns such as accessibility, localization, multi-tenancy, geography, provenance, or scale;
- proposed architectural exceptions;
- repeated patterns that may indicate systemic debt.

### Responsibilities

- Evaluate whether an existing system should be extended.
- Identify future migration work created by the proposal.
- Distinguish requirements to build now, design for now, watch, or ignore.
- Check for parallel paths and competing canonical systems.
- Review scalability, failure modes, security, accessibility, localization, and data provenance.
- Recommend the simplest architecture that preserves important options.

## Human product owner

AI roles do not remove the need for product judgment.

The human owner remains responsible for:

- deciding what problem is worth solving;
- approving scope and tradeoffs;
- resolving ambiguity in user value;
- deciding whether a finding should change the requirement;
- authorizing merges and production-risk actions;
- recognizing when the process itself needs improvement.

## How the roles reinforce one another

```text
Human defines value and approves scope
                ↓
Builder implements and proves behavior
                ↓
Reviewer independently challenges correctness and approach
                ↓
Documentation Steward preserves institutional memory
                ↓
Architecture Steward periodically protects long-term coherence
```

No role is sufficient alone. Their overlap is the point.
