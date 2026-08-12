# Change It Once

## Failure pattern

As similar features accumulated, the same behavior began appearing in multiple places.

That included things such as:

- formatting rules;
- comparison wording;
- ranking conventions;
- freshness logic;
- renderers;
- localization behavior;
- design patterns;
- calculations;
- presentation contracts.

At first, duplication can look harmless. Two implementations may even behave identically.

The problem appears later, when one changes and the other does not.

Then the product begins disagreeing with itself.

## Why it happened

The immediate feature is always easier to see than the shared capability underneath it.

AI makes this especially easy because it can quickly create another helper, renderer, formatter, or workflow that solves the local problem. If every task is treated independently, similar logic spreads faster than anyone notices.

That creates a maintenance trap:

- one fix has to be repeated in several files;
- one version receives tests while another does not;
- wording or calculations drift;
- future builders do not know which implementation is canonical;
- regressions become harder to predict.

## System or process introduced

Repeated behavior is increasingly pulled into shared primitives and canonical contracts.

Examples include:

- shared renderers instead of per-feature rendering paths;
- shared change-presentation helpers;
- centralized formatting and locale utilities;
- common freshness and date-comparison logic;
- common design standards;
- reusable geographic and comparison conventions;
- one canonical document for a rule rather than several overlapping descriptions.

The architectural rule is simple:

> Before creating a new implementation, determine whether the existing system should be extended instead.

Once behavior becomes shared, tests are written against the shared primitive and against representative consumers so a change in one place can be proven across multiple outputs.

## How it helped

The obvious benefit is less duplicated code.

The larger benefit is consistency.

A correction made to the shared component can propagate across many products, geographies, datasets, or views without requiring dozens of independent edits.

That makes development faster, but more importantly it reduces the number of places where the product can quietly diverge.

Centralization also improves review. Instead of asking whether ten implementations all behave the same way, reviewers can focus on one contract and verify that consumers use it correctly.

## Caution

Not everything should be abstracted immediately.

Premature abstraction can create an overly generic component that is harder to understand than two genuinely different implementations.

The goal is not maximum reuse. The goal is one source of truth for behavior that is actually shared.

A useful signal is repeated change: if the same conceptual fix keeps being required in multiple places, the abstraction is probably overdue.

## Reusable takeaway

**If one product behavior is supposed to be consistent everywhere, make it changeable in one place.**

Centralize shared rules before inconsistency becomes a product feature.

The highest-leverage engineering work is often invisible: build the shared primitive once so the next ten changes are cheaper, safer, and more consistent.