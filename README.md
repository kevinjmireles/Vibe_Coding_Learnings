# From Vibe Coding to Production

> Lessons learned, tips, tricks, and tools from my journey from novice vibe coder to mobile-first, AI-enabled software developer.

## Why this repository exists

About a year ago, I was not a programmer. I did, however, have nearly three decades of experience leading software and product initiatives at startups and global companies, including FedEx. I had seen what it takes to build scalable software—and hundreds of ways software projects fail.

AI suddenly made it possible for me to participate directly in implementation. For the first few weeks, that felt almost magical. Then I tried to deploy, everything blew up, and several days of “one more fix” made it clear that AI had not eliminated the need for software engineering.

I did not begin with a deliberate methodology. Most improvements came from frustration: something failed, duplicated, drifted, became impossible to transfer between devices, or produced a result I could not trust. I then introduced a system or rule to make that class of failure less likely to recur.

This repository documents that evolution.

> **Vibe gets you started. Systems get you to production.**

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
6. [Cloud-First Was Born from Frustration](docs/006-cloud-first-was-born-from-frustration.md)
7. [Document Everything Worth Remembering](docs/007-document-everything-worth-remembering.md)
8. [Small, Self-Contained Issues Scale Better](docs/008-small-self-contained-issues-scale-better.md)
9. [Audit Before You Refactor](docs/009-audit-before-you-refactor.md)
10. [Systems Catch What People Miss](docs/010-systems-catch-what-people-miss.md)
11. [Every Manual Step Eventually Belongs in GitHub](docs/011-every-manual-step-eventually-belongs-in-github.md)
12. [How I Failed My Way into Mobile Software Development](docs/012-how-i-failed-my-way-into-mobile-software-development.md)
13. [Build a Team, Even If You Are the Only Person](docs/013-build-a-team-even-if-you-are-the-only-person.md)

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

The full story lives in [How I Failed My Way into Mobile Software Development](docs/012-how-i-failed-my-way-into-mobile-software-development.md). The reusable process lesson lives separately in [Cloud-First Was Born from Frustration](docs/006-cloud-first-was-born-from-frustration.md).

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