# Cloud-First Was Born from Frustration

## Failure pattern

When I worked with Claude and Cursor on a laptop, the work did not automatically show up when I moved to my phone. When I made progress from mobile, the laptop repository could be behind or different.

Switching devices created a second job: figuring out which version was current, reconstructing what had happened, and moving plans or results between tools.

Claude mobile added another source of friction: there was no convenient way to copy an entire long response. Moving a plan, review, or implementation summary often meant awkward selection and repeated copy-and-paste.

## Why it happened

The workflow was still organized around a local computer:

- the local repository was treated as the real workspace;
- important context lived in application-specific conversations;
- handoffs depended on copying long blocks of text;
- device synchronization was assumed rather than designed;
- progress made in one environment was not automatically visible in another.

There was no brilliant cloud strategy. I was simply frustrated by repeatedly losing continuity.

## System or process introduced

The source of truth moved into cloud systems that were available from every device:

- GitHub issues held requirements and acceptance criteria;
- branches and pull requests held current implementation state;
- repository documents held architecture, instructions, and decisions;
- CI held independent validation results;
- review comments held actionable feedback and resolution history.

AI was increasingly instructed to document its work directly in GitHub rather than returning large blocks that I had to transfer manually.

The workflow became cloud-first not because every activity happens in a browser, but because no single device contains the only authoritative copy of the work.

## How it helped

I could begin on a phone, continue on a laptop, switch models, or open a new conversation without manually rebuilding the project state.

Documentation also improved because the easiest handoff became the durable one. Instead of copying a long explanation from one chat to another, the Builder updated the issue, pull request, or canonical document where the next participant could read it.

This reduced synchronization mistakes and made the development process more resilient.

## Unexpected benefit

The frustration exposed weaknesses that would have affected a larger team too. A process that depends on one laptop, one conversation, or one person's working memory is difficult to scale even if nobody uses a phone.

Designing for device independence forced clearer ownership, better handoffs, and more explicit status.

## Reusable takeaway

**Cloud-first and mobile-first were not brilliant strategies. They were the eventual solution to synchronization problems and terrible copy-and-paste workflows.**

Make authoritative work visible from any device, and have AI write durable handoffs directly into the shared system rather than making humans transport them.