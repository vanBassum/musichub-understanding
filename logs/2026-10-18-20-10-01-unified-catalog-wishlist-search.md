# Decision: Unified catalog, wishlist and external search
Date: 2026-10-18
Status: Accepted

## Context
The user wants missing desired music to be represented in the catalog, rather than maintaining a separate disconnected wishlist catalog. Search must find existing catalog content and music available through external metadata providers.

## Decision
- Catalog tracks may exist without an audio file. Whether audio is available is distinct from whether the user explicitly wants acquisition; the wishlist represents explicit user intent, not merely absence of audio.
- A global search field filters local catalog results immediately and automatically searches external providers after a short debounce. External search results are visibly separate from catalog entries and do not enter the catalog just because they were viewed.
- External results can be explicitly added to the wishlist; this creates or reuses the appropriate catalog identity and marks the requested item as wanted. Existing catalog identities must not be duplicated.
- Search includes tracks and artists, with configurable searchable fields: Title and Artist enabled by default, Album disabled by default. A gear/settings popover toggles fields; future fields can be added.
- Search field preferences are persisted per browser using localStorage, not the server database. Each browser can have different preferences.
- No search-result caching is required initially; caching may be reconsidered later.

## Rationale
Keep one authoritative catalog, preserve explicit acquisition consent, make discovery quick, and avoid unnecessary backend persistence for personal search UI preferences.

## Open
Exact external providers, cross-provider matching rules, debounce interval, detailed search-result ranking, and cache strategy.
