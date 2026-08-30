# Portfolio Pro Template — Commercial Product & Distribution Requirements

**Status:** Approved
**Version:** 1.0
**Parent:** `docs/PRD.md`, `docs/PRODUCT-SCOPE.md`

## 1. Purpose

Define the commercial delivery requirements for selling Portfolio Pro as a digital product, initially through Gumroad, while keeping the technical product maintainable and platform-independent.

## 2. Commercial Product Model

Portfolio Pro is a downloadable digital product.

The initial commercial model is:

```text
                 PORTFOLIO PRO
                      │
          ┌───────────┴───────────┐
          │                       │
        FREE                    PRO
          │                       │
    Core product             Full product
    / entry point            / premium value
```

Gumroad is the initial distribution channel, not a core runtime dependency of the website.

The portfolio template itself should not require Gumroad APIs, accounts, or network access to function.

## 3. Buyer Journey

The intended purchase journey is:

```text
Discover
   ↓
View demo
   ↓
Evaluate features
   ↓
Review accessibility/customization quality
   ↓
Purchase
   ↓
Receive product package
   ↓
Read quick start
   ↓
Customize
   ↓
Test
   ↓
Deploy
```

The purchase experience and the downloaded-product experience are separate concerns.

## 4. Required Product Package

The Pro release package should contain, at minimum:

```text
Portfolio-Pro/
├── source/
├── documentation/
├── examples/
├── assets/
├── license/
└── README.md
```

The exact final package structure is an implementation/release decision and may evolve.

### Source

Contains the production template source required to customize and build/deploy the product.

### Documentation

Contains customer-facing setup, customization, deployment, troubleshooting, and licensing guidance.

### Examples

Contains appropriate demonstration content or examples that help customers understand intended usage.

### Assets

Contains product assets that are legitimately included with the license.

### License

Contains the applicable license terms in a clearly accessible form.

### README

Provides the shortest path from download to successful local setup.

## 5. Free Edition Distribution

The Free edition should be distributed as a legitimate usable product or clearly defined repository/download experience.

It should demonstrate:

- code quality
- visual quality
- accessibility
- responsive behavior
- customization approach
- documentation quality

The Free edition must not contain deliberate defects intended to pressure conversion.

## 6. Pro Edition Distribution

The Pro edition should provide a complete package with the premium features defined by the approved product scope.

The buyer should be able to identify before purchase:

- what is included
- supported technologies/requirements
- what customization is possible
- what hosting options are supported
- what license applies
- what support/update expectations exist
- what is not included

## 7. Licensing Requirements

A final license must clearly define:

- personal use
- commercial use
- permitted number of projects/sites if restricted
- client work permissions
- agency/team usage
- modification rights
- redistribution restrictions
- resale restrictions
- template/source-code redistribution restrictions
- update rights
- support rights

The license must be readable by a normal customer and must not depend on hidden technical enforcement.

## 8. Licensing Direction

The product should favor a straightforward commercial license that allows legitimate customization and project use while preventing customers from simply repackaging and reselling the template itself as a competing template product.

Exact legal wording must be finalized before commercial release and should be reviewed appropriately rather than treated as an engineering decision.

## 9. Customer Delivery Requirements

After purchase, the customer should have access to:

- product files
- version information
- license
- quick-start instructions
- full customization documentation
- deployment documentation
- troubleshooting guidance
- update information
- support/contact information where offered

The product should remain usable if the customer is offline after downloading it, except for optional third-party integrations that inherently require network access.

## 10. Versioning

Every commercial release should have an identifiable version.

Version information should be available in:

- product package
- README
- documentation
- release notes

Updates should explain:

- new features
- fixes
- accessibility changes
- security changes
- breaking changes
- migration/customization changes

## 11. Update Strategy

The product should be designed so updates can be released without unnecessarily destroying customer customization.

This means architecture should favor clear separation between:

- reusable product code
- customer content
- customer theme/configuration
- generated/build output

The exact update strategy will be finalized during architecture and deployment planning.

## 12. Support Strategy

The initial product should aim for documentation-first support.

Documentation should answer common questions before customers need direct assistance.

Potential future support tiers may include:

- documentation-only
- community support
- paid support
- customization services

These are not v1.0 commitments.

## 13. Gumroad Requirements

Gumroad is the initial sales/distribution platform.

The product listing should eventually communicate:

- product name
- concise value proposition
- screenshots
- live demo where available
- feature summary
- accessibility positioning
- technology requirements
- included files
- Free vs Pro differences
- license summary
- update policy
- support policy
- refund/consumer terms as applicable

The website source must remain independent of Gumroad so the product can later be distributed through another marketplace or direct sales channel without architectural redesign.

## 14. Product Demo Requirements

The demo should represent the quality of the actual product.

It should demonstrate:

- responsive behavior
- accessible navigation
- project presentation
- case-study presentation
- theme behavior where supported
- visual hierarchy
- realistic content
- performance-conscious behavior

The demo must not claim features that are absent from the downloadable edition.

## 15. Commercial Quality Gate

Before Pro launch:

- package installs successfully from a clean environment
- README gets the customer started
- documentation covers common customization
- license is present and understandable
- version is identifiable
- demo matches the product
- included files are intentional
- no secrets are included
- accessibility target has been reviewed
- deployment path is documented
- release notes are prepared

## 16. Platform Independence

The technical architecture must not make Gumroad a runtime dependency.

The following should remain replaceable:

- marketplace
- payment provider
- download provider
- hosting provider
- analytics provider

This preserves future distribution options.

## 17. Commercial Metrics — Future

Possible future metrics include:

- demo visits
- conversion rate
- Free downloads
- Pro purchases
- refund rate
- documentation completion/support requests
- repeat purchases
- update adoption

These metrics are not required for the template's runtime and should not drive unnecessary tracking into the product.

## 18. Commercial Scope Gate

Step 1.5 is complete when the buyer journey, package structure, edition distribution, licensing requirements, delivery, versioning, updates, support direction, Gumroad positioning, demo requirements, and platform-independence requirements are documented.

## 19. Phase 1 Completion

With this document approved, Phase 1 Product Definition is complete.

The project is ready to enter **Phase 2 — Architecture & Technical Design**.

Next step: **Phase 2 — Step 2.1: Architecture Goals & Technical Constraints.**
