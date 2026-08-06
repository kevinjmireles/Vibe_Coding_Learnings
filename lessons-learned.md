# Lessons Learned

This document records the mistakes, recurring problems, and process weaknesses encountered while building a production application with AI—and the systems introduced to prevent them from recurring.

The lessons are organized around a practical sequence:

1. **Mistake or issue encountered**
2. **Why it happened**
3. **System or process introduced**
4. **How it helped**
5. **Reusable takeaway**

## 1. Important knowledge was trapped in AI conversations

### Mistake or issue encountered

Product decisions, architecture ideas, implementation details, and follow-up work often existed only inside long ChatGPT or Claude conversations. A different model—or even the same model in a new conversation—could not reliably continue the work.

This created several risks:

- decisions could be forgotten or contradicted;
- context had to be repeatedly reconstructed;
- unfinished ideas could disappear;
- a model could confidently proceed from incomplete information;
- the project became too dependent on individual chat histories.

### Why it happened

Chat was originally the easiest place to think through the product. As the project grew, conversations became an informal project-management and architecture system without being designed for that role.

### System or process introduced

The repository became the durable source of truth. Important information began moving into:

- architecture documents;
- decision records;
- implementation guides;
- issue descriptions;
- pull-request descriptions;
- runbooks;
- session notes;
- document registries.

AI instructions were also moved into repository files so different models could read the same rules.

### How it helped

Work became easier to resume across devices, conversations, and models. The project relied less on memory and more on discoverable written evidence.

This also made the development process more resilient. If one AI product disappeared or a conversation became inaccessible, the important decisions would still exist with the code.

### Reusable takeaway

**The repository should remember more than the AI.**

Use chat for exploration, but move durable decisions, rules, and unresolved work into a shared system of record.

---

## 2. AI could produce code faster than I could evaluate it

### Mistake or issue encountered

AI made it possible to generate features and fixes very quickly. That initially felt like pure acceleration, but it also increased the amount of code, architecture, and behavior that needed to be understood and validated.

A plausible implementation could look complete while still containing:

- hidden edge cases;
- duplicated logic;
- inconsistent terminology;
- missing tests;
- architectural shortcuts;
- stale documentation;
- security or operational risks.

### Why it happened

Code generation became easier before the review process became stronger. The bottleneck moved from writing code to determining whether the code was correct, maintainable, and aligned with the product.

### System or process introduced

Development responsibilities were separated into distinct roles:

- **Builder** — implements the issue and provides evidence of completion;
- **Reviewer** — independently evaluates the implementation, tests, documentation, and alternative approaches;
- **Steward** — protects architecture, conventions, and long-term institutional knowledge.

The Reviewer is expected to form an independent assessment rather than simply confirming the Builder's explanation.

### How it helped

Review became a separate reasoning step rather than an extension of implementation. This caught missing requirements, better implementation paths, documentation gaps, and architectural problems that a single-agent workflow often missed.

### Reusable takeaway

**Do not let the same reasoning process both create and validate meaningful work.**

Even when all roles are performed by AI, separate their instructions, context, and responsibilities.

---

## 3. “Looks good” was not enough evidence

### Mistake or issue encountered

Early reviews could end with a general statement that a change appeared correct. That did not establish whether existing behavior remained intact or whether edge cases had been tested.

### Why it happened

AI is very good at producing confident explanations. A convincing summary can substitute for actual validation unless the workflow explicitly requires evidence.

### System or process introduced

Pull requests increasingly require concrete proof, including:

- regression tests;
- boundary and failure-case tests;
- full-suite test results;
- continuity and freshness checks;
- duplicate prevention;
- strict date validation;
- fail-closed behavior;
- comparisons against acceptance criteria;
- explicit documentation updates.

The review process also added a quality grade, confidence level, and justification.

### How it helped

The discussion shifted from “this should work” to “here is the evidence that it works and that previous behavior remains protected.”

Regression tests turned discovered failures into permanent safeguards.

### Reusable takeaway

**Require proof proportional to the risk of the change.**

A confident explanation is not a substitute for tests, observable behavior, and documented validation.

---

## 4. One-off implementations created inconsistency

### Mistake or issue encountered

Similar features were sometimes implemented separately. Over time, this produced repeated formatting logic, inconsistent calculations, duplicated UI patterns, and subtle differences between outputs that were supposed to follow the same rules.

### Why it happened

When focused on delivering the next visible feature, it was easy to solve the immediate problem without first identifying the reusable capability underneath it.

### System or process introduced

Repeated behavior was progressively moved into shared systems, including:

- common renderers;
- shared comparison logic;
- reusable formatting utilities;
- centralized presentation contracts;
- consistent freshness validation;
- common geographic and ranking conventions;
- documented design standards.

Audits were used to inventory inconsistencies before refactoring them.

### How it helped

New features required less bespoke logic, and fixes could be applied in one place. Shared contracts also made it easier to test consistency across multiple outputs.

### Reusable takeaway

**When the second similar feature appears, examine whether both are expressions of one underlying capability.**

Do not abstract everything prematurely, but do not allow repeated behavior to drift indefinitely.

---

## 5. Documentation kept falling behind the code

### Mistake or issue encountered

A feature could be correctly implemented while the architecture guide, operational documentation, examples, or pull-request description still reflected an earlier design.

This made the repository misleading even when the code itself worked.

### Why it happened

Documentation was initially treated as a follow-up activity rather than part of implementation.

### System or process introduced

Documentation became part of the definition of done. Meaningful changes now consider whether they require updates to:

- architecture;
- data dictionaries;
- operating runbooks;
- development instructions;
- decision logs;
- session notes;
- registries;
- examples and templates.

The Reviewer checks documentation rather than assuming the Builder handled it.

### How it helped

The repository became more useful to future contributors and AI models. Decisions could be traced, and stale guidance was more likely to be caught before merge.

### Reusable takeaway

**Documentation is not commentary on the product. It is part of the product's operating system.**

Include documentation impact in issue scope, implementation, and review.

---

## 6. Large prompts became difficult to maintain

### Mistake or issue encountered

As more rules and lessons accumulated, prompts became longer and more repetitive. Important instructions could be buried, contradicted, or omitted when switching tools.

### Why it happened

Prompts were being used as both immediate task instructions and permanent organizational policy.

### System or process introduced

Durable process rules moved into repository documents. Prompts became short entry points such as:

- read the Builder guide;
- read the Reviewer protocol;
- implement the linked issue;
- review the pull request under the documented grading system.

### How it helped

Instructions became easier to update once and reuse across ChatGPT, Claude, Cursor, and other tools. Shorter prompts also worked much better on mobile.

### Reusable takeaway

**Prompts should point to the system, not contain the entire system.**

Store stable policy in version-controlled files and reserve prompts for the current task.

---

## 7. Production risks were easy to ignore while focused on features

### Mistake or issue encountered

Early development naturally emphasized visible functionality. Less visible concerns—backups, environment separation, recovery, stale data, secret handling, and operational failure—could remain underdeveloped.

### Why it happened

Feature progress is immediately visible. Operational resilience often becomes visible only after something goes wrong.

### System or process introduced

The project added or strengthened:

- backup scripts and runbooks;
- environment and access guidance;
- disaster-recovery planning;
- fail-closed secret handling;
- data-freshness thresholds;
- ingest validation;
- send deduplication;
- security audits;
- documentation of responsibility boundaries between humans and AI.

### How it helped

The product became less dependent on optimistic assumptions. Recovery and failure handling became designed behaviors rather than improvised responses.

### Reusable takeaway

**A production feature is incomplete if there is no credible answer to how it fails, how the failure is detected, and how the system recovers.**

---

## 8. Frustration pushed the workflow into the cloud

### Mistake or issue encountered

There was no grand mobile-first or cloud-first strategy. The workflow changed because working across devices was frustrating.

When I used Claude or Cursor on my laptop, the work often was not visible when I moved to my phone. When I started work from my phone, the local repository on my laptop could be behind or out of sync. I had to remember which device held the latest version, copy context between tools, and worry about whether local and remote work matched.

Claude on mobile created another practical problem: it did not provide an easy **copy all** option for long responses. Moving a large implementation plan, review, or decision from a mobile conversation into another tool could require awkward, repeated copying and pasting.

### Why it happened

The workflow had grown around individual tools and devices rather than around one durable system of record.

- Local repositories tied important state to a particular computer.
- AI conversations contained decisions that other tools could not automatically see.
- Mobile interfaces made large context transfers especially painful.
- Each transition between Claude, Cursor, ChatGPT, GitHub, laptop, and phone created another opportunity for context or code to diverge.

### System or process introduced

Mostly out of frustration, I shifted the work into the cloud and made GitHub the central handoff point.

The process gradually became:

- GitHub-first rather than local-first;
- cloud-based rather than tied to one device;
- issue-driven rather than dependent on copying entire conversations;
- documented in the repository rather than left in AI chat;
- organized into small pull requests that could be reviewed independently;
- supported by Builder, Reviewer, and Steward instructions stored with the code;
- test-backed so confidence did not depend on reproducing every step manually;
- prompt-light because the prompt could point to durable instructions already in GitHub.

The inability to easily copy everything from Claude mobile also created a useful forcing function: instead of repeatedly transferring large blocks of text, I instructed the AI to document decisions, findings, and next steps directly in GitHub.

### How it helped

The latest code, decisions, review findings, and documentation became available from either device and to whichever model was working next. Switching from laptop to phone stopped requiring the entire working context to be manually reconstructed.

It also made mobile development practical. I can now manage almost the entire development lifecycle from an iPhone. In one recent week, I worked through roughly 30 pull requests primarily from my phone, including defining work, directing implementation, reviewing results, resolving defects, documenting decisions, evaluating CI, and merging changes.

The process became more portable not because mobile development tools suddenly became ideal, but because repeated annoyances forced state and knowledge out of individual devices and conversations.

### Reusable takeaway

**Cloud-first and mobile-first were not brilliant strategies. They were the eventual solution to synchronization problems and terrible copy-and-paste workflows.**

That is still a useful lesson: pay attention to recurring friction. The workaround you are forced to build may become a stronger operating model than the workflow you originally intended.

---

## Next lessons to document

Future additions will cover:

- issue quality and acceptance criteria;
- independent “parallel path” review;
- architecture decisions and ADRs;
- audit-first refactoring;
- accessibility and localization as architecture concerns;
- data consistency across related products;
- separating product decisions from implementation decisions;
- model selection and multi-model collaboration;
- what I would establish on day one if starting again.