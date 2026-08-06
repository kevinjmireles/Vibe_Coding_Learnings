# Every Manual Step Eventually Belongs in GitHub

## Failure pattern

Important quality steps originally depended on someone remembering to perform them: verify acceptance criteria, update documentation, record tests, consider architecture, grade the PR, and confirm review findings were resolved.

Repeated reminders helped, but they did not make the process reliable.

## Why it happened

The workflow was growing faster than any one person—or AI conversation—could consistently remember. Mobile work made the weakness more obvious because long checklists and repeated copy-and-paste were especially cumbersome.

## System or process introduced

Repeated reminders were progressively moved into GitHub:

- issue templates;
- pull-request templates;
- required testing and documentation fields;
- Builder self-grades;
- independent Reviewer grades and confidence;
- review-round records;
- automated CI checks;
- branch protection and required status checks that prevent merge until required conditions pass.

Documentation remained a core Builder responsibility, with the Reviewer and Architecture Steward checking it where relevant. It did not require a separate recurring prompt.

## How it helped

The workflow became less dependent on memory and more consistent across models and devices. Missing information became visible before merge, and automated checks could stop incomplete work rather than merely warning about it.

This also shortened prompts. Instead of restating the process, the human could say `Build #123` or `Review PR #456`, and GitHub supplied the durable instructions and gates.

## Reusable takeaway

**The best process is one you cannot accidentally skip.**

When the same reminder appears repeatedly, first turn it into a checklist or template. When the condition is objectively testable, automate it and make the check required before merge.