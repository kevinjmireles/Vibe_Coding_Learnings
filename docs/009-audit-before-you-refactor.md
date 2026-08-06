# Audit Before You Refactor

## Failure pattern

When inconsistencies appeared across similar features, the instinct was often to fix the first visible example. That could improve one output while leaving the broader pattern untouched—or create yet another variation.

This happened with repeated presentation logic, calculations, terminology, accessibility patterns, and documentation. A narrow fix treated the symptom without establishing how many implementations existed or which behavior should become canonical.

## Why it happened

The first defect discovered is rarely the complete problem. AI is especially prone to treating the file or example named in the prompt as the full scope unless asked to search for related implementations.

Refactoring before understanding the landscape creates several risks:

- missing hidden duplicates;
- selecting the wrong implementation as canonical;
- changing behavior unintentionally;
- combining research and implementation in one unreviewable change;
- declaring completion while inconsistencies remain.

## System or process introduced

For cross-cutting problems, the workflow became audit-first:

1. inventory every relevant implementation;
2. document similarities, differences, and known defects;
3. identify the intended canonical behavior;
4. separate true defects from acceptable variation;
5. create focused implementation issues;
6. add regression tests that enforce the shared contract;
7. close or promote the audit into durable documentation once findings are accepted.

The audit itself is treated as research, not as permission to quietly rewrite production code.

## How it helped

The audit creates a map before changes begin. Builders can work from explicit findings rather than discovering scope halfway through implementation. Reviewers can verify that all identified cases were addressed and that legitimate differences were preserved.

This approach also reduces duplication. When several implementations are visible together, the underlying shared capability becomes easier to recognize.

In Fido, audits helped reveal where separate formatters, renderers, labels, and presentation rules had drifted. The resulting work could then establish shared contracts rather than patching individual examples indefinitely.

## When to use it

An audit is especially valuable when:

- the same problem appears in more than one feature;
- a search reveals several similar helpers or components;
- terminology or calculations disagree across outputs;
- documentation and code describe different designs;
- the likely fix affects architecture rather than one isolated defect.

For a truly local bug, an audit may be unnecessary overhead. The point is to match the process to the breadth of the failure pattern.

## Reusable takeaway

**When a defect suggests a pattern, inventory the pattern before refactoring it.**

A good audit separates discovery from implementation, identifies the canonical behavior, and turns scattered inconsistencies into a controlled sequence of changes.