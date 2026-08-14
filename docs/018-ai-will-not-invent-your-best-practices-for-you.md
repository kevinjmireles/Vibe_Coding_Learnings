# 018 — AI Will Not Invent Your Best Practices for You

## The problem

AI agents are very good at completing the task they were given. That does not mean they will automatically stop and choose the best long-term engineering pattern.

A proposed implementation can be technically valid, pass tests, and still be the wrong architecture.

One example from Fido was a design that called an external API during runtime. The implementation could have worked as proposed. The important question came from outside the implementation itself:

> Why are we calling this API at runtime?

That question exposed a better design direction. The data did not necessarily need to be fetched synchronously on every user request. Pre-ingestion, caching, precomputation, or another asynchronous path could reduce latency, external dependency risk, cost, and failure modes.

If that architectural question had not been asked, the original implementation could easily have shipped.

## Why this happens

AI optimizes primarily for satisfying the explicit assignment.

If an issue says "fetch this information and display it," a runtime API call may be the shortest path to success. Unless the repository explicitly says otherwise, the agent may not independently optimize for:

- resilience to third-party outages;
- latency;
- cost at scale;
- rate limits;
- caching opportunities;
- precomputation;
- operational simplicity;
- consistency with existing architecture; or
- long-term maintainability.

Humans make the same mistake. AI simply makes it possible to implement the locally reasonable solution much faster.

## The system introduced

When a better pattern is discovered, do not rely on remembering the conversation.

Turn it into a durable system:

> **Observation → principle → repository rule → measurable goal → review gate → automation where practical**

For example, a project might adopt a rule such as:

> Prefer ingestion, precomputation, caching, or asynchronous processing when external data does not need to be fetched synchronously for each user request. New runtime third-party dependencies require explicit justification.

Then make the rule visible in the places that matter:

- `CLAUDE.md` or equivalent repository instructions;
- architecture principles;
- issue and design review questions;
- Reviewer instructions;
- measurable performance or reliability goals; and
- automated checks where a safe objective check is possible.

The lesson is not the specific rule about APIs. The lesson is the process for converting hard-won engineering judgment into repeatable behavior.

## The human role changes

A non-programmer does not need to know how to implement the better architecture to challenge the proposed one.

The high-leverage human contribution may simply be asking:

- Why is this happening at runtime?
- Why is this a new system instead of extending the existing one?
- Why does the user need to wait for this?
- What happens if the provider is down?
- How does this behave at 100× the current volume?
- Are we fixing the shared primitive or one visible symptom?

The AI can help design and implement the answer. The human still has to recognize when the question needs to be asked.

## Best practices must become explicit

A practice is not reliable merely because it is considered "best practice" in software engineering.

If it matters to this project, identify it, document it, and define the desired outcome clearly enough to review.

This is especially important for principles that are easy to sacrifice in favor of the fastest local implementation:

- avoid unnecessary runtime dependencies;
- reuse before creating parallel systems;
- centralize shared behavior;
- fail safely when data is missing or stale;
- keep important operations observable;
- preserve idempotency and retry safety;
- validate real production-shaped data;
- separate creation from independent review; and
- require evidence rather than confidence.

Many of these are already documented elsewhere in this repository. The important pattern is that they became reliable only after being made explicit.

## Reusable takeaway

> **AI does not automatically implement your best practices. Your repository has to teach them.**

When you catch an implementation that is locally reasonable but architecturally weak, do not just fix that implementation.

Capture the broader principle so the next Builder starts with better instincts and the next Reviewer knows what to challenge.

---

Created by **Kevin J. Mireles** as part of *From Vibe Coding to Production / Vibe Coding Learnings*. Licensed for reuse under CC BY 4.0; attribution is required when sharing or adapting this work.