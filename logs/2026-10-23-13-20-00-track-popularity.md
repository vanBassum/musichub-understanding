# Popularity ranking for external artist tracks

Date: 2026-10-23
Status: Approved

## Context
On the external artist page, tracks are currently listed alphabetically because the connected source provides no popularity ranking. This places obscure recordings ahead of familiar songs and makes discovery inconvenient.

## Decision
- Popularity is measured and presented per song, not per individual recording or release.
- The default artist track ordering is by popularity, with alphabetical ordering available as an alternative.
- Prefer the normal studio recording/version when presenting a song. Live recordings, remixes, and alternate versions remain accessible through the existing “Show all versions” option, rather than dominating the default list.
- ListenBrainz is an approved external source for popularity signals; MusicBrainz identity data alone is not treated as a popularity score.
- Tracks with no usable popularity signal remain discoverable and must not receive fabricated scores.

## Rationale and boundaries
The default artist view should emphasize recognizable songs without conflating distinct recordings in the canonical catalog. Popularity is a discovery and ordering signal, not a reason to merge distinct versions or automatically add music to the library or wishlist.

## Open implementation details
Choose the appropriate ListenBrainz endpoint, mapping from recordings to songs, refresh/caching strategy, and fallback ordering for missing or ambiguous popularity data during implementation. Do not imply that popularity data is complete or globally authoritative.
