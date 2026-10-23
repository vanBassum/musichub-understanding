# Adding an album registers all edition tracks in the Library

Status: Approved
Date: 2026-10-23

## Decision
Before adding an album, the user explicitly selects a release/edition; the original/standard edition may be suggested but is not silently chosen. Adding the edition registers the album and every track in its fixed ordered list in the Library, even when no audio files are available. Existing matching catalog tracks are reused, without duplicating them; distinct mastered versions remain distinct. Albums remain visible at 0/N available and expose per-track availability based on linked files, e.g. 8/12. Multiple editions can be registered concurrently and share track references where identity truly matches.

## Clarification
There is no separate wishlist entity required for this operation: wanted tracks are catalog tracks that currently lack linked audio files. This supersedes earlier wording that adding an album creates wishlist entries or wishlist-track rows. Adding an album does not automatically acquire unrelated albums, editions or an artist's discography.

## Open
Precise rules for choosing a suggested original edition and behavior when a provider returns incomplete or ambiguous track lists need further product decisions; do not guess or fabricate tracks.
