# Unidentified files and content-addressed storage

## Status
Accepted principles; quarantine location and hash implementation remain open.

## Context
Some incoming tracks cannot be identified with adequate confidence. The user wants to avoid admitting uncertain identities into the managed library. The internal physical layout should also avoid artist-folder ambiguity and straightforward exact duplicates.

## Decision
- Files below the required identification confidence are not imported into the managed library.
- Such source files remain available for later identification, either in the import area or a dedicated quarantine area; exact placement remains undecided.
- MusicHub's canonical internal file storage should use content hashes/hashed identities rather than artist and title as physical storage paths.
- Identical file content can be deduplicated by content hash.
- Content-hash equality must not be confused with musical identity: different encodings, tags or other byte differences may yield different hashes for the same recording. Musical duplicate detection remains a separate responsibility of the identification pipeline.

## Rationale
Protect library correctness and simplify stable physical storage and exact-file deduplication without depending on naming or single-artist ownership.

## Not decided
- Import-folder retention versus dedicated quarantine folder.
- Hash algorithm and whether hashes are calculated over whole files or normalized audio data.
- Canonical selection when two different files represent the same recording.
- Retry and manual review workflows.

## History
Refines the confidence-based identification pipeline and canonical storage separation decisions.
