# Album package acquisition and per-track upgrades

## Status
Accepted.

## Context
When a requested album is partly present in the library, acquiring the entire album as a package can be practical even though only some tracks are missing.

## Decision
- MusicHub may acquire a complete album as a package, even when some tracks are already present.
- Following acquisition, MusicHub evaluates each track separately against the canonical library and configured quality profile.
- Missing tracks are imported.
- Existing tracks may be upgraded when the newly acquired file is preferred under the configured quality profile and upgrade cutoff.
- Existing tracks are retained when the newly acquired file does not qualify as an upgrade.
- Identity and the user-selected album edition must be respected; a different mix, remaster or performance is not silently substituted merely because of better encoding quality.

## Not decided
- Whether to prefer whole-album packages or individual tracks in specific search scenarios.
- Exact comparison of encoding quality and audio integrity.
- Whether replacement removes or archives the previous canonical audio file.
- How package downloads and unwanted duplicate files are staged and cleaned up.

## History
Extends explicit album edition selection, canonical track storage, and configurable audio quality profiles.
