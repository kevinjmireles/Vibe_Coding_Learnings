# Simplify. Quantify. Clarify.

> **AI can generate more detail than any product manager can reasonably absorb. If we do not simplify the decision, quantify the impact, and make it easy to ask questions, approval can become little more than fatigue.**

I learned this the expensive way.

We were building a much more sophisticated email-delivery system for Fido.

The work looked great.

There were detailed plans. Multiple pull requests. Tests. Reviews. Failure handling. Retry logic. Rollback plans. Lots and lots of thoughtful explanation.

I read it.

Then I skimmed it.

Then, if I am being completely candid, my eyes started to glaze over.

And I kept saying yes.

I am the product manager. I am supposed to be making the decision. But the explanations had become so technical and so detailed that I was no longer really evaluating the decision.

I was looking for signals that smart work had been done and approving it.

Then I asked one very simple question:

> **How long would this take to send 100,000 emails?**

The answer was about **14 days**.

Wait. What?

We were building a new system partly because we wanted email delivery to scale better.

The new design could process about **5 emails a minute**.

The existing system could process roughly **1,200–3,000 a minute**.

We had built something hundreds of times slower than what we already had.

All the technical detail had obscured the one thing I actually needed to understand.

That was the moment this became a much bigger lesson for me.

## This is not really an engineering problem

It is a product-management problem.

I have spent nearly 30 years working in and around software. One of the dirty little secrets of product management is that **we do not always completely understand what y'all are doing.**

We understand the customer.

We understand the problem.

We understand the business.

We understand what outcome we are trying to create.

But when an engineer starts talking about queues, leases, caching strategies, concurrency models, database locks, retry semantics, or whatever else is happening six layers below the product, there is a point where a product manager's understanding gets fuzzy.

That is normal.

A product manager should not need to understand every implementation detail.

But we **do** need to understand enough to answer some very basic questions:

- Is this the right problem?
- How big is the problem?
- Is the proposed solution actually better?
- What will it cost?
- What are we giving up?
- Should we do this at all?

Good product and engineering teams have always had to bridge that gap.

**Vibe coding makes the problem much bigger.**

Now my “engineering team” can generate code, tests, architecture, documentation, and a 5,000-word explanation at machine speed.

I can go through multiple rounds of implementation in an evening.

The AI can produce technical detail much faster than I can absorb it.

So the danger is not merely that the AI writes bad code.

The danger is that it writes **plausible, sophisticated, well-documented code that I approve without really understanding the decision I just made.**

Eventually, that bites you in the ass.

So I have reduced the solution to three words:

# Simplify. Quantify. Clarify.

## 1. Simplify

The first job is not to simplify the engineering.

Complex systems sometimes require complex engineering.

The job is to **simplify the decision**.

If I have to read 3,000 words and understand five previous pull requests before I can decide whether to approve the sixth, the process has already failed.

Give me the decision first.

What are we doing?

Why?

What will be different afterward?

What does it cost?

What do you need me to decide?

Then put all the engineering detail underneath it for the people and AI agents who need it.

This also applies to the solution itself.

Before we build something complicated, ask:

> **What is the simplest thing that could solve this problem?**

Could we change a setting?

Could we use something we already built?

Does the vendor already provide the capability?

Could we simply rerun the process if it fails?

Could we do nothing yet?

In our email example, several dramatically simpler options already existed.

We had not really forced ourselves to consider them because the conversation had already jumped to **how to build the new system**, rather than **whether we needed to build it**.

That is classic product management.

AI just lets us make the mistake much faster.

## 2. Quantify

Simplifying the explanation is not enough.

The explanation also needs numbers.

And they need to be **product numbers**, not engineering numbers.

“Batch size: 25.”

“Lease duration: 120 seconds.”

“Five retry attempts.”

Those are numbers.

But they do not tell me whether the product is getting better.

Tell me:

**5 emails per minute.**

**1,200–3,000 emails per minute today.**

**100,000 emails = roughly 14 days with the proposed design.**

Now I understand the decision.

That is the difference.

The basic comparison should usually be painfully simple:

**Today → After**

How long does it take today?

How long will it take afterward?

How many people can we support today?

How many afterward?

How much does it cost today?

How much afterward?

How often does this problem actually happen?

How bad is it when it does?

And what number are we actually trying to reach?

That last question turned out to be especially important.

The original email work had at least started with a useful trigger: we should move away from synchronous delivery before normal sends got beyond roughly 100 recipients or regularly took more than 10–15 seconds.

But as implementation continued, that original number disappeared from the conversation.

Worse, we never replaced it with a clear target for how quickly the new system itself should complete delivery.

So people could make perfectly reasonable technical decisions inside each individual pull request while the overall product slowly drifted away from the reason we started the work.

This is another thing AI changes.

A requirement no longer has months to get lost.

It can get lost **in an afternoon**.

So the original number has to travel with the work.

Not because engineers love metrics.

Because numbers give the product manager something concrete to judge.

## 3. Clarify

This may be the most important one.

We need to make it **easy to say “I do not understand.”**

Product managers do not like looking stupid.

Neither do executives.

Neither do founders.

When a technically sophisticated explanation lands in front of you, there is a subtle pressure to assume the people who wrote it know what they are doing.

And when you have already read 2,000 words, asking someone to explain it again can feel like you are slowing everyone down.

So you approve it.

AI makes that dynamic worse because the AI does not get tired.

It is always ready for the next instruction.

If I misunderstand something and say “go,” it goes.

Fast.

So I have started making clarification an explicit part of the decision process.

For meaningful work, there are three perfectly legitimate responses:

**Approve.**

**Clarify: [my question].**

**Not now.**

That is it.

“Clarify” is not a failure.

It is not an admission that the product manager is not technical enough.

It is part of the process.

If I do not understand why we are doing something, how much it matters, or what will happen afterward, **the correct product-management action is to ask.**

The system should make asking easier than nodding along.

## The five lines I actually need

We have started turning this into a very small Decision Brief at the top of meaningful issues and pull requests.

It is deliberately short:

**What is this?**

One plain-English sentence.

**What number started this work?**

The original trigger or target.

**Today → After**

The actual change in business terms.

**Cost**

Pull requests, money, operational complexity, or other meaningful cost.

**Ask**

Approve / Clarify / Not now.

That is the interface between the detailed engineering work and the human responsible for the product decision.

The detailed analysis still exists.

Tests still exist.

Architecture still exists.

The engineering discussion can be as sophisticated as it needs to be.

**I just should not have to understand all of it before I can understand the decision.**

And we are deliberately not copying the whole problem analysis into every pull request.

The original issue owns the deep thinking.

The pull request gives me the short version and links back.

Otherwise we would solve information overload by generating even more information.

The mechanics behind this live in the repository's [Quality Gates](../rules/quality-gates.md), but the management principle is much simpler than the mechanism:

> **Simplify the decision. Quantify the impact. Make clarification normal.**

## This is bigger than vibe coding

I think this may turn out to be one of the more important lessons I have learned from building software with AI.

The promise of vibe coding is not that product managers suddenly become engineers.

I still do not write the code.

The promise is that people like me can work much closer to implementation and move dramatically faster than we could before.

But that creates a new problem:

**Execution is getting faster than human understanding.**

That changes the bottleneck.

Writing the code may no longer be the slow part.

Understanding what we are building, deciding whether it is worth building, and keeping the work aligned with the product may become the slow part.

Which means product management does not become less important in an AI world.

It becomes **more important**.

The answer is not for the product manager to read faster.

And it is not to ask the AI for another 5,000 words.

It is to create a better interface between machine-speed execution and human judgment.

**Simplify the decision.**

**Quantify the impact.**

**Make clarification normal.**

Then let the engineers—or the AI—go as deep as they need to underneath it.

This is the same broader idea behind [Process as Product](023-process-as-product.md): if AI changes how quickly work can move, the management system around the work has to evolve too.

## The reusable takeaway

The biggest risk in vibe coding is not necessarily bad code.

It may be **good-looking work that moves so fast, with so much convincing detail, that the human responsible for the product stops truly evaluating it.**

That is a management problem.

And the fix is surprisingly simple:

# Simplify. Quantify. Clarify.

If the AI cannot explain the decision simply, put meaningful numbers around the outcome, and make it easy for the human to question the work, then it is not ready for approval.
