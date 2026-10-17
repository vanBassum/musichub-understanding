# Explicit album edition selection

## Status
Accepted.

## Context
Albums can have original releases, remasters, deluxe editions and other variants. The user wants to choose the edition explicitly.

## Decision
- When adding an album, MusicHub lets the user choose the specific edition/release.
- The standard/original release is prominently displayed at the top of the available editions as the default suggested choice.
- Other editions remain available for explicit selection.
- MusicHub must not silently substitute a different edition for the user's selection.

## Not decided
- How MusicHub identifies the authoritative original release when multiple country/format editions exist.
- Exact presentation and labeling of editions.
- Whether a preselected default requires explicit confirmation before wishlist addition.
