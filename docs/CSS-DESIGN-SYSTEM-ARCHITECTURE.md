# Portfolio Pro Template — CSS / Design-System Architecture

**Status:** Approved
**Version:** 1.0
**Phase:** Phase 2 — Architecture & Technical Design
**Step:** 2.7 — CSS / Design-System Architecture

## 1. Purpose

Define the CSS architecture and design-token system that will power Portfolio Pro while keeping the product accessible, responsive, customizable, maintainable, and suitable for commercial distribution.

## 2. Design-System Principle

The design system is a **constraint system**, not merely a collection of colors and components.

It must establish predictable relationships between:

```text
Tokens
  ↓
Theme
  ↓
Foundations
  ↓
Layout
  ↓
Components
  ↓
Pages
```

Customization should happen through intentional tokens and configuration rather than arbitrary overrides scattered throughout the project.

## 3. CSS Strategy

The project uses **native CSS** as the primary styling technology.

Use modern platform capabilities where they provide clear value:

- custom properties
- cascade layers
- Flexbox
- CSS Grid
- logical properties
- media queries
- container queries where justified
- `clamp()` for fluid values where appropriate
- `prefers-reduced-motion`
- `prefers-color-scheme` where appropriate
- `:focus-visible`

Do not introduce a utility framework for v1.0.

## 4. CSS Layer Model

The intended cascade architecture is:

```css
@layer reset, tokens, base, layout, components, utilities, overrides;
```

Not every layer must exist as a separate file.

### `reset`

Only normalization/reset rules that provide a clear cross-browser foundation.

### `tokens`

Design variables and theme values.

### `base`

Element defaults, typography foundations, links, forms, focus foundations, and global accessibility styling.

### `layout`

Containers, grids, flow, spacing relationships, and responsive structure.

### `components`

Component-specific presentation.

### `utilities`

Small intentional utility classes.

### `overrides`

A tightly controlled final layer for documented exceptions. It must not become a dumping ground.

## 5. Token Architecture

Tokens are organized conceptually into:

```text
Primitive tokens
      ↓
Semantic tokens
      ↓
Component tokens
```

### Primitive tokens

Raw values such as:

- color scales
- spacing scale
- type scale
- radii
- shadows
- durations

### Semantic tokens

Meaning-based variables such as:

```text
--color-bg
--color-surface
--color-text
--color-text-muted
--color-border
--color-primary
--color-on-primary
--color-focus
```

### Component tokens

Only where a component genuinely needs an additional controllable value.

Example conceptually:

```text
--button-padding-inline
--button-radius
```

Avoid exposing every CSS property as a public design token.

## 6. Token Naming

Token names should describe **meaning or role**, not a particular visual value.

Prefer:

```text
--color-primary
--color-surface
--space-md
--radius-md
```

Avoid:

```text
--blue-500
--gray-300
--thing-margin
```

Primitive scales may use numerical/value-oriented names internally, but customer-facing theme variables should generally be semantic.

## 7. Color Architecture

The color system must separate raw palette values from semantic usage.

```text
Palette
  ↓
Semantic roles
  ↓
Components
```

Required semantic roles include, at minimum:

- page background
- surface
- elevated surface where needed
- primary text
- secondary/muted text
- border
- primary action
- action text
- link
- focus indicator
- success/warning/error states where required

Color must never be the sole means of communicating meaning.

## 8. WCAG Contrast Requirement

The design system targets **WCAG 2.2 AA**.

Color combinations must be tested rather than judged visually.

The system must account for:

- normal text
- large text
- UI components
- focus indicators
- disabled states where applicable
- links
- surfaces/backgrounds

The exact contrast requirements will be verified during accessibility implementation/testing.

## 9. Theme Architecture

The system should support theme customization through semantic variables.

Conceptually:

```css
:root {
  /* default semantic theme */
}

[data-theme="dark"] {
  /* dark semantic theme */
}
```

The exact theme mechanism will be finalized during JavaScript/accessibility architecture.

If no JavaScript is available, the site must still have a usable default theme.

## 10. System Preference

Where dark mode is supported, `prefers-color-scheme` may provide a default preference, but the implementation must avoid creating inaccessible contrast combinations.

An explicit user-selected theme, if implemented, should have a predictable precedence over the system preference.

## 11. Typography System

Typography is tokenized by role rather than hard-coded throughout components.

Conceptual roles:

```text
font-family-body
font-family-heading
font-size-xs
font-size-sm
font-size-md
font-size-lg
font-size-xl
font-size-display
line-height-tight
line-height-normal
line-height-relaxed
font-weight-regular
font-weight-medium
font-weight-bold
```

The final type scale will be selected during visual design implementation and must be validated at mobile and desktop sizes.

## 12. Fluid Typography

Use fluid typography only where it improves responsive behavior and remains understandable.

`clamp()` may be used for selected display sizes.

Do not make every token fluid merely because CSS supports it.

## 13. Spacing System

Spacing should use a consistent scale rather than arbitrary values throughout components.

Conceptually:

```text
--space-1
--space-2
--space-3
--space-4
--space-5
--space-6
...
```

The final numeric scale is a visual design decision, but implementation should minimize one-off values.

## 14. Layout System

The layout system should provide a small number of predictable primitives.

Conceptually:

```text
Page shell
   ↓
Container
   ↓
Section
   ↓
Flow / Stack / Grid
```

A common content container should control readable page width while allowing full-bleed sections where intentionally designed.

## 15. Responsive Architecture

The project is **mobile-first**.

Base CSS represents the smallest supported viewport behavior.

Larger layouts are progressively enhanced through media/container queries.

Avoid designing primarily for desktop and then hiding/rearranging content for mobile.

## 16. Breakpoint Strategy

Breakpoints should be based on layout failure rather than device-name assumptions.

Do not create breakpoints such as `iphone`, `tablet`, or `desktop` as semantic concepts.

Use a small number of breakpoints supported by evidence from the actual layout.

Exact breakpoint values are deferred to visual implementation.

## 17. Container Queries

Container queries may be used for components whose layout depends more naturally on their available container width than on viewport width.

They are not mandatory for every component.

Prefer the simpler responsive mechanism when it is sufficient.

## 18. Logical Properties

Use logical CSS properties where practical:

```text
margin-inline
padding-inline
inset-inline
border-inline
text-align: start/end
```

This improves internationalization and reduces assumptions about left-to-right layouts.

## 19. Component Styling

Component styles should be scoped/organized so they do not accidentally leak into unrelated components.

Global styles should establish foundations; component styles should establish component presentation.

Avoid deeply nested selectors.

## 20. Specificity Strategy

Keep specificity intentionally low.

Preferred order:

```text
Element/base
  ↓
Class/component
  ↓
State
  ↓
Intentional variant
```

Avoid `!important` except for documented exceptional cases such as certain accessibility utilities where it is genuinely necessary.

## 21. Utility Strategy

Utilities are allowed but must remain small and intentional.

Examples may include:

- visually hidden
- flow/stack helpers
- text alignment
- display helpers where justified

Utilities must not become a second component framework.

## 22. Focus Architecture

Keyboard focus must be visually identifiable.

The system should use `:focus-visible` for keyboard-oriented focus presentation while preserving usable focus behavior for other input methods.

Focus indicators must meet applicable WCAG requirements for visibility and contrast.

Do not globally remove outlines without providing an equivalent accessible focus indicator.

## 23. Motion Architecture

Motion is optional enhancement.

Animations should:

- communicate meaningful state or hierarchy
- remain short and purposeful
- avoid unnecessary decorative movement
- not prevent users from completing tasks

Respect:

```css
@media (prefers-reduced-motion: reduce) {
  /* reduce/remove non-essential motion */
}
```

Reduced motion is a first-class requirement, not a post-launch patch.

## 24. Interaction States

Interactive components should define appropriate states where applicable:

```text
rest
hover
focus-visible
active
selected
expanded
disabled
invalid
```

Not every component needs every state.

States must remain understandable without relying solely on color.

## 25. Form Styling

Forms require explicit treatment for:

- labels
- input fields
- focus
- errors
- help text
- disabled state
- required state
- success/confirmation where applicable

Placeholder text must not substitute for a visible/accessible label.

## 26. Dark Theme Accessibility

Dark mode is not simply inverted colors.

The semantic color system must be tested for:

- text contrast
- link contrast
- borders where needed
- focus indicators
- controls
- images/background interactions

## 27. Design Token Customization Boundary

The commercial template should expose a controlled set of high-value theme variables.

Likely customer customization includes:

```text
Brand colors
Typography choices
Content width
Spacing density
Corner radius
Shadow intensity
Theme mode
```

The product should not require customers to edit dozens of component CSS files for normal branding changes.

## 28. Accessibility vs Customization Rule

Customization must not silently disable accessibility.

Examples:

- customer-selected colors should be contrast-tested/documented
- focus indicators must remain visible
- typography customization must preserve readable defaults
- motion customization must respect reduced-motion preferences
- low-contrast theme combinations must not be presented as compliant defaults

## 29. CSS Asset Strategy

Only required CSS should reach production where practical.

Avoid shipping unused framework CSS or large third-party stylesheets.

Astro's build process should handle bundling/minification according to the final build configuration.

## 30. Critical Rendering Considerations

The styling architecture should prioritize fast first render.

Avoid:

- JavaScript-dependent styling for core layout
- large blocking third-party CSS
- unnecessary font payloads
- layout shifts caused by missing dimensions/assets

Font strategy will be finalized during performance architecture.

## 31. Component Token Example

Conceptually:

```css
.button {
  --_button-bg: var(--color-primary);
  --_button-fg: var(--color-on-primary);
  --_button-radius: var(--radius-md);

  background: var(--_button-bg);
  color: var(--_button-fg);
  border-radius: var(--_button-radius);
}
```

Private component variables may map global semantic tokens to component-specific implementation values.

## 32. CSS File Responsibilities

The approved source organization is:

```text
src/styles/
├── tokens.css
├── globals.css
├── base.css
├── layout.css
├── utilities.css
└── components/
```

### `tokens.css`

Design tokens and theme variables.

### `globals.css`

Global stylesheet entry/orchestration and high-level global rules.

### `base.css`

Element defaults and accessibility foundations.

### `layout.css`

Containers, sections, grids, stacks, and responsive structure.

### `utilities.css`

Intentional utility classes.

### `components/`

Component-specific styles when separation improves maintainability.

## 33. Design-System Documentation

The customer-facing design-system documentation should explain:

- available theme tokens
- how to customize brand colors
- typography customization
- responsive expectations
- accessibility constraints
- supported theme modes
- component variants

Documentation is part of the product, not an afterthought.

## 34. Free / Pro Strategy

Free and Pro should share the same foundational token architecture.

Pro may introduce additional themes, component variants, or visual systems, but these should consume the same semantic foundations where practical.

Do not fork the entire CSS system for each edition without a demonstrated need.

## 35. Anti-Patterns

Avoid:

- arbitrary color literals throughout components
- arbitrary spacing values everywhere
- deep selector nesting
- global `!important` usage
- desktop-first CSS followed by extensive mobile overrides
- CSS framework dependency for simple primitives
- JavaScript-driven layout
- inaccessible custom focus removal
- motion without reduced-motion handling
- color-only state communication
- customer customization through scattered overrides

## 36. Design Token Governance

A new public token should be introduced only when:

1. it represents a meaningful design concept
2. it is reused or intentionally customer-configurable
3. its name communicates purpose
4. its accessibility implications are understood

Avoid token explosion.

## 37. Architecture Invariants

1. Native CSS is the primary styling system.
2. Tokens are the primary customization mechanism.
3. Semantic tokens separate meaning from raw palette values.
4. Mobile-first is mandatory.
5. Accessibility is part of the CSS architecture.
6. Focus indicators cannot be removed without an accessible replacement.
7. Reduced motion is supported.
8. Color is never the sole communication mechanism.
9. CSS specificity remains intentionally manageable.
10. AI agents must preserve the token/cascade architecture unless an approved design-system change is made.

## 38. Architecture Gate

Step 2.7 is complete when the CSS technology, cascade model, token hierarchy, naming, color/typography/spacing systems, layout and responsive strategy, themes, focus/motion architecture, customization boundary, component styling rules, and governance rules are documented.

Next step: **Phase 2 — Step 2.8: JavaScript / Progressive Enhancement Architecture.**
