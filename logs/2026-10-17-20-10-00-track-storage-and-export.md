# Separate canonical track storage from exported collections

## Status
Accepted architectural and product principles; storage implementation remains open.

## Context
Tracks may appear on multiple albums, compilations and playlists, and collaborations do not fit a single artist-folder hierarchy. The user also wants convenient music copies on a phone.

## Decision
- MusicHub manages one canonical stored copy per genuinely identical track performance/version; distinct mixes, remixes and other genuinely different performances must not overwrite each other.
- Physical storage organization is independent of artist, album, compilation and playlist membership.
- Albums, compilations and playlists are logical groupings/references, not reasons to duplicate the canonical audio.
- MusicHub can generate a separate export with readable artist/title naming and suitable metadata for use on external devices, including phones.
- Additional storage consumption from such an export is acceptable.

## Rationale
Avoid duplicate tracks in the managed collection and repeated identical songs when shuffling, while retaining convenient file-based portability and allowing multi-artist relationships.

## Not decided
- Exact identity matching and deduplication algorithm.
- Canonical file layout, names or identifiers.
- Export folder structure, synchronization mechanism and playlist file format.
- Filesystem versus S3-compatible storage such as MinIO.

## History
Extends the managed-library and authoritative-library decisions.
