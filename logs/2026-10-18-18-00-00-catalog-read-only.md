# Catalog is read-only to users

Status: accepted decision (2026-10-18).

## Context

The earlier central music catalog decision allowed manually registering tracks and viewing/searching them. Implementation PR vanBassum/musichub#59 introduced POST and PUT track endpoints. Discussion clarified that manual catalog mutation is not the intended product behavior.

## Decision

The catalog is a read-only view for users: users can browse, inspect and search tracks and their relationships, but cannot directly create, replace, edit or delete catalog tracks through the catalog interface or user-facing catalog API. The catalog's user-facing API therefore exposes read operations only (including listing/search and detail). Remove POST /api/tracks and PUT /api/tracks/{id} from the current PR.

Tracks may enter or change in the catalog as outcomes of other system processes, not through direct user catalog editing. The behavior and policies of importing, identifying, correcting identities, and internal writes are explicitly outside the scope of this decision and remain to be discussed in their own sessions. This decision supersedes the earlier suggestion of manually registering tracks in the initial catalog delivery; it does not negate the track/artist/audio-file domain model.

## Rationale

The catalog represents system-established music knowledge, rather than a manually maintained database. Separating its read interface from upstream processes prevents accidental creation of a second manual catalog-management workflow.
