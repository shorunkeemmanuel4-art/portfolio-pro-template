# Portfolio Pro Template — JavaScript / Progressive Enhancement Architecture

**Status:** Approved
**Version:** 1.0
**Phase:** Phase 2 — Architecture & Technical Design
**Step:** 2.8 — JavaScript / Progressive Enhancement Architecture

## 1. Purpose

Define when JavaScript is allowed, how client-side behavior is structured, how state is owned, and how the portfolio remains usable when JavaScript is unavailable or fails.

## 2. Governing Principle

> **HTML works. CSS works. JavaScript enhances.**

JavaScript must not be the foundation of core content, navigation, readability, or basic page access.

## 3. Progressive Enhancement Model

The implementation follows:

```text
Semantic HTML
      ↓
Accessible CSS
      ↓
Optional JavaScript enhancement
```

The baseline experience must provide:

- readable content
- usable navigation
- accessible links
- accessible forms where supported
- responsive layout
- meaningful page structure

## 4. JavaScript Budget

JavaScript is treated as a limited resource.

Use client-side code only when it provides behavior that cannot be achieved adequately with HTML/CSS.

Do not add JavaScript merely for:

- layout
- decorative effects
- styling
- content that can be rendered statically
- navigation that works as ordinary links

## 5. Astro Islands / Hydration Strategy

The site should remain predominantly static/server-rendered.

Only interactive islands should receive client-side JavaScript.

Conceptually:

```text
Static page
├── Hero              → no JS
├── Projects          → no JS
├── Article content   → no JS
├── Navigation        → JS only if enhancement requires it
├── Theme control     → JS if user-controlled switching exists
└── Contact behavior  → JS only where genuinely required
```

Do not hydrate an entire page for one small interaction.

## 6. Initial Interactive Features

Potential v1 interactive behavior:

1. mobile navigation enhancement
2. theme switching, if included
3. disclosure/accordion behavior where required by the final UX
4. form enhancement where required
5. other narrowly scoped accessibility-preserving interactions approved during implementation

No feature becomes interactive merely because a framework makes it easy.

## 7. Mobile Navigation

The navigation must have a safe baseline.

Preferred behavior:

```text
No JS
  ↓
Navigation remains accessible

JS available
  ↓
Mobile menu enhancement
```

The enhancement must manage:

- toggle semantics
- expanded state
- keyboard operation
- focus behavior
- close behavior
- outside interaction only where appropriate
- Escape handling where appropriate

The exact interaction pattern will be validated during implementation.

## 8. Theme Switching

If theme switching is implemented, JavaScript may manage an explicit user preference.

The CSS system remains responsible for the visual theme.

Conceptually:

```text
Theme control
      ↓
Document theme state
      ↓
CSS semantic tokens
```

Theme switching must not duplicate the entire design system in JavaScript.

A usable default theme must exist without JavaScript.

## 9. Disclosure / Accordion

Disclosure behavior should use native HTML capabilities where they adequately satisfy the requirement.

Where custom behavior is necessary, the component must preserve:

- keyboard access
- state communication
- focus behavior
- semantic relationships
- no-JS fallback where practical

Do not build custom disclosure controls when `<details>`/`<summary>` is sufficient for the approved UX.

## 10. Form Enhancement

Forms must retain meaningful labels, validation feedback, and usability without depending entirely on client-side JavaScript.

Client-side validation may improve feedback, but it must not be considered the security boundary.

Server-side/backend validation remains necessary for any actual submission endpoint.

## 11. State Ownership

State belongs to the smallest component capable of owning it correctly.

Examples:

```text
Mobile menu state
    → Navigation

Disclosure state
    → Disclosure component

Theme preference
    → Theme controller
```

Avoid global state management for isolated portfolio interactions.

## 12. DOM State

Prefer simple, inspectable DOM state where practical.

Examples include:

```text
aria-expanded
hidden
open
[data-theme]
```

State should be represented semantically when the platform provides a suitable mechanism.

## 13. Event Handling

Event listeners should be attached only where needed.

Prefer:

- component-local initialization
- event delegation for repeated elements when appropriate
- cleanup where lifecycle requires it
- small modules with clear responsibilities

Avoid a single global script containing unrelated behavior.

## 14. Module Organization

The intended source organization is:

```text
src/scripts/
├── navigation.ts
├── theme.ts
├── disclosure.ts
├── forms.ts
└── index.ts
```

The exact files may change as implementation evidence emerges.

`index.ts` should coordinate approved initialization rather than becoming a large implementation file.

## 15. Initialization Strategy

Client modules should initialize predictably after the required DOM is available.

A module must not assume that unrelated components exist on every page.

Preferred conceptual pattern:

```text
Page loads
   ↓
Find required component(s)
   ↓
If present → initialize
If absent  → do nothing
```

## 16. No-JS Contract

Every interactive feature must document its no-JS behavior.

Example:

```text
Feature: mobile navigation
JS available: collapsible menu
JS unavailable: normal navigation remains reachable
```

A feature that has no acceptable no-JS baseline requires explicit architectural approval.

## 17. Accessibility Requirements

Dynamic behavior must preserve WCAG 2.2 AA goals.

At minimum, interactive scripts must consider:

- keyboard access
- focus visibility
- focus order
- accessible names
- accessible state
- reduced motion
- screen-reader announcements where needed
- pointer and touch interaction
- failure states

Do not use JavaScript to hide information from assistive technology merely for visual effects.

## 18. Focus Management

Focus must be deliberately managed for interactions that change the user's navigation context.

Examples:

- opening a modal-like interface may require moving focus
- closing it may require returning focus to the invoking control
- mobile navigation must not trap focus accidentally

Simple show/hide interactions should not introduce unnecessary focus movement.

## 19. Keyboard Interaction

Keyboard behavior must follow platform expectations.

Do not invent keyboard shortcuts for ordinary navigation unless there is a compelling product requirement.

Interactive controls must remain reachable and operable without a pointer.

## 20. Reduced Motion

JavaScript-triggered animations must respect the same reduced-motion architecture defined in CSS.

If reduced motion is requested:

```text
Decorative animation
    ↓
reduce/remove

Functional state change
    ↓
retain understandable state transition
```

## 21. Error Handling

Client-side failures must fail safely.

For example:

```text
Script fails
   ↓
Static content remains available
```

Do not replace essential content with an empty application shell that depends on successful JavaScript execution.

## 22. Network Independence

Core portfolio content must not require a runtime network request to become readable.

External services may be used for optional functionality only when explicitly approved.

## 23. Third-Party JavaScript

Third-party client-side dependencies should be avoided unless they provide substantial value that cannot reasonably be implemented with platform APIs.

Any approved third-party script must be evaluated for:

- bundle cost
- privacy implications
- accessibility
- security
- maintenance risk
- failure behavior
- licensing

## 24. Analytics

Analytics, if included, must remain non-essential to core functionality.

Analytics failure must not affect page rendering or interaction.

Privacy and consent requirements will be addressed during the SEO/privacy and deployment architecture stages.

## 25. Performance Rules

Client JavaScript should be:

- minimal
- modular
- deferred/appropriately loaded
- narrowly hydrated
- free from unnecessary polling
- free from unnecessary large dependencies

Avoid long-running main-thread work.

## 26. DOM Mutation Rules

Prefer updating only the necessary DOM state.

Do not repeatedly rebuild large page sections for small state changes.

Prefer platform features such as:

```text
hidden
open
aria-expanded
class/data attributes
```

where appropriate.

## 27. Security Boundary

Client-side validation and state are not trusted security boundaries.

Never place secrets, private API keys, or credentials in browser JavaScript.

Any external service requiring credentials must use an appropriate server-side architecture.

## 28. Static Hosting Compatibility

The core portfolio must remain deployable to static hosting.

Client-side features must not require a persistent application server unless the feature is explicitly categorized as optional infrastructure.

## 29. SEO Implications

Important content must be present in the initial rendered HTML.

Do not require client-side JavaScript to create:

- page titles
- headings
- core portfolio content
- project descriptions
- important navigation links
- canonical page structure

## 30. Testing Strategy

Interactive JavaScript should be tested at three levels where appropriate:

```text
Module behavior
      ↓
Component interaction
      ↓
Real page accessibility/smoke test
```

Important tests include:

- JS enabled
- JS unavailable/degraded
- keyboard-only operation
- focus behavior
- state attributes
- mobile viewport behavior
- reduced-motion preference where applicable

## 31. Browser API Preference

Prefer stable native browser APIs over large abstraction libraries.

Examples:

- `matchMedia()` for media preferences
- `classList` / attributes for simple state
- native form APIs where appropriate
- `<dialog>` where its semantics match the approved interaction
- `<details>`/`<summary>` for suitable disclosures

Use abstractions only when they materially improve reliability or maintainability.

## 32. TypeScript Strategy

Client-side scripts should use TypeScript when project configuration supports it.

Types should model meaningful boundaries rather than adding ceremonial types to trivial DOM operations.

DOM assumptions should be guarded where elements are optional.

## 33. Progressive Enhancement Decision Tree

Before adding JavaScript:

```text
Can HTML solve it?
   ├── Yes → use HTML
   └── No
        ↓
Can CSS solve it?
   ├── Yes → use CSS
   └── No
        ↓
Can a native browser API solve it?
   ├── Yes → prefer native API
   └── No
        ↓
Add minimal JavaScript
```

## 34. Anti-Patterns

Do not introduce:

- JavaScript-dependent navigation
- JavaScript-dependent core content
- global state for local interactions
- hydration of static sections
- large UI libraries for a few interactions
- custom controls where native controls suffice
- client-only SEO content
- client-side secrets
- polling without a real requirement
- animation loops for decoration
- a single monolithic `app.js`

## 35. Free / Pro Strategy

Shared interactive infrastructure should remain shared where behavior is identical.

Pro-only interactions may be added without forcing JavaScript onto Free pages that do not use them.

Edition differences must not produce duplicated global scripts unnecessarily.

## 36. AI Agent Rules

Aider/Qwen must not introduce JavaScript merely to solve a visual problem.

Before adding a client script, the agent should document:

1. Why HTML is insufficient.
2. Why CSS is insufficient.
3. Why a native browser feature is insufficient.
4. What the no-JS behavior is.
5. What accessibility states are required.
6. How the behavior will be tested.

This keeps AI-generated implementation aligned with the architecture.

## 37. Architecture Invariants

1. Core content works without JavaScript.
2. Navigation has a safe baseline.
3. JavaScript is enhancement, not foundation.
4. Hydration is limited to interactive islands.
5. State is locally owned.
6. Native browser semantics are preferred.
7. Client-side validation is never the security boundary.
8. No secrets are shipped to the browser.
9. Reduced motion is respected.
10. JavaScript failures must degrade safely.
11. Performance is treated as an architectural constraint.
12. AI agents must preserve progressive enhancement unless an approved architecture change is made.

## 38. Architecture Gate

Step 2.8 is complete when JavaScript boundaries, progressive enhancement, hydration strategy, interactive features, state ownership, accessibility behavior, focus management, no-JS behavior, error handling, security, performance, testing, and AI-agent rules are documented.

Next step: **Phase 2 — Step 2.9: Accessibility Architecture.**
