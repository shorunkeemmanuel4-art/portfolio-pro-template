# Portfolio Pro Template — System Architecture

**Status:** Approved
**Version:** 1.0
**Phase:** Phase 2 — Architecture & Technical Design
**Step:** 2.3 — System Architecture

## 1. Purpose

Define the high-level runtime and build-time architecture for Portfolio Pro v1.0. This document translates the approved product requirements and technology decision into explicit system boundaries and data flow.

## 2. Architectural Model

Portfolio Pro is a **content-driven static website with progressive enhancement**.

```text
CUSTOMER CONTENT + CONFIGURATION
              │
              ▼
       ASTRO BUILD SYSTEM
              │
       ┌──────┼──────┐
       ▼      ▼      ▼
    CONTENT  PAGES  COMPONENTS
       │      │      │
       └──────┼──────┘
              ▼
       CSS / DESIGN TOKENS
              │
              ▼
      OPTIONAL JS ENHANCEMENTS
              │
              ▼
        STATIC OUTPUT
              │
              ▼
       STATIC HOST / CDN
              │
              ▼
        PORTFOLIO VISITOR
```

The browser receives pre-rendered HTML and assets. JavaScript is loaded only where an approved interaction requires it.

## 3. System Layers

### Layer 1 — Content

Owns portfolio information rather than presentation behavior.

Examples:

- identity
- biography
- skills
- experience
- projects
- case studies
- services
- testimonials
- articles
- social/contact information

### Layer 2 — Site Configuration

Owns global customer-controlled settings.

Examples:

- site name
- navigation
- metadata defaults
- social links
- contact details
- theme configuration
- feature/section switches where approved

### Layer 3 — Presentation Components

Own reusable visual and semantic structures.

Examples:

- Header
- navigation
- hero
- section shell
- project card
- case-study block
- buttons/links
- forms
- footer

Components consume content/configuration but should not own customer data.

### Layer 4 — Styling / Design System

Owns:

- design tokens
- typography
- spacing
- layout primitives
- color system
- responsive rules
- states
- accessibility-related visual behavior

### Layer 5 — Behavior

Owns only client-side enhancements that require JavaScript.

Examples:

- mobile navigation state
- theme switching when implemented
- disclosure behavior
- optional filtering

### Layer 6 — Build

Astro transforms source, content, components, styles, and approved client-side behavior into the deployable static site.

### Layer 7 — Deployment

Static output is deployed to a supported static host/CDN.

## 4. Build-Time vs Runtime Responsibilities

| Responsibility | Build time | Browser runtime |
|---|---:|---:|
| Content rendering | Yes | No for core content |
| Page generation | Yes | No |
| Metadata generation | Yes | No for initial document |
| CSS generation/bundling | Yes | Browser applies CSS |
| Project/case-study markup | Yes | No |
| Navigation links | Yes | Browser follows links |
| Mobile menu state | No | Yes, if implemented with JS |
| Optional interactive enhancements | No | Yes |
| Analytics | Optional | Only if explicitly configured |

## 5. Rendering Strategy

### Default

Use static rendering for public portfolio content.

### Client-side rendering

Do not use client-side rendering for the entire site.

### Hydration

Hydrate/island-render only interactive components that demonstrably require client-side state or browser APIs.

### Server runtime

No server runtime is required for the v1.0 core product.

## 6. Page Architecture

The exact page inventory will be finalized during UX and content architecture, but the system must support at least:

```text
/
├── Home
├── About or profile content
├── Projects
│   └── Project detail / case study
├── Services (if enabled)
├── Articles / blog presentation (if enabled)
└── Contact
```

Some sections may remain on the homepage while others may be promoted to routes. The final route map must be documented before implementation.

## 7. Content-to-Page Flow

```text
Structured Content
       │
       ▼
Content Validation / Type Checking
       │
       ▼
Page / Route Data
       │
       ▼
Astro Components
       │
       ▼
Semantic HTML
       │
       ├── CSS
       │
       └── Optional JS enhancement
       │
       ▼
Static HTML + Assets
```

Invalid content shapes should be caught as early as practical during development/build rather than becoming silent runtime failures.

## 8. Component Boundary Rules

1. Components should have one clear presentation/interaction responsibility.
2. Components should receive data through explicit props/content interfaces.
3. Components should not silently fetch remote application data for core content.
4. Interactive components must own their accessibility behavior.
5. Global configuration must not be duplicated inside components.
6. Reuse must not create abstractions that are harder to understand than the duplicated markup they replace.

## 9. Content Ownership Rules

Customer-editable information should have an obvious ownership location.

```text
CUSTOMER DATA
├── Identity
├── Navigation
├── Projects
├── Case Studies
├── Experience
├── Services
├── Testimonials
├── Articles
├── Contact
└── SEO defaults
```

The exact file/directory representation is deferred to Step 2.5.

## 10. Styling Boundary

Styling must not require components to contain arbitrary customer-specific values.

```text
Design Tokens
      ↓
Theme / Global Styles
      ↓
Component Styles
      ↓
Page Composition
```

Customer theme changes should primarily occur through documented token/configuration mechanisms.

## 11. JavaScript Boundary

JavaScript is isolated from content rendering wherever possible.

```text
CORE CONTENT ───────────────► HTML
                                  ▲
                                  │
OPTIONAL BEHAVIOR ──► JS ─────────┘
```

Failure of a non-essential enhancement must not remove access to core content.

## 12. Accessibility Boundary

Accessibility applies across every layer:

```text
CONTENT
  ↓ semantic meaning
COMPONENTS
  ↓ names / roles / states
CSS
  ↓ contrast / focus / reflow / motion
JS
  ↓ keyboard / focus / state management
OUTPUT
  ↓ usable document
```

Accessibility cannot be isolated into a single utility or component.

## 13. SEO Boundary

SEO responsibilities are distributed:

- content provides meaningful information
- pages provide document structure
- configuration provides site defaults
- metadata components provide page metadata
- routes provide stable URLs
- static rendering exposes crawlable HTML

SEO is not delegated entirely to a package.

## 14. Security Boundary

The static core has a deliberately small attack surface.

Security responsibilities include:

- no secrets in repository/source
- safe handling of configurable URLs and content
- dependency review
- safe external-link practices where appropriate
- careful handling of any future form/integration service

A contact form service, analytics provider, or other third-party integration is outside the core static runtime unless explicitly approved.

## 15. External Service Boundary

External services are optional adapters around the core product.

```text
                  PORTFOLIO CORE
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
       Contact      Analytics    Hosting
       Adapter       Adapter      Adapter
          │            │            │
       Optional      Optional     Replaceable
```

No external provider should be required for basic portfolio content to render.

## 16. Free / Pro Boundary

Free and Pro should share the same architectural foundations.

Potential differences should occur through:

- content packages
- additional components
- additional layouts
- configuration
- packaging
- licensing

Avoid creating two unrelated application architectures.

## 17. Deployment Flow

```text
Source Repository
       │
       ▼
Install Dependencies
       │
       ▼
Validate / Test
       │
       ▼
Astro Build
       │
       ▼
Static Artifact
       │
       ▼
Static Host / CDN
```

The exact CI/CD implementation is deferred to Step 2.11.

## 18. Failure Philosophy

The architecture should fail safely.

Examples:

- optional JS fails → core content remains usable
- analytics fails → portfolio remains usable
- optional external integration fails → core site remains usable
- missing optional content → section is omitted or handled intentionally
- invalid required content → build should fail clearly

## 19. Observability / Diagnostics

For v1.0, diagnostics should primarily operate during development/build rather than introducing a runtime monitoring platform.

Build errors should identify:

- invalid content
- invalid configuration
- broken references where detectable
- type errors
- test failures

## 20. Architecture Invariants

The following are architectural invariants unless a future approved decision changes them:

1. Core portfolio content is statically rendered.
2. JavaScript is progressive enhancement.
3. No mandatory backend exists for v1.0.
4. Gumroad is not a runtime dependency.
5. Customer content/configuration has a clear boundary from reusable implementation.
6. Free and Pro share architectural foundations.
7. Accessibility is cross-layer.
8. SEO is designed into the generated document.
9. Dependencies require justification.
10. AI coding agents do not autonomously change these invariants.

## 21. Architecture Gate

Step 2.3 is complete when the system layers, rendering model, data flow, page model, component boundaries, content ownership, styling/behavior boundaries, external-service boundaries, security model, deployment flow, failure philosophy, and architecture invariants are documented.

Next step: **Phase 2 — Step 2.4: Repository Architecture & Directory Structure.**
