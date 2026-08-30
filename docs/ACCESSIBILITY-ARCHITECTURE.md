# Portfolio Pro Template — Accessibility Architecture

**Status:** Approved
**Version:** 1.0
**Phase:** Phase 2 — Architecture & Technical Design
**Step:** 2.9 — Accessibility Architecture

## 1. Purpose

Define accessibility as a first-class architectural requirement for Portfolio Pro.

The product targets **WCAG 2.2 AA** and follows an accessibility-first, design-for-all approach. Accessibility must be preserved across content, components, CSS, JavaScript, responsive behavior, themes, documentation, testing, and AI-assisted development.

## 2. Governing Principle

> **Accessibility is a product requirement, not a finishing step.**

The portfolio must be usable by people with different:

- visual abilities
- hearing abilities
- mobility abilities
- cognitive abilities
- speech abilities
- language and literacy needs
- input methods
- device constraints
- temporary or situational impairments

## 3. Conformance Target

The architecture targets **WCAG 2.2 Level AA**.

Conformance is not claimed merely because automated tooling passes. Final accessibility quality requires a combination of:

```text
Requirements
   ↓
Semantic implementation
   ↓
Automated testing
   ↓
Keyboard testing
   ↓
Screen-reader testing where appropriate
   ↓
Responsive/reflow testing
   ↓
Manual review
```

## 4. Accessibility Architecture Layers

Accessibility responsibilities exist at every layer:

```text
Content
  ↓
Semantic HTML
  ↓
CSS / Visual presentation
  ↓
Interaction / JavaScript
  ↓
Pages / routes
  ↓
Build / QA
```

A later layer must not undermine accessibility established by an earlier layer.

## 5. Semantic HTML First

Use native HTML semantics whenever possible.

Preferred elements include:

```text
<header>
<nav>
<main>
<section>
<article>
<aside>
<footer>
<h1>–<h6>
<a>
<button>
<form>
<label>
<input>
<details>
<summary>
```

Do not use generic `<div>` elements plus ARIA roles to imitate native controls when a native element is suitable.

## 6. Landmark Architecture

A standard page should expose an understandable landmark structure.

Conceptually:

```text
banner/header
   ↓
navigation
   ↓
main
   ↓
content sections
   ↓
contentinfo/footer
```

Landmarks must have meaningful accessible names when multiple landmarks of the same type require differentiation.

## 7. Skip Navigation

The site should provide a keyboard-accessible mechanism to bypass repeated navigation and reach the main content.

The skip link must:

- be reachable by keyboard
- become visibly identifiable when focused
- target a valid main-content destination
- not be permanently hidden from assistive technology

## 8. Heading Architecture

Headings communicate document structure, not visual size.

Rules:

1. Pages should have a clear primary heading.
2. Sections use headings that reflect their hierarchy.
3. Heading levels must not be chosen merely for typography.
4. CSS controls visual size independently from semantic level.
5. Empty/optional sections must not create meaningless headings.

## 9. Link Architecture

Links must have meaningful accessible names and identify their destination or purpose.

Avoid vague standalone link text such as:

```text
Click here
Read more
Learn more
```

unless the surrounding accessible context makes the destination unambiguous.

Where a link opens a new browsing context or leaves the site, communicate that when needed by the UX.

## 10. Button Architecture

Buttons are for actions; links are for navigation.

Buttons must have:

- accessible name
- appropriate state where applicable
- keyboard operation
- visible focus
- predictable activation

Do not implement a button solely with a clickable `<div>` or `<span>`.

## 11. Keyboard Accessibility

All functionality must be operable using a keyboard without requiring a mouse or touch input.

Test at minimum:

- Tab
- Shift+Tab
- Enter
- Space where applicable
- Escape where applicable
- arrow keys only where the interaction pattern requires them

Keyboard focus must follow a logical order.

## 12. Focus Visibility

Keyboard focus must remain visible.

The design system must provide a consistent focus treatment with sufficient visibility and contrast.

Never use:

```css
outline: none;
```

without an accessible replacement.

`:focus-visible` should be preferred for modern keyboard-oriented styling while ensuring focus remains usable across supported interaction methods.

## 13. Focus Management

Dynamic interfaces must manage focus intentionally.

Examples:

```text
Open modal/dialog
    ↓
move focus appropriately

Close modal/dialog
    ↓
return focus appropriately
```

For simple disclosures, do not move focus unnecessarily.

Mobile navigation must not create inaccessible focus traps.

## 14. Screen Reader Architecture

Content must remain understandable through assistive technologies.

Requirements include:

- meaningful document structure
- semantic landmarks
- meaningful names
- correct control states
- appropriate relationships
- useful alternative text
- no important information communicated solely through visual styling

ARIA should supplement native semantics rather than replace them unnecessarily.

## 15. Accessible Names

Every interactive control must have an accessible name.

The accessible name should come from the most appropriate source, preferably visible text or an associated label.

Icon-only controls require an explicit accessible name.

## 16. Images

Images must have intentional alternative-text treatment.

### Informative image

Provide meaningful `alt` text that conveys the relevant information.

### Decorative image

Use intentionally empty alternative text where appropriate.

### Complex image

Provide an appropriate textual explanation when the image communicates information that cannot reasonably be represented by short alt text alone.

Never generate alt text solely by copying a filename.

## 17. Decorative Icons

Icons that duplicate adjacent visible text should generally be hidden from assistive technology.

Icons must not become the only way a user understands an action.

## 18. Color and Contrast

The system targets WCAG 2.2 AA contrast requirements.

Test:

- body text
- headings
- links
- controls
- focus indicators
- borders where they communicate component boundaries
- status messaging
- dark and light themes

Do not communicate information using color alone.

Examples of additional cues include:

- text
- icons with accessible names
- patterns
- borders
- state indicators

## 19. Reflow and Zoom

The site must remain usable when content is enlarged and at narrow viewport sizes according to applicable WCAG requirements.

Do not design layouts that depend on a fixed desktop canvas.

Avoid horizontal scrolling for ordinary page content except where the content type legitimately requires it.

## 20. Responsive Accessibility

Responsive behavior must preserve:

- reading order
- logical focus order
- accessible names
- touch/keyboard access
- content visibility
- semantic structure

Do not hide important information on small screens merely to simplify visual design unless an equivalent accessible experience exists.

## 21. Touch and Pointer Interaction

Interactive targets must provide sufficient usable area and spacing in accordance with WCAG 2.2 requirements.

Do not rely exclusively on hover.

Any hover-revealed information that is important must have an accessible equivalent.

## 22. Forms

Forms must provide:

- visible labels
- programmatic label/control association
- instructions where needed
- required-field communication
- accessible error identification
- useful error descriptions
- focus behavior that helps users recover from errors
- status/confirmation communication where needed

Placeholder text is not a replacement for a label.

## 23. Form Errors

Errors should identify:

1. what went wrong
2. which field is affected
3. how to correct it

Error presentation must not rely on color alone.

Where appropriate, associate errors programmatically with the relevant control.

## 24. Validation

Client-side validation is an enhancement, not the only validation mechanism.

The final submission architecture must validate data appropriately at the server/service boundary when a backend exists.

## 25. Motion and Animation

Motion must be purposeful and non-essential decoration should be reducible or removed when the user requests reduced motion.

Respect:

```css
@media (prefers-reduced-motion: reduce) {
  /* reduce non-essential motion */
}
```

Avoid rapid flashing or motion that may create accessibility or seizure-related risk.

## 26. Auto-Playing Content

Do not introduce automatically playing audio/video as a default portfolio behavior.

If time-based or moving content is ever introduced, its controls and accessibility requirements must be explicitly designed and tested.

## 27. Content Accessibility

Customer content is part of the accessibility experience.

Documentation should encourage:

- meaningful headings
- descriptive links
- concise descriptions
- useful alt text
- readable language
- sufficient content structure

The template should provide accessible defaults but cannot make inaccessible customer-authored content automatically accessible in every case.

## 28. Typography and Readability

Typography must support readability across viewport sizes and user settings.

Avoid:

- excessively small default text
- overly tight line-height
- long unreadable line lengths
- text embedded in images where avoidable
- layout that breaks when text size increases

## 29. Language and Internationalization

The document language must be correctly declared.

The architecture should avoid unnecessary assumptions about:

- language direction
- text length
- date formats
- name structure

Logical CSS properties support future right-to-left layouts where required.

## 30. Accessible Themes

Every supported theme must preserve accessibility.

Theme changes must not remove:

- readable contrast
- visible focus
- distinguishable states
- readable links
- usable controls

User-selected themes must have safe defaults and documented customization constraints.

## 31. Progressive Enhancement

Accessibility must survive JavaScript failure wherever practical.

```text
JS enabled
   ↓
Enhanced experience

JS unavailable/fails
   ↓
Accessible baseline
```

Interactive enhancements must not turn core navigation or content into an inaccessible blank state.

## 32. Accessibility and Astro Islands

Hydrated components remain responsible for preserving the semantic and accessible structure produced by their server-rendered baseline.

Do not replace accessible server HTML with a client-only widget unless the interaction genuinely requires it and the replacement is fully accessible.

## 33. Automated Testing

Automated accessibility testing should be integrated into the development/QA workflow.

It should check common machine-detectable issues such as:

- missing accessible names
- invalid ARIA
- missing labels
- structural problems
- contrast issues where the tool can reliably evaluate them
- invalid heading/landmark patterns where detectable

Automated testing is necessary but insufficient.

## 34. Manual Accessibility Testing

Manual review must include:

### Keyboard

- complete navigation
- visible focus
- no accidental traps
- sensible focus order

### Zoom/reflow

- enlarged text/content
- narrow viewport
- no important content loss

### Screen reader

Test representative critical flows with at least one supported screen reader during QA.

### Reduced motion

Verify non-essential motion is reduced/removed.

## 35. Browser and Assistive Technology Testing

The project should establish a practical support matrix rather than claiming every browser/AT combination.

At minimum, test the primary supported browser families on desktop/mobile and a representative screen reader environment before release.

The exact matrix will be recorded in the QA/release documentation.

## 36. Accessibility Regression Testing

Accessibility testing must run after meaningful changes to:

- navigation
- forms
- themes
- responsive layout
- components
- JavaScript interactions
- typography
- design tokens

A visual redesign is not considered safe merely because screenshots look correct.

## 37. Accessibility Acceptance Criteria

A feature is not complete until, where applicable:

```text
Semantic structure       ✓
Keyboard operation       ✓
Visible focus            ✓
Accessible name          ✓
Accessible state         ✓
Contrast                 ✓
Responsive behavior      ✓
Reduced motion            ✓
No-JS fallback            ✓
Automated checks          ✓
Manual review             ✓
```

Not every criterion applies identically to every feature, but applicable criteria must be explicitly considered.

## 38. Accessibility Documentation

Customer/developer documentation should explain:

- accessibility goals
- semantic component usage
- keyboard behavior
- theme customization constraints
- image alt-text expectations
- form requirements
- testing commands
- how to report accessibility issues

## 39. AI Agent Accessibility Contract

GPT, Aider, Qwen, and any other development agent must treat accessibility as a hard constraint.

Before modifying a UI feature, the agent should consider:

1. What is the semantic HTML element?
2. What is the accessible name?
3. How does a keyboard user operate it?
4. What is the focus behavior?
5. What state is exposed to assistive technology?
6. Does the feature work without JavaScript where practical?
7. Does it work at narrow widths and enlarged text?
8. Does it preserve contrast?
9. Does it respect reduced motion?
10. What automated and manual tests verify the change?

## 40. AI Explanation Requirement

Every AI-generated implementation change should be accompanied in the development workflow by a concise explanation of:

- what was changed
- why it was changed
- which architecture rule it follows
- accessibility implications
- tests performed
- any known limitations

This supports reviewability and prevents opaque AI-driven changes.

## 41. Accessibility Issue Severity

Issues should be prioritized by user impact.

Conceptually:

```text
Blocker
  ↓
Critical task/function cannot be accessed

High
  ↓
Major accessibility barrier

Medium
  ↓
Meaningful usability degradation

Low
  ↓
Minor improvement
```

The final project issue/QA workflow may map these to its own labels.

## 42. Third-Party Accessibility

Third-party widgets are not considered accessible merely because their vendor claims accessibility.

Any external UI that affects a core task must be evaluated before adoption.

Prefer native platform capabilities where practical.

## 43. Accessibility and Performance

Accessibility improvements must not require unnecessarily large client bundles.

Prefer native HTML/CSS semantics over JavaScript-heavy accessibility abstractions where they provide equivalent reliable behavior.

## 44. Accessibility and SEO

Semantic structure benefits both accessibility and machine understanding.

The architecture therefore favors:

- meaningful headings
- landmarks
- descriptive links
- valid document structure
- server-rendered core content

SEO optimization must never override accessibility semantics.

## 45. Accessibility Anti-Patterns

Do not introduce:

- clickable `<div>`/`span` controls
- keyboard-inaccessible custom widgets
- hidden focus outlines with no replacement
- icon-only controls without accessible names
- placeholder-only labels
- color-only status communication
- hover-only functionality
- auto-playing media by default
- inaccessible modal/focus behavior
- client-only core content
- arbitrary ARIA replacing native semantics
- inaccessible theme variants
- animation without reduced-motion consideration

## 46. Accessibility Architecture Invariants

1. WCAG 2.2 AA is the target.
2. Semantic HTML is the default.
3. Keyboard operation is mandatory for functionality.
4. Focus must remain visible and logical.
5. Interactive controls require accessible names.
6. Color is never the sole means of communication.
7. Forms require accessible labels and errors.
8. Reduced motion is respected.
9. Responsive/reflow behavior must preserve access to content.
10. JavaScript failure must not unnecessarily destroy accessibility.
11. Automated testing does not replace manual testing.
12. Every UI change must consider accessibility before implementation.
13. AI agents must explain accessibility-relevant changes.
14. Accessibility is a release requirement, not optional polish.

## 47. Architecture Gate

Step 2.9 is complete when the WCAG target, semantic structure, landmarks, headings, keyboard/focus model, screen-reader considerations, images, forms, contrast, responsive/reflow behavior, touch interaction, motion, themes, progressive enhancement, testing strategy, acceptance criteria, and AI accessibility contract are documented.

Next step: **Phase 2 — Step 2.10: SEO / Performance Architecture.**
