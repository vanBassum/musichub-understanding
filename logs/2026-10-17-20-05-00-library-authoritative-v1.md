# Authoritative library ownership for version 1

## Status
Accepted for version 1 (provisional scope); two-way synchronization remains open for future discussion.

## Context
MusicHub's managed files may be synchronized to a phone, for example through Google Drive. Changes made on another device could otherwise add or remove tracks in the managed library, raising synchronization and conflict questions.

## Decision
- MusicHub is the authoritative manager of its own library.
- In version 1, external devices and services may read or copy library files for use elsewhere.
- Changes on a phone or another synchronized copy must not automatically modify, add to, or delete files in MusicHub's authoritative library.
- Two-way synchronization is not part of version 1; it can be reconsidered later.

## Rationale
Avoid accidental deletion, duplicates, and synchronization conflicts while establishing a clear source of truth.

## Not decided
- How exports or one-way synchronization are implemented, including Google Drive integration.
- Whether future two-way sync is desirable and how conflicts would be resolved.
- Whether MusicHub should detect and repair out-of-band edits to its own managed folder.

## History
Follows the initial managed-library boundary decision.
