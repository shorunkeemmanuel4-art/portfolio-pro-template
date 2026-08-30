# Portfolio Pro Template — Target Users & Personas

**Status:** Approved
**Version:** 1.0
**Parent:** `docs/PRD.md`

## 1. Purpose

Define the primary and secondary customers Portfolio Pro is designed to serve. These personas guide product requirements, UX decisions, accessibility decisions, customization design, documentation, and commercial positioning.

Personas are behavioral product models, not claims about every person in the target market.

## 2. Primary Persona A — Developer / Software Engineer

### Profile

A developer who wants a professional portfolio but would rather spend time on engineering work than build a portfolio site from scratch.

### Goals

- Present technical work professionally.
- Demonstrate projects and engineering capability.
- Explain difficult projects through case studies.
- Customize the site without learning a new framework.
- Deploy quickly.

### Frustrations

- Generic portfolio templates.
- Excessive dependencies.
- Poor documentation.
- Difficult customization.
- Templates that look good but perform poorly.
- Weak accessibility.

### Technical expectations

Medium to high technical ability. Comfortable editing source files but values a clear structure and sensible defaults.

### Product implications

- Clean source code.
- Predictable file structure.
- Clear configuration/content boundaries.
- Developer-friendly documentation.
- Easy deployment.

## 3. Primary Persona B — UX/UI / Product Designer

### Profile

A designer who needs a portfolio that communicates visual quality, process, outcomes, and case studies.

### Goals

- Make projects visually compelling.
- Tell strong case-study stories.
- Demonstrate design process and outcomes.
- Maintain a polished personal brand.
- Control typography, colors, spacing, and imagery.

### Frustrations

- Templates designed only for code portfolios.
- Limited visual customization.
- Weak case-study layouts.
- Poor responsive behavior.
- Inaccessible interaction patterns.

### Technical expectations

Low to medium coding requirement. Should be able to customize common content and visual settings through documented mechanisms without becoming an expert developer.

### Product implications

- Strong visual hierarchy.
- Flexible project/case-study presentation.
- Clear theme customization.
- Excellent typography and responsive behavior.
- Customer-facing documentation written in plain language.

## 4. Primary Persona C — Freelancer / Independent Professional

### Profile

An independent professional who needs a portfolio to establish credibility and generate inquiries or client work.

### Goals

- Build trust quickly.
- Showcase selected work.
- Explain services clearly.
- Provide an obvious contact path.
- Look professional without hiring a developer.

### Frustrations

- Complex installation.
- Unclear editing instructions.
- Templates that require paid services to function.
- Weak mobile experience.
- Contact experiences that are difficult to configure.

### Technical expectations

Low to medium. The customer needs a guided customization experience and clear deployment instructions.

### Product implications

- Fast setup.
- Strong documentation.
- Obvious customization points.
- Useful defaults.
- Contact and conversion UX must be clear without being manipulative.

## 5. Secondary Persona D — Early-Career Professional / Student

### Profile

A student or early-career professional building their first serious professional presence.

### Goals

- Present projects despite limited experience.
- Build credibility.
- Learn from a professional structure.
- Deploy at low cost.

### Frustrations

- Expensive templates.
- Overly complex setup.
- Not knowing what content belongs in each section.

### Product implications

- A useful free or low-cost entry point is valuable.
- Documentation should explain both how to customize and what each section is for.
- Demo content should teach good portfolio structure without requiring the buyer to copy it blindly.

## 6. Secondary Persona E — Small Agency / Team

### Profile

A small team that may use the template as a starting point for client or internal portfolio projects.

### Goals

- Start from a professional foundation.
- Customize branding.
- Reuse the system across projects.
- Reduce development time.

### Frustrations

- Restrictive licenses.
- Difficult codebases.
- Poor maintainability.
- Lack of reusable components.

### Product implications

- Licensing must clearly define allowed commercial/team use.
- Architecture should support reuse without encouraging unauthorized redistribution of the source product.
- Component consistency matters.

## 7. Shared User Needs

Across personas, Portfolio Pro should prioritize:

1. Fast understanding.
2. Easy customization.
3. Strong mobile experience.
4. Accessibility.
5. Professional visual hierarchy.
6. Clear project presentation.
7. Straightforward deployment.
8. Maintainable code.
9. Useful documentation.
10. Reasonable performance.

## 8. Accessibility User Model

Accessibility is not represented as a single persona. Users may combine different needs, devices, and assistive technologies.

The product therefore must support, as applicable:

- keyboard-only navigation
- screen-reader use
- zoom and text resizing
- reduced motion
- users with low vision
- users with color-vision differences
- touch interaction
- different viewport sizes
- users with temporary or situational impairments

Design and implementation decisions must account for this broader user model.

## 9. Buyer vs End-User Distinction

The person purchasing the template may be the same person who visits the resulting portfolio, but not always.

There are therefore two product experiences:

### Buyer/developer experience

- discovery
- evaluation
- purchase
- download
- installation
- customization
- deployment
- updates

### Portfolio visitor experience

- first impression
- navigation
- understanding the professional identity
- evaluating work
- reading case studies
- understanding services/experience
- contacting the portfolio owner

Both experiences must be designed intentionally.

## 10. Priority Matrix

| Persona | Priority | Main product need |
|---|---|---|
| Developer / Engineer | Primary | Clean, customizable, deployable code |
| UX/UI / Product Designer | Primary | Visual quality and case-study storytelling |
| Freelancer | Primary | Fast setup and credibility/conversion |
| Student / Early Career | Secondary | Affordable, guided professional foundation |
| Small Agency / Team | Secondary | Reusability and commercial licensing |

## 11. Persona-Based Acceptance Questions

Before a major product decision is approved, ask:

- Can a developer understand and customize this?
- Can a designer achieve a strong visual result?
- Can a freelancer deploy it without unnecessary technical friction?
- Is there a reasonable path for a beginner without compromising the professional product?
- Does the architecture remain reusable for legitimate team/agency use?
- Does the experience remain accessible to people with different abilities and input methods?

## 12. Persona Gate

Step 1.2 is complete when the target customers, their goals/frustrations, technical expectations, accessibility considerations, buyer/end-user distinction, and product implications are documented.

Next step: **Phase 1 — Step 1.3: Product Requirements & Feature Prioritization.**
