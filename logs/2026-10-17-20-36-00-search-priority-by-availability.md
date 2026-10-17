# Search priority based on track availability and quality

## Status
Accepted principle; exact intervals and priority settings remain open.

## Context
Missing music is more important to obtain than upgrading already-available music to a higher bitrate or format.

## Decision
- MusicHub periodically searches for missing wanted tracks and for better-quality versions of tracks below their configured quality cutoff.
- Missing tracks should normally receive higher search priority and/or more frequent searches than tracks already present but eligible for quality upgrades.
- Search intervals and priorities should be configurable; one uniform cadence is not required.
- Tracks already meeting their quality cutoff need not continue upgrade searches.

## Rationale
Focus search resources on acquiring unavailable music while allowing less urgent quality improvements over time.

## Not decided
- Actual default intervals, scheduling rules and backoff.
- Whether settings apply globally, by profile, by track, or by task type.
- How search providers and rate limits influence scheduling.

## History
Extends the configurable audio quality profiles decision.
