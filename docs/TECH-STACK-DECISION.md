# Portfolio Pro Template — Technology & Stack Decision

**Status:** Approved
**Version:** 1.0
**Phase:** Phase 2 — Architecture & Technical Design
**Decision:** Astro + TypeScript + native CSS + minimal client-side JavaScript

## 1. Decision Summary

Portfolio Pro v1.0 will use:

- **Astro** as the primary web framework/site generator.
- **TypeScript** for typed project logic and utilities where typing provides value.
- **Native CSS** with CSS custom properties/design tokens as the primary styling system.
- **Vanilla/browser JavaScript** for progressive enhancement and isolated interactive behavior.
- **Astro content collections/content APIs** for structured content where appropriate.
- **Astro static output** as the default deployment model.
- **npm** for the initial package workflow.

React, Vue, Svelte, Tailwind CSS, Next.js, a custom backend, and a CMS are not required for v1.0 and must not be introduced without an approved architectural reason.

## 2. Why Astro

Portfolio Pro is fundamentally a content-heavy, static-first portfolio rather than a highly interactive application. Astro is therefore a strong product fit: its official documentation provides site-oriented components, islands architecture, content collections, and static-generation capabilities, including support for portfolio sites and structured Markdown/MDX content.

The intended model is:

```text
CONTENT
  ↓
ASTRO PAGES / COMPONENTS
  ↓
STATIC HTML + CSS + ONLY NEEDED JS
  ↓
STATIC HOST
```

This directly supports the approved accessibility, SEO, performance, maintainability, and static-deployment goals.

## 3. Why Not React/Next.js First

React and Next.js are capable technologies, but Portfolio Pro does not currently require a React application or server-oriented runtime.

Using them as the default would introduce additional architectural concepts and dependencies that are not justified by the v1.0 requirements.

This is a product-fit decision, not a claim that React or Next.js are poor technologies.

> Use application frameworks when application behavior requires them; do not make a portfolio template an application merely because the ecosystem is popular.

A future requirement can trigger a documented architecture review.

## 4. Why Not Plain Vite as the Site Architecture

Vite is an excellent build tool and produces static deployable output. However, a plain Vite project would leave more site-specific architecture for us to design and maintain, including page generation, content routing, metadata conventions, and static page patterns.

Astro provides those site-oriented primitives while using the Vite ecosystem underneath.

Therefore:

**Astro is the site architecture; Vite is part of its underlying build ecosystem.**

## 5. Why Native CSS

Portfolio Pro is itself a commercial design product. The styling layer should be understandable and customizable by customers without requiring them to learn a utility-class system first.

Native CSS provides:

- CSS custom properties
- cascade/layers
- media queries
- container queries where justified
- Grid/Flexbox
- logical properties
- reduced-motion media queries
- direct accessibility-oriented styling

The project will build its own documented design-token layer rather than depend on Tailwind for v1.0.

## 6. Why TypeScript

TypeScript is selected for maintainability and build-time correctness.

It is particularly useful for:

- structured portfolio content
- configuration objects
- component interfaces
- utility functions
- validation
- reducing data-shape errors

TypeScript is a build-time/development concern; the deployed website does not require TypeScript at runtime.

## 7. JavaScript Strategy

JavaScript is **progressive enhancement**, not the default delivery mechanism.

Likely uses include:

- mobile navigation state
- theme preference controls
- accessible disclosure/accordion behavior
- optional filtering/sorting
- other small isolated enhancements approved during UX/architecture design

Avoid:

- global application state
- client-side rendering of the entire site
- unnecessary hydration
- JavaScript-only access to core content
- large UI libraries for simple interactions

## 8. Content Strategy

Structured portfolio content will use Astro's content capabilities where they provide a clear benefit.

Likely content domains include:

- projects
- case studies
- articles
- testimonials
- experience entries

Simple site configuration such as identity, navigation, contact details, and metadata may use a typed configuration module.

The exact content/configuration boundary will be finalized in **Step 2.5 — Content Architecture**.

## 9. Static Deployment

Static output is the default because the product requirements do not require a custom backend.

The product should produce deployable static assets and HTML suitable for GitHub Pages, Cloudflare Pages, Netlify, Vercel, and similar static hosts.

The final Astro configuration will determine the exact output directory and deployment instructions.

## 10. Dependency Policy

Dependencies must have a documented purpose and meaningful benefit.

Acceptable reasons include:

- significant accessibility benefit
- significant productivity benefit
- meaningful functionality that would be unreasonable to maintain internally
- build-time capability that materially improves product quality

For simple functionality, prefer platform APIs and native web capabilities.

## 11. Accessibility Implications

The stack does not automatically make the product accessible.

Accessibility remains an engineering requirement across:

- semantic HTML
- Astro components
- CSS states
- keyboard interaction
- focus management
- forms
- client-side enhancements
- responsive behavior
- reduced motion

Implementation must be verified against `docs/REQUIREMENTS.md`.

## 12. SEO Implications

Astro's static/content-oriented model is well suited to crawlable HTML and metadata-driven pages.

SEO will still be explicitly designed and tested. The framework choice is not treated as automatic SEO compliance.

## 13. Performance Implications

The architecture will prioritize HTML and CSS plus only the JavaScript required for interactive enhancements.

No blanket client-side hydration strategy is permitted.

Measurable performance budgets will be established before release.

## 14. Aider / Qwen Compatibility

The selected stack is suitable for the planned repository-based AI workflow.

Aider can work against:

- `.astro` components
- TypeScript
- CSS
- Markdown/content
- JSON/configuration
- test/configuration files

**Qwen3 4B** will be used for bounded implementation tasks with explicit requirements and context.

**Qwen3 8B** will handle more difficult implementation/reasoning tasks, refactoring, debugging, and local review.

**GPT** remains responsible for architecture, planning, requirement interpretation, and prompt engineering.

## 15. Technology Matrix

| Option | Product fit | Static/SEO fit | Complexity | Decision |
|---|---|---|---|---|
| Astro | Excellent | Excellent | Low–moderate | **Selected** |
| Plain Vite + HTML/TS | Strong | Strong | Low | Not selected as primary site architecture |
| Eleventy | Strong | Excellent | Low | Not selected; Astro provides a stronger component/content model for this product |
| Next.js/React | Capable | Capable | Higher than required | Not selected for v1.0 |
| React SPA + Vite | Weak fit for content-first product | More work required | Moderate | Not selected |

## 16. Consequences

### Benefits

- Strong fit for content-heavy portfolio pages.
- Static-first output.
- Good separation between content and interactive behavior.
- Minimal client-side JavaScript by default.
- Component-based development without requiring a full SPA.
- Good compatibility with the planned AI-assisted workflow.
- Native CSS keeps the commercial template understandable.

### Costs

- Customers unfamiliar with Astro will need documentation.
- Contributors must understand `.astro` components.
- Advanced interactions require careful client-side boundaries.
- The product has a framework dependency rather than being entirely raw HTML.

These costs are accepted because the product-fit benefits outweigh them.

## 17. Reconsideration Rule

This decision is for v1.0.

A future stack change requires:

1. a new requirement or demonstrated problem
2. documented alternatives
3. impact analysis
4. accessibility/performance review
5. migration implications
6. an approved architecture decision

An AI coding agent may not switch frameworks because it personally prefers another stack.

## 18. Technology Gate

Step 2.2 is complete when the primary technology stack, rationale, alternatives, dependency philosophy, deployment model, and AI-development implications are documented.

Next step: **Phase 2 — Step 2.3: System Architecture.**
