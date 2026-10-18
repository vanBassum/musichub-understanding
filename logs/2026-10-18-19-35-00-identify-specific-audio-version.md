# Identify the specific audio version, with realistic uncertainty

Date: 2026-10-18
Status: Accepted

## Context
A musical work or performance can have many materially different released audio versions, including original masters, later remasters, radio edits, remixes and other variants. External databases may not consistently distinguish them. The user wants identification to be as precise and correct as practicable, without pretending certainty that evidence cannot support.

## Decision
- Identification aims to determine the **specific audio version actually present** in the supplied stream, not merely the song title, artist, composition or broad recording family.
- Distinguish original masters, remasters, mixes, edits, remixes and other version differences whenever evidence supports doing so, even if there are many versions.
- The correct release association must correspond to that particular version. Do not silently substitute a better-known original or another version to satisfy a preferred release association.
- When evidence identifies a broader recording but cannot reliably distinguish its exact version, do not falsely claim an exact-version identification. The identification service may return no identity rather than guess.
- This is a best-effort accuracy objective, not a guarantee of perfect recognition. Providers and resolvers should preserve uncertainty and acknowledge the limits of available evidence.
- External catalog concepts such as a MusicBrainz recording ID need not correspond one-to-one to MusicHub's required version distinction; technical modeling is left to implementation.

## Rationale
Correct version identity matters even when a file is derived from a compilation or has misleading metadata. Prioritizing precision and acknowledging uncertainty prevents silently misidentifying remasters or alternate edits.

## Relationship to prior decisions
This refines the earlier recording-first/original-single preference: exact audio version correctness takes precedence over a convenient original release association. It retains the single-identity-or-no-identity public service outcome and does not prescribe implementation details or thresholds.
