# Decision: direct playback of stored audio independent of catalog identity

Status: accepted by owner on 2026-10-19.

Context: MusicHub receives and stores audio files before they necessarily have a validated recording identity or a catalog track association. Listening to a stored audio file should not require catalog registration or identification.

Decision:
- Any audio file whose upload/storage status is confirmed Stored may be played directly from the Files area, regardless of whether it has been identified or linked to a catalog track.
- Direct file playback and catalog-track playback use the same user-facing player and shared playback state. The player distinguishes a stored-file source from a catalog track source without requiring a catalog write.
- Playback must not implicitly identify, import into the catalog, or add the file to the wishlist.
- A file's actual audio encoding and browser support determine whether it can play. Unsupported formats should produce a clear non-destructive message rather than pretending to play.
- Seeking and ordinary playback controls should work for supported stored files; delivery of audio should support efficient partial reads.
- Files that are not confirmed Stored, are deleted, or cannot be read must not be presented as successfully playable.
- Access to stored-file audio follows the existing MusicHub internal Files API boundary; no new authentication design is implied by this decision.

Rationale: Enable immediate listening and inspection of uploaded audio without conflating storage with music identity.

Boundary: This describes the intended final product behavior. Implementation order, endpoint details, tests and mock/placeholder replacement belong in implementation issues.
