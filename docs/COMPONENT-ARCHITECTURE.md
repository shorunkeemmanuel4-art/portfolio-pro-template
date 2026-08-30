# Portfolio Pro Template — Component Architecture

**Status:** Approved
**Version:** 1.0
**Phase:** Phase 2 — Architecture & Technical Design
**Step:** 2.6 — Component Architecture

## 1. Purpose

Define the component hierarchy, responsibilities, interfaces, composition rules, accessibility responsibilities, and reuse boundaries for Portfolio Pro v1.0.

## 2. Component Philosophy

Components exist to create **clear, reusable semantic structures**, not to maximize component count.

The governing rule is:

> Create a component when a structure has a stable responsibility, meaningful reuse, or independent interaction/accessibility behavior.

Do not create components solely because a block contains a few lines of markup.

## 3. Component Hierarchy

The approved conceptual hierarchy is:

```text
SITE SHELL
├── BaseLayout
│
├── Header
│   ├── Brand
│   └── Navigation
│       └── NavigationItem
│
├── Main
│   ├── Hero
│   ├── AboutSection
│   ├── SkillsSection
│   ├── ExperienceSection
│   ├── ProjectsSection
│   │   └── ProjectCard
│   ├── CaseStudy
│   │   ├── CaseStudyHeader
│   │   ├── CaseStudySection
│   │   ├── Results
│   │   └── Gallery
│   ├── ServicesSection
│   │   └── ServiceCard
│   ├── TestimonialsSection
│   │   └── TestimonialCard
│   ├── ArticlesSection
│   │   └── ArticleCard
│   └── ContactSection
│
└── Footer
```

This is a conceptual hierarchy. The final source tree may combine or split components when implementation evidence justifies it.

## 4. Component Categories

Components are grouped by responsibility rather than by page.

```text
src/components/
├── accessibility/
├── layout/
├── navigation/
├── sections/
├── projects/
├── case-studies/
├── forms/
└── ui/
```

### Accessibility

Components or helpers whose primary purpose is reusable accessibility behavior or document-level accessibility infrastructure.

Examples may include skip navigation or visually-hidden content helpers.

### Layout

Structural wrappers and layout composition.

### Navigation

Header/navigation interactions and navigation presentation.

### Sections

Major portfolio sections that compose page content.

### Projects

Project-specific presentation components.

### Case studies

Detailed project narrative components.

### Forms

Contact and other user-input components.

### UI

Small reusable interface primitives with stable contracts.

## 5. BaseLayout Responsibility

`BaseLayout.astro` owns document-level structure such as:

- `<html>`
- language attribute
- `<head>` integration
- global styles
- metadata integration
- document body structure
- accessibility foundations

It must not own portfolio-specific content.

## 6. Header Responsibility

The header owns global site identity and navigation presentation.

It should receive navigation/configuration rather than duplicate navigation data.

If a mobile menu requires JavaScript, the enhanced state must remain accessible and the navigation must have a safe non-JavaScript baseline.

## 7. Navigation Responsibility

Navigation owns:

- site navigation links
- current/active state where appropriate
- mobile navigation behavior where implemented
- keyboard interaction
- focus behavior
- accessible naming/state

Navigation must not own page content.

## 8. Hero Responsibility

The hero introduces the portfolio owner and primary value proposition.

It may consume:

- name
- role
- short introduction
- primary CTA
- secondary CTA
- optional image

The hero must not become a container for unrelated homepage sections.

## 9. Section Components

Section components provide meaningful content groups such as About, Skills, Experience, Projects, Services, Testimonials, Articles, and Contact.

Each section should:

- have an appropriate semantic heading
- handle empty/optional data intentionally
- consume structured content
- avoid duplicating content schema logic
- maintain predictable spacing/layout behavior

## 10. ProjectCard Responsibility

`ProjectCard` presents a project summary and relevant actions.

It may consume:

- title
- summary
- image
- category
- skills
- project links
- case-study link

It must not fetch project data itself.

## 11. CaseStudy Responsibility

Case-study components present detailed project narratives.

The case-study system should support optional sections without rendering empty headings.

Narrative structure should remain semantic rather than relying on visual styling to communicate hierarchy.

## 12. Card Components

Cards are presentation patterns, not data models.

A card component should receive content and render it consistently.

Do not create a generic `Card` abstraction until there is evidence that multiple cards share a stable structural contract.

Avoid excessive generic configuration such as:

```text
<Card variant="x" size="y" layout="z" tone="q" />
```

when specialized components would be clearer.

## 13. UI Primitive Rules

UI primitives should be created only for stable patterns such as:

- Button/link treatment
- Badge/tag
- visually hidden utility
- icon wrapper where needed
- container/layout primitive where appropriate

A primitive must have a clear semantic contract.

## 14. Button vs Link Rule

Use a link for navigation.

Use a button for an action.

Do not style a semantic link as a button while using button semantics for navigation merely for visual convenience.

The component API should make the correct semantic choice straightforward.

## 15. Component Contracts

Component inputs should be explicit.

Conceptually:

```text
Component
   │
   ├── required props
   ├── optional props
   └── content/data
```

Avoid hidden dependence on global mutable state.

Where TypeScript interfaces materially improve correctness, use them.

## 16. Data Flow

Preferred direction:

```text
Content / Config
       ↓
Page / Route
       ↓
Section Component
       ↓
Specialized Component
       ↓
UI Primitive
```

Components should not reach upward to obtain page-level data.

## 17. Composition Rule

Prefer composition over inheritance or deeply configurable universal components.

Example:

```text
ProjectsSection
      ↓
   ProjectCard
      ↓
  Link / media primitives
```

The parent decides composition; the child owns its own presentation responsibility.

## 18. Accessibility Responsibility

Every interactive component owns its accessibility behavior.

For example:

### Navigation

- keyboard access
- visible focus
- expanded/collapsed state when applicable
- correct relationships

### Dialog/disclosure-like behavior

- correct semantic control
- state exposure
- focus management where required
- escape/close behavior where appropriate

### Forms

- labels
- descriptions/errors
- keyboard usability
- programmatic associations

Accessibility is not a separate optional component layer added after implementation.

## 19. Semantic HTML Rule

Components must use the native semantic element that matches their purpose whenever practical.

Prefer:

```text
<nav>
<header>
<main>
<section>
<article>
<footer>
<button>
<a>
<form>
```

over generic containers with ARIA roles used to imitate native semantics.

ARIA should supplement semantics, not replace native HTML unnecessarily.

## 20. Heading Hierarchy

Components must not independently invent arbitrary heading levels based on visual size.

Page composition determines document hierarchy.

A component may expose a heading when it represents a meaningful section, but the final heading level must remain semantically appropriate to its context.

## 21. Image Responsibility

Image-presenting components must consume accessible image data.

They must support:

- meaningful alternative text
- intentionally decorative images
- predictable dimensions where available
- captions where required

Components must not silently invent alt text from filenames.

## 22. Responsive Responsibility

Components must remain usable across supported viewport sizes.

Responsive behavior belongs primarily in CSS.

JavaScript must not be required merely to make basic layout responsive.

## 23. State Ownership

State should live at the lowest component boundary that can correctly own it.

Examples:

```text
Mobile menu state
    → Navigation

Disclosure state
    → Disclosure component

Theme preference state
    → Theme controller/system
```

Do not create a global state system for isolated interactions.

## 24. Client-Side Boundary

Only components requiring client-side behavior should become interactive/hydrated islands.

The default component remains server/build-rendered.

```text
Static component
      ↓
HTML

Interactive component
      ↓
HTML + minimal client JS
```

## 25. Error / Empty States

Components consuming optional content must define intentional empty behavior.

For example:

```text
Projects = []
      ↓
Do not render a broken empty grid.
```

If a required data contract is invalid, validation should fail before the component reaches production rendering.

## 26. Variants

Variants should represent meaningful semantic or product differences.

Good:

```text
ProjectCard featured
```

Potentially bad:

```text
ProjectCard styleA
ProjectCard styleB
ProjectCard styleC
```

when those styles merely reflect arbitrary visual experimentation.

Prefer design tokens and composition for visual customization.

## 27. Free / Pro Component Strategy

Free and Pro should share common components where functionality is shared.

Pro-only components may be introduced when they represent genuine premium functionality.

Avoid spreading edition checks throughout ordinary components.

Preferred conceptual model:

```text
Shared Components
       │
   ┌───┴───┐
   ↓       ↓
 Free     Pro
package  package
```

Exact packaging mechanics remain a later implementation/release decision.

## 28. Component Naming

Use names that communicate responsibility.

Examples:

```text
ProjectCard
CaseStudyHeader
ArticleCard
SiteHeader
PrimaryNavigation
ContactForm
```

Avoid vague names such as:

```text
Box
Thing
ContentBlock
GenericSection
Wrapper2
```

unless their abstraction has a genuinely stable purpose.

## 29. Component Size Rule

There is no arbitrary line-count limit.

A component should be split when:

- it has multiple independent responsibilities
- a part is reused
- a part has independent state/accessibility behavior
- a part has a stable API
- splitting materially improves readability/testing

Do not split simply to produce more files.

## 30. Testing Responsibilities

Components with behavior should have focused tests where practical.

Critical interaction components should be tested for:

- keyboard operation
- accessible state
- focus behavior
- expected interaction
- failure/disabled states where applicable

Pure static presentation may rely more heavily on page-level accessibility/smoke tests when isolated unit tests provide little value.

## 31. Component Dependency Rules

Preferred dependency direction:

```text
UI primitives
     ↑
Specialized components
     ↑
Sections
     ↑
Pages
```

Lower-level components must not import page-level components.

Avoid circular component dependencies.

## 32. Anti-Patterns

Do not introduce:

- a universal component with dozens of unrelated props
- page-specific components pretending to be global primitives
- components that fetch their own unrelated content
- duplicated navigation configuration
- global mutable state for local interactions
- JavaScript for CSS-only behavior
- ARIA roles replacing native HTML without need
- accessibility behavior hidden in undocumented wrappers

## 33. Component Decision Checklist

Before creating a component, ask:

1. Does it have one clear responsibility?
2. Is it reused or likely to have a stable reuse case?
3. Does it have independent behavior or accessibility requirements?
4. Will a component make the page materially easier to understand?
5. Does its API remain simple?
6. Does it preserve semantic HTML?

If most answers are no, keep the markup local.

## 34. Approved Initial Component Set

The implementation should begin with the smallest useful set and expand only when requirements demand it.

Initial likely components:

```text
BaseLayout
SiteHeader
PrimaryNavigation
SkipLink
Hero
SectionHeading
AboutSection
SkillsSection
ExperienceSection
ProjectsSection
ProjectCard
CaseStudy
ServicesSection
ServiceCard
TestimonialsSection
TestimonialCard
ArticlesSection
ArticleCard
ContactSection
ContactForm (if approved)
SiteFooter
```

This list is a starting contract, not permission to implement all components before their requirements are needed.

## 35. Architecture Invariants

1. Components have clear responsibilities.
2. Content remains outside presentation components.
3. Pages compose; they do not become component libraries.
4. Accessibility belongs to the component that owns the interaction.
5. Semantic HTML is preferred over ARIA imitation.
6. JavaScript is limited to approved interactive behavior.
7. State is local unless a real cross-component requirement exists.
8. Generic abstractions require evidence.
9. Free/Pro differences do not contaminate every component.
10. AI agents must preserve component boundaries unless an approved architecture change is made.

## 36. Component Architecture Gate

Step 2.6 is complete when the component hierarchy, categories, responsibilities, contracts, composition rules, accessibility responsibilities, state boundaries, responsive strategy, Free/Pro strategy, testing expectations, and anti-patterns are documented.

Next step: **Phase 2 — Step 2.7: CSS / Design-System Architecture.**
