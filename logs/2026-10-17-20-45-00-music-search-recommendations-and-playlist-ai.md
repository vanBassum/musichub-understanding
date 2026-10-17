# Music search, recommendations, and AI playlists

## Status
Accepted direction; playlist-to-wishlist interaction remains open.

## Context
The user clarified that user-curated wishlist does not mean MusicHub cannot help discover music. MusicHub should offer in-app search and may display recommendations. An AI that constructs playlists is expected to be the main source of suggestions.

## Decision
- Users can search for music inside MusicHub and add chosen results to their wishlist.
- MusicHub may present a Recommended list as suggestions, without automatically adding suggestions to the wishlist.
- AI-generated playlists are expected to be a major source of music suggestions, including potentially music not yet in the library.
- Discovery and recommendation are distinct from authorizing acquisition: wishlist additions remain user-controlled unless a later decision explicitly changes this boundary.
- MusicHub may automatically search for and acquire music that has been explicitly added to the wishlist, according to its configured workflows.

## Not decided
- Which search sources are supported and how results are grouped by track, album, and artist.
- How AI playlists reference unavailable music and whether they offer one-click or bulk wishlist additions.
- Recommendation ranking and whether the Recommended list is AI-generated or sourced elsewhere.
- Whether adding an album or artist automatically expands to constituent tracks.

## History
Clarifies the prior user-curated wishlist decision without superseding its authorization boundary.
