# Portfolio Pro Template — SEO / Performance Architecture

**Status:** Approved
**Version:** 1.0
**Phase:** Phase 2 — Architecture & Technical Design
**Step:** 2.10 — SEO / Performance Architecture

## 1. Purpose

Define the architecture required for Portfolio Pro to be discoverable, shareable, fast, and technically efficient while preserving accessibility and maintainability.

The product is intended to be a professional, commercially distributable portfolio template. SEO and performance are therefore product capabilities, not optional polish.

## 2. Governing Principle

> **Content should be crawlable, pages should render quickly, and performance must not be purchased by sacrificing accessibility.**

The architecture prioritizes:

```text
Static/server-rendered HTML
        ↓
Semantic accessible structure
        ↓
Minimal CSS/JS
        ↓
Optimized assets
        ↓
Search/social metadata
        ↓
Measured performance
```

## 3. SEO Architecture

Core SEO information must be generated as part of the page's initial HTML/document metadata rather than requiring client-side JavaScript.

Required foundations include:

- unique page title
- useful meta description
- canonical URL strategy
- robots directives where required
- semantic headings
- crawlable internal links
- XML sitemap
- robots.txt
- Open Graph metadata
- social sharing metadata
- appropriate structured data where justified

## 4. URL Architecture

URLs should be:

- stable
- human-readable
- descriptive
- lowercase where practical
- free from unnecessary query parameters
- organized around meaningful content

Avoid changing public URLs without a migration/redirect strategy.

## 5. Page Metadata

Each indexable page should have configurable metadata.

Conceptually:

```text
Page
├── title
├── description
├── canonical URL
├── Open Graph title
├── Open Graph description
├── Open Graph image
└── robots directive where needed
```

The default metadata system must provide sensible fallbacks without creating duplicate or meaningless titles/descriptions.

## 6. Title Architecture

Every important page should have a meaningful unique `<title>`.

The title should describe the page and support the user's understanding of the result in search/browser interfaces.

Do not generate titles by blindly repeating the site name.

## 7. Meta Description Architecture

Descriptions should summarize the page's actual content.

They are not a direct ranking guarantee, but they are useful for search-result presentation and sharing contexts.

Avoid a single identical description across every page.

## 8. Canonical URL Architecture

Canonical URLs should identify the preferred public URL for indexable content.

The system must avoid accidental self-conflicts caused by:

- trailing slash inconsistencies
- alternate hostnames
- duplicate route variants
- tracking parameters

The final deployment hostname will be configured as project/site data rather than hard-coded throughout templates.

## 9. Robots Architecture

`robots.txt` should be generated or maintained as part of the deployment/build architecture.

It must not accidentally block the public portfolio from crawling.

Sensitive or non-public routes must not rely on robots.txt as an access-control mechanism.

## 10. Sitemap Architecture

An XML sitemap should represent the public indexable routes appropriate to the final site.

Do not include:

- private content
- irrelevant utility routes
- duplicate URLs
- routes intentionally marked `noindex`

The final build/deployment architecture will determine whether sitemap generation is static, build-generated, or provided by the hosting layer.

## 11. Internal Linking

Important portfolio content should be reachable through normal HTML links.

Internal linking should create a clear information architecture:

```text
Home
 ↓
Projects / Services / Articles
 ↓
Individual content
```

Do not hide critical navigation behind JavaScript-only interactions.

## 12. Structured Data

Structured data may be used where it accurately describes the page/content.

Potential schema types will be evaluated based on the actual template content rather than added indiscriminately.

Examples that may be appropriate include:

- Person
- Organization
- WebSite
- WebPage
- Article
- BreadcrumbList
- CreativeWork/Project-related types where valid

Structured data must represent visible/actual content and must not be used to make unsupported claims.

## 13. Social Sharing

The template should support Open Graph metadata and appropriate platform sharing metadata.

The architecture should provide configurable:

- social title
- social description
- social image
- canonical URL

Social preview assets should be optimized and should have appropriate dimensions/aspect ratios for their intended platforms.

## 14. Semantic HTML and SEO

SEO must build on the semantic HTML architecture.

Do not add meaningless elements, hidden keyword blocks, or duplicated text for search engines.

Accessibility semantics take precedence over superficial SEO tactics.

## 15. Content Architecture and SEO

Portfolio content should support discoverability through meaningful:

- project titles
- descriptions
- services
- case studies
- articles
- headings
- links

AI-generated content must not automatically be treated as SEO-quality content. Human review remains required for commercially published copy.

# Performance Architecture

## 16. Performance Principle

Performance is a product constraint.

The template should aim to deliver a fast experience on both modern desktop connections and constrained mobile networks/devices.

The architecture favors static output, small payloads, optimized media, and minimal client JavaScript.

## 17. Core Web Vitals

Performance validation should consider Google's Core Web Vitals:

- Largest Contentful Paint (LCP)
- Interaction to Next Paint (INP)
- Cumulative Layout Shift (CLS)

The project should target healthy user-experience thresholds rather than optimizing only for synthetic scores.

## 18. Performance Budgets

The project should establish measurable budgets during implementation.

Budgets should cover, where practical:

```text
HTML size
CSS size
JavaScript size
font payload
image payload
third-party payload
number of requests
```

Initial exact byte limits are deferred until the actual visual/content implementation exists. Once measured, they should be recorded in the performance/QA documentation and enforced where practical.

## 19. Static Generation

Portfolio pages should be statically generated wherever content does not require runtime server computation.

Benefits include:

- fast delivery
- simpler deployment
- strong resilience
- CDN compatibility
- reduced runtime infrastructure
- improved SEO baseline

## 20. Server-Side Rendering / Runtime Data

Runtime rendering should only be introduced where a genuine requirement exists.

A portfolio template must not become a server-dependent application simply to render static portfolio content.

## 21. Image Architecture

Images are expected to be a major performance consideration.

Use:

- appropriately sized source images
- responsive image delivery
- modern formats where supported/appropriate
- explicit dimensions/aspect ratios
- lazy loading for below-the-fold images where appropriate
- eager/high-priority treatment only for genuinely important above-the-fold imagery

Do not lazy-load the primary LCP image by default.

## 22. Image Layout Stability

Images should reserve their layout space using intrinsic dimensions or an equivalent stable aspect-ratio strategy.

This reduces cumulative layout shift.

## 23. Image Alt and Performance

Image optimization must not remove or compromise intentional alternative text.

Accessibility metadata and performance metadata are separate concerns and both must be preserved.

## 24. Font Architecture

Fonts should be selected conservatively.

Avoid shipping unnecessary font families, weights, and character subsets.

Where self-hosting is appropriate, the project should consider local font assets to reduce third-party dependency and improve privacy/control.

Font loading must avoid unnecessary layout shifts and blocking behavior.

The final font strategy will be finalized during visual implementation and validated with performance measurements.

## 25. CSS Performance

CSS should remain small and structured.

Avoid:

- unused framework payloads
- repeated declarations caused by AI-generated duplication
- excessive selector complexity
- unnecessary animations
- CSS-driven rendering hacks

The design-system token architecture should reduce duplication.

## 26. JavaScript Performance

JavaScript should be limited to progressive enhancements defined by the JavaScript architecture.

Rules:

- hydrate only interactive islands
- defer non-critical behavior appropriately
- avoid large client dependencies
- avoid unnecessary event listeners
- avoid long main-thread tasks
- avoid client-side rendering of static content

## 27. Third-Party Performance

Third-party services are performance liabilities and must be justified.

Before adoption, evaluate:

- transfer size
- blocking behavior
- runtime cost
- privacy impact
- failure behavior
- necessity

Do not add third-party scripts simply for convenience.

## 28. Preload / Priority Strategy

Resource priority should be intentional.

Only genuinely critical resources should receive preload/high-priority treatment.

Overusing preload can reduce rather than improve performance.

## 29. Lazy Loading

Use lazy loading for resources that are not needed immediately.

Do not lazy-load content that is required for the initial user experience or likely to become the LCP element.

## 30. Caching and CDN

The generated site should be compatible with CDN/static hosting caching.

Immutable hashed assets should be cacheable for long periods where the hosting setup supports it.

HTML caching/revalidation strategy will be finalized during deployment architecture.

## 31. Asset Naming and Fingerprinting

Build-generated assets should use cache-safe naming/fingerprinting where supported by the framework/build pipeline.

Do not manually implement cache-busting unless required by the selected deployment platform.

## 32. Layout Stability

Avoid unexpected movement caused by:

- images without dimensions
- late font swaps without appropriate strategy
- injected banners
- dynamically inserted content
- client-side layout calculations

Reserve space for content that may load later.

## 33. Runtime JavaScript Failure

Performance architecture and progressive enhancement share an important invariant:

```text
Slow/failing JS
      ↓
Core content still works
```

The page should not wait for client JavaScript to become readable.

## 34. Offline / Network Constraints

The static architecture should remain resilient on slow networks.

Where a PWA/offline feature is eventually introduced, caching must be designed deliberately rather than indiscriminately caching every resource.

Offline architecture is not required to make the core portfolio content dependent on a service worker.

## 35. Accessibility and Performance

Performance optimization must not remove accessibility.

Examples:

- do not remove focus indicators for speed
- do not hide text merely to reduce rendering
- do not replace semantic HTML with canvas/image text
- do not lazy-load essential accessible content incorrectly

## 36. SEO and Performance Interaction

SEO and performance decisions should reinforce one another:

```text
Static HTML
 +
Semantic structure
 +
Fast assets
 +
Minimal JS
 =
Strong baseline
```

Do not pursue search-engine tricks that degrade the actual user experience.

## 37. Performance Testing

The QA workflow should include a combination of:

- Lighthouse
- browser performance tools
- build-size inspection
- Core Web Vitals measurement where real-user data becomes available
- mobile/constrained-network testing

Synthetic scores are signals, not the only measure of performance quality.

## 38. Performance Test Scenarios

Test at minimum:

1. first visit with cold cache
2. repeat visit with warm cache
3. mobile viewport
4. constrained network
5. JavaScript enabled
6. JavaScript disabled/degraded
7. light theme
8. dark theme where supported
9. pages with large imagery
10. pages with representative content volume

## 39. SEO Testing

Validate:

- title presence/uniqueness
- description presence where appropriate
- canonical correctness
- robots behavior
- sitemap output
- crawlable links
- heading structure
- structured data validity where used
- Open Graph metadata
- broken links

## 40. Performance Acceptance Targets

The project should aim for strong Core Web Vitals and a high Lighthouse performance result on representative production builds.

Exact numerical acceptance thresholds should be finalized after real assets and content are implemented rather than inventing unrealistic numbers during architecture planning.

The release gate should prioritize real user experience over achieving an arbitrary perfect score.

## 41. SEO Acceptance Criteria

A release candidate should satisfy:

```text
Unique meaningful titles       ✓
Useful descriptions            ✓
Canonical strategy              ✓
Sitemap                         ✓
Robots configuration            ✓
Crawlable navigation            ✓
Semantic headings               ✓
Social metadata                 ✓
Structured data where justified ✓
No accidental noindex           ✓
No broken critical links        ✓
```

## 42. Performance Acceptance Criteria

A release candidate should demonstrate:

```text
Optimized images                ✓
Stable image dimensions         ✓
Minimal client JS               ✓
Minimal CSS                     ✓
Reasonable font payload         ✓
No unnecessary third parties    ✓
No major layout shifts           ✓
Responsive performance          ✓
Core Web Vitals reviewed        ✓
Production build measured      ✓
```

## 43. Commercial Template Requirement

The default template must ship with sensible SEO and performance defaults.

Customers should not need to understand:

- bundlers
- caching headers
- Core Web Vitals
- structured data internals
- hydration

in order to publish a reasonably optimized portfolio.

Advanced customization can remain available for developers.

## 44. AI Agent SEO Rules

AI agents must not:

- keyword-stuff pages
- duplicate hidden content
- invent structured-data claims
- create fake reviews/ratings
- add invisible SEO text
- mark important pages `noindex` without approval
- change canonical URLs casually
- generate meaningless metadata

AI-generated metadata should be reviewed for accuracy and usefulness.

## 45. AI Agent Performance Rules

AI agents must not add dependencies, scripts, fonts, animations, or media without considering their performance cost.

Before adding a dependency, the agent should explain:

1. what problem it solves
2. why native/platform functionality is insufficient
3. approximate performance implications
4. whether it affects hydration/bundle size
5. how it will be tested

## 46. Measurement Before Optimization

Agents must avoid premature optimization based solely on assumptions.

Preferred process:

```text
Implement
   ↓
Build
   ↓
Measure
   ↓
Identify bottleneck
   ↓
Optimize
   ↓
Measure again
```

## 47. Anti-Patterns

Avoid:

- client-rendered core portfolio content
- giant JavaScript bundles
- unnecessary third-party analytics/widgets
- oversized unoptimized images
- loading every font weight
- excessive preloads
- lazy-loading above-the-fold critical content
- layout shifts
- hidden SEO text
- duplicate metadata
- fake structured data
- arbitrary performance targets without measurement

## 48. Architecture Invariants

1. Core content is crawlable in initial HTML.
2. SEO metadata does not depend on client JavaScript.
3. Public URLs are stable and meaningful.
4. Static generation is preferred for static portfolio content.
5. Images are optimized and dimensioned.
6. JavaScript remains minimal and island-scoped.
7. Third-party resources require justification.
8. Core Web Vitals are part of performance evaluation.
9. Accessibility must not be sacrificed for performance.
10. SEO must not override semantic/accessibility architecture.
11. Performance decisions are measured rather than guessed.
12. AI agents must explain material SEO/performance changes.

## 49. Architecture Gate

Step 2.10 is complete when SEO metadata, URL/canonical strategy, sitemap/robots, structured data, social sharing, internal linking, static rendering, Core Web Vitals, performance budgets, image/font/CSS/JS optimization, caching, testing, acceptance criteria, commercial defaults, and AI SEO/performance rules are documented.

Next step: **Phase 2 — Step 2.11: Build & Deployment Architecture.**
