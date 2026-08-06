# Separate Builder, Reviewer, and Steward

## Failure pattern

When the same AI planned a change, implemented it, and then reviewed its own work, the review often repeated the Builder's explanation rather than independently testing the result.

A coherent story could be mistaken for a correct implementation. Missing requirements, weaker architectural choices, and documentation gaps were easy to overlook because the reviewer inherited the same assumptions that shaped the code.

## Why it happened

The Builder is naturally invested in completing the assigned task. Its context is organized around the approach it chose. Asking it to immediately review that approach does not reliably reset its assumptions.

This is not unique to AI. Humans also struggle to find problems in work they just created. AI adds another complication: it can produce a very persuasive summary of why its own work is correct.

## System or process introduced

The development workflow was divided into distinct roles:

- **Builder** — implements the issue, adds tests, updates documentation, and provides evidence.
- **Reviewer** — independently reads the issue, inspects the implementation, evaluates tests, checks documentation, and considers alternative approaches.
- **Steward** — protects long-term architecture, terminology, standards, and institutional memory across individual changes.

The Reviewer is instructed to form its own assessment before being influenced by the Builder's self-grade. Reviews include a quality grade, confidence level, evidence, and actionable findings.

A further technique is **parallel-path review**: the Reviewer asks not only whether the submitted implementation works, but whether a substantially better path should have been chosen.

## How it helped

The roles catch different problems:

- Builders catch implementation details while doing the work.
- Reviewers catch missed requirements, weak tests, hidden edge cases, and better alternatives.
- Stewards catch architectural drift, duplication, terminology inconsistencies, and missing durable documentation.

The separation also makes disagreements useful. A Builder can defend a choice with evidence, while the Reviewer must explain the risk rather than merely declaring that something feels wrong.

## Practical implementation

The roles do not require three people. They can be performed by different models, different conversations, or deliberately separated sessions.

What matters is independence of reasoning:

1. Give the Reviewer the original issue and repository rules.
2. Have it inspect the actual change.
3. Require evidence for conclusions.
4. Let it read the Builder's self-assessment only after forming an initial view.
5. Preserve the findings in the pull request.

## Reusable takeaway

**Do not let the same reasoning process both create and validate meaningful work.**

Separate implementation, independent review, and architectural stewardship—even when AI performs all three roles.