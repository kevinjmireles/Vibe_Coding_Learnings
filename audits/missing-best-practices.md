# Missing Best Practices Audit

This is a working audit of engineering practices that are important enough to consider for repository-level AI instructions, but are not yet clearly or comprehensively encoded in the reusable guidance.

The purpose is **not** to dump every software-engineering rule into `CLAUDE.md`. The purpose is to identify high-leverage defaults that AI agents may otherwise overlook while optimizing for the immediate task.

## Already covered well

The current reusable instructions already address:

- simplicity and smallest-complete-slice scope;
- reuse before creating parallel systems;
- issues as the source of planned work;
- evidence over confidence;
- regression tests;
- safe failure behavior;
- documentation as part of implementation;
- separating data from presentation;
- security/privacy basics;
- focused commits and factual PR descriptions; and
- durable session continuity.

Those should remain canonical rather than being duplicated elsewhere.

## Best practices not yet explicit enough

### 1. Avoid unnecessary runtime dependencies

**Proposed default:** Prefer ingestion, precomputation, caching, or asynchronous processing when data does not need to be fetched synchronously for each user request. A new third-party runtime dependency should require explicit justification.

**Why:** Runtime dependencies add latency, cost, rate-limit exposure, outage coupling, and user-facing failure modes.

**Review question:** Why does this need to happen while the user is waiting?

---

### 2. Design to explicit performance and latency goals

**Proposed default:** Important user-facing or operational paths should have a stated target when delay materially affects value. If the real target is zero unnecessary wait, say zero.

**Why:** "Keep it fast" and "minimize delay" are too vague to drive architecture or review.

**Review question:** What is the target, and does this design make that target possible?

---

### 3. Treat external systems as unreliable

**Proposed default:** Every external API, database, queue, model, scraper, or provider should be assumed to become slow, unavailable, rate-limited, inconsistent, or changed without notice.

Design should consider:

- timeouts;
- bounded retries;
- backoff;
- circuit-breaking or graceful degradation where appropriate;
- stale-but-safe fallback where appropriate;
- provider response validation; and
- clear observability when dependencies fail.

**Review question:** What happens to the user and system when this provider is down for an hour?

---

### 4. Make retries idempotent by default

**Proposed default:** Any operation likely to be retried—imports, sends, jobs, webhooks, scheduled tasks, payments, writes—should be designed so retrying does not create duplicate effects.

**Why:** Retries are normal production behavior, not an edge case.

**Review question:** What happens if this executes twice?

---

### 5. Put boundaries around expensive or unbounded work

**Proposed default:** Any loop, query, AI call, external fetch, batch job, or user-driven operation that can grow with data volume needs an explicit bound, pagination strategy, budget, or backpressure mechanism.

**Why:** AI often produces implementations that work on today's small dataset but scale linearly into cost or reliability problems.

**Review question:** What happens at 10× and 100× today's volume?

---

### 6. Centralize configuration and policy

**Proposed default:** Thresholds, feature behavior, freshness limits, presentation standards, and other shared policy should have one canonical owner rather than being repeated as literals across the codebase.

**Why:** Scattered configuration creates silent divergence even when the underlying logic is shared.

**Review question:** If this value changes next month, how many places must change?

---

### 7. Prefer deterministic logic for deterministic problems

**Proposed default:** Do not use an LLM, probabilistic model, or heuristic where a deterministic parser, lookup, rule, or calculation can reliably solve the same problem.

**Why:** Probabilistic systems add cost, latency, testing difficulty, and variability.

**Review question:** Does this actually require intelligence, or only computation?

---

### 8. Separate write paths from read/presentation paths

**Proposed default:** User-facing reads should not casually trigger expensive mutations, ingestion, enrichment, or external synchronization unless that coupling is intentional and justified.

**Why:** Hidden writes make latency, failure recovery, retries, and debugging harder.

**Review question:** Is rendering this page/email unexpectedly changing system state?

---

### 9. Make data provenance and freshness first-class

**Proposed default:** Data-derived output should preserve enough metadata to know source, period, retrieval/release time, and freshness/validity status when those affect interpretation.

**Why:** Correct calculations on stale or ambiguous data can still produce misleading products.

**Review question:** Can we explain where this value came from and whether it is current enough to use?

---

### 10. Validate production-shaped combinations, not only isolated units

**Proposed default:** For systems whose failures emerge from combinations—geographies, locales, data sources, time periods, permissions, content modules—maintain reusable production test tools or matrices in addition to unit tests.

**Why:** A feature can pass its isolated tests while failing when real components interact.

**Review question:** What representative combinations have actually been exercised end to end?

---

### 11. Make observability part of feature design

**Proposed default:** Important production behavior should answer: how will we know it worked, failed, degraded, or silently stopped running?

Prefer structured logs, counts, statuses, timestamps, diagnostics, and alerts appropriate to the risk.

**Why:** A failure that cannot be observed becomes a user report or a mystery.

**Review question:** How would we know tomorrow that this stopped working tonight?

---

### 12. Design migrations and compatibility intentionally

**Proposed default:** Contract, schema, token, API, and data-model changes should state whether they are backward compatible, how old paths are migrated/deprecated, and when they can be removed.

**Why:** AI can solve the new state cleanly while overlooking existing callers and stored data.

**Review question:** What existing consumer or stored record breaks when this changes?

---

### 13. Minimize irreversible operations

**Proposed default:** Destructive production operations should prefer preview, dry run, scoped targeting, backup, reversible migration, or explicit confirmation where practical.

**Why:** AI makes execution easy; production recovery may not be easy.

**Review question:** If this is wrong, how do we undo it?

---

### 14. Make accessibility and localization architectural concerns early

**Proposed default:** Shared user-facing components should not bake language, formatting assumptions, inaccessible interactions, or presentation semantics so deeply into logic that later localization/accessibility requires parallel implementations.

**Why:** Retrofitting these concerns after components proliferate creates duplication and rework.

**Review question:** Does this design make another locale, keyboard interaction, or assistive technology materially harder later?

---

## How to promote these into canonical rules

Do not add all fourteen to `CLAUDE.md` merely because they sound sensible.

Use the repository's evidence-based lifecycle:

> **Idea → Issue → Review → Implement → Observe → Learn → Document → Reuse**

For each candidate rule:

1. identify a real failure, near miss, or repeated review finding;
2. decide whether the principle is general enough to recur;
3. define the desired outcome or metric where possible;
4. add the smallest useful wording to repository instructions;
5. add a Reviewer question or quality gate if judgment is required;
6. automate only where the check is objective and safe; and
7. remove or revise rules that do not improve outcomes.

## Highest-priority candidates

Based on the failures already encountered in Fido, the strongest candidates to promote next are:

1. **Avoid unnecessary runtime dependencies.**
2. **Treat external systems as unreliable.**
3. **Design to explicit performance/latency goals.**
4. **Make retries idempotent by default.**
5. **Bound work for 10×/100× scale.**
6. **Make observability part of feature design.**
7. **Centralize configuration and policy.**

These are common places where an implementation can be locally correct while creating avoidable production risk.

---

Created by **Kevin J. Mireles** as part of *From Vibe Coding to Production / Vibe Coding Learnings*. Licensed for reuse under CC BY 4.0; attribution is required when sharing or adapting this work.