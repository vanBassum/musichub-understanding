# External providers implement capability-specific interfaces

Date: 2026-10-23
Status: Approved

## Context
The earlier approved decision in `2026-10-23-13-35-00-shared-metadata-provider-interface.md` required MusicBrainz and ListenBrainz to implement the same interface, returning empty results for unsupported capabilities. Reviewing the ListenBrainz implementation exposed unnecessary methods for capabilities a provider does not offer.

## Decision
- **Supersede the earlier requirement that every external metadata provider implement one common interface.**
- Define separate capability-oriented contracts, including music discovery/search (`IExternalMusicSearch`) and popularity enrichment (`IExternalPopularitySource`).
- A provider may implement either or both contracts, depending on its capabilities. Providers must not implement irrelevant interfaces solely to return empty results.
- MusicBrainz currently supplies catalog identity/search. ListenBrainz currently supplies popularity. ListenBrainz search capabilities may be integrated later through the search contract, but are not required in the present popularity work.
- A supported operation with no matching data returns an empty result; provider failure/unavailability is a distinguishable outcome.
- Combine results using stable music identities where possible, preserve distinct recordings, and never invent popularity values.
- Optional enrichment failure must not break catalog discovery.

## Rationale and boundaries
Capability interfaces keep integrations extensible and avoid conflating independent operations. This changes only the interface architecture, not the approved song-level popularity, preferred studio-version presentation, or acquisition rules.
