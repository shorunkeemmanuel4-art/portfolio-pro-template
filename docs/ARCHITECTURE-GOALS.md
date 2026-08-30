# Portfolio Pro Template — Architecture Goals & Technical Constraints

**Status:** Approved
**Version:** 1.0
**Phase:** Phase 2 — Architecture & Technical Design
**Parent:** `docs/PRD.md`, `docs/REQUIREMENTS.md`, `docs/PRODUCT-SCOPE.md`, `docs/COMMERCIAL-DISTRIBUTION.md`

## 1. Purpose

This document establishes the architectural goals and technical constraints that the detailed system architecture must satisfy.

It deliberately does not select the final framework, build tool, or implementation structure. Those choices must be justified against these constraints in the next architecture steps.

## 2. Architecture North Star

Build a **lightweight, accessible, responsive, SEO-friendly, customizable, maintainable, commercially distributable portfolio template** that can be understood and modified by developers without requiring a large runtime ecosystem.

## 3. Architectural Goals

### AG-001 — Product-first architecture

Technical decisions must support the approved product requirements rather than determine them.

### AG-002 — Accessibility by construction

Accessibility must be designed into semantic structure, components, styling, interaction, focus management, forms, and motion rather than added as a final audit step.

Target: WCAG 2.2 Level AA.

### AG-003 — Mobile-first

The system must support small screens first and progressively enhance for larger viewports.

### AG-004 — Performance-conscious

The architecture should minimize shipped code, unnecessary JavaScript, third-party dependencies, blocking resources, and avoidable network requests.

### AG-005 — SEO-ready

The architecture must allow crawlable content, meaningful metadata, semantic document structure, clean URLs where applicable, and social metadata without unnecessary client-side rendering dependencies.

### AG-006 — Configuration-friendly customization

Common customer changes should be separated from reusable implementation logic where practical.

### AG-007 — Maintainability

A competent external developer should be able to understand the source tree, identify responsibilities, modify components, and debug the product without depending on hidden project knowledge.

### AG-008 — Static-first deployment

The default architecture should support static hosting unless a documented requirement proves that server-side infrastructure is necessary.

### AG-009 — Platform independence

Gumroad, payment providers, analytics, hosting providers, and download platforms must not become runtime dependencies of the portfolio template.

### AG-010 — Product edition compatibility

Free and Pro editions should be supportable from a coherent architecture without maintaining unrelated implementations.

### AG-011 — Progressive enhancement

Core content and navigation should remain useful with minimal client-side behavior. JavaScript should enhance experiences rather than unnecessarily become a prerequisite for basic content access.

### AG-012 — Documentation-driven development

Architecture decisions must be recoverable from repository documentation. Implementation agents must not rely on private chat history for essential requirements.

## 4. Technical Constraints

### TC-001 — Minimal dependency burden

Dependencies must have a clear purpose and measurable benefit. Avoid adding a framework or package merely because it is conventional.

### TC-002 — No unnecessary backend

The v1.0 product should not require a custom backend unless an approved requirement cannot reasonably be met otherwise.

### TC-003 — No mandatory proprietary runtime service

The downloaded template must remain functional without a mandatory proprietary SaaS runtime.

### TC-004 — No secrets in source

The template must never require customers to commit secrets or private credentials into public source files.

### TC-005 — Customer customization must survive normal updates

Architecture should minimize coupling between customer-owned content/configuration and product implementation.

### TC-006 — Accessibility cannot be an edition downgrade

Free and Pro editions must not intentionally ship materially inferior accessibility foundations.

### TC-007 — Browser support must be explicit

Supported browser versions must be documented before release. Unsupported browser behavior must not be guessed during implementation.

### TC-008 — Performance budgets must become measurable

Qualitative performance goals are insufficient for release. Specific budgets and test methods must be established before v1.0 release.

### TC-009 — Build output must be deployable

The architecture must produce a clear deployable artifact and document how it is generated.

### TC-010 — Source must be portable

The product should not depend on a single developer's machine paths, undocumented global packages, or local-only services.

## 5. Architectural Quality Attributes

The architecture will be evaluated against:

| Attribute | Target |
|---|---|
| Accessibility | WCAG 2.2 AA target |
| Responsiveness | Mobile-first |
| Performance | Lightweight, measurable budgets |
| SEO | Strong technical foundation |
| Security | Safe defaults, no shipped secrets |
| Maintainability | Clear boundaries and documentation |
| Customizability | Centralized content/theme controls |
| Deployment | Static-first |
| Portability | Minimal environment assumptions |
| Commercial packaging | Free/Pro compatible |

## 6. Architecture Boundaries

The detailed architecture must distinguish at least these conceptual concerns:

```text
CONTENT / CUSTOMER DATA
        │
        ▼
PRESENTATION / COMPONENTS
        │
        ▼
STYLES / DESIGN TOKENS
        │
        ▼
BEHAVIOR / ENHANCEMENT
        │
        ▼
BUILD / OUTPUT
        │
        ▼
DEPLOYMENT
```

The final architecture may refine these boundaries, but responsibilities must remain understandable.

## 7. Content Architecture Goal

Portfolio content should be represented in a way that makes routine changes predictable.

The architecture should answer:

- Where does personal identity live?
- Where do projects live?
- How are case studies represented?
- Where are social links configured?
- Where is site metadata configured?
- How are optional sections enabled or disabled?

The exact content model remains an open decision for the detailed architecture phase.

## 8. Styling Architecture Goal

The styling system should support:

- semantic design tokens
- responsive behavior
- theme customization
- accessible states
- component-level styles without uncontrolled global leakage
- maintainable CSS

The final styling methodology remains open until the architecture decision process.

## 9. JavaScript Architecture Goal

JavaScript should be:

- minimal
- modular
- progressively enhanced
- accessible
- testable
- avoidant of unnecessary global state

The final JavaScript strategy remains an open decision.

## 10. Component Architecture Goal

Reusable components should have clear responsibility and stable contracts.

A component should not own unrelated application concerns merely because it is convenient.

Components must support accessibility states as first-class behavior.

## 11. Free/Pro Architecture Goal

The technical system should permit edition differences through maintainable composition/configuration/packaging rather than duplicated codebases.

The exact implementation mechanism remains open.

## 12. AI/Agent Architecture Constraint

AI coding agents are implementation participants, not architectural authorities.

The workflow is:

```text
Approved requirements
        ↓
GPT architecture/planning
        ↓
Approved architecture
        ↓
GPT task/prompt engineering
        ↓
Aider + local model implementation
        ↓
Verification
        ↓
GPT review / escalation
```

If an implementation agent identifies a conflict with the approved architecture, it must report the conflict rather than silently redesigning the system.

## 13. Architecture Decision Rule

A technology should be selected only after evaluating:

1. product fit
2. accessibility support
3. performance impact
4. SEO implications
5. customization experience
6. maintainability
7. deployment simplicity
8. dependency burden
9. developer familiarity/availability
10. commercial packaging implications

Popularity alone is not sufficient justification.

## 14. Explicit Non-Goals

The architecture will not optimize for:

- maximum framework complexity
- maximum number of dependencies
- premature abstraction
- backend infrastructure without need
- vendor lock-in
- AI-generated code volume
- feature count at the expense of quality

## 15. Architecture Gate

Step 2.1 is complete when the architecture goals, quality attributes, technical constraints, boundaries, AI governance, and technology-selection criteria are documented.

Next step: **Phase 2 — Step 2.2: Technology & Stack Decision.**
