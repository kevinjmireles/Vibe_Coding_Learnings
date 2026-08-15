# 020 — Check Before You Hand-Roll It

## AI suffers from Builderitis

AI loves to build.

Give it a problem and it will happily start writing code. It does not particularly care whether it is building something genuinely new, recreating something that already exists elsewhere in your own repository, or reinventing a wheel that thousands of developers solved years ago.

Unless you explicitly tell it to check first, **it will often just build.**

I discovered this after spending two or three days working through Fido's new maps. We were building maps, fixing maps, checking maps on different devices, fixing them again, and I was manually looking at map after map trying to figure out whether they rendered correctly.

Eventually I found myself wondering:

> **Why the hell am I spending this much time checking something that must have been solved before?**

So I asked.

And, sure enough, it had.

Our `CountyBoundaryChoropleth.tsx` component contained custom geographic projection and viewport-fitting math: `lonLatToWebMercator`, `makeProjector`, and `computeViewBox`.

It worked — until it didn't.

PR #652 had to fix a real mobile letterboxing problem. A narrow state such as Delaware could occupy only about 39% of the available map width because our custom fitting logic used a fixed-aspect-ratio box instead of fitting the viewport to the state's actual geometry.

Then we discovered that `d3-geo`, a small and extremely well-established open-source library, already provides `geoFitExtent` and `geoFitSize` for essentially this exact problem.

We had spent days building, testing, debugging, and reviewing custom code for a problem we probably never needed to solve ourselves.

## Builderitis isn't stupidity

This wasn't because the AI did a bad job.

That's what makes the lesson important.

The AI did exactly what we asked it to do: **build a map.**

Writing projection math was a perfectly coherent way to accomplish the assignment. Modern coding agents are so capable that writing a few more functions barely feels expensive while they're doing it.

The expense comes later.

Now we own the code. We have to test it. Debug it. Review it. Make it work on Delaware and Texas, desktop and mobile, and whatever comes next.

> **AI makes creating new code extraordinarily cheap. It does not make owning unnecessary code free.**

And that's Builderitis.

## There are two kinds

I had already encountered one form of Builderitis.

**Internal Builderitis:** AI rebuilds something that already exists inside your own system.

That's what [AI Defaults to Duplication](003-ai-defaults-to-duplication.md) is about.

This map experience exposed another.

**External Builderitis:** AI builds something from scratch that a mature external library already solves.

The remedy is similar in both cases:

> **Check before you build.**

Before creating something non-trivial:

1. **Look inward:** Does our repository already have something we should reuse or extend?
2. **Look outward:** Is there a mature, appropriately sized, well-maintained library that already solves this?
3. **Then decide:** Reuse, adopt, or hand-roll deliberately — and document why.

## Why this happens

AI agents are especially prone to Builderitis because writing code is easy for them.

Given "render county boundaries as an SVG map," hand-rolling projection math is a completely reasonable, locally coherent path. It produces working, testable code that does what was asked. Nothing about that task necessarily forces the agent to ask whether a battle-tested library already exists for the sub-problem.

This is a different flavor of the duplication problem in [Lesson 003](003-ai-defaults-to-duplication.md). That lesson is about rebuilding something that already exists *inside your own codebase*. This lesson is about rebuilding something that already exists *outside it*.

## The system introduced

Rather than fix just this one file, the lesson became a standing rule, applied symmetrically to both roles:

- **Builder-facing:** before starting non-trivial hand-rolled work — geographic/geometric math, date/timezone handling, parsing/formatting, scheduling, and similar already-solved mechanisms — check whether a small, well-maintained package already solves it.
- **Reviewer-facing:** ask the same question again independently at sign-off, regardless of whether the Builder already asked it.

The rule does not mandate an outcome. It mandates a documented decision: adopted, considered-and-declined, or not applicable.

A dependency is not automatically better than hand-rolled code. A two-line date comparison does not need a package, and every dependency carries its own footprint, maintenance surface, and security exposure. The rule's job is to make the comparison happen on purpose, not to pick a side.

The actual library-adoption decision — whether to adopt `d3-geo` — was deliberately *not* made in the same change. It was folded into the larger issue already rebuilding the map-geometry pipeline end to end. Whoever touches that code will decide server-side versus client-side rendering at the same time. That is the same architectural decision, better made once than twice.

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