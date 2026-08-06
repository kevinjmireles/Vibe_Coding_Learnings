# Small, Self-Contained Issues Scale Better

## Failure pattern

Large, loosely defined requests produced unpredictable results. AI might solve the most visible part, overlook constraints, expand scope, or combine several architectural decisions into one difficult-to-review change.

Long conversations also encouraged requirements to drift. By implementation time, the Builder might be acting on a partial or outdated understanding of the task.

## Why it happened

AI works best when the objective, constraints, and evidence of completion are explicit. Broad requests force the model to make more assumptions.

Large changes also make independent review harder. When a pull request mixes architecture, refactoring, product behavior, documentation, and unrelated cleanup, reviewers struggle to determine which change caused a problem or whether every requirement was met.

## System or process introduced

Work increasingly moved into focused GitHub issues with:

- a clear problem statement;
- current behavior and desired behavior;
- explicit scope;
- exclusions and deferred work;
- acceptance criteria;
- testing expectations;
- documentation impact;
- dependencies and risks.

Large initiatives were divided into sequenced issues. Research and audits were separated from implementation when the correct solution was not yet known.

The goal was not to make every issue tiny. The goal was to make each one coherent enough that a Builder could implement it and a Reviewer could verify it without reconstructing the entire project.

## How it helped

Smaller, self-contained issues reduced ambiguity and context loss. They made it easier to:

- assign work to different models;
- resume from mobile;
- review changes independently;
- isolate failures;
- revert safely;
- preserve deferred ideas without expanding the current task;
- keep pull-request descriptions accurate.

They also improved architecture. When an issue could not be explained clearly, that often signaled that the underlying design had not been resolved.

## A caution

Splitting work too aggressively can create artificial fragmentation and dependency overhead. A single user-visible capability may require coordinated changes across code, tests, and documentation, and those belong together.

The useful boundary is a verifiable outcome, not a fixed number of files or lines.

## Reusable takeaway

**Define work in units that one Builder can complete and one independent Reviewer can verify.**

A strong issue is not just a task list. It is the contract connecting product intent, implementation, evidence, and documentation.