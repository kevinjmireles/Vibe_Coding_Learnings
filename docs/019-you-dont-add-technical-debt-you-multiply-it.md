# 019 — You Don’t Add Technical Debt, You Multiply It

## The problem

Technical debt is often described as if each shortcut adds one more item to a backlog.

That understates the problem.

When the debt is duplication — multiple implementations of behavior that should be shared — each additional copy creates another place to maintain, test, forget, and allow to drift. As the product gains more datasets, geographies, languages, channels, and features, those copies interact with every new dimension of the system.

You do not simply add technical debt. **You multiply it.**

## The simplest math: maintenance grows with every copy

Suppose one shared behavior exists in `N` separate implementations instead of one canonical component.

If changing and validating one implementation requires effort `E`, then approximately:

```text
Change effort = N × E
```

If a change takes 30 minutes to implement and verify correctly:

| Implementations | Approximate work |
|---:|---:|
| 1 | 30 minutes |
| 5 | 2.5 hours |
| 20 | 10 hours |
| 50 | 25 hours |

A shared component does not make the underlying product requirement disappear. It removes repeated implementation work for the same requirement.

## The probability of inconsistency also compounds

Assume each individual implementation has probability `p` of being missed or changed incorrectly during an update.

The probability that **at least one** implementation is wrong is:

```text
P(at least one failure) = 1 - (1 - p)^N
```

Even with an optimistic 2% miss/error probability per implementation:

| Implementations | Chance at least one is wrong |
|---:|---:|
| 1 | 2.0% |
| 5 | 9.6% |
| 10 | 18.3% |
| 20 | 33.2% |
| 50 | 63.6% |

So a process that is 98% reliable for each individual edit can still produce roughly a **64% chance of at least one inconsistency** when the same change must be made independently in 50 places.

The problem is not necessarily that the software crashes. Often the product simply stops agreeing with itself.

## Product dimensions multiply the test surface

Duplication gets more expensive as the product gains dimensions.

If a behavior exists in:

- `N` implementations,
- across `D` datasets,
- `G` geography types,
- `L` languages,
- and `C` delivery channels,

then a simple representation of the behavioral surface is:

```text
Test surface = N × D × G × L × C
```

For example:

```text
8 implementations
× 5 datasets
× 4 geography types
× 3 languages
× 3 channels
= 1,440 implementation/context combinations
```

Centralize the behavior and the implementation dimension becomes one:

```text
1 × 5 × 4 × 3 × 3 = 180
```

The inherent complexity of supporting datasets, geographies, languages, and channels still exists. But 1,260 duplicate implementation/context surfaces have disappeared.

This is why duplication that seems harmless in a small product becomes punishing as the product grows.

## Drift relationships grow even faster

There is another way to visualize the risk.

If `N` implementations are all supposed to behave the same way, the number of unique pairs that can disagree is:

```text
N(N - 1) / 2
```

| Copies | Pairwise relationships |
|---:|---:|
| 2 | 1 |
| 5 | 10 |
| 10 | 45 |
| 20 | 190 |
| 50 | 1,225 |

This does **not** mean a team literally needs 1,225 tests for 50 components. It illustrates the number of relationships in which supposedly equivalent implementations can diverge.

> **One duplicate doubles the places you have to fix. Ten duplicates create 45 ways for supposedly identical implementations to disagree.**

## What this looked like while building Fido

This became visible repeatedly as Fido grew.

Similar FIUs and presentation paths could independently implement ranking logic, comparison wording, change formatting, freshness behavior, localization, and rendering conventions. Each implementation could look reasonable in isolation while producing a product that was inconsistent across modules.

The response was increasingly to create shared primitives: common renderers, presentation contracts, formatting helpers, canonical rules, reusable test tools, and centralized implementations for behavior that was genuinely the same.

The lesson was not merely “write less code.”

It was:

> **Fix the shared primitive, not every symptom.**

That is the difference between correcting one implementation and correcting the system.

## The important exception: do not centralize different policies

Anti-duplication can itself be applied badly.

Two things that happen to have the same value today are not necessarily the same policy.

Fido encountered the inverse failure with unemployment-claims freshness thresholds: state and national claims had different publication behavior. Treating them as one shared threshold because they initially looked similar created the wrong abstraction. The correct design gave each conceptually distinct policy its own explicitly named owner.

So the rule is **not**:

> Centralize everything that looks similar.

It is:

> **Centralize behavior that is genuinely the same. Keep conceptually different policies distinct even when their current implementations or values happen to coincide.**

## A useful mental model

The cost of duplication can be thought of as three related effects:

```text
Maintenance cost      ≈ N
Context/test surface  ≈ N × D × G × L × C
Potential drift pairs = N(N - 1) / 2
```

This is not a precise accounting formula. It is a way to understand why technical debt can accelerate instead of accumulating one item at a time.

A shortcut creates another implementation. That implementation must then survive every future feature, dataset, language, channel, policy change, and bug fix.

Today's duplicate becomes tomorrow's multiplier.

## What to do instead

Before adding another implementation of existing behavior, ask:

1. Does this behavior already exist somewhere else?
2. Are the two behaviors actually the same policy or merely similar today?
3. If I fix one later, should the other automatically receive the same fix?
4. Can the shared behavior have one canonical owner?
5. Can tests validate the shared contract rather than every copy independently?

If the answer to #3 is yes, that is a strong signal that the behavior belongs behind a shared primitive.

## Reusable takeaway

> **You don’t add technical debt. You multiply it.**

Duplication increases immediate maintenance roughly with the number of copies, multiplies the testing surface across every product dimension, and creates rapidly growing opportunities for supposedly equivalent implementations to drift apart.

The scalable response is not simply to work harder at keeping the copies synchronized.

> **Make the change happen in one place.**

---

Created by **Kevin J. Mireles** as part of *From Vibe Coding to Production / Vibe Coding Learnings*. Licensed for reuse under CC BY 4.0; attribution is required when sharing or adapting this work.