# Compare identification confidence of existing and incoming audio

## Status
Accepted principle; decision thresholds and automatic replacement policy remain open.

## Context
When a downloaded track has uncertain identity, the appropriate response depends in part on the identification confidence of the audio already in the library. The user also wants the option to retain candidates for later review.

## Decision
- Evaluate the identification confidence of both the existing library recording and the incoming candidate when deciding whether to accept or replace audio.
- Do not automatically displace a confidently identified existing recording with a less certain candidate merely because its encoding quality is better.
- A candidate that has stronger identification evidence than the existing recording can be preferred for further evaluation, subject to configured import thresholds and identity/version checks.
- Uncertain candidates may be retained outside the canonical accepted library and displayed in a later review overview.
- Identity confidence and audio quality are separate decision dimensions; do not collapse them into one quality score.
- Existing acceptance thresholds still apply: low-confidence audio must not silently enter the canonical library.

## Not decided
- Exact confidence comparison rules, thresholds, and whether automatic replacement is allowed when both are uncertain.
- How to store, retain, review, approve, reject or clean up uncertain candidates.
- How uncertainty provenance and manual decisions influence future searches.

## History
Refines configurable identification, per-track validation and retained audio version decisions.
