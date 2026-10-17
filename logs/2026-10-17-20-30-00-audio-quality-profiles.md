# Configurable audio quality profiles

## Status
Accepted principle; specific quality ranking and upgrade automation remain open.

## Context
MusicHub may encounter multiple audio files of different qualities representing the same recording. The user wants a Sonarr-like configurable list of acceptable qualities and an upgrade cutoff.

## Decision
- MusicHub supports configurable audio quality profiles.
- A profile defines which qualities are acceptable, their preference order, and a cutoff at which a stored track no longer needs upgrading.
- Below the cutoff, MusicHub should prefer replacing an existing lower-quality file with a better acceptable version of the same recording when one becomes available.
- Reaching the configured cutoff means the track is considered good enough; higher qualities need not trigger replacement.
- Quality ranking must be configurable rather than hardcoding a universal preference for a particular format or bitrate.
- An upgrade must preserve the identified recording/version and must not silently substitute a different mix, performance or remaster.

## Rationale
Enable gradual improvement of library audio quality without repeated unnecessary replacement or loss of recording identity.

## Not decided
- Quality attributes, profiles and default ranking.
- How profiles are assigned and whether several profiles can coexist.
- Whether replacement is automatic or requires confirmation, and handling of original files.
- Search cadence and interaction with downloads.

## History
Extends canonical recording identification and hash-based internal storage decisions.
