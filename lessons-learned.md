# Lessons Learned at a Glance

This page is an index, not a second copy of the lessons. Each topic has one canonical document in `docs/`.

1. [There Is No Vibe in Production](docs/001-there-is-no-vibe-in-production.md) — AI can accelerate implementation, but production requires systems, evidence, and discipline.
2. [The Repository Should Remember More Than the AI](docs/002-the-repository-should-remember-more-than-the-ai.md) — durable knowledge belongs in version control, not only in conversations.
3. [AI Defaults to Duplication](docs/003-ai-defaults-to-duplication.md) — require reuse or extension of existing systems before creating parallel ones.
4. [Separate Builder, Reviewer, and Steward](docs/004-separate-builder-reviewer-and-steward.md) — creation and validation should be independent reasoning steps.
5. [Regression Tests Are Compounding Assets](docs/005-regression-tests-are-compounding-assets.md) — every discovered defect can become a permanent safeguard.
6. [The Repository Replaced My Laptop](docs/006-the-repository-replaced-my-laptop.md) — the shared repository, not a particular workstation, became the authoritative place where the project lives.
7. [Document Everything Worth Remembering](docs/007-document-everything-worth-remembering.md) — documentation is part of the product's operating system.
8. [Small, Self-Contained Issues Scale Better](docs/008-small-self-contained-issues-scale-better.md) — bounded work improves implementation, review, and recovery.
9. [Audit Before You Refactor](docs/009-audit-before-you-refactor.md) — inventory the real problem before standardizing or rebuilding it.
10. [Systems Catch What People Miss](docs/010-systems-catch-what-people-miss.md) — overlapping controls catch different classes of failure.
11. [Every Manual Step Eventually Belongs in GitHub](docs/011-every-manual-step-eventually-belongs-in-github.md) — repeated reminders should become templates, checks, or required workflow steps.
12. [How I Failed My Way into Mobile Software Development](docs/012-how-i-failed-my-way-into-mobile-software-development.md) — practical life constraints and recurring frustration accidentally produced a mobile-first workflow.
13. [Build a Team, Even If You Are the Only Person](docs/013-build-a-team-even-if-you-are-the-only-person.md) — one human can orchestrate multiple independent engineering functions without trusting any single person or AI to get everything right.
14. [GitHub Actions Turn Rules into Guardrails](docs/014-github-actions-turn-rules-into-guardrails.md) — convert important process rules from reminders into automated checks and, where appropriate, merge-blocking gates.
15. [Build Production Test Tools, Not Just Tests](docs/015-build-production-test-tools-not-just-tests.md) — reusable diagnostic tools let you exercise many datasets, geographies, locales, and production paths instead of rebuilding the test process each time.
16. [Change It Once](docs/016-change-it-once.md) — centralize truly shared behavior so one fix can improve many outputs without creating drift.
17. [If It Matters, Give It a Metric](docs/017-if-it-matters-give-it-a-metric.md) — vague goals get lost in fast-moving AI work; observable targets, including zero, don't.
18. [AI Will Not Invent Your Best Practices for You](docs/018-ai-will-not-invent-your-best-practices-for-you.md) — a technically valid implementation can still be the wrong architecture; the repository has to teach the better pattern explicitly.
19. [You Don't Add Technical Debt, You Multiply It](docs/019-you-dont-add-technical-debt-you-multiply-it.md) — duplication's maintenance and drift cost grows with every copy, not by one item at a time.
20. [Check Before You Hand-Roll It](docs/020-check-before-you-hand-roll-it.md) — before writing non-trivial mechanism code, check whether a well-maintained library already solved it.
21. [Is the Juice Worth the Squeeze?](docs/021-is-the-juice-worth-the-squeeze.md) — optimize the product as a whole, not one dimension in isolation; consciously weigh evidence, reversibility, future pain, and opportunity cost before adding complexity.

For readers looking for the smallest useful starting point, see [Steal This: Five Practices to Copy First](principles/steal-this.md).