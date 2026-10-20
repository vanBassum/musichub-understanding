# Missing music is a library view, not a wishlist

Status: Approved
Date: 2026-10-20

## Context
The earlier understanding treated wishlist membership as an explicit user-controlled property, represented in implementation by Track.WantedAt. During discussion the owner clarified that tracks are catalog/library records independently of audio availability; the useful list is music with no available file.

## Decision
- The library contains all registered tracks, whether or not an audio file is available.
- “Missing Music” (Dutch discussion name: “Ontbrekende muziek”) is a filtered library view of tracks with no linked available/stored FileRecord. “Available Music” is the complementary view.
- No separate wishlist entity, wishlist membership state or WantedAt field is required. Track.CreatedAt records when the track record was created.
- Adding a selected track or selected album edition creates/uses catalog records; missingness follows from file availability, not a separate wish action.
- The missing-music view can later be a starting point for search and acquisition. The exact authorization and scheduling rules for automatic acquisition must be revisited; earlier wishlist-based authorization must not silently be transferred to all catalog entries.

## Supersedes
Earlier explicit-wishlist membership semantics in the projections and their supporting logs, only insofar as they require a separate wanted state. Selection scope for tracks and album editions remains applicable.

## Not decided
Automatic acquisition authorization for missing tracks; handling of unavailable versus non-stored linked files beyond the available/stored distinction.
