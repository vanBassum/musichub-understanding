# Per-track validated album import

## Status
Accepted.

## Context
A downloaded album package may contain both correctly identified tracks and a wrong or uncertain recording.

## Decision
- Validate and process downloaded album contents per track rather than treating the package as an all-or-nothing transaction.
- Import only tracks whose identities meet the configured acceptance rules.
- Correctly validated tracks may be imported immediately even if other tracks in the same package fail validation.
- Incorrect or insufficiently identified tracks must not enter the canonical library.
- Album tracks still missing after validation remain eligible for future acquisition searches.

## Not decided
- Whether rejected package files remain in staging or a quarantine area, and for how long.
- User review and reprocessing controls for rejected tracks.
- How partial album completeness is presented.

## History
Extends the configurable identification pipeline, quarantine policy and album package acquisition decisions.
