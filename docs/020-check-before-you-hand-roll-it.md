# 020 — Check Before You Hand-Roll It

## The problem

`CountyBoundaryChoropleth.tsx` hand-rolled its own geographic projection and viewport-fitting math from scratch — `lonLatToWebMercator`, `makeProjector`, `computeViewBox` — to turn Census county boundary coordinates into an SVG map. It worked. A later fix (PR #652) had to patch a real bug in it: mobile letterboxing, where a narrow state like Delaware filled only ~39% of the available map width because the hand-rolled fitting logic used a fixed-aspect-ratio box instead of fitting each state's actual geometry.

The fix worked. The question that mattered came after the fix, not during it: *"seems like a lot of work for something that should already be solved for."*

It was right. `d3-geo` — a small, extremely well-established open-source library — has functions (`geoFitExtent`, `geoFitSize`) that solve exactly this problem: fitting arbitrary geographic geometry into a target viewport. Three custom functions and a real bug were built to reinvent something a widely-used library already does correctly.

## Why this happens

Same root cause as duplication generally (see [003](003-ai-defaults-to-duplication.md)), but a different flavor of it. That lesson is about rebuilding something that already exists *inside your own codebase*. This is about rebuilding something that already exists *outside it*, in a package you could just install.

AI agents are especially prone to this version of the problem because writing the code is easy. Given "render county boundaries as an SVG map," hand-rolling projection math is a completely reasonable, locally coherent path — it produces working, testable code that does what was asked. Nothing about the task description flags that a battle-tested library already exists for exactly this sub-problem. The AI has no innate sense that "this specific kind of math has a canonical open-source solution" unless told to check.

## The system introduced

Rather than fix just this one file, the fix became a standing rule, applied symmetrically to both roles:

- **Builder-facing:** before starting non-trivial hand-rolled work — geographic/geometric math, date/timezone handling, parsing/formatting, scheduling, and similar already-solved mechanisms — check whether a small, well-maintained package already solves it.
- **Reviewer-facing:** the same question, asked again independently at sign-off, regardless of whether the Builder already asked it.

The rule does not mandate an outcome. It mandates a documented decision: adopted, considered-and-declined, or not applicable. A dependency is not automatically better than hand-rolled code — a two-line date comparison doesn't need a package, and every dependency carries its own footprint, maintenance surface, and security exposure. The rule's job is to make the comparison happen on purpose, not to pick a side.

The actual library-adoption decision (whether to adopt `d3-geo`) was deliberately *not* made in the same change. It was folded into the larger issue already rebuilding the map-geometry pipeline end to end — whoever touches that code will decide server-side vs. client-side rendering at the same time, and that's the same decision, better made once than twice.

## Distinct from a nearby lesson

This project's map-rendering saga produced two lessons that are easy to conflate because they touch the same file:

- [AI Will Not Invent Your Best Practices for You](018-ai-will-not-invent-your-best-practices-for-you.md) is about *where* a computation happens — should this run synchronously against a third-party API at request time, or be precomputed and cached?
- This lesson is about *whether the computation should be written at all* — does a well-maintained library already solve this exact math?

Both questions are worth asking about the same piece of code. Neither substitutes for the other.

## Reusable takeaway

> **Before you hand-roll a non-trivial mechanism, ask whether someone already solved it well. If you decide to build it anyway, write down why.**

The AI will happily write the code either way. Deciding whether that code should exist at all is still a human-shaped question — or, once the check itself is written into the repository, an increasingly automatic one.

---

Created by **Kevin J. Mireles** as part of *From Vibe Coding to Production / Vibe Coding Learnings*. Licensed for reuse under CC BY 4.0; attribution is required when sharing or adapting this work.