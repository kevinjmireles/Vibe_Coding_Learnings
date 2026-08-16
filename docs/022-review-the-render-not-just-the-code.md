# 22. Review the Render, Not Just the Code

## Failure pattern

I had a pull request that compiled, deployed, and passed roughly 1,500 automated tests.

Then I opened the actual page on my phone.

The map was a giant pale-blue square with a tiny cluster of county geometry inside it.

Nothing in the code review or test suite had told me that the thing a user would actually see was obviously broken.

That was the moment the distinction became unavoidable: **code correctness and rendered correctness are not the same thing.**

For years, software teams have automated builds, unit tests, integration tests, security scans, and linting as part of pull-request review. But a user does not experience a passing test suite. A user experiences the rendered product.

If the rendered product matters, the render itself needs to become review evidence.

## Why it happened

Most software review systems are optimized around artifacts that machines understand easily:

- source-code diffs;
- type checking;
- unit and integration tests;
- build success;
- security and dependency scans;
- structured logs and status checks.

Those are essential, but they are indirect evidence for user-facing work.

A visualization can be technically valid and still be unusable. A page can return HTTP 200 and still look ridiculous. A responsive layout can pass every unit test and still collapse on a phone. Copy can be wired through the correct localization machinery and still show the wrong state's name.

The particular map failure that triggered this lesson came from geometry/projection behavior. The SVG existed. It had non-zero dimensions. The page loaded successfully. The automated tests were green. Yet the result was visibly wrong.

That meant adding more conventional assertions would not have solved the larger problem. We needed a way for reviewers to see what the browser actually rendered.

## System introduced

I turned rendered visual evidence into part of the pull-request workflow.

The basic pattern is:

```text
Pull request
    ↓
Preview deployment
    ↓
GitHub Actions
    ↓
Real browser via Playwright
    ↓
Open the deployed preview
    ↓
Capture mobile + desktop screenshots
    ↓
Run basic rendered-state / accessibility / diagnostics checks
    ↓
Upload screenshots and reports as GitHub Actions artifacts
    ↓
Human or AI reviewer retrieves and inspects the evidence
    ↓
Review comments → fix → redeploy → recapture → re-review
```

The important part is that the workflow tests the **real deployed preview**, not a mocked component in isolation.

In Fido, the first version used Playwright in GitHub Actions to:

1. wait for the Vercel preview deployment;
2. launch Chromium;
3. visit registered review routes;
4. capture full-page mobile and desktop screenshots;
5. verify that the expected primary visualization exists and has non-zero dimensions;
6. collect browser console and failed-network diagnostics;
7. run a basic Axe accessibility scan;
8. upload the screenshots and reports as GitHub Actions artifacts.

The artifacts could then be retrieved by an AI reviewer through GitHub and visually inspected in the same review loop as the code.

This is not the same as pixel-diff regression testing. I deliberately started with **evidence-first visual QA** rather than immediately creating a brittle collection of screenshot baselines.

The first goal was simpler: make sure the reviewer can reliably see what the user sees.

## What it caught

Once the rendered evidence existed, the visual-review loop caught problems that code review and green CI had missed:

### 1. A catastrophic renderer failure

The original map rendered as a giant blue rectangle even though the page loaded, the SVG existed, and the automated test suite passed.

### 2. The wrong implementation being reviewed

Our first visual-QA branch accidentally exercised an older renderer lineage. The screenshots looked fine—but they were proving the wrong thing. The review process caught that and moved the tests onto the actual renderer that had produced the defect.

That was a useful reminder that **evidence is only useful if it comes from the implementation you think you are testing.**

### 3. Hard-coded state-specific copy

Delaware and Missouri maps displayed Ohio-specific explanatory text, including references to 88 Ohio counties and Franklin County.

The data and maps were correct. The words were wrong.

Rendered review made the error obvious, and the fix became a parameterized localization path plus a regression test.

### 4. Letterboxing and wasted map space

A renderer rewrite had quietly reintroduced an earlier aspect-ratio problem. Delaware's geography was technically correct but squeezed into a fixed square canvas, wasting space and making labels unnecessarily small.

The screenshot exposed the regression. The fix changed the projection/viewBox logic rather than merely increasing font sizes.

### 5. Label collisions and readability problems

Missouri's St. Louis-area labels collided. Delaware's low-count labels were too small. The rendered evidence let us iterate on the shared label-placement and sizing system using real output rather than guessing from code.

### 6. Excess whitespace

Even after the map itself was correct, the mobile map card still felt unnecessarily tall. A human review of the live preview identified the remaining space-efficiency issue and led to a conservative padding adjustment.

At that point a more sophisticated convex-hull or population-weighted fitting approach was considered—and deliberately rejected.

The existing result already cleared the V1 visual bar. Building a more complex map-fitting system for a now-minor gap would have violated another lesson in this repository: **optimize against evidence, not possibility.**

## How it helped

This changed visual review from an occasional manual chore into a repeatable engineering capability.

Before:

- I manually opened preview links;
- checked pages one at a time on my phone;
- tried to remember which states and layouts needed review;
- described problems back to an AI agent;
- repeated the process after every fix.

After:

- the repository knows which pages are visual-QA scenarios;
- GitHub Actions runs a real browser against the deployed preview;
- screenshots are produced consistently at defined mobile and desktop sizes;
- the evidence is attached to the exact commit that produced it;
- AI and human reviewers can inspect the same artifacts;
- visual findings become PR comments, regression tests, shared fixes, and durable repository knowledge.

That last point matters especially for AI-native development.

An AI code reviewer is excellent at reading diffs. It is much more useful when the review package also includes **what the code actually produced**.

The repository can now hand the reviewer both:

```text
Here is the code change.
Here are the tests.
Here is the deployed page.
Here is what it looked like on a phone.
Here is what it looked like on desktop.
Now review it.
```

That is a much stronger evidence package than "CI passed."

## What this is — and is not

Using GitHub Actions for pull-request checks is completely normal. CI systems routinely run builds, tests, linters, security scans, browser tests, and other automated validation on PRs.

Using Playwright in GitHub Actions is also a standard pattern. Playwright's own CI documentation includes GitHub Actions examples that run browser tests and upload the HTML report as an artifact.

What is less universal is the **specific review loop** used here:

- trigger from the real preview deployment;
- capture a curated set of mobile and desktop rendered pages;
- store the screenshots as PR-linked artifacts;
- have an AI reviewer retrieve and visually inspect those artifacts;
- use that evidence as a formal UI review gate;
- iterate until the rendered review is explicitly accepted.

Visual regression platforms such as Chromatic, Percy, Applitools, and similar tools already institutionalize the broader idea of reviewing rendered UI changes in pull requests. So the underlying concept is established industry practice.

The distinctive part is combining those established pieces into a lightweight, repository-native workflow that works well for a one-person, AI-enabled development team: **GitHub Actions becomes the transport layer for visual evidence, and independent AI review becomes part of the pull-request loop.**

## A practical starting point

Do not begin by screenshot-testing every page.

Start with a small proving ground:

1. Choose one user-facing feature where visual failure would be obvious and expensive.
2. Pick a handful of representative routes or states, including meaningful edge cases.
3. Capture one mobile and one desktop view.
4. Assert only durable structural conditions at first: page loaded, critical visualization exists, dimensions are non-zero.
5. Upload screenshots and diagnostics as artifacts.
6. Require a reviewer to inspect the rendered evidence before accepting the UI change.
7. Turn defects discovered during review into targeted regression tests or shared fixes.
8. Add pixel-diff baselines only where repeated evidence shows they would add more value than maintenance burden.

For Fido, the proving ground was unemployment maps across Ohio, Delaware, Missouri, and the District of Columbia. That small set was enough to catch multiple classes of production-facing failure.

## Reusable takeaway

**If users see it, reviewers should be able to see it too.**

A pull request should not be considered visually validated merely because:

- it compiles;
- tests pass;
- the preview deployed;
- the DOM element exists;
- the author says it looks right.

For material user-facing changes, create rendered evidence from the actual preview and make that evidence part of review.

The principle is simple:

> **Review the render, not just the code.**

And when the process is working well:

> **Diffs explain what changed. Tests prove known behavior. Rendered evidence shows what the user will actually experience.**

## Related lessons

- [Separate Builder, Reviewer, and Steward](004-separate-builder-reviewer-and-steward.md)
- [Regression Tests Are Compounding Assets](005-regression-tests-are-compounding-assets.md)
- [Systems Catch What People Miss](010-systems-catch-what-people-miss.md)
- [Every Manual Step Eventually Belongs in GitHub](011-every-manual-step-eventually-belongs-in-github.md)
- [GitHub Actions Turn Rules into Guardrails](014-github-actions-turn-rules-into-guardrails.md)
- [Build Production Test Tools, Not Just Tests](015-build-production-test-tools-not-just-tests.md)
- [Is the Juice Worth the Squeeze?](021-is-the-juice-worth-the-squeeze.md)

## References

- [GitHub Actions overview](https://docs.github.com/en/actions/get-started/understand-github-actions)
- [GitHub pull requests and automated checks](https://docs.github.com/en/pull-requests/get-started/about-pull-requests)
- [Playwright continuous integration / GitHub Actions](https://playwright.dev/docs/ci)
