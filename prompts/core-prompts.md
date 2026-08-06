# Core Prompts

The prompts are deliberately tiny because the repository contains the durable instructions.

## Typical prompts

### Document

```text
Document this.
```

### Build

```text
Build #563.
```

### Review a pull request

```text
Review PR #571.
```

### Review a commit

```text
Review commit abc123.
```

### Re-review after fixes

```text
Re-review PR #571.
```

### Draft an issue

```text
Draft issue.
```

### Architecture review

```text
Review architecture.
```

## Why this works

The short prompt identifies the assignment. The repository supplies:

- project context;
- role responsibilities;
- issue scope and acceptance criteria;
- architecture rules;
- anti-duplication checks;
- testing requirements;
- documentation responsibilities;
- quality gates;
- handoff and merge rules.

Documentation is not normally triggered by a separate documentation prompt. It is part of the Builder's responsibility and is checked by the Reviewer and Architecture Steward where relevant.

## The evolution

Earlier prompts tried to restate the entire process. They became difficult to maintain, inconsistent across AI products, and painful to copy on mobile.

Moving stable instructions into version-controlled files made the real prompts two or three words long.

> **The AI should identify the task. The repository should define how the work is done.**

See [Prompt Evolution](../evolution/prompt-evolution.md).