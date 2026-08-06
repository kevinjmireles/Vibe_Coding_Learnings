# From Vibe Coding to Production

> Lessons learned, tips, tricks, and tools from my journey from novice vibe coder to mobile-first, AI-enabled software developer.

## Why this repository exists

About a year ago, I was not a programmer. I did, however, have nearly three decades of experience leading software and product initiatives at startups and global companies, including FedEx. I had seen what it takes to build scalable software—and hundreds of ways software projects fail.

AI suddenly made it possible for me to participate directly in implementation. For the first few weeks, that felt almost magical. Then I tried to deploy, everything blew up, and several days of “one more fix” made it clear that AI had not eliminated the need for software engineering.

I did not begin with a deliberate methodology. Most improvements came from frustration: something failed, duplicated, drifted, became impossible to transfer between devices, or produced a result I could not trust. I then introduced a system or rule to make that class of failure less likely to recur.

This repository documents that evolution.

> **Vibe gets you started. Systems get you to production.**

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

## Process evolution

The current process is more useful when readers can see how it developed and which failures caused each change.

- [Process Evolution Index](evolution/README.md)
- [Prompt Evolution](evolution/prompt-evolution.md)
- [Issue Evolution](evolution/issue-evolution.md)
- [Pull Request Evolution](evolution/pr-evolution.md)
- [Repository Instructions Evolution](evolution/claude-md-evolution.md)
- [Testing Evolution](evolution/testing-evolution.md)
- [Documentation Evolution](evolution/documentation-evolution.md)

Future revisions will add direct comparisons of representative production artifacts such as PR #1, #100, #200, #300, and later milestones, along with sample issues and the current issue and PR templates.

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

This did not begin as a mobile strategy. Work performed with Claude and Cursor on a laptop did not reliably appear when I moved to mobile, and mobile work could leave the laptop repository out of sync. Claude mobile also made copying an entire long response difficult. Repeated synchronization and copy-and-paste frustration pushed the authoritative work into GitHub.

The result was not merely a better phone workflow. It was a more cloud-based, documented, modular, and reproducible engineering process on every device.

## Who this is for

This repository may be useful to non-programmers building with AI, product managers and founders, publishers exploring AI-enabled development, experienced developers evaluating AI-native workflows, and organizations trying to increase development speed without abandoning quality.

## Current status

This is a living collection of working drafts extracted from real Fido development experiences. The next step is to add concrete production examples showing the evolution of pull requests, issues, templates, tests, and repository instructions over time.