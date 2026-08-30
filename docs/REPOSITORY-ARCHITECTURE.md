# Portfolio Pro Template — Repository Architecture

**Status:** Approved
**Version:** 1.0
**Phase:** Phase 2 — Architecture & Technical Design
**Step:** 2.4 — Repository Architecture

## 1. Purpose

Define the physical repository structure that implements the approved system architecture while keeping customer content, reusable product code, design-system code, tests, documentation, and build configuration clearly separated.

## 2. Target Repository Tree

```text
portfolio-pro-template/
├── .github/
│   └── workflows/
│       ├── ci.yml
│       └── deploy.yml
│
├── docs/
│   ├── PRD.md
│   ├── UX.md
│   ├── DESIGN-SYSTEM.md
│   ├── ARCHITECTURE.md
│   ├── ARCHITECTURE-GOALS.md
│   ├── TECH-STACK-DECISION.md
│   ├── SYSTEM-ARCHITECTURE.md
│   ├── REPOSITORY-ARCHITECTURE.md
│   ├── REQUIREMENTS.md
│   ├── USER-PERSONAS.md
│   ├── PRODUCT-SCOPE.md
│   ├── COMMERCIAL-DISTRIBUTION.md
│   └── decisions/
│       └── README.md
│
├── public/
│   ├── favicon.svg
│   ├── robots.txt
│   └── ...static-public-assets
│
├── src/
│   ├── components/
│   │   ├── accessibility/
│   │   ├── layout/
│   │   ├── navigation/
│   │   ├── sections/
│   │   ├── projects/
│   │   ├── case-studies/
│   │   ├── forms/
│   │   └── ui/
│   │
│   ├── content/
│   │   ├── config.ts
│   │   ├── projects/
│   │   ├── case-studies/
│   │   ├── articles/
│   │   ├── testimonials/
│   │   └── experience/
│   │
│   ├── config/
│   │   ├── site.ts
│   │   ├── navigation.ts
│   │   └── theme.ts
│   │
│   ├── layouts/
│   │   ├── BaseLayout.astro
│   │   └── ...additional-approved-layouts
│   │
│   ├── pages/
│   │   ├── index.astro
│   │   ├── about.astro
│   │   ├── projects/
│   │   │   ├── index.astro
│   │   │   └── [...slug].astro
│   │   ├── services.astro
│   │   ├── articles/
│   │   │   ├── index.astro
│   │   │   └── [...slug].astro
│   │   ├── contact.astro
│   │   └── 404.astro
│   │
│   ├── scripts/
│   │   ├── navigation.ts
│   │   ├── theme.ts
│   │   └── ...approved-enhancements
│   │
│   ├── styles/
│   │   ├── tokens.css
│   │   ├── globals.css
│   │   ├── base.css
│   │   ├── layout.css
│   │   ├── utilities.css
│   │   └── components/
│   │       └── ...component styles where justified
│   │
│   └── types/
│       ├── content.ts
│       └── site.ts
│
├── tests/
│   ├── accessibility/
│   ├── components/
│   ├── content/
│   ├── pages/
│   ├── performance/
│   └── smoke/
│
├── scripts/
│   ├── validate-content.ts
│   ├── validate-links.ts
│   └── ...approved-build/release scripts
│
├── .editorconfig
├── .gitignore
├── astro.config.ts
├── package.json
├── package-lock.json
├── tsconfig.json
├── README.md
└── LICENSE
```

The tree is an **approved target architecture**, not a requirement to create every empty directory immediately. Directories should be created when they have real content or when a toolchain requires them.

## 3. Root Responsibilities

### `src/`

All primary application/site source code.

### `public/`

Files copied directly to the final output without going through the normal source transformation pipeline. Only genuinely public/static assets belong here.

### `tests/`

Verification code and automated quality checks.

### `scripts/`

Repository maintenance, validation, or release tooling that is not part of the deployed website runtime.

### `docs/`

Human-readable product, UX, design, architecture, commercial, and engineering decisions.

### `.github/`

Repository automation and CI/CD workflows.

## 4. Source Boundaries

### `src/components/`

Reusable presentation and interaction components.

Components should not become a dumping ground for content or configuration.

### `src/content/`

Customer-editable structured portfolio content.

This directory is deliberately separated from reusable components so a customer can change portfolio data without modifying presentation implementation.

### `src/config/`

Global customer/site configuration that is not naturally represented as repeatable content entries.

Examples:

- site identity
- navigation
- global metadata defaults
- theme configuration

### `src/layouts/`

Page-level structural wrappers and document layouts.

### `src/pages/`

Astro route entry points.

Pages compose content, layouts, and components. They should not contain large amounts of reusable component markup.

### `src/scripts/`

Client-side progressive-enhancement modules.

No arbitrary application-wide JavaScript state should be placed here.

### `src/styles/`

Global CSS and design-system styles.

### `src/types/`

Shared TypeScript contracts where keeping types separate improves clarity. Types should not be duplicated unnecessarily across the repository.

## 5. Customer Customization Boundary

The intended customization boundary is:

```text
CUSTOMER-OWNED / COMMONLY EDITED
├── src/content/
├── src/config/
└── src/styles/tokens.css

PRODUCT IMPLEMENTATION
├── src/components/
├── src/layouts/
├── src/pages/
├── src/scripts/
├── src/styles/base.css
└── src/styles/layout.css
```

This boundary is a design goal. Exact customer-facing customization instructions will be finalized after the content and design-system architecture steps.

## 6. Page Responsibility Rule

A page should primarily:

1. obtain the appropriate data
2. compose the appropriate layout
3. select components
4. provide route-specific metadata

A page should not become the permanent home for reusable markup.

## 7. Component Responsibility Rule

A component should:

- have a clear responsibility
- accept explicit data/props
- render semantic structure
- own its relevant accessibility behavior
- avoid hidden dependencies on unrelated global state

## 8. Content Responsibility Rule

Content entries should describe information, not reproduce presentation markup.

For example, a project entry should contain information such as:

```text
slug
name
summary
description
role
skills
image
links
featured
```

It should not contain arbitrary HTML/CSS intended to bypass the component system unless a future content architecture decision explicitly permits a controlled rich-content format.

## 9. CSS Responsibility Rule

### `tokens.css`

Design tokens and theme variables.

### `globals.css`

Global CSS configuration and high-level defaults.

### `base.css`

Element normalization, typography defaults, focus foundations, and base accessibility behavior.

### `layout.css`

Shared layout primitives and responsive structural rules.

### `utilities.css`

Only small, intentional utilities that improve consistency and do not become a replacement for component architecture.

### `styles/components/`

Component-specific styles only where colocating styles materially improves maintainability.

## 10. JavaScript Responsibility Rule

Client scripts must be:

- narrowly scoped
- independently understandable
- keyboard/accessibility aware
- safe when unavailable
- tested where behavior is critical

The preferred failure mode is that enhanced behavior disappears while core content remains usable.

## 11. Test Architecture

Tests are grouped by quality concern rather than implementation file alone.

```text
Accessibility
   ↓
Components
   ↓
Content
   ↓
Pages
   ↓
Performance
   ↓
Smoke / integration
```

The exact test runner and tools will be selected during implementation planning.

## 12. Documentation Architecture

The repository documentation should remain the source of truth for decisions that affect implementation.

Architecture decisions should be recorded so that a future coding agent can reconstruct project intent from the repository itself.

## 13. Architecture Decision Records

`docs/decisions/` will contain significant architecture decision records after the detailed architecture establishes decisions that deserve individual history.

Do not create an ADR for every trivial implementation choice.

## 14. CI/CD Boundary

`.github/workflows/` should contain automated workflows for quality verification and deployment only after those workflows are approved.

CI should validate the same quality gates expected locally where practical.

## 15. File Naming Rules

Use consistent naming appropriate to the technology:

- Astro components: `PascalCase.astro`
- TypeScript modules: `kebab-case.ts` unless a strong convention requires otherwise
- CSS files: `kebab-case.css`
- Content entries: stable human-readable slugs/names appropriate to the content system
- Documentation: `UPPERCASE-WITH-HYPHENS.md` for major project documents

The final naming convention may be refined if the selected Astro/content tooling imposes a better established pattern.

## 16. Import / Dependency Direction

Preferred direction:

```text
CONTENT / CONFIG
       ↓
   COMPONENTS
       ↓
     PAGES
       ↓
     OUTPUT
```

Shared types/utilities may support multiple layers, but lower-level styling or utility modules must not import page-level application modules.

Avoid circular dependencies.

## 17. Build Artifacts

Generated output must not be treated as source.

Build artifacts should remain outside source-controlled directories unless a deployment strategy explicitly requires otherwise.

Typical generated directories such as `dist/` must not be manually edited.

## 18. Environment Files

Environment variables are allowed only where a future optional integration genuinely requires them.

Rules:

- never commit secrets
- provide safe example configuration where necessary
- distinguish public build-time configuration from private secrets
- document required variables

The v1.0 static core should require no secrets to build.

## 19. Free / Pro Packaging Boundary

Free and Pro assets should not be mixed ambiguously inside ordinary source directories.

The final packaging strategy may use separate release assembly directories or build/package scripts.

The source architecture should remain unified wherever possible.

## 20. Repository Cleanliness Rules

Do not commit:

- dependency directories
- generated build output
- local machine paths
- editor-specific temporary files
- credentials/secrets
- debugging artifacts
- customer-specific private information

## 21. Aider/Qwen Working Rules

Before modifying files, an AI coding agent must:

1. read the relevant requirements
2. read the relevant architecture document
3. identify the files in scope
4. avoid unrelated refactoring
5. preserve architectural boundaries
6. run the required verification after changes
7. explain what changed, what was not changed, and why

An agent must not create a new top-level architectural directory merely because it finds the existing structure inconvenient.

## 22. Initial Implementation Order

When implementation begins, the repository should be established in approximately this order:

```text
1. Toolchain/configuration
2. Global styles/tokens
3. Content/configuration model
4. Base layout
5. Accessibility/navigation foundations
6. Core components
7. Homepage
8. Project/case-study routes
9. Optional sections
10. Progressive enhancements
11. Tests
12. Documentation
13. Build/deployment automation
```

This is a sequencing guide, not permission to implement before architecture is frozen.

## 23. Directory Creation Rule

Do not create speculative directories for hypothetical future functionality.

Every directory should have:

- an approved responsibility
- an expected consumer
- a reason to exist

This keeps the commercial template approachable for customers.

## 24. Repository Architecture Gate

Step 2.4 is complete when the target repository tree, directory responsibilities, source boundaries, customization boundary, dependency direction, test/documentation structure, environment rules, packaging boundary, and AI working rules are documented.

Next step: **Phase 2 — Step 2.5: Content Architecture & Data Model.**
