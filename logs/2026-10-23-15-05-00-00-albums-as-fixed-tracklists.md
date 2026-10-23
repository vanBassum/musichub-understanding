# Albums are fixed ordered collections of tracks

Status: Approved
Date: 2026-10-23

## Decision
MusicHub albums represent existing published releases, including studio albums, greatest-hits collections and multi-artist compilations. Each album edition/release has its own fixed, ordered list of references to catalog tracks. A mandatory album-artist domain attribute is not needed; each track retains its own artist attribution. Album titles, artwork and release metadata may be retained. Different editions may coexist and share identical catalog tracks, but different remasters or mixes are distinct tracks. Users cannot edit published album track lists; editable user collections are playlists.

## Scope
No user-created albums in the current scope. External metadata may include an album-artist credit, but this does not require a canonical album-artist entity. Missing or ambiguous external track lists must not be invented.
