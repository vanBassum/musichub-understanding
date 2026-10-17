# User-curated wishlist

## Status
Accepted.

## Context
MusicHub needs to know which music to seek. Automatic discovery and automatic addition to the wishlist were discussed.

## Decision
- The user decides which music to add to the wishlist.
- MusicHub does not autonomously discover and add new artists, albums, or tracks to the wishlist.
- Once the user has added an item, MusicHub may perform previously agreed automated searching, downloading and quality upgrades within configured rules.

## Rationale
The user wants to curate desired music rather than delegate music selection to MusicHub.

## Not decided
- Wishlist entry types, input methods, and whether recommendations may be displayed without automatic addition.
- How search and download tasks are initiated for new wishlist entries.
