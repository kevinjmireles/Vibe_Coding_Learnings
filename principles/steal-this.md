# Steal This: Five Practices to Copy First

You do not need to adopt an entire methodology. Start with a few practices that reduce the most common AI-development failures.

## 1. Make GitHub issues the canonical requirements

Define the problem, scope, and observable acceptance criteria before implementation. Then use a tiny prompt such as `Build #123.`

## 2. Separate Builder and Reviewer responsibilities

Do not let the same reasoning process both create and validate meaningful work. The Reviewer should compare the issue, code, tests, documentation, and possible alternative approaches.

## 3. Move durable instructions into the repository

Stop pasting the same long prompt. Put stable rules in a repository instruction file and role documents that every model can read.

## 4. Require reuse before creating another system

Before adding a component, workflow, helper, document, or data path, require the Builder to identify the existing system it should extend—or explain why extension is inappropriate.

## 5. Turn recurring mistakes into enforced workflow

A reminder is weaker than a template. A template is weaker than an automated check. When possible, move required information and validation into PR templates, CI, branch protection, and required status checks.

## Start small

Adopt one practice, use it on real work, and change it when it fails. The system in this repository was not designed all at once. It grew one painful lesson at a time.