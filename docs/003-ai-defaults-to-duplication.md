# AI Defaults to Duplication

## Failure pattern

One of the most persistent AI development failure patterns I encountered was duplication.

AI often responded to a new requirement by creating a new helper, workflow, renderer, data path, document, or subsystem instead of first checking whether an existing capability could be extended.

The proposed solutions usually worked in isolation. The problem was what they did to the system as a whole.

## What it looked like in practice

The pattern appeared repeatedly:

- similar calculations implemented independently;
- multiple renderers solving nearly the same presentation problem;
- new formatting logic instead of shared formatters;
- parallel documentation that competed with the canonical source;
- separate geographic or identity workflows instead of one system with provider-specific components;
- new ingestion paths where an existing pipeline could be extended.

A recent example involved Global Alerts. A proposal introduced a separate location and subscriber system for the global product. The individual design was plausible, but it would have duplicated capabilities already present in the core platform.

The better design was one shared system that can use different providers or components depending on geography and need.

## Why it happened

AI is naturally optimized to satisfy the current prompt. Creating a new component is often the shortest path to a locally complete answer.

The model does not automatically experience the future cost of maintaining two similar systems. It also may not search broadly enough to discover existing capabilities unless explicitly instructed to do so.

Humans duplicate too. AI simply makes it possible to duplicate at much greater speed.

## System or process introduced

An explicit rule was added to `CLAUDE.md`:

> Before creating a new system, component, helper, workflow, or document, determine whether an existing one can be extended or generalized.

Plans and reviews now ask questions such as:

- What existing capability already addresses part of this problem?
- Why can it not be extended?
- Is this genuinely a different concern or merely a variation?
- Which document is canonical?
- Will this create two sources of truth?

Audits are also used before major consolidation work to inventory duplication and inconsistency.

## How it helped

The rule has prevented unnecessary parallel systems multiple times. It improves scale, quality, and clarity because each capability has fewer implementations to test, document, secure, and maintain.

It also encourages better architecture. Instead of forcing every use case into identical behavior, the design can share a common core while allowing provider-specific or geography-specific components where they are truly needed.

## Why duplication is so expensive

Every duplicate adds more than one new thing. It adds:

- another place for bugs;
- another test surface;
- another documentation obligation;
- another migration path;
- another opportunity for behavior to drift;
- another decision future contributors must understand.

The complexity compounds.

## Reusable takeaway

**Before creating anything new, require proof that the existing system cannot reasonably be extended.**

AI should not merely solve the immediate task. It should solve it with the smallest sustainable increase in system complexity.