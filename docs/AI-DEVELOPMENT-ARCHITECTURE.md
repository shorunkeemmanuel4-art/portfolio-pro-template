# Portfolio Pro Template — AI Development Architecture

**Status:** Approved
**Version:** 1.0
**Phase:** Phase 2 — Architecture & Technical Design
**Step:** 2.12 — AI Development Architecture

## 1. Purpose

Define the controlled collaboration between GPT, Aider, and local Qwen models during development of Portfolio Pro.

The goal is not to make one model responsible for everything. The goal is to assign each AI system the work it is best suited to perform while keeping architecture, quality, accessibility, security, and product decisions under explicit control.

## 2. Governing Principle

> **GPT plans and governs. Aider operates the codebase. Qwen implements within defined boundaries. Tests verify. GPT reviews.**

AI is an engineering multiplier, not the source of architectural authority.

## 3. AI System Roles

### GPT

GPT is the primary:

- product-planning assistant
- architecture owner/architectural planner
- prompt engineer
- documentation author/reviewer
- task decomposer
- acceptance-criteria author
- implementation reviewer
- reasoning and trade-off partner
- release-readiness reviewer

GPT does not blindly delegate architectural decisions to a local coding model.

### Aider

Aider is the repository-operating coding agent.

Responsibilities:

- inspect repository files
- apply approved implementation tasks
- edit/create/delete project files as authorized
- run local commands/tests
- inspect failures
- make bounded implementation corrections
- produce a concise implementation report

Aider is the execution layer, not the product architect.

### Qwen 1.5B

Qwen 1.5B is the lightweight/context-oriented local worker.

Preferred uses:

- small code transformations
- file summarization
- simple documentation edits
- context extraction
- repetitive low-risk tasks
- lightweight checks
- preparing compact context for larger models

It should not independently make major architecture decisions.

### Qwen 4B

Qwen 4B is the default local implementation/reasoning worker for moderate tasks.

Preferred uses:

- component implementation
- CSS/HTML work
- moderate refactoring
- tests
- accessibility fixes
- ordinary bug fixes
- implementation from precise task specifications

### Qwen 8B

Qwen 8B is the higher-capability local worker for harder coding tasks.

Preferred uses:

- complex component implementation
- multi-file changes
- difficult debugging
- architecture-constrained refactoring
- integration work
- deeper code reasoning before implementation

It remains subordinate to the approved project architecture.

## 4. Authority Model

The authority hierarchy is:

```text
Product requirements
        ↓
Approved architecture
        ↓
Architecture/documentation rules
        ↓
Task specification
        ↓
Implementation
        ↓
Tests/validation
```

AI suggestions do not automatically override an approved architectural decision.

## 5. Human Authority

The project owner remains the final authority for product direction and material decisions.

GPT acts as the architecture/planning/review layer and must surface meaningful trade-offs rather than silently making irreversible product decisions.

## 6. AI Pipeline

The standard workflow is:

```text
User goal
   ↓
GPT analysis
   ↓
Architecture check
   ↓
Task decomposition
   ↓
Prompt engineering
   ↓
Aider
   ↓
Qwen worker(s)
   ↓
Code changes
   ↓
Tests / validation
   ↓
Aider report
   ↓
GPT review
   ↓
Accept / revise / reject
```

## 7. Planning Before Coding

No substantial implementation task should begin from a vague request when it can reasonably be specified first.

GPT should convert the request into:

- objective
- scope
- files likely affected
- constraints
- architecture references
- acceptance criteria
- tests
- explicit non-goals

## 8. Prompt Engineering Role

GPT is the project's prompt engineer.

Prompts sent to Aider/Qwen should be:

- scoped
- architecture-aware
- testable
- explicit about constraints
- explicit about what must not change
- explicit about required explanation

Avoid prompts such as:

```text
Build the portfolio website.
```

Prefer bounded tasks such as:

```text
Implement the approved navigation component.
Follow the component, CSS, JavaScript, and accessibility architecture.
Do not modify unrelated files.
Add/adjust tests.
Report what changed, why, files changed, tests run, and limitations.
```

## 9. Context Architecture

AI context must be layered rather than dumping the entire repository into every prompt.

Preferred context order:

```text
Task
 ↓
Relevant architecture document(s)
 ↓
Relevant design/content specification
 ↓
Relevant source files
 ↓
Relevant tests
 ↓
Recent failure/output
```

## 10. Context Minimization

Use the smallest context that preserves correctness.

Large irrelevant context can:

- increase latency
- consume model capacity
- dilute constraints
- cause irrelevant edits
- reduce reasoning quality

## 11. Architecture Documents as AI Contracts

The `docs/` architecture documents are not passive documentation.

They function as constraints for AI implementation.

Relevant documents should be referenced before implementation of the corresponding layer.

## 12. Task Contract

Every non-trivial AI coding task should have:

```text
TASK
OBJECTIVE
CONTEXT
CONSTRAINTS
FILES IN SCOPE
FILES OUT OF SCOPE
ACCEPTANCE CRITERIA
TESTS
REPORTING REQUIREMENTS
```

## 13. Scope Control

Aider/Qwen must not broaden a task unnecessarily.

If implementation reveals a requirement outside scope, the agent should report it rather than silently expanding the change.

## 14. File Ownership

For each task, GPT should identify expected file ownership where practical.

Example:

```text
Allowed:
- src/components/Nav.astro
- src/scripts/navigation.ts
- relevant test

Do not modify:
- deployment configuration
- unrelated pages
- design tokens
```

## 15. Change Isolation

Prefer small, reviewable changes over giant AI-generated commits.

A single task should ideally produce one coherent architectural change.

## 16. Explanation Contract

Every AI implementation task must end with an implementation report containing:

1. What changed.
2. Why it changed.
3. Files changed.
4. Architecture rules followed.
5. Tests/checks run.
6. Results.
7. Known limitations.
8. Any assumptions made.
9. Any recommended follow-up.

## 17. No Silent Changes

Agents must not silently:

- change architecture
- add dependencies
- change public URLs
- alter deployment behavior
- weaken accessibility
- remove tests
- change security boundaries
- change product requirements

without surfacing the change.

## 18. Model Routing

Model selection should be based on task complexity.

### Route to Qwen 1.5B when

```text
Small
Predictable
Low-risk
Repetitive
Context extraction
```

### Route to Qwen 4B when

```text
Moderate coding
Component work
CSS/HTML
Tests
Routine debugging
```

### Route to Qwen 8B when

```text
Complex reasoning
Multi-file changes
Hard debugging
Integration
High-risk refactoring
```

### Route to GPT when

```text
Architecture
Product trade-offs
Ambiguous requirements
Cross-system reasoning
Review
Release decisions
Prompt design
```

## 19. Escalation Strategy

A task should escalate rather than repeatedly retrying a weak model when:

- requirements are ambiguous
- architecture is affected
- repeated attempts fail
- tests reveal non-local problems
- the model proposes a major dependency
- security/accessibility is at risk

Conceptually:

```text
1.5B
 ↓ failure/complexity
4B
 ↓ failure/complexity
8B
 ↓ architectural ambiguity
GPT review
```

## 20. Retry Policy

Retries should be evidence-driven.

Do not repeatedly issue the same prompt after the same failure.

Each retry should incorporate the failure information and narrow/correct the task.

## 21. Debugging Loop

The standard debugging cycle is:

```text
Failure
 ↓
Capture exact error
 ↓
Identify affected layer
 ↓
Inspect relevant files
 ↓
Form hypothesis
 ↓
Apply smallest fix
 ↓
Run targeted test
 ↓
Run regression tests
```

## 22. Test-Driven Guardrails

Tests are the primary automated constraint on implementation.

Agents should prefer:

```text
Change
 ↓
Test
 ↓
Evidence
```

over:

```text
Change
 ↓
Looks right
 ↓
Done
```

## 23. Architecture Validation

After meaningful multi-file or architectural changes, GPT should review:

- architecture consistency
- dependency impact
- accessibility
- SEO
- performance
- security
- maintainability
- customer customization

## 24. Documentation Synchronization

When implementation changes an architectural invariant or approved behavior, documentation must be updated before the task is considered complete.

Code and architecture documentation must not intentionally diverge.

## 25. Git Workflow

The preferred AI workflow is:

```text
Inspect
 ↓
Plan
 ↓
Edit
 ↓
Test
 ↓
Review diff
 ↓
Commit
```

Agents should avoid destructive Git operations unless explicitly authorized.

## 26. Commit Strategy

Commits should be:

- coherent
- descriptive
- reviewable
- related to one logical change

Avoid giant commits containing unrelated AI-generated modifications.

## 27. Branch Strategy

For significant implementation work, use a feature/fix branch when practical.

Architecture changes should not be mixed with unrelated visual polish unless the task explicitly requires it.

## 28. Safe Tool Use

AI agents must treat shell commands and file operations as potentially destructive.

Before executing a destructive command, the agent should verify:

- target path
- intended effect
- scope
- recoverability

Never use broad destructive commands as shortcuts.

## 29. Dependency Governance

AI agents may recommend dependencies, but dependency adoption requires justification.

The recommendation must include:

- purpose
- alternatives
- size/build impact
- maintenance considerations
- security implications
- accessibility implications
- licensing implications

## 30. Architecture Change Protocol

If an agent discovers that the approved architecture is insufficient:

```text
Stop broad implementation
        ↓
Describe conflict
        ↓
Propose options
        ↓
GPT evaluates architecture
        ↓
Owner approves material change
        ↓
Update documentation
        ↓
Resume implementation
```

Do not silently rewrite architecture through code.

## 31. Design-to-Code Workflow

When a Figma design is available, the design should be treated as implementation input, not permission to ignore project architecture.

Workflow:

```text
Figma/design specification
       ↓
GPT extracts requirements
       ↓
Map to design system
       ↓
Map to accessibility requirements
       ↓
Create implementation task
       ↓
Aider/Qwen implements
       ↓
Visual + semantic + accessibility review
```

## 32. Design System Protection

AI agents must reuse approved design tokens and components before creating new variants.

Do not introduce one-off values merely because they appear convenient in a design.

## 33. Accessibility Protection

Accessibility architecture is a hard constraint.

An AI agent may not knowingly trade away keyboard access, semantic structure, focus visibility, contrast, reduced motion, or accessible names to make implementation easier.

## 34. SEO Protection

AI agents must preserve:

- semantic headings
- crawlable links
- metadata
- canonical strategy
- sitemap/robots behavior
- server/static content rendering

No SEO shortcuts may undermine accessibility or content quality.

## 35. Performance Protection

AI agents must consider:

- bundle size
- image payload
- font payload
- hydration
- third-party scripts
- runtime work

A visually impressive implementation is not acceptable if it introduces unjustified performance cost.

## 36. Security Protection

AI agents must never expose secrets or weaken security controls simply to make development convenient.

## 37. Customer-Safety Principle

Because Portfolio Pro is a commercial template, AI-generated code must be understandable and maintainable by a customer developer.

Avoid cleverness that increases customization difficulty without meaningful user value.

## 38. Commercial Product Constraints

AI implementation must preserve:

- easy installation
- predictable customization
- static-host compatibility
- documentation quality
- licensing boundaries
- Free/Pro edition boundaries where applicable

## 39. AI Output Quality Levels

Tasks can be classified:

```text
L0 — Mechanical
L1 — Routine implementation
L2 — Moderate reasoning
L3 — Complex implementation
L4 — Architectural/product decision
```

Suggested routing:

```text
L0 → 1.5B
L1 → 4B
L2 → 4B / 8B
L3 → 8B + GPT review
L4 → GPT-led decision
```

## 40. Context Handoff

When moving a task between models, pass a compact handoff containing:

```text
Goal
Current state
Relevant files
Architecture constraints
What was attempted
Exact failure
What must not change
Next requested action
```

Do not make the next model rediscover known facts unnecessarily.

## 41. Failure Handoff

If Qwen fails, Aider should capture the exact failure rather than paraphrasing it beyond recognition.

A useful handoff includes:

- command
- output/error
- changed files
- expected behavior
- actual behavior
- last successful checkpoint

## 42. Review Levels

### Local review

Aider checks its own change and tests.

### Architecture review

GPT checks compliance with approved architecture.

### Release review

GPT evaluates the integrated product against release gates.

## 43. Human Review Triggers

Human/owner review should be requested for:

- architecture changes
- security-sensitive changes
- deployment changes
- licensing changes
- major dependency additions
- public URL changes
- major product-scope changes
- irreversible data/destructive operations

## 44. AI Cost/Resource Strategy

Use the smallest capable model first.

Do not spend 8B/GPT-level resources on mechanical tasks that 1.5B can perform reliably.

However, do not force a small model onto complex tasks merely to save compute if repeated failures cost more time and risk.

## 45. Local-First Development

Where practical, routine coding work should use local Qwen models through Aider.

GPT is reserved for higher-value reasoning, planning, prompt engineering, architecture, and review.

This reduces external AI usage while preserving a high-quality reasoning layer.

## 46. Offline/Network Resilience

The development workflow should remain useful when external AI access is unavailable.

Local Qwen/Aider should be capable of completing appropriately scoped implementation tasks using repository-local documentation and context.

GPT-dependent decisions may wait until connectivity is restored when they cannot safely be delegated.

## 47. Prompt Versioning

Important reusable prompts should eventually be stored in the repository rather than living only in chat history.

Potential location:

```text
prompts/
├── planning/
├── implementation/
├── review/
├── debugging/
└── release/
```

Exact structure will be finalized during implementation.

## 48. AI Instructions File

The project should provide an agent-facing instruction file containing concise non-negotiable rules derived from the architecture.

Potential candidates include project-supported Aider/agent instruction files and a canonical `AGENTS.md` if adopted.

The canonical source must avoid duplicating contradictory rules across multiple files.

## 49. Context Hierarchy for Agents

Agents should prioritize:

```text
1. Current task
2. Explicit owner instruction
3. Approved architecture
4. Relevant project docs
5. Existing code conventions
6. Agent/model preference
```

An agent preference must never override an explicit higher-priority project constraint.

## 50. AI Review Checklist

Before accepting a substantial AI-generated change:

```text
Requirement satisfied          ✓
Scope respected                ✓
Architecture respected        ✓
Accessibility reviewed        ✓
SEO reviewed                  ✓
Performance reviewed          ✓
Security reviewed             ✓
Tests pass                    ✓
Diff is understandable        ✓
Documentation synchronized    ✓
AI explanation provided       ✓
```

## 51. Definition of Done for AI Tasks

An AI task is complete only when:

1. implementation exists
2. required tests/checks pass
3. scope is respected
4. architecture remains valid
5. relevant documentation is synchronized
6. the agent reports what changed and why
7. known limitations are disclosed

## 52. Anti-Patterns

Do not:

- let a small model rewrite architecture
- paste the entire repository into every prompt unnecessarily
- accept code because it merely compiles
- hide failing tests
- let agents silently broaden scope
- install dependencies without justification
- allow AI-generated SEO spam
- trade accessibility for visual convenience
- expose secrets
- use destructive commands as shortcuts
- make huge unreviewable AI commits
- allow code and architecture documentation to drift

## 53. Architecture Invariants

1. GPT is the architecture/planning/review authority within the AI workflow.
2. GPT serves as prompt engineer and task decomposer.
3. Aider is the repository execution layer.
4. Qwen 1.5B handles suitable low-risk/lightweight work.
5. Qwen 4B handles routine/moderate implementation.
6. Qwen 8B handles harder coding/debugging tasks.
7. Model routing is complexity-based.
8. Approved architecture outranks model preference.
9. Every substantial AI task has explicit scope and acceptance criteria.
10. Every substantial AI task produces an explanation/report.
11. Tests and evidence are required for completion.
12. Architecture changes require explicit review rather than silent code drift.
13. Accessibility, SEO, performance, and security are hard constraints.
14. Secrets never enter source or client output.
15. The smallest capable model should be used where reliable.
16. Context should be compact, relevant, and structured.
17. Failed attempts must be handed off with exact evidence.
18. Commercial maintainability is part of code quality.

## 54. Architecture Gate

Step 2.12 is complete when the roles of GPT, Aider, Qwen 1.5B/4B/8B, authority model, task contracts, context strategy, prompt engineering, model routing, escalation, debugging, testing, documentation synchronization, Git workflow, design-to-code workflow, accessibility/SEO/performance/security protections, cost strategy, offline/local-first behavior, prompt versioning, agent instructions, review gates, and AI definition-of-done are documented.

Next step: **Phase 2 — Step 2.13: Architecture Review & Freeze.**
