# Portfolio Pro Template — Project Rules

**Status:** Approved foundation rules
**Version:** 1.0
**Applies to:** Entire repository and every human/AI contributor

## 1. Purpose

Portfolio Pro Template is a commercial-grade, accessible, customizable portfolio website template intended for distribution as a digital product. The repository is developed as a product, not as a one-off personal website.

These rules establish the development authority, engineering constraints, AI workflow, quality expectations, and change-control process used throughout the project.

## 2. Source of Truth

The project documentation is the source of truth for product and engineering decisions.

Priority order:

1. Explicit project decisions approved by the project owner and recorded in the documentation.
2. `docs/PRD.md` for product requirements.
3. `docs/ARCHITECTURE.md` for technical architecture.
4. `docs/UX.md` and `docs/DESIGN-SYSTEM.md` for UX and visual-system decisions.
5. Other project documentation for its defined scope.
6. Implementation code.

If code conflicts with approved documentation, the conflict must be reported rather than silently redefining the specification.

## 3. Architecture Authority

GPT-5.6 Luna is the project's architecture and planning authority, acting as:

- Product architect
- Technical architect
- UX architecture reviewer
- Documentation owner
- Prompt engineer
- Task decomposer
- Acceptance reviewer

A local coding model must not independently redefine the product architecture.

If implementation reveals a genuine architectural problem, the model must report it with evidence and proposed options. Architecture changes require explicit approval and documentation before implementation.

## 4. AI Team Responsibilities

### GPT-5.6 Luna

Responsible for product planning, requirements, architecture, UX direction, design-system direction, documentation, task decomposition, prompts, acceptance criteria, reviews, and architectural decisions.

### Qwen3 8B

Senior local engineering/review model. Used for architecture-sensitive implementation, difficult debugging, refactoring, security/accessibility/performance review, and complex code review.

### Qwen3 4B

Primary implementation model. Used for normal HTML, CSS, JavaScript, component, page, and feature development.

### Qwen2.5 1.5B

Utility model. Used for lightweight repository inspection, simple edits, formatting, mechanical transformations, and other low-risk tasks.

### Aider

Repository-aware execution interface. Aider applies approved tasks to the codebase, presents diffs, and works with the selected local model. Aider is not the architectural authority.

## 5. Required AI Development Loop

Every meaningful implementation task follows this sequence:

1. GPT defines the task.
2. GPT identifies affected files and constraints.
3. GPT defines acceptance criteria.
4. GPT writes or approves the model-specific prompt.
5. Aider executes the task with the selected model.
6. The implementation is inspected and tested.
7. Qwen3 8B reviews when the task is architecture-sensitive or quality-critical.
8. GPT performs the project-level acceptance review.
9. Required fixes are implemented.
10. The task passes its gate.
11. A focused Git commit is created.
12. The next task begins.

## 6. Change Control

AI agents must:

- Modify only files necessary for the assigned task.
- Avoid unrelated refactors.
- Avoid speculative dependencies.
- Preserve existing approved architecture.
- Never overwrite user work without explicit approval.
- Report unexpected repository state before making consequential changes.
- Explain what changed, why it changed, and what was verified.

A task is not complete merely because the code runs. It must satisfy its acceptance criteria.

## 7. Architecture Stability

No agent may perform a broad architectural rewrite during an ordinary feature task.

The following require an architecture review:

- changing the application structure
- changing the build/deployment strategy
- introducing a major framework
- adding a major dependency
- changing the data/content model
- changing component boundaries
- changing the styling architecture
- changing the accessibility strategy
- changing public configuration APIs

## 8. Accessibility-First Requirement

Accessibility is a first-class product requirement.

The target is **WCAG 2.2 Level AA**.

Accessibility must be considered during design and implementation, not postponed to final QA.

Expected considerations include:

- semantic HTML
- keyboard access
- visible focus states
- logical focus order
- accessible names and labels
- screen-reader compatibility
- sufficient color contrast
- reduced-motion support
- zoom and text resizing
- touch target usability
- accessible forms and errors
- meaningful link/button semantics
- responsive layouts

Accessibility regressions are release-blocking when they affect core functionality or WCAG 2.2 AA conformance targets.

## 9. UX and Design Principles

The product must be:

- mobile-first
- responsive
- accessible
- clear
- usable without unnecessary interaction complexity
- visually professional
- customizable
- maintainable
- progressively enhanced where practical

Design decisions must support users with different abilities, devices, input methods, and viewport sizes.

## 10. Engineering Principles

Prefer:

- simple solutions
- semantic HTML
- modern CSS
- modular JavaScript
- progressive enhancement
- reusable components
- explicit configuration
- minimal dependencies
- maintainable naming
- predictable behavior
- performance-conscious implementation

Avoid:

- unnecessary frameworks
- unnecessary build complexity
- duplicated logic
- hidden global state
- inaccessible custom controls
- premature abstraction
- dependency bloat
- clever code that is difficult for customers to customize

## 11. Productization Requirements

The repository must eventually produce a package that a customer can download, understand, customize, and deploy without requiring the original developer to manually repair the product.

Customer-facing concerns include:

- installation
- customization
- content editing
- theme customization
- deployment
- troubleshooting
- licensing
- updates

The commercial product must be considered throughout development rather than added only at release time.

## 12. Documentation Rules

Documentation must be updated when an approved architectural, product, UX, design-system, API, configuration, or workflow decision changes.

Documentation must explain decisions clearly enough for another developer or AI agent to implement the project without relying on hidden conversation context.

AI prompts should reference authoritative project documents rather than repeating large amounts of potentially divergent specification text.

## 13. Testing Rules

Testing must cover, as applicable:

- functional behavior
- responsive behavior
- accessibility
- browser compatibility
- SEO fundamentals
- performance
- deployment/installability
- customer customization paths

A feature with unverified critical behavior is not considered finished.

## 14. Security Rules

Never commit:

- API keys
- passwords
- private tokens
- credentials
- personal secrets
- production secrets

Customer-facing functionality must use safe defaults and validate untrusted input where applicable.

Dependencies must be justified and kept to the minimum necessary set.

## 15. Git Rules

Use focused commits with clear messages.

Do not combine unrelated changes into one commit.

Before a milestone is considered complete:

- the working tree should be understood
- tests should be run as applicable
- the relevant documentation should be current
- the final diff should be reviewed

Git history should make the product's development understandable.

## 16. Definition of Done

A task is done only when:

- the requested behavior is implemented
- acceptance criteria are satisfied
- affected documentation is updated
- relevant tests/checks pass
- accessibility implications are reviewed
- no unrelated files were changed unnecessarily
- the implementation does not contradict approved architecture
- the final change is clearly reported

A phase is done only when its phase gate is explicitly passed.

## 17. Stop Conditions

An AI agent must stop and ask for review when:

- requirements are contradictory
- required architecture is missing
- a requested change would invalidate an approved architectural decision
- credentials or secrets are requested
- the agent cannot safely determine the intended behavior
- a destructive or irreversible operation is required
- unrelated existing work would need to be overwritten

## 18. Rule for Model Escalation

Use the smallest capable model for routine work, but escalate when reasoning complexity or risk increases.

Suggested routing:

- Simple/repetitive → Qwen2.5 1.5B
- Normal implementation → Qwen3 4B
- Complex/architecture-sensitive/review → Qwen3 8B
- Product/architecture/documentation/prompt decisions → GPT-5.6 Luna

Model size does not override project authority.

## 19. Rule for AI Reports

After every implementation task, the responsible agent must report:

1. What was changed.
2. Why it was changed.
3. Which files were affected.
4. What tests/checks were run.
5. What passed.
6. What remains unresolved, if anything.

## 20. Project Owner Authority

The project owner has final authority over product direction and release decisions.

GPT-5.6 Luna translates those decisions into an implementable product and architecture plan. Local models execute within those approved boundaries.
