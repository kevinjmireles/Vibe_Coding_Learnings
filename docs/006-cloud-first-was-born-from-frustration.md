# Cloud-First Was Born from Frustration

## Failure pattern

Work was split across a laptop, phone, local repository, AI conversations, and several tools. Progress made in one place was not always visible in another. Switching devices meant reconstructing context, checking which version was current, and manually moving long responses between systems.

Claude mobile made that friction especially obvious because copying an entire long response was difficult. Local development also meant that the laptop could contain important state that was unavailable from the phone.

## Why it happened

The workflow was organized around a device rather than a shared source of truth:

- the local repository was treated as the real workspace;
- important decisions lived in application-specific conversations;
- handoffs depended on copying and pasting;
- progress in one environment was not automatically available in another; and
- routine terminal work created an additional barrier for a non-programmer.

There was no brilliant cloud strategy. The existing workflow was simply too frustrating to keep using.

## System or process introduced

GitHub became the authoritative workspace:

- issues hold requirements and acceptance criteria;
- branches and pull requests hold implementation state;
- repository documents hold architecture, instructions, and decisions;
- review comments hold feedback and resolution history; and
- CI holds independent validation results.

AI agents increasingly document their work directly in GitHub instead of returning large blocks that must be transported manually.

## How it helped

No single device contains the only authoritative copy of the work. I can begin from a phone, continue elsewhere, change AI models, or open a new conversation without rebuilding the project state from memory.

The terminal also became largely optional for my day-to-day role. I can direct work, review changes, inspect tests and CI, request revisions, and merge from the cloud rather than maintaining a local development environment I do not understand well.

The full personal story—full-time job, middle-of-the-night ideas, not wanting to wake my wife, and accidentally making an iPhone my primary development workstation—is documented in [How I Failed My Way into Mobile Software Development](012-how-i-failed-my-way-into-mobile-software-development.md).

## Reusable takeaway

**Cloud-first was not a strategy. It was an escape from synchronization, copy-and-paste, and local-environment friction.**

Make authoritative work visible from any device. Have AI write durable handoffs directly into the shared system rather than making people carry context between tools.