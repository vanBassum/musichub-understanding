# Explicit album wishlist expansion

## Status
Accepted.

## Context
MusicHub allows adding music to a wishlist from search. The user distinguished explicitly selecting an album from selecting other entities.

## Decision
- When the user explicitly adds an album to the wishlist, MusicHub should resolve its track list and seek the album's constituent tracks, subject to its existing library and acquisition rules.
- Adding a single track does not implicitly request its entire album.
- Adding an artist does not implicitly request the artist's entire discography.
- The scope of automatic acquisition must follow the explicit item selected by the user, not inferred broader interests.

## Not decided
- What adding an artist means operationally, if supported at all.
- How editions, deluxe releases, bonus tracks and album variants are selected.
- How missing track listings or ambiguous album identity are handled.

## History
Refines the user-curated wishlist and in-app search decisions.
