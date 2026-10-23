# Separate external Search from local Library search

## Context
Earlier decisions described one combined local/external search experience. During the 2026-10-22/23 search redesign discussion, the product owner explicitly chose fully external Search and a small search field above Library. This supersedes the earlier unified search requirement.

## Approved decision
- The dedicated Search page searches external music metadata only, including artists, tracks and albums/compilations. Search results are shown inline on the page, not in a popup.
- Library has its own compact search field above its content and searches the locally registered collection only.
- Do not mix local Library results into the dedicated external Search page. Local availability indicators on external results may still be displayed where supported; they do not turn Search into a local result search.

## Rationale and trade-offs
The user chose a clear separation between discovery and navigating owned/registered music, avoiding duplicated combined-search behavior. Separate entry points are accepted.

## Supersedes
The combined local/external Search behavior in the 2026-10-19 mobile-search-player-more-navigation and 2026-10-18 unified-catalog-wishlist-search decisions, only insofar as they require combined search results. Other aspects remain unchanged.

## Status
Approved by product owner in the MusicHub search discussion; implementation and deployment must be verified separately.