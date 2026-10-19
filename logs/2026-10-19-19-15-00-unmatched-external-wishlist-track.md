# Unmatched external wishlist tracks may create a catalog identity

Date: 2026-10-19
Status: Approved product decision

## Context
The earlier autonomous wishlist identity-resolution decision prioritized avoiding duplicate catalog recordings and left unresolved external track candidates for review. In actual use the owner prefers a functional, low-friction wishlist over strict catalog deduplication. This log supersedes the conflicting create-only-with-positive-distinctness constraint for an explicitly selected external track.

## Decision
- When a user explicitly adds an external track to the wishlist, MusicHub first tries to link it to an existing catalog track using available trustworthy external identifiers and matching evidence.
- If no existing catalog track can be linked with sufficient confidence, MusicHub **may create a new catalog track** for that selected external result and mark it wanted. Positive proof that it is a distinct recording is **not required**. A duplicate catalog entry is an acceptable consequence.
- Do not knowingly create another record when the same external source and identifier already maps to a catalog track. Repeated wishlist actions on the same known identity remain idempotent.
- An uncertain resemblance (e.g. similar artist/title) must not silently merge distinct catalog identities. It also must not block adding the explicitly selected track to the wishlist.
- Catalog duplicates may be detected and cleaned up later. Exact duplicate review, merge, repair and cleanup strategy are explicitly **deferred** until experience from real use; no destructive automatic deduplication is authorized.
- This relaxation applies to **catalog identity creation on an explicit wishlist action**, not to audio file identification, canonical audio storage or automatic wishlist additions. The user still decides what to wishlist.

## Rationale and trade-off
Occasional duplicate catalog entries are acceptable. Avoiding false matches and keeping user-requested wishlist additions functional take priority over deduplication perfection.

## Open
Later duplicate detection, cleanup/merge UX and how to reconcile conflicting metadata or references; do not invent a cleanup policy now.
