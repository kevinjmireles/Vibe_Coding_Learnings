# Reusable Principles

These are the short ideas that emerged repeatedly while building Fido. Each principle is backed by a longer failure pattern, process rule, or evolution study elsewhere in this repository.

- **Vibe gets you started. Systems get you to production.**
- **The development process is itself a product.** Design, test, maintain, and improve the system that produces the software.
- **Deliver the required product quality at the lowest total lifecycle cost.** Minimize development, compute, queries, APIs, AI/model usage, maintenance, rework, migration, and opportunity cost without dropping below the product-quality bar.
- **Avoid → Reuse → Do once → Batch/cache/precompute → Right-size → Optimize.** Use this as an economic instinct, not a rigid checklist.
- **The best prompt is a GitHub issue.**
- **The repository should remember more than the AI.**
- **Every recurring mistake deserves a system.**
- **Every manual step eventually belongs in the workflow.**
- **If you explain it twice, document it.**
- **If you build it twice, you probably need one shared system.**
- **The best process is one you cannot accidentally skip.**
- **Architecture is cheaper than rework.**
- **Regression tests are compound interest for software.**
- **Evidence is stronger than confidence.**
- **The AI should identify the task; the repository should define how work is done.**

## Ideas become durable through evidence

A useful idea in a chat is not yet a process rule or lesson. The default lifecycle is:

> **Idea → Issue → Review → Implement → Observe → Learn → Document → Reuse**

In operational terms, that usually means:

1. **Idea in chat** — explore the possibility without pretending it is already proven.
2. **GitHub issue** — move work worth pursuing into the durable system of record.
3. **Reviewed design** — challenge assumptions, scope, duplication, architecture, and expected value before implementation.
4. **Implementation** — build the smallest useful version.
5. **Evidence from actual use** — test it, use it, review what worked, and capture what failed.
6. **Evolution note** — record how and why the process changed.
7. **Reusable lesson** — promote the finding only when experience supports a broader takeaway.
8. **Template or system update** — when appropriate, make the proven practice easier for the next person or project to adopt.

### Not every idea graduates

This is a learning pipeline, not a content-production pipeline. An idea may stop during design review. An implementation may prove the original hypothesis wrong. A useful Fido-specific solution may not be general enough to become a reusable lesson. Evidence can also justify removing or reversing a previous practice.

The goal is not to manufacture best practices. It is to let observed experience earn its way into the reusable system.

The [Process Evolution](../evolution/README.md) section records the evidence behind changes. GitHub issues track proposed work and experiments; the numbered lesson documents capture learnings that have survived implementation and review.

These are not universal laws. They are practical defaults created in response to real failures.
