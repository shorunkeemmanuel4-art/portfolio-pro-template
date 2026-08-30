# Portfolio Pro Template — Content Architecture & Data Model

**Status:** Approved
**Version:** 1.0
**Phase:** Phase 2 — Architecture & Technical Design
**Step:** 2.5 — Content Architecture

## 1. Purpose

Define how portfolio information is represented, validated, related, and consumed by the Astro site.

The content architecture must make normal customer customization simple while keeping presentation code reusable.

## 2. Core Principle

**Content describes the user's work; components describe how that work is presented.**

```text
CUSTOMER CONTENT
      ↓
VALIDATED CONTENT MODEL
      ↓
PAGE / ROUTE DATA
      ↓
REUSABLE COMPONENTS
      ↓
STATIC HTML
```

Content must not contain presentation-specific implementation by default.

## 3. Content Categories

The v1.0 model is divided into two categories.

### Structured collections

Use repeatable entries for information that naturally occurs as a list or has its own identity/slug.

```text
projects/
case-studies/
articles/
experience/
testimonials/
```

### Global configuration

Use typed configuration for information that describes the site as a whole.

```text
site.ts
navigation.ts
theme.ts
```

## 4. Site Identity Model

The site configuration must support at least:

```text
site
├── name
├── title
├── description
├── url
├── locale
├── author
│   ├── name
│   ├── role
│   └── bio/summary
├── contact
│   ├── email (optional)
│   └── location (optional)
├── socialLinks
└── seoDefaults
```

Required/optional status will be enforced through TypeScript/content validation.

Sensitive credentials must never be represented as portfolio content.

## 5. Navigation Model

Navigation should be represented as structured configuration rather than hard-coded independently in multiple pages.

Conceptually:

```text
navigation[]
├── label
├── href
├── external
├── order
└── visible
```

Only fields genuinely needed by the implementation should be retained.

Navigation labels must be meaningful and should not be used as a substitute for accessible names where a component requires a more specific accessible label.

## 6. Project Model

A project represents a portfolio item and may optionally link to a detailed case study.

Conceptual schema:

```text
Project
├── slug                 required
├── title                required
├── summary              required
├── description          optional
├── role                 optional
├── year                 optional
├── client               optional
├── category             optional
├── skills[]             optional
├── image                optional
├── featured             optional/default false
├── order                optional
├── links[]              optional
└── caseStudy            optional reference
```

### Project links

A link should distinguish at least:

```text
label
url
kind
external
```

The final allowed `kind` values will be defined in the implementation schema.

## 7. Case Study Model

A case study provides deeper project information.

Conceptual schema:

```text
CaseStudy
├── slug                 required
├── title                required
├── project              required reference
├── excerpt              optional
├── heroImage            optional
├── overview             optional
├── problem              optional
├── goals[]              optional
├── process[]            optional
├── solution             optional
├── outcome              optional
├── results[]            optional
├── technologies[]       optional
├── gallery[]            optional
└── links[]              optional
```

The model should support narrative content without forcing every customer to fill every section.

Empty optional sections should not render empty headings or visual gaps.

## 8. Experience Model

Experience entries represent employment, freelance work, internships, or other approved professional history.

Conceptual schema:

```text
Experience
├── id/slug              required
├── role                 required
├── organization         required
├── location             optional
├── startDate            required
├── endDate              optional
├── current              optional/default false
├── summary              optional
├── responsibilities[]   optional
├── achievements[]       optional
└── technologies[]       optional
```

Dates should use machine-readable values while presentation formatting remains a UI responsibility.

## 9. Skills Model

Skills are primarily reusable labels associated with expertise and projects.

A skill may be represented by a simple string where no additional metadata is required.

If additional metadata becomes necessary, use a typed object rather than embedding presentation markup.

Avoid premature rating systems such as arbitrary percentage proficiency unless a product requirement establishes a meaningful accessible representation.

## 10. Services Model

Services are optional repeatable offerings.

Conceptual schema:

```text
Service
├── id/slug
├── title
├── summary
├── description (optional)
├── features[] (optional)
├── icon (optional)
└── order (optional)
```

The service icon must never be the only source of meaning.

## 11. Testimonial Model

Conceptual schema:

```text
Testimonial
├── id/slug
├── quote
├── person
├── role (optional)
├── organization (optional)
├── image (optional)
└── order (optional)
```

Testimonials should be treated as content claims supplied by the customer. The template must not invent testimonials.

## 12. Article Model

Articles are optional in v1.0 but the content architecture should support them without forcing a blog onto every portfolio.

Conceptual schema:

```text
Article
├── slug                 required
├── title                required
├── description          required
├── publishedDate        required
├── updatedDate          optional
├── author               optional/reference
├── tags[]               optional
├── image                optional
├── draft                optional/default false
└── body                 required
```

The body may use the structured content format supported by the final Astro content implementation.

## 13. Contact Model

Contact information belongs in global configuration when it describes how the site owner can be reached.

Conceptually:

```text
contact
├── email
├── phone (optional)
├── location (optional)
├── availability (optional)
└── links[] (optional)
```

A contact form is a separate interaction concern and must not require a custom backend for the static core.

## 14. SEO Metadata Model

Each page/content entry should be able to provide metadata where appropriate.

Conceptual model:

```text
seo
├── title
├── description
├── canonicalUrl (optional)
├── image (optional)
├── noindex (optional)
└── social metadata overrides (optional)
```

Global defaults should provide sensible fallbacks.

Page-specific metadata overrides must not accidentally remove required global metadata.

## 15. Media Model

Media references should contain enough information for accessible and predictable rendering.

Conceptually:

```text
image
├── src
├── alt
├── width (where known)
├── height (where known)
└── caption (optional)
```

Decorative imagery must have an intentionally empty alternative text value where appropriate rather than invented descriptive text.

The exact media handling strategy will be finalized during performance/build architecture.

## 16. Relationships

Primary relationship:

```text
Project
   │
   └──────► CaseStudy
```

Additional relationships may include:

```text
Project ───► Skills
Article ───► Tags
Experience ─► Skills
```

References should use stable identifiers/slugs rather than duplicated large content objects.

Broken required references should fail validation/build clearly.

## 17. Required vs Optional Content

The model must distinguish between required information and optional sections.

### Required at site level

Enough information to produce:

- a meaningful document title
- an identifiable site/author
- navigable core content

### Optional

Examples include:

- services
- testimonials
- experience
- articles
- phone number
- location
- individual project fields

Optional data must be handled intentionally by components.

## 18. Empty-State Rule

The content system must never require customers to insert placeholder content merely to make a component render.

```text
Data exists     → render section
Data absent     → omit/handle intentionally
Required data absent → build/validation error
```

## 19. Ordering

Collections that need ordering may support an explicit `order` field or derive ordering from a documented content convention.

The same collection must use one predictable ordering strategy rather than mixing arbitrary mechanisms.

## 20. Slug Rules

Slugs must be:

- stable
- URL-safe
- unique within their collection
- independent of visual title formatting where practical

Changing a title should not automatically change a URL unless the customer intentionally changes the slug.

## 21. Draft Rules

Draft content must not accidentally appear in production output.

Where drafts are supported:

```text
Draft = true
     ↓
excluded from production routes/listings
```

The exact implementation depends on the final content tooling.

## 22. Validation Strategy

Validation should occur at build/development time.

Validation should catch at least:

- missing required fields
- invalid dates
- malformed URLs where detectable
- duplicate slugs
- invalid references
- invalid enum values
- invalid configuration shapes

The final validation implementation will be documented during build architecture.

## 23. Content Security Rules

Customer content must not be treated as trusted executable code.

Avoid allowing arbitrary customer-provided scripts or unsafe HTML by default.

If rich HTML/MDX is permitted, the security and content-authoring boundary must be explicitly documented and tested.

## 24. Customer Editing Experience

Documentation should make the common workflow predictable:

```text
Edit content
   ↓
Run local development server
   ↓
Review visually
   ↓
Run validation/tests
   ↓
Build
   ↓
Deploy
```

A customer should not need to understand the internal component architecture to perform routine content edits.

## 25. Content / Presentation Separation

Do not place these inside normal content data:

- CSS classes chosen only for visual styling
- arbitrary component imports
- client-side state
- JavaScript implementation
- secret credentials
- duplicated navigation markup

Controlled semantic variants may be introduced later if they solve a real product requirement.

## 26. Free / Pro Content Strategy

Free and Pro may contain different content examples, layouts, or collections, but the underlying content contracts should remain compatible wherever practical.

A Pro-only content field should be introduced only when it represents a genuine Pro capability.

The content schema must not become a collection of arbitrary edition flags.

## 27. Accessibility Requirements in the Data Model

Content schemas must support accessible output.

Examples:

- images support alternative text
- links have meaningful labels
- headings come from semantic content hierarchy rather than arbitrary visual labels
- dates have machine-readable values
- decorative content can be explicitly marked/handled

Accessibility responsibility remains with the consuming component as well as the content model.

## 28. Example Conceptual Project

```yaml
slug: redesign-client-site
title: Client Website Redesign
summary: Redesigned a responsive marketing website.
role: UX Designer & Developer
year: 2026
skills:
  - UX Design
  - Accessibility
  - Frontend Development
featured: true
caseStudy: redesign-client-site
links:
  - label: View project
    url: https://example.com
    kind: live
```

This is illustrative only; the final serialization/schema syntax is an implementation decision.

## 29. Data Flow

```text
Content Files
     ↓
Astro Content Layer
     ↓
Schema Validation
     ↓
Typed Collection Data
     ↓
Route Generation
     ↓
Components
     ↓
Accessible HTML
```

## 30. Content Architecture Invariants

1. Content and presentation remain separate.
2. Required data is validated.
3. Optional data does not create broken UI.
4. Stable slugs identify route content.
5. References are validated.
6. Drafts do not leak into production.
7. Customer content cannot require secrets.
8. Content does not contain arbitrary implementation logic by default.
9. Accessibility-supporting fields are available where needed.
10. Free/Pro variants do not create uncontrolled schema fragmentation.

## 31. Architecture Gate

Step 2.5 is complete when the content categories, global configuration, schemas, relationships, validation rules, media strategy, accessibility implications, customization boundary, and Free/Pro content strategy are documented.

Next step: **Phase 2 — Step 2.6: Component Architecture.**
