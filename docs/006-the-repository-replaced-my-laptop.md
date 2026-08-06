# The Repository Replaced My Laptop

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

The laptop was not merely a tool. It had accidentally become the place where the project lived.

## System or process introduced

GitHub became the authoritative workspace:

- issues hold requirements and acceptance criteria;
- branches and pull requests hold implementation state;
- repository documents hold architecture, instructions, and decisions;
- review comments hold feedback and resolution history; and
- CI holds independent validation results.

AI agents increasingly document their work directly in GitHub instead of returning large blocks that must be transported manually.

The repository replaced the laptop as the center of the development process. The laptop could still be used, but it no longer contained the only current or authoritative version of the work.

## How it helped

No single device contains the only authoritative copy of the project. I can begin from a phone, continue elsewhere, change AI models, or open a new conversation without rebuilding project state from memory.

The terminal also became largely optional for my day-to-day role. I can direct work, review changes, inspect tests and CI, request revisions, and merge from the cloud rather than maintaining a local development environment I do not understand well.

This made the process device-independent, easier to resume, and less dependent on one computer, one application, or one AI conversation.

The personal story behind this change—full-time work, middle-of-the-night ideas, not wanting to wake my wife, and accidentally making an iPhone my primary development workstation—is documented separately in [How I Failed My Way into Mobile Software Development](012-how-i-failed-my-way-into-mobile-software-development.md).

## Reusable takeaway

**Do not let a workstation become the system of record.**

Put requirements, implementation state, evidence, decisions, and handoffs in shared systems that remain available when the device, tool, model, or conversation changes.