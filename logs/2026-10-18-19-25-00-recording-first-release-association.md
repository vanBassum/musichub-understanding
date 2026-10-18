# Identify the exact recording before associating a release

Date: 2026-10-18
Status: Accepted

## Context
Incoming audio may carry metadata from a compilation (for example a Top 100 collection). That compilation may not be the best canonical association for the actual recording. Exporting different presentation metadata is a separate future concern.

## Decision
- The smallest identification unit is the **individual recording**: the actual performance, mix and edit represented by the incoming audio, not the composition, album, or compilation.
- Identify that exact recording as accurately as possible before deriving release metadata.
- Prefer association with the original single release that contains **that same recording**. If none exists, prefer the appropriate original album release containing that same recording.
- Compilation metadata is useful as an input hint but is not automatically the selected canonical release association.
- Never select a different performance, mix, edit, remaster or recording merely to obtain a preferred single/album association.
- This functional policy applies to both rule-based and AI identification strategies.
- Future export/playlist functionality may render different metadata; this is outside the current identification scope.

## Rationale
Canonical identification should reflect what the audio actually is, independent of how the input was packaged or tagged. Presentation-specific metadata can be handled separately later.

## Relationship to prior decisions
Clarifies and reinforces the existing preference for original single, then original album, without overriding the requirement for exact recording identity. Does not prescribe technical interfaces or algorithms.
