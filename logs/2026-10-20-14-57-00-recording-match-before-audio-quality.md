# Correct recording takes priority over audio quality

Status: Approved
Date: 2026-10-20

## Context
MusicHub's initial autonomous acquisition prefers the best available MP3, while accepting lower bitrate when necessary. Soulseek search results may represent different recordings or versions (studio, live, remix).

## Decision
- Select candidates matching the intended specific recording or performance before considering MP3 bitrate or audio quality.
- Never prefer a higher-bitrate file for a different performance, live version, remix or otherwise mismatched recording.
- Among sufficiently matching candidates, prefer the best available MP3 quality, allowing lower-quality fallback.
- A download candidate's filename or search metadata alone does not establish definitive identification; existing identification safeguards still apply.

## Open
Evidence requirements and scoring for recording matching, ambiguity handling, and quality ranking details.
