# Portfolio Pro Template — Build & Deployment Architecture

**Status:** Approved
**Version:** 1.0
**Phase:** Phase 2 — Architecture & Technical Design
**Step:** 2.11 — Build & Deployment Architecture

## 1. Purpose

Define how Portfolio Pro moves safely from source code to a validated production build and a distributable commercial template.

The architecture prioritizes reproducibility, static hosting compatibility, security, accessibility, performance, and simple customer deployment.

## 2. Governing Principle

> **Build once, validate the artifact, deploy the validated result.**

The production pipeline should be deterministic and should prevent an untested build from becoming the release artifact.

## 3. Deployment Model

The primary product architecture is static-first:

```text
Git repository
    ↓
Development
    ↓
Validation
    ↓
Production build
    ↓
Artifact inspection
    ↓
Static hosting / CDN
```

Runtime server infrastructure is not required for the core portfolio.

## 4. Source of Truth

Git is the source of truth for the project.

The repository contains:

- application source
- configuration
- documentation
- tests
- build configuration
- CI configuration
- approved assets

Generated build output should not become the primary source of application code.

## 5. Branch Strategy

The repository should use a protected production/default branch and short-lived feature branches where practical.

Conceptually:

```text
main
 ↑
feature/*
fix/*
refactor/*
```

Changes should be reviewed before becoming release-quality when collaboration/review infrastructure is available.

## 6. Development Environment

Development should be reproducible from documented setup instructions.

The environment must define:

- supported Node.js version/range
- package manager
- required commands
- environment variables
- build command
- test command
- preview command

Exact versions are finalized in the project configuration and lockfile rather than duplicated across documentation.

## 7. Package Management

Use one package manager consistently.

Commit the corresponding lockfile.

Do not mix package managers during normal development because this can produce inconsistent dependency resolution.

## 8. Dependency Policy

Dependencies must be justified by actual product requirements.

Before adding a dependency, evaluate:

- functionality gained
- bundle/build impact
- maintenance status
- license
- security considerations
- accessibility implications
- whether native/platform functionality is sufficient

## 9. Build Pipeline

The production pipeline follows:

```text
Install locked dependencies
        ↓
Static/type/lint validation where configured
        ↓
Tests
        ↓
Production build
        ↓
Build artifact inspection
        ↓
SEO/accessibility/performance validation
        ↓
Release/deploy
```

The exact command names are implementation details and must be sourced from the repository configuration.

## 10. Build Reproducibility

Production builds should use the committed lockfile and a clean environment.

Do not rely on developer-machine state, globally installed packages, or untracked generated files.

## 11. Environment Separation

Where environment variables are required, distinguish:

```text
Development
Preview
Production
```

Values should be supplied by the appropriate environment rather than committed to source control.

## 12. Environment Variables

Public configuration and secrets must be treated differently.

```text
Public site configuration
    → may be exposed to client/build output when intentionally designed as public

Secrets/private credentials
    → never committed or exposed to client bundles
```

The project must document required variables and whether each variable is safe for client exposure.

## 13. Secrets

Never commit:

- API keys
- private tokens
- passwords
- private certificates
- production credentials
- service-account secrets

If a secret is accidentally committed, removing it from the latest file is insufficient; the credential should be rotated/revoked according to the service involved.

## 14. Static Hosting Compatibility

The core portfolio must be deployable to static hosting platforms that support the generated output.

The template should avoid requiring:

- persistent application servers
- database infrastructure
- server-side sessions
- runtime secrets

for the default portfolio experience.

## 15. Hosting Adapter Strategy

The application architecture should remain hosting-agnostic where possible.

The core build produces a standard deployable artifact. Platform-specific adapters/configuration may be added only when a hosting target genuinely requires them.

## 16. Preview Deployments

Pull requests/feature branches should be previewable where the selected Git hosting/deployment platform supports it.

A preview should use the same production build process as closely as practical.

Preview environments must not accidentally use production secrets or production-only integrations.

## 17. CI Architecture

Continuous integration should validate changes before release.

A practical pipeline is:

```text
Checkout
  ↓
Install locked dependencies
  ↓
Lint/type checks where configured
  ↓
Unit/component tests where configured
  ↓
Build
  ↓
Accessibility checks
  ↓
SEO checks
  ↓
Performance/build-size checks
  ↓
Artifact validation
```

The final CI implementation will reflect the actual tools selected during implementation.

## 18. Pull Request Gate

A production-bound change should not be merged when required validation fails.

At minimum, the project should prevent obvious failures such as:

- broken build
- failed required tests
- invalid critical configuration
- accidental secret exposure

## 19. Build Artifact

The production output should be treated as a release artifact.

Before deployment, verify:

- expected files exist
- routes are generated
- assets resolve correctly
- metadata is present
- no development-only files are exposed
- no secret values are present

## 20. Artifact Inspection

Artifact inspection should cover representative HTML and asset output.

Check for:

```text
HTML
CSS
JS
images
fonts
robots.txt
sitemap
metadata
structured data where used
```

## 21. Static Route Strategy

Routes should be generated according to the content architecture.

If a route does not require runtime computation, it should preferably become static output.

Dynamic routing must not be introduced merely for convenience.

## 22. 404 Strategy

The deployment must provide an appropriate not-found experience compatible with the selected static host.

The 404 page should retain:

- site identity
- useful navigation
- accessible structure
- recovery path to important content

## 23. Redirect Strategy

When public URLs change, redirects should be defined where the hosting platform supports them.

Avoid silently breaking established links.

Redirect rules belong in deployment configuration rather than scattered through client-side JavaScript.

## 24. Caching Strategy

Static hashed assets should be suitable for long-lived caching.

HTML caching/revalidation depends on the hosting platform and final deployment model.

The architecture should avoid cache behavior that causes stale assets to reference incompatible files.

## 25. CDN Compatibility

The generated static site should work naturally behind a CDN.

Assets should be immutable/fingerprintable where the build system supports it.

## 26. Security Headers

Where the selected hosting platform permits configuration, production should consider appropriate security headers such as:

- Content Security Policy
- Strict-Transport-Security
- X-Content-Type-Options
- Referrer-Policy
- Permissions-Policy

Exact policies must be validated against actual site behavior rather than copied blindly. A CSP that breaks required functionality is not an acceptable default.

## 27. HTTPS

Production deployment should use HTTPS.

Mixed-content resources must not be introduced.

## 28. Domain Strategy

The template should not hard-code the creator's production domain into reusable content.

Site URL/domain belongs in configurable site data/build configuration.

## 29. Deployment Safety

Before production deployment:

```text
Build
 ↓
Test
 ↓
Inspect
 ↓
Deploy
 ↓
Smoke test
```

Do not deploy directly from an unvalidated working tree when a reproducible CI artifact is available.

## 30. Post-Deployment Smoke Test

After deployment, verify representative critical paths:

- homepage
- navigation
- project pages
- article/content pages where present
- contact path where present
- theme switching where present
- mobile layout
- 404 page
- sitemap
- robots
- canonical metadata
- social metadata where practical

## 31. Rollback Strategy

The deployment platform should retain or make reproducible previous known-good releases.

If a deployment introduces a critical regression:

```text
Identify bad release
      ↓
Restore previous known-good artifact
      ↓
Verify
      ↓
Investigate/fix
      ↓
Release again
```

## 32. Release Versioning

Commercial releases should have identifiable versions.

Recommended semantic structure:

```text
MAJOR.MINOR.PATCH
```

Use version changes consistently with the project's release policy.

## 33. Changelog

Material releases should document:

- new features
- fixes
- breaking changes
- accessibility changes
- performance changes
- migration instructions where required

## 34. Commercial Distribution Architecture

Portfolio Pro has two related outputs:

```text
Development repository
        ↓
Validated product source
        ↓
Commercial release package
```

The commercial package should contain what customers need to install/customize the template without exposing internal development-only artifacts unnecessarily.

## 35. Gumroad Package Boundary

The Gumroad distribution package should be assembled from a known release state rather than manually copying arbitrary working files.

The package should include, as appropriate:

- source code
- public assets
- configuration examples
- documentation
- customization guide
- installation instructions
- license
- changelog/version information

Private development files, credentials, local caches, and internal automation secrets must never enter the package.

## 36. Free / Pro Distribution

If Free and Pro editions are offered, their build/package boundaries must be explicit.

Do not create accidental differences by manually deleting files from one copy.

The release process should make edition-specific inclusions reproducible.

## 37. Customer Configuration

Customer-editable configuration should be clearly separated from framework/source internals.

The documentation should tell customers where to change:

- site identity
- author/profile information
- navigation
- projects
- services
- social links
- theme tokens
- SEO defaults
- deployment settings

## 38. Customer Build Independence

A customer should be able to build the template using the documented supported environment without access to the original developer's machine, credentials, or private services.

## 39. Licensing

The commercial package must contain an explicit license defining permitted use, modification, redistribution, and other applicable rights.

The final license text is a product/legal decision and should be reviewed appropriately before sale.

## 40. Documentation Distribution

Customer-facing documentation should explain at minimum:

1. prerequisites
2. installation
3. local development
4. configuration
5. customization
6. build
7. deployment
8. SEO setup
9. accessibility expectations
10. support/troubleshooting

## 41. Deployment Documentation

The project should provide platform-specific deployment guides only for platforms the product explicitly supports.

Do not claim compatibility that has not been tested.

## 42. Build and Deployment Testing Matrix

Before release, test the production build in:

```text
Local production preview
        ↓
Primary supported static host
        ↓
Mobile browser
        ↓
Desktop browser
```

Additional hosts may be validated as compatibility expands.

## 43. Dependency and Supply-Chain Checks

CI should use lockfile-based installation and should review dependency/security warnings where tooling supports it.

Dependency upgrades should be tested rather than blindly applied.

## 44. Build Failure Policy

A failed production build is a release blocker.

Do not bypass CI validation merely to publish quickly.

Any intentional exception must be documented and approved.

## 45. Observability

The static portfolio does not require heavy runtime observability.

Production monitoring should focus on practical signals such as:

- availability
- broken deployments
- critical client errors where monitored
- performance/user experience where measurement is available

Optional analytics must remain non-essential.

## 46. Privacy

Deployment architecture must not require unnecessary collection of visitor data.

Third-party analytics, forms, or external services must be evaluated against privacy requirements before inclusion.

## 47. AI Agent Build/Deployment Contract

AI agents must not modify deployment configuration casually.

Before changing build/deployment infrastructure, the agent must explain:

1. What problem the change solves.
2. Which environment is affected.
3. Whether secrets/configuration are affected.
4. Whether static-host compatibility changes.
5. Whether the release artifact changes.
6. What tests were run.
7. How rollback would work.

## 48. AI Agent Release Rules

AI agents must never:

- commit secrets
- invent environment variables
- change deployment targets without approval
- remove security/accessibility checks to make CI pass
- bypass failing tests silently
- publish unvalidated artifacts
- add a hosting dependency without architectural justification

## 49. Architecture Invariants

1. Git is the source of truth.
2. Production builds are reproducible.
3. Locked dependencies are used for release builds.
4. Core portfolio content remains static-first.
5. Secrets never enter source or client output.
6. Preview and production environments are separated.
7. Production artifacts are validated before deployment.
8. Static hosting remains the default deployment model.
9. Deployment failures are release blockers.
10. Previous known-good releases remain recoverable.
11. Commercial packages are reproducibly assembled.
12. Free/Pro boundaries are explicit.
13. Customer setup does not depend on private developer infrastructure.
14. AI agents must explain material build/deployment changes.

## 50. Architecture Gate

Step 2.11 is complete when source control, branching, reproducible builds, dependency management, environment separation, secrets, static hosting, previews, CI, artifact validation, routing/404/redirects, caching, security headers, deployment safety, rollback, versioning, commercial packaging, customer configuration, licensing/documentation boundaries, testing, privacy, and AI release rules are documented.

Next step: **Phase 2 — Step 2.12: AI Development Architecture.**
