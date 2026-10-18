# Decision: Integrated artist detail page
Date: 2026-10-18
Status: Accepted

## Context
Users should be able to open an artist found in local or external search, discover the artist's music, and add individual tracks or whole albums to the wishlist. A visual concept for the artist page was approved, with a separate implementation layout issue (vanBassum/musichub#88).

## Decision
- Clicking any artist search result opens a single artist detail page. Local and external artist data appear together; there is no separate external-only artist page.
- The page has an artist hero/header with identity, image and descriptive information, a Popular tracks section and an Albums section. It can offer navigation to fuller track/album lists and album details.
- Each section loads independently and shows its own loading/empty/error state, so a slow or failed provider does not block the entire page.
- Local availability and external provenance are clearly distinguishable. Viewing an externally found artist or track never automatically adds it to the catalog or wishlist.
- Popular tracks may be shown when a provider supplies credible popularity data; do not fabricate a ranking when such data is unavailable.
- Tracks may be added individually to the wishlist. Complete albums may also be added, retaining the existing rule that the user selects the release/edition and MusicHub seeks that edition's constituent tracks.
- The page is responsive and follows the MusicHub UI language (English). The visual layout concept is guidance, not a pixel-perfect or provider-specific requirement.

## Rationale
A unified artist view gives the user a coherent browsing experience while retaining catalog boundaries and explicit wishlist consent. Independent loading makes external metadata enrichment resilient.

## Open
Which provider supplies popularity data, how artist identities are reconciled across sources, album detail page behavior, and exact UI interactions beyond the approved layout.
