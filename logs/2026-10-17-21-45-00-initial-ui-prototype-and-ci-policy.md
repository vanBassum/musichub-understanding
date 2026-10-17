# Initial MusicHub UI prototype and delivery policy

Date: 2026-10-17
Status: Accepted by product owner

## Context

The first MusicHub UI shell (implementation issue vanBassum/musichub#5) is a small, replaceable visual prototype. The supplied concept screenshot is a reference for this implementation, not a permanent visual contract. The previous design projection left visual direction, navigation and layout undecided, which blocked the issue.

## Decisions

- **Provisional visual direction:** Use the supplied issue #5 screenshot as the reference. A dark, desktop-first interface with a horizontal top navigation/header, and a library area consisting of a left filter sidebar, central track table and right selected-track details panel. Compact information density, album artwork and blue accents. Approximate the composition without requiring pixel-perfect fidelity. Responsive layout may adapt or collapse panels. This is an initial direction only: future UI redesigns are explicitly permitted without treating the screenshot or layout as a permanent constraint.
- **UI language:** English only. Translate any Dutch labels visible in the screenshot to English. No multilingual or internationalization framework is required.
- **Prototype interaction:** Use mock music data. Selecting a track updates the selected row and its details panel. Other not-yet-implemented controls and filters remain visible as visually faded, disabled placeholders, not deceptive interactive elements. No backend, database, or API integration is part of this prototype.
- **Component policy:** Prefer existing or newly added shadcn/ui components, with Tailwind for styling. Compose reusable React components where useful. Adding shadcn/ui components is allowed. Introducing other dependencies requires explicit owner approval beforehand.
- **Build and deployment policy:** Implementation agents do not run local builds or test suites. For pull requests, GitHub Actions performs compile/build validation and linting; failing required checks must block merging to main. After merging to main, build the deployable Docker image and deploy it to acceptation. The post-merge image build is distinct from PR validation. Do not duplicate Docker image builds during PR validation solely for this purpose. CI failures are addressed from CI results. This is a general MusicHub development rule, not just issue #5.

## Scope and rationale

These decisions unblock a limited UI proof of concept while leaving room to evolve the product design. Reuse established UI components and avoid extra dependencies. CI provides the automated validation rather than duplicating it inside an AI coding session.

## Open / not decided

Future production visual design, real library data integration, search/filter behavior, playback, and broader navigation functionality remain separate implementation decisions. This log does not assert that the current CI workflow already implements the stated desired build/deployment policy; verify and adjust the implementation pipeline separately.
