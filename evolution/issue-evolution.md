# Issue Evolution: The Best Prompt Became a GitHub Issue

## Early approach

Work often began as a sentence in chat: fix this, add that, change this wording. The AI could start immediately, but the request might not define the real problem, expected behavior, boundaries, or proof of completion.

## What failed

Ambiguous requests created predictable problems:

- implementation started before the problem was understood;
- related work was split incorrectly or bundled too broadly;
- acceptance criteria changed during implementation;
- decisions remained trapped in chat;
- a new model could not reliably continue the work.

## What changed

GitHub issues became the canonical source of planned engineering work. A useful issue now records:

- the problem being solved;
- proposed scope;
- observable acceptance criteria;
- affected systems;
- risks and architectural decisions;
- questions and explicit exclusions;
- related documents, issues, and PRs.

The goal is not a long issue. It is a complete one.

## Why this is better

A Builder can implement from the issue. A Reviewer can assess the result against the same issue. The human product owner can correct the plan before code is written. The issue then remains as durable context for future work.

## Reusable takeaway

**The best prompt is often a well-written issue.**

Put the durable definition of the work in GitHub and use the chat prompt only to identify which issue to build or review.