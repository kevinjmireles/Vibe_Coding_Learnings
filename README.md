# From Vibe Coding to Production

> Lessons learned, tips, tricks, and tools from my journey from novice vibe coder to mobile-first, AI-enabled software developer.

## Why this repository exists

About a year ago, I was not a programmer. I did, however, have nearly three decades of experience leading software and product initiatives at startups and global companies, including FedEx. I had seen what it takes to build scalable software—and hundreds of ways software projects fail.

AI suddenly made it possible for me to participate directly in implementation. For the first few weeks, that felt almost magical. Then I tried to deploy, everything blew up, and several days of “one more fix” made it clear that AI had not eliminated the need for software engineering.

I did not begin with a deliberate methodology. Most improvements came from frustration: something failed, duplicated, drifted, became impossible to transfer between devices, or produced a result I could not trust. I then introduced a system or rule to make that class of failure less likely to recur.

This repository documents that evolution.

The thesis is not that vibe coding is bad. It is simpler:

> **Vibe gets you started. Systems get you to production.**

## Initial failure patterns and lessons

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

## The recurring format

Each page generally follows the same structure:

1. **Failure pattern** — what went wrong or became difficult.
2. **Why it happened** — the underlying process, architecture, or communication gap.
3. **System or process introduced** — what changed to reduce recurrence.
4. **How it helped** — the practical impact.
5. **Reusable takeaway** — what another builder or organization can apply.

This framing is intentional. These practices were not invented as a polished methodology. They emerged from building and operating a real production product.

## Mobile-first development

One unexpected result is that I can now manage nearly the full development lifecycle from an iPhone:

- define and refine issues;
- make product and architecture decisions;
- direct AI implementation;
- review pull requests;
- evaluate tests and CI;
- document decisions;
- request revisions;
- merge completed work.

In one recent week, I worked through roughly 30 pull requests primarily from my phone.

This did not begin as a mobile strategy. Work performed with Claude and Cursor on a laptop did not reliably appear when I moved to mobile, and mobile work could leave the laptop repository out of sync. Claude mobile also made copying an entire long response difficult. Repeated synchronization and copy-and-paste frustration pushed the authoritative work into GitHub.

The result was not merely a better phone workflow. It was a more cloud-based, documented, modular, and reproducible engineering process on every device.

## Who this is for

This repository may be useful to:

- non-programmers beginning to build with AI;
- product managers and founders creating software products;
- publishers exploring AI-enabled product development;
- experienced developers evaluating AI-native workflows;
- organizations trying to preserve quality while increasing development speed;
- anyone moving from experimental vibe coding toward dependable production software.

## Current status

This is a living collection. The initial pages are working drafts extracted from real Fido development experiences. They will be refined, expanded, and supplemented with practical tools, examples, and checklists over time.

The earlier consolidated notes remain available in [Lessons Learned](lessons-learned.md).