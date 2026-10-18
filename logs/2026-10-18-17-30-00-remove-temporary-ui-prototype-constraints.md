# Correction: temporary UI prototype constraints are not target product behavior

Date: 2026-10-18
Status: Accepted

## Context
The Features projection currently describes an *initial* UI prototype with mock data and no backend integration. It also requires nonfunctional controls and filters to appear as disabled placeholders. These statements describe temporary implementation stages, not the intended end-state of MusicHub.

## Decision
Withdraw the following as enduring product requirements:
- The UI is initially a mock-data prototype without backend integration.
- Controls and filters that have not yet been implemented must be displayed as disabled placeholders.

These temporary implementation constraints must not be projected as MusicHub's target features or treated as blockers to incremental implementation choices.

Keep the durable product choices intact: the UI is English-only; the visual layout is provisional and replaceable. The library view, filters, track table, and track detail interactions remain valid product concepts, without requiring a particular temporary implementation stage.

## Rationale
Understanding records what MusicHub should ultimately do. Intermediate delivery steps belong to implementation planning and may be selected independently without creating new product decisions.

## History
Supersedes only the temporary mock-data/no-backend and disabled-placeholder statements currently appearing in `features/features.md` section 10. No projection is edited by this log.
