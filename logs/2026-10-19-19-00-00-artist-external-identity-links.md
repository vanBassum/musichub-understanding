# Catalog external identifiers and correctable artist matching

Date: 2026-10-19
Status: Approved product decision

## Context
MusicHub's internal catalog must connect artist identities from multiple external music sources. Existing artist records cannot safely be reconciled on name equality alone. The integrated artist page should display local and external information for the same actual artist without fabricating identity.

## Approved
- Maintain MusicHub's own canonical internal artist identity.
- Associate an artist with zero or more source-scoped external identifiers. A link identifies the source/provider and its identifier; different providers may identify the same internal artist.
- Keep this mapping as a distinct durable catalog relation, rather than treating an external ID as the canonical internal artist key.
- Matching and link discovery should run automatically as much as reasonably possible, based on reliable evidence; names alone are not proof of identity.
- Automated matching can be wrong. Users must be able to inspect, correct and unlink an incorrect external association, and manually associate the correct identity.
- Corrections must not be silently reverted by subsequent automation. Record sufficient provenance of automatic links and user corrections to support review and troubleshooting.
- The mapping should be extensible to other catalog entity types when those are designed, but this decision authorizes artist identity linkage first.

## Deferred / open
- Album and release identity/modeling and album edition wishlist behavior are explicitly deferred.
- Exact confidence thresholds, ambiguity UX, collision/merge strategy for pre-existing duplicated local artist records, external provider-specific IDs and background scheduling remain implementation/design questions; do not silently assume a global auto-merge of artists.
- User believes upload works; runtime verification is separate and not part of this decision.

## Rationale
A source-qualified identifier link enables accurate cross-provider reconciliation while preserving MusicHub's own identity and allowing manual repair of occasional mistakes.
