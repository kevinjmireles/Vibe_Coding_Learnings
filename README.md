# From Vibe Coding to Production

> Lessons learned, tips, tricks, and tools from my journey from novice vibe coder to mobile-first, AI-enabled software developer.

## Why this repository exists

About a year ago, I was not a software engineer. I had product ideas, experience defining problems and building solutions, and growing curiosity about whether AI could help me create software that previously would have required a development team.

I did not begin with a deliberate engineering methodology. For much of the journey, I did not know what I was doing. I encountered problems, made mistakes, discovered weaknesses in my process, and then built systems to keep those problems from recurring.

Over time, that reactive learning became a much more disciplined development process. I moved from asking AI to produce features toward managing a production application through documented architecture, independent review, regression testing, reusable components, operational safeguards, and durable institutional memory.

This repository documents that evolution.

It is not intended to be a definitive guide to AI-assisted software development. It is a practical record of:

- mistakes and issues I encountered;
- why those problems occurred;
- systems and processes I introduced in response;
- how those changes improved speed, quality, and confidence;
- lessons that may be reusable by other builders, publishers, and organizations.

Everything here comes from building and operating a real product rather than from toy projects or theoretical exercises.

## The recurring pattern

Most lessons in this repository follow the same structure:

1. **Mistake or issue encountered** — what went wrong or became difficult.
2. **Why it happened** — the underlying process, architecture, or communication gap.
3. **System or process introduced** — what changed to reduce the chance of recurrence.
4. **How it helped** — the practical impact on development.
5. **Reusable takeaway** — what another person or organization could adopt.

This framing is intentional. Most of the improvements were not part of a master plan. They emerged because the existing process failed in a visible way.

## What this repository will cover

- Moving from loosely defined requests to structured GitHub issues
- Separating AI Builder, Reviewer, and Steward responsibilities
- Making the repository—not an AI chat—the source of truth
- Using architecture documents and decision records
- Building regression tests around discovered failures
- Requiring evidence rather than accepting “looks good”
- Treating documentation as part of the product
- Preventing repeated one-off implementations
- Improving security, backups, and operational readiness
- Designing work so it can be completed almost entirely from a phone
- Coordinating multiple AI models without losing context
- Simplifying prompts by moving durable instructions into the repository

## Mobile-first development

One unexpected result of these process improvements is that I can now do nearly all development work from an iPhone.

That does not mean manually typing every line of code on a phone. It means managing the full development lifecycle from a mobile device:

- defining and refining issues;
- making product and architecture decisions;
- directing AI implementation;
- reviewing pull requests;
- evaluating tests and CI results;
- documenting decisions;
- requesting revisions;
- merging completed work.

In one recent week, I worked through roughly 30 pull requests primarily from my phone.

The phone did not create this workflow by itself. It exposed every part of the process that depended too heavily on a local machine, an oversized prompt, one AI conversation, or information held only in my head. Making the workflow mobile forced the project to become more cloud-based, documented, modular, and reproducible.

The result was not merely a better mobile workflow. It was a better engineering workflow on every device.

## Who this is for

This repository may be useful to:

- non-engineers beginning to build with AI;
- product managers and founders creating their first software products;
- publishers exploring AI-enabled product development;
- experienced developers evaluating AI-native workflows;
- organizations trying to preserve quality while increasing development speed;
- anyone attempting to move from experimental vibe coding toward dependable production software.

## Current status

This is a living collection. It will grow as earlier conversations, decisions, mistakes, and improvements are extracted and documented.

Start with [Lessons Learned](lessons-learned.md).