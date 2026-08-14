# 017 — If It Matters, Give It a Metric

## The problem

Important intentions are surprisingly easy to lose inside a fast-moving AI-assisted development process.

A team can say that performance matters, reviews should be fast, documentation should stay current, duplication should be avoided, or a workflow should have no unnecessary delay. But if the expectation is only prose, it competes with every other instruction in the repository.

AI agents are especially good at satisfying the requirements that are explicit and easy to verify. Vague aspirations are much easier to overlook.

## What I learned

If something genuinely matters, define the desired outcome clearly enough that a human, an AI agent, or an automated check can tell whether it happened.

A particularly useful pattern is to define the ideal state as **zero** whenever zero is actually the goal.

For example:

- unnecessary waiting: **0**
- known unresolved critical regressions at merge: **0**
- undocumented intentional architecture exceptions: **0**
- avoidable duplicate implementations of one canonical behavior: **0**

"Minimize waiting" is an aspiration. **Zero unnecessary wait** is a target.

The point is not that every metric must literally be zero. The point is that important expectations need an observable definition of success.

## Why this matters with AI

AI can move quickly enough that soft requirements disappear beneath implementation detail.

If the instruction says "keep this fast," an agent can reasonably decide that a small delay is acceptable. If the requirement says "the target is zero unnecessary wait between these stages," the agent has something concrete to design and review against.

The same applies to people. Clear goals reduce interpretation, make reviews more objective, and make recurring failures easier to identify.

## From aspiration to guardrail

A useful progression is:

> **Value → goal → metric → evidence → guardrail**

For example:

1. **Value:** We do not want process overhead slowing development.
2. **Goal:** Work should move immediately when no real dependency exists.
3. **Metric:** Zero unnecessary wait between eligible workflow stages.
4. **Evidence:** Measure or inspect where work sits idle and why.
5. **Guardrail:** Automate handoffs or flag avoidable waiting when practical.

Not every goal needs a dashboard or GitHub Action. But every important goal should be specific enough to review.

## Measure outcomes, not bureaucracy

Metrics can create their own failure modes. A bad metric can reward gaming, encourage unnecessary process, or optimize the measurable thing instead of the useful thing.

Use metrics when they clarify an important outcome. Do not invent measurements simply because they are measurable.

Ask:

- What behavior are we trying to protect?
- What would success look like?
- Can we tell objectively when we missed it?
- Is the metric measuring the outcome or merely activity?
- Can the target be enforced automatically, or does it require judgment?

## Reusable takeaway

> **If it matters, give it a goal. If the goal can be measured, give it a metric. If the metric can be enforced safely, turn it into a guardrail.**

And when the true desired state is none:

> **Say zero.**

"Reduce," "minimize," and "try to avoid" are easy to overlook. A clear target is much harder to accidentally ignore.

---

Created by **Kevin J. Mireles** as part of *From Vibe Coding to Production / Vibe Coding Learnings*. Licensed for reuse under CC BY 4.0; attribution is required when sharing or adapting this work.