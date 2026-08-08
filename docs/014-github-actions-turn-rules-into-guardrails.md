# GitHub Actions Turn Rules into Guardrails

## Failure pattern

A written rule is useful, but it still depends on somebody remembering to follow it.

That was a problem in an AI-assisted workflow because the same omission could recur even after it had been documented. A Builder could forget a required PR field. A Reviewer could miss a checklist item. An issue could be opened without enough information. A pull request could look complete while still lacking evidence, documentation, or required review metadata.

The process was becoming better, but too much quality still depended on memory.

## Why it happened

Documentation, templates, and agent instructions are advisory unless something checks them.

Humans forget things. AI agents forget things too. Both are especially likely to skip process details when focused on solving the immediate problem.

That creates an important distinction:

- a **rule** explains what should happen;
- a **template** reminds someone what should happen;
- an **automated check** verifies whether it happened; and
- a **required GitHub check** can prevent the work from moving forward until it happens.

## System or process introduced

GitHub Actions became part of the quality system.

Instead of relying only on instructions in `CLAUDE.md`, agent role files, issue templates, or PR templates, automated workflows can inspect issues and pull requests and verify that required information is present.

Examples include checking that a pull request contains:

- a clear problem statement or linked issue;
- acceptance-criteria status;
- test and validation evidence;
- documentation impact;
- known limitations or follow-up work;
- Builder self-grade;
- Reviewer grade and confidence when required; and
- other project-specific fields that the team has decided are mandatory.

Actions can also validate objective conditions such as:

- tests passing;
- type checking;
- linting;
- builds;
- migration or schema checks;
- generated-file consistency;
- forbidden files or patterns;
- required labels or metadata; and
- issue or PR formatting rules.

For issues, automation can check whether required sections, labels, or fields are present before the issue enters a workflow that assumes it is implementation-ready.

The important part is not the individual check. It is that GitHub becomes an active participant in enforcing the operating model.

## How the pieces work together

The strongest process uses several layers:

1. **Repository instructions** define the standing rules.
2. **Issue and PR templates** make the expected structure obvious.
3. **AI roles** tell Builders and Reviewers how to apply the rules.
4. **GitHub Actions** verify that required evidence or structure is actually present.
5. **CI** tests the software itself.
6. **Branch protection / required status checks** can block merge when an enforced check fails.
7. **Human judgment** remains responsible for deciding whether the change should ultimately proceed.

This is defense in depth. No single layer has to catch everything.

## Why this matters especially with AI

AI is excellent at completing the task directly in front of it. It is less reliable at remembering every standing procedural requirement surrounding that task.

That means repository rules alone are not enough for the most important requirements.

If a rule repeatedly matters to quality, ask whether it can be made machine-checkable.

For example:

> "Every PR should include test evidence" is guidance.

> "The PR-quality workflow fails when the validation section is missing" is a guardrail.

> "The branch cannot merge while that check is failing" is enforcement.

That progression significantly reduces dependence on memory and prompt quality.

## A caution

Not every judgment should become an automated rule.

Automation works best for things that are observable and reasonably deterministic. It should not pretend to replace architectural judgment, product judgment, or meaningful code review.

A GitHub Action can confirm that a section called `Documentation` exists. It cannot reliably determine whether the documentation is actually good.

Use automation to enforce the floor, not to pretend that the floor is the ceiling.

## Reusable takeaway

**If a rule matters enough that forgetting it can create a bad merge, do not rely only on people or AI remembering it. Make GitHub check it.**

The progression is:

**lesson → rule → template → automated check → required gate.**

That is how a recurring mistake becomes part of the engineering system instead of remaining another reminder in a document.

See also [Quality Gates](../rules/quality-gates.md) and [Every Manual Step Eventually Belongs in GitHub](011-every-manual-step-eventually-belongs-in-github.md).