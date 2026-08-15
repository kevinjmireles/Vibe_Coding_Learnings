# From Vibe Coding to Production

> Lessons learned, tips, tricks, and tools from my journey from novice vibe coder to mobile-first, AI-enabled software developer.

## Why this repository exists

About a year ago, I was not a programmer. I did, however, have nearly three decades of experience leading software and product initiatives at startups and global companies, including FedEx. I had seen what it takes to build scalable software—and hundreds of ways software projects fail.

AI suddenly made it possible for me to participate directly in implementation. For the first few weeks, that felt almost magical. Then I tried to deploy, everything blew up, and several days of “one more fix” made it clear that AI had not eliminated the need for software engineering.

I did not begin with a deliberate methodology. Most improvements came from frustration: something failed, duplicated, drifted, became impossible to transfer between devices, or produced a result I could not trust. I then introduced a system or rule to make that class of failure less likely to recur.

This repository documents that evolution.

> **Vibe gets you started. Systems get you to production.**

## The thesis: AI needs management

Coding agents can be brilliant individual contributors. But brilliance is not a development process.

Left largely unmanaged, agents can make locally reasonable decisions, duplicate existing systems, miss architectural implications, apply inconsistent standards, and produce technically functional solutions that are wrong for production.

The central lesson from building Fido has been that **AI does not eliminate the need for management. It increases the value of good management.**

The goal of this project is to capture the layer that coding tools largely leave to you: goals, architecture, best practices, roles, repository memory, bounded assignments, independent review, testing, quality gates, evidence, and organizational learning.

You do not necessarily need to know how to write the code. But somebody—or some system—must define and continually improve **what good looks like**.

> **The difference between a collection of brilliant AI agents and an effective engineering team is the system that manages them.**

### How the pieces work together

The system is not one magic prompt. It is a set of components that reinforce one another:

1. **Goals and metrics define the outcome.** Clear targets tell agents what success means. When the real target is zero—zero unnecessary wait, zero avoidable runtime dependencies, zero known critical regressions—say zero rather than “minimize.”
2. **Architectural principles and best practices define what good looks like.** AI does not automatically arrive with the right production architecture for your product. Important practices need to be discovered, challenged, documented, and made explicit.
3. **The repository provides durable memory.** Requirements, architecture, decisions, lessons, and rules should survive individual chats, agents, devices, and sessions. The repository remembers more than the AI.
4. **Issues turn goals into bounded assignments.** Instead of giant conversational prompts, a well-structured issue defines the problem, context, constraints, acceptance criteria, and evidence expected. The working prompt can become as short as `Build #563.`
5. **Specialized roles create separation of duties.** Builder, Reviewer, and Architecture Steward agents have different responsibilities. The agent that created the work should not be the only agent deciding whether the work is good enough.
6. **Independent review challenges locally reasonable decisions.** Review is not just syntax checking. It asks whether the implementation duplicates something, violates architecture, introduces avoidable dependencies, misses edge cases, or solves the wrong problem.
7. **Tests and production test tools provide evidence.** Unit and regression tests catch known failure modes; reusable production-oriented tools exercise multiple datasets, geographies, locales, channels, and real system paths.
8. **GitHub Actions and required gates enforce the floor.** Templates remind. Actions verify. Required checks can block. Human judgment still decides whether the result is actually good.
9. **Shared components reduce future work and drift.** Behavior that is genuinely the same should have one canonical owner. Otherwise technical debt multiplies across every dataset, geography, language, channel, and future change.
10. **Failures improve the system.** A recurring problem should not merely be fixed once. The durable path is **Idea → Issue → Review → Implement → Observe → Learn → Document → Reuse**. When appropriate, the lesson becomes a rule, test, quality gate, shared primitive, or template that future agents inherit.

The result is a feedback loop:

```text
Raw AI capability
        ↓
Goals + metrics
        ↓
Architecture + best practices
        ↓
Repository memory
        ↓
Bounded issues
        ↓
Builder / Reviewer / Steward roles
        ↓
Tests + production evidence
        ↓
GitHub Actions + quality gates
        ↓
Human judgment
        ↓
Lessons fed back into the system
        ↺
```

A mistake therefore has the potential to become organizational learning rather than merely another bug fix:

> **Failure → lesson → rule → test or gate → future agents inherit the learning.**

That is the larger purpose of the practices in this repository: turn capable but uneven AI individual contributors into a more disciplined, evidence-driven development team with increasingly predictable outcomes.

## New to this? Start here

You do not need to understand CI, branch protection, or software architecture to use the core lessons.

The simplest version is:

1. **Do not let important knowledge live only in an AI conversation.** Put requirements, decisions, and lessons in a shared repository.
2. **Do not trust one person or AI to create and validate the same work.** Use independent implementation and review roles.
3. **When the same failure happens twice, turn the lesson into a rule, test, template, or automated check.**

For the five practices with the fastest payoff, see [Steal This](principles/steal-this.md). For the personal story behind the mobile-first workflow, see [How I Failed My Way into Mobile Software Development](docs/012-how-i-failed-my-way-into-mobile-software-development.md).

## Failure patterns and lessons

1. [There Is No Vibe in Production](docs/001-there-is-no-vibe-in-production.md)
2. [The Repository Should Remember More Than the AI](docs/002-the-repository-should-remember-more-than-the-ai.md)
3. [AI Defaults to Duplication](docs/003-ai-defaults-to-duplication.md)
4. [Separate Builder, Reviewer, and Steward](docs/004-separate-builder-reviewer-and-steward.md)
5. [Regression Tests Are Compounding Assets](docs/005-regression-tests-are-compounding-assets.md)
6. [The Repository Replaced My Laptop](docs/006-the-repository-replaced-my-laptop.md)
7. [Document Everything Worth Remembering](docs/007-document-everything-worth-remembering.md)
8. [Small, Self-Contained Issues Scale Better](docs/008-small-self-contained-issues-scale-better.md)
9. [Audit Before You Refactor](docs/009-audit-before-you-refactor.md)
10. [Systems Catch What People Miss](docs/010-systems-catch-what-people-miss.md)
11. [Every Manual Step Eventually Belongs in GitHub](docs/011-every-manual-step-eventually-belongs-in-github.md)
12. [How I Failed My Way into Mobile Software Development](docs/012-how-i-failed-my-way-into-mobile-software-development.md)
13. [Build a Team, Even If You Are the Only Person](docs/013-build-a-team-even-if-you-are-the-only-person.md)
14. [GitHub Actions Turn Rules into Guardrails](docs/014-github-actions-turn-rules-into-guardrails.md)
15. [Build Production Test Tools, Not Just Tests](docs/015-build-production-test-tools-not-just-tests.md)
16. [Change It Once](docs/016-change-it-once.md)
17. [If It Matters, Give It a Metric](docs/017-if-it-matters-give-it-a-metric.md)
18. [AI Will Not Invent Your Best Practices for You](docs/018-ai-will-not-invent-your-best-practices-for-you.md)
19. [You Don’t Add Technical Debt, You Multiply It](docs/019-you-dont-add-technical-debt-you-multiply-it.md)
20. [Check Before You Hand-Roll It](docs/020-check-before-you-hand-roll-it.md)

A concise linked index is also available in [Lessons Learned at a Glance](lessons-learned.md).

## Process evolution

The current process is more useful when readers can see how it developed and which failures caused each change.

- [Process Evolution Index](evolution/README.md)
- [Prompt Evolution](evolution/prompt-evolution.md)
- [Issue Evolution](evolution/issue-evolution.md)
- [Pull Request Evolution](evolution/pr-evolution.md)
- [Repository Instructions Evolution](evolution/claude-md-evolution.md)
- [Testing Evolution](evolution/testing-evolution.md)
- [Documentation Evolution](evolution/documentation-evolution.md)

Representative production pull requests are archived in [evolution/sample-prs](evolution/sample-prs/README.md). Because GitHub issues and pull requests share one numbering sequence, the archive uses real PRs that best show the process at different stages rather than forcing round-number milestones that may be issues instead of pull requests.

## Reusable toolkit

### Start here

- [Reusable AI Development Instructions](templates/AI_INSTRUCTIONS.md)
- [AI Development Roles](roles/agent-roles.md)
- [Quality Gates](rules/quality-gates.md)
- [Reusable Principles](principles/README.md)
- [Steal This: Five Practices to Copy First](principles/steal-this.md)
- [Missing Best Practices Audit](audits/missing-best-practices.md)

### Copy-ready prompts and templates

- [Core Prompts](prompts/core-prompts.md)
- [Issue Template](templates/issue-template.md)
- [Pull Request Template](templates/pull-request-template.md)

The prompts now reflect the real workflow: `Document this.`, `Build #563.`, or `Review PR #571.` Stable rules belong in version-controlled repository files; prompts identify the current assignment.

## The recurring format

Each lesson generally follows the same structure:

1. **Failure pattern** — what went wrong or became difficult.
2. **Why it happened** — the underlying process, architecture, or communication gap.
3. **System or process introduced** — what changed to reduce recurrence.
4. **How it helped** — the practical impact.
5. **Reusable takeaway** — what another builder or organization can apply.

## Mobile-first development

One unexpected result is that I can now manage nearly the full development lifecycle from an iPhone: defining issues, making architecture decisions, directing implementation, reviewing pull requests, evaluating tests and CI, documenting decisions, requesting revisions, and merging completed work.

In one recent week, I worked through roughly 30 pull requests primarily from my phone.

This did not begin as a mobile strategy. It emerged from device-sync problems, copy-and-paste pain, limited desktop time, discomfort with terminal workflows, and a desire to act on middle-of-the-night ideas without getting out of bed and waking my wife.

The full personal story lives in [How I Failed My Way into Mobile Software Development](docs/012-how-i-failed-my-way-into-mobile-software-development.md). The reusable systems lesson lives separately in [The Repository Replaced My Laptop](docs/006-the-repository-replaced-my-laptop.md).

## Who this is for

This repository may be useful to non-programmers building with AI, product managers and founders, publishers exploring AI-enabled development, experienced developers evaluating AI-native workflows, and organizations trying to increase development speed without abandoning quality.

## About the author and project

I am **Kevin J. Mireles**, the only human developer and product owner behind this process. I still do not write code myself. I use AI agents, GitHub, tests, CI, documentation, and structured review to recreate many of the functions of a software team while retaining human responsibility for product judgment and final decisions.

These lessons were developed while building **[Your Friend Fido](https://www.yourfriendfido.com)**, a personalized civic and local-information platform.

- [Kevin Mireles on GitHub](https://github.com/kevinjmireles)
- [Your Friend Fido](https://www.yourfriendfido.com)

## Reuse

The original lessons, prompts, checklists, and templates are available under the [Creative Commons Attribution 4.0 International License](LICENSE.md). You may copy and adapt them with attribution.

## Current status

This is a living collection of working drafts extracted from real Fido development experiences. The next step is to keep adding production evidence, reusable examples, and lessons as new failure patterns emerge.