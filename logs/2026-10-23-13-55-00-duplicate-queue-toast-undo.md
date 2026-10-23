# Undo action on duplicate queue addition warning

Date: 2026-10-23
Status: Approved

## Context
The previously approved direct queue addition behavior allows duplicates and shows a nonblocking warning. The user refined the warning to allow reversing the addition.

## Decision
- When adding a track that is already present in the current playback queue, append it immediately and show a nonblocking toast with an **Undo** action.
- Activating Undo removes only the specific queue entry just appended, not earlier occurrences of the same track.
- No confirmation dialog or additional step is required to add a duplicate.
- This refines the duplicate-warning behavior in the earlier direct queue addition decision; all other aspects remain unchanged.

## Rationale
The action remains fast while making accidental duplicate additions easy to reverse.
