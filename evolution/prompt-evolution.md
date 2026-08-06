# Prompt Evolution: The Repository Became the Prompt

## Early approach

Early prompts tried to carry everything: requirements, architecture, coding standards, testing expectations, documentation rules, and review instructions. Every new conversation required copying large blocks of context.

This was especially painful on mobile, where moving long Claude responses between tools was difficult and there was no convenient way to copy an entire response.

## What changed

Durable instructions moved into the repository:

- project-wide AI instructions;
- Builder and Reviewer role contracts;
- architecture documents;
- issue and PR templates;
- testing and documentation rules;
- naming and design standards.

Once those rules lived beside the code, prompts became extremely short.

## Typical prompts now

```text
Document this.
```

```text
Build #563.
```

```text
Review PR #571.
```

```text
Review commit abc123.
```

The prompt identifies the task. The repository supplies the process.

## Why this is better

- Every model reads the same instructions.
- Rules are updated once instead of pasted repeatedly.
- Prompts work well on mobile.
- Less context is lost between sessions and tools.
- The workflow is less dependent on any one AI product.

## Reusable takeaway

**When prompts get shorter because the repository gets smarter, the process is maturing.**

A large recurring prompt is often a sign that durable project knowledge belongs in version control.