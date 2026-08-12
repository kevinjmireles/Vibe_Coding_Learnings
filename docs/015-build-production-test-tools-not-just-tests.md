# Build Production Test Tools, Not Just Tests

## Failure pattern

As the product became more data-heavy, unit tests and one-off manual checks were no longer enough.

A feature could work for one dataset, geography, locale, or time period and still fail somewhere else. Many problems only appeared when real production paths interacted: fresh versus stale data, state versus county logic, one FIU versus another, English versus Spanish, or different subscriber configurations.

Manually reproducing those combinations became slow and unreliable.

## Why it happened

Traditional automated tests are good at proving specific behaviors. They are less useful when a human needs to repeatedly explore many combinations of real or production-shaped data.

Without reusable diagnostic tools, every investigation risks becoming a custom exercise:

- write a new SQL query;
- hand-build a test CSV;
- trigger a special send;
- inspect one geography at a time;
- compare outputs manually;
- reconstruct the same test setup later.

That does not scale.

## System or process introduced

The project increasingly treated internal testing capability as production infrastructure.

Examples include:

- token and FIU test tools;
- admin previews that exercise real rendering paths;
- CSV templates that can test many geographies or cases at once;
- reusable SQL and diagnostic queries;
- integration tests that run through real resolution paths rather than isolated helpers;
- multi-locale validation;
- real-data or production-shaped checks where mocks are not sufficient;
- test sends containing many FIUs together so cross-component inconsistencies are visible.

The goal is not merely to add more automated tests. It is to build repeatable tools that let a human or AI inspect the system across many datasets and edge conditions without inventing a new testing method every time.

## How it helped

Reusable test surfaces shorten the feedback loop.

A new dataset, FIU, geography, language, or customer configuration can be exercised against an existing harness instead of requiring bespoke validation.

They also expose problems that isolated unit tests can miss because the same production path is used repeatedly across different combinations of data.

The test infrastructure becomes a product capability in its own right.

## Caution

Do not confuse a diagnostic tool with proof that the system is correct.

Internal test surfaces complement, rather than replace:

- unit tests;
- regression tests;
- integration tests;
- CI;
- independent review; and
- real user-facing validation.

A test harness can make investigation faster, but the underlying behavior still needs objective protection.

## Reusable takeaway

**Test the system, not just the feature.**

When a product handles many datasets, geographies, locales, or configurations, invest in reusable production-oriented testing tools that can exercise many combinations through the same paths real users depend on.

The best test tool is one you can reuse for the next ten datasets instead of rebuilding the test process ten times.