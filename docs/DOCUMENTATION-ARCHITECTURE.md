# Portfolio Pro Template — Documentation Architecture

**Status:** Approved
**Version:** 1.0
**Purpose:** Define the documentation system that serves as the project's shared source of truth for humans and AI agents.

## 1. Documentation Principle

Documentation is part of the product architecture. It is not an afterthought and must not depend on hidden conversation context.

Every important product, architecture, UX, design-system, engineering, testing, deployment, AI-workflow, and commercial decision must be recoverable from the repository.

The documentation system is designed so that a fresh AI agent can enter the repository and understand the approved project without needing previous chat history.

## 2. Documentation Ownership

Each document has one primary responsibility. Documents must not silently duplicate or contradict another document's authority.

| Document | Primary authority | Owns |
|---|---|---|
| `PROJECT-RULES.md` | Governance | Development rules, AI roles, change control, quality principles |
| `PRD.md` | Product | Product vision, users, requirements, scope, acceptance goals |
| `ARCHITECTURE.md` | Technical architecture | System structure, modules, boundaries, data/config architecture |
| `UX.md` | UX | Information architecture, journeys, interaction patterns, responsive behavior |
| `DESIGN-SYSTEM.md` | Visual/design system | Tokens, typography, color, spacing, components, states, motion |
| `COMPONENTS.md` | Component contract | Component inventory, APIs, variants, states, accessibility contracts |
| `DEVELOPMENT.md` | Engineering workflow | Local setup, development commands, conventions, contribution workflow |
| `AI-DEVELOPMENT.md` | AI engineering | Model routing, Aider workflow, prompts, context rules, AI task protocol |
| `TESTING.md` | Quality assurance | Test strategy, test levels, accessibility/performance/browser checks |
| `DEPLOYMENT.md` | Delivery | Build, hosting, deployment, environment requirements, release procedure |
| `CUSTOMIZATION.md` | Customer experience | How buyers customize content, themes, pages, assets, configuration |
| `GUMROAD.md` | Commercial product | Packaging, versions, licensing, pricing assumptions, product-page requirements |

## 3. Authority Hierarchy

When two documents appear to conflict, use this order:

1. `PROJECT-RULES.md` — project-wide governance
2. `PRD.md` — product requirements
3. `ARCHITECTURE.md` — technical architecture
4. `UX.md` — UX decisions
5. `DESIGN-SYSTEM.md` — visual-system decisions
6. Domain-specific operational documents
7. Source code and implementation details

A lower-level document must not redefine a higher-level decision without an explicit architectural/product change.

## 4. Document Lifecycle

Each document follows this lifecycle:

```text
Draft → Review → Approved → Implemented → Maintained
```

Only approved decisions should be treated as binding implementation requirements.

A change that affects an approved decision must update the relevant document before or together with implementation, according to the task plan.

## 5. Required Document Header

Authoritative documents should begin with:

- Status
- Version
- Purpose
- Scope where useful

Recommended statuses:

- `Draft`
- `Under Review`
- `Approved`
- `Superseded`

## 6. Document Specifications

### 6.1 PROJECT-RULES.md

Defines the rules all contributors and AI agents must follow.

It answers:

- Who has authority?
- How do AI agents work?
- What quality bar applies?
- What changes require review?
- What must never be done?

### 6.2 PRD.md

Defines what the product is and why it exists.

It will contain:

- product vision
- problem statement
- goals
- non-goals
- target users
- personas
- use cases
- functional requirements
- non-functional requirements
- accessibility requirements
- SEO requirements
- performance requirements
- customization requirements
- commercial requirements
- release scope
- acceptance criteria

It must not contain implementation details unless a requirement genuinely constrains implementation.

### 6.3 ARCHITECTURE.md

Defines how the product is technically constructed.

It will contain:

- architectural goals
- technology choices
- system boundaries
- repository structure
- application layers
- module responsibilities
- component boundaries
- data/content architecture
- configuration architecture
- styling architecture
- JavaScript architecture
- asset architecture
- build strategy
- deployment architecture
- dependency policy
- security boundaries
- architectural decisions

Architecture decisions should explain the reason for important choices, not merely record the choice.

### 6.4 UX.md

Defines how users experience and navigate the product.

It will contain:

- information architecture
- navigation model
- page hierarchy
- primary user journeys
- interaction patterns
- responsive behavior
- accessibility interaction requirements
- content hierarchy
- empty/error/success states
- motion principles
- usability principles

### 6.5 DESIGN-SYSTEM.md

Defines the visual language.

It will contain:

- design principles
- color tokens
- semantic color roles
- typography
- spacing scale
- sizing
- borders
- radii
- elevation
- breakpoints
- motion tokens
- focus styles
- component visual rules
- light/dark themes

The design system must use semantic tokens where practical so customer customization does not require editing every component individually.

### 6.6 COMPONENTS.md

Defines reusable component contracts.

Each significant component should document:

- purpose
- semantic HTML expectations
- anatomy
- inputs/data
- variants
- states
- responsive behavior
- accessibility requirements
- customization hooks
- dependencies

This document should be implementation-oriented but must not replace `ARCHITECTURE.md`.

### 6.7 DEVELOPMENT.md

Defines how developers work with the repository.

It will contain:

- prerequisites
- installation
- local development
- Docker workflow
- commands
- formatting/linting conventions
- development conventions
- Git workflow
- troubleshooting

### 6.8 AI-DEVELOPMENT.md

Defines how AI agents work in the repository.

It will contain:

- model roles
- model routing
- Aider usage
- context-loading rules
- task prompt structure
- escalation rules
- change-report format
- review workflow
- prohibited AI behavior
- documentation update rules

It must complement, not override, `PROJECT-RULES.md`.

### 6.9 TESTING.md

Defines the quality strategy.

It will contain:

- test pyramid/levels
- unit checks where appropriate
- integration checks
- browser checks
- responsive checks
- accessibility checks
- SEO checks
- performance checks
- installation/customization tests
- release gates

### 6.10 DEPLOYMENT.md

Defines how the finished product is built and delivered.

It will contain:

- supported hosting targets
- static deployment
- traditional hosting considerations
- build process if applicable
- deployment verification
- production checklist
- release procedure
- rollback/update considerations

### 6.11 CUSTOMIZATION.md

Written primarily for customers.

It will contain:

- quick start
- changing identity/content
- adding projects
- changing colors
- changing typography
- changing sections
- adding/removing pages
- replacing assets
- deployment customization
- troubleshooting

The documentation should favor copy/paste-safe instructions and clear examples.

### 6.12 GUMROAD.md

Defines the commercial packaging strategy.

It will contain:

- product editions
- free/pro boundaries
- package contents
- licensing model
- update policy
- support policy
- product-page requirements
- screenshots/demo requirements
- release checklist
- future monetization options

Commercial assumptions must not be allowed to distort core technical architecture without an explicit decision.

## 7. Cross-Document References

Documents should link to the authoritative document when a concept is owned elsewhere.

Examples:

- Product requirement → `PRD.md`
- Technical implementation → `ARCHITECTURE.md`
- Interaction requirement → `UX.md`
- Visual token → `DESIGN-SYSTEM.md`
- Component contract → `COMPONENTS.md`
- Test gate → `TESTING.md`
- Customer instruction → `CUSTOMIZATION.md`

Avoid copying the same requirement into multiple documents unless a short contextual reference is necessary.

## 8. Decision Records

Important architectural decisions should be recorded in `ARCHITECTURE.md` or a future dedicated decision-record directory if the volume becomes large.

Each decision should include:

- context
- problem
- decision
- alternatives considered
- consequences
- status

Do not create a separate decision file for trivial implementation choices.

## 9. AI Context Strategy

AI agents should load only the documents necessary for their current task, while always respecting the project-wide rules.

### Minimum context

Every implementation task:

1. `PROJECT-RULES.md`
2. relevant section of `PRD.md`
3. relevant section of `ARCHITECTURE.md`
4. task-specific UX/design/component/testing documents

### Example

A button task should normally use:

- `PROJECT-RULES.md`
- relevant `PRD.md` requirement
- relevant `ARCHITECTURE.md` section
- `DESIGN-SYSTEM.md`
- `COMPONENTS.md`
- relevant `TESTING.md` requirements

A deployment task should use:

- `PROJECT-RULES.md`
- `ARCHITECTURE.md`
- `DEVELOPMENT.md`
- `DEPLOYMENT.md`
- `TESTING.md`

## 10. Prompt Engineering Rule

GPT-generated implementation prompts must identify authoritative documents instead of relying on conversational memory.

A good prompt should state:

- objective
- context documents
- scope
- files to inspect
- files allowed to change
- constraints
- acceptance criteria
- required verification
- required change report

The prompt must not encourage an AI model to invent missing requirements.

## 11. Documentation Quality Gate

Before a phase is closed, documentation must answer:

- What was decided?
- Why was it decided?
- What changed?
- What remains unresolved?
- What should the next agent know?

If an important decision exists only in chat, it is not considered safely captured project knowledge.

## 12. Planned Documentation Tree

The target documentation structure is:

```text
docs/
├── PROJECT-RULES.md
├── DOCUMENTATION-ARCHITECTURE.md
├── PRD.md
├── ARCHITECTURE.md
├── UX.md
├── DESIGN-SYSTEM.md
├── COMPONENTS.md
├── DEVELOPMENT.md
├── AI-DEVELOPMENT.md
├── TESTING.md
├── DEPLOYMENT.md
├── CUSTOMIZATION.md
└── GUMROAD.md
```

Files should be created as their content becomes sufficiently defined. The tree is the planned documentation architecture, not permission to fill documents with speculative requirements.

## 13. Completion Criteria for Step 0.3

Step 0.3 is complete when:

- documentation ownership is explicit
- authority hierarchy is explicit
- each planned document has a defined purpose
- AI context strategy is defined
- prompt-engineering requirements are defined
- documentation lifecycle is defined
- the planned documentation tree is recorded

The next project step is **Phase 1 — Step 1.1: Product Vision**. Before that step, the authoritative PRD and related documents should be created from approved product decisions rather than assumptions.
