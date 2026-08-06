# Document Everything Worth Remembering

## Failure pattern

Important decisions were often made correctly but not recorded where future contributors could find them. A feature might be implemented, reviewed, and merged while the architecture guide, data dictionary, examples, or operating instructions still described the old system.

The code worked, but the repository told conflicting stories.

## Why it happened

Documentation was treated as a separate activity to complete after the real work. By the time implementation was finished, the next task was already waiting.

AI made this easier to overlook because a model could explain the change clearly in chat or a pull-request comment. That explanation felt documented even though it was not part of the durable product record.

## System or process introduced

Documentation became part of the definition of done.

Every meaningful issue and review now considers whether the change affects:

- architecture documents;
- data dictionaries;
- decision records;
- operating runbooks;
- development instructions;
- design standards;
- session notes;
- examples or templates;
- documentation registries;
- issue and pull-request descriptions.

The key question is not simply, “Did we write documentation?” It is, “Which existing source is canonical, and does it now reflect reality?”

This distinction prevents another common failure: creating a new document instead of updating the authoritative one.

## How it helped

Documentation became an active quality-control layer.

Writing down a design often exposed missing assumptions, ambiguous ownership, inconsistent terminology, or a workflow that was more complicated than it first appeared. Reviewers could compare the implementation against the documented contract and identify drift.

It also improved AI performance. New models could read the repository and act from explicit context rather than guessing from code or relying on conversation history.

## What deserves documentation

Not every temporary idea needs a file. Documentation is most valuable when the information will affect future work:

- why a design was chosen;
- what behavior is required;
- where data comes from;
- who or what owns a process;
- how a failure is detected and recovered;
- which terminology and patterns are canonical;
- what work remains intentionally deferred.

A useful rule is: if forgetting it would cause rework, inconsistency, or risk, record it.

## Reusable takeaway

**Documentation is not commentary on the software. It is part of the software's operating system.**

Make documentation impact an explicit part of planning, implementation, and review. Update the canonical source rather than leaving the truth scattered across chats and pull requests.