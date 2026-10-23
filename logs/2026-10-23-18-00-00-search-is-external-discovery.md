# Search is external music discovery

Status: approved by product owner, 2026-10-23.

Context: The Search surface currently emphasizes local tracks/artists, while the owner wants to find external music including compilation albums (e.g. Top 2000 collections).

Decision: Search is exclusively for external music catalog discovery, not a combined local-library search. Search covers albums including multi-artist compilations, tracks and artists. Album selection follows the existing release/edition choice and tracklist/wishlist rules; no silent edition substitution. Results must preserve source identity and recording/release distinctions. A compilation is a legitimate album/release grouping with different track artists, not a single-artist album.

Rationale: Separate discovery of new music from finding owned music. Do not infer that external results are already in the library.

Open: Search ranking, exact external provider composition and multi-source reconciliation remain undecided.
