# Shared interface for external metadata providers

Date: 2026-10-23
Status: Approved

## Context
MusicHub uses MusicBrainz for music identity and plans to use ListenBrainz for song popularity. Separate specialized provider interfaces would create unnecessary architectural divergence.

## Decision
- MusicBrainz and ListenBrainz implement the same external metadata provider interface.
- Each provider returns only the fields or results it can supply; unsupported data yields an empty result rather than a fabricated value or error.
- MusicBrainz may return identity/catalog metadata without popularity. ListenBrainz may return popularity without complete catalog metadata.
- MusicHub combines available provider results by stable music identity where possible.
- Distinguish an ordinary empty/unsupported result from provider failure or unavailability, so a failing provider does not silently masquerade as no data.
- External popularity enrichment remains optional and must not prevent core artist/track discovery when unavailable.

## Rationale
A common contract keeps provider integration consistent while allowing sparse and complementary metadata sources.

## Implementation boundary
Exact contract shape, field-level merge rules, caching, and error representations are implementation details to validate against current code; do not overwrite authoritative identifiers with untrusted enrichment.
