# Direct addition and drag-and-drop in the current playback queue

Date: 2026-10-23
Status: Approved

## Context
Adding a track to the current playback queue currently presents further choices. The user wants direct, predictable queue actions.

## Decision
- Dragging a track into the current playback queue appends it to the queue.
- The track's add (+) action immediately appends it to the end of the current playback queue, without presenting an options menu.
- Adding a track does not automatically start playback; playback remains a separate action.
- Reordering existing entries by dragging within the current queue is supported.
- Duplicate entries are allowed: the same track may occur multiple times in the queue.
- When a track already exists in the current queue, adding another occurrence still succeeds immediately, with a nonblocking warning that the track is already present. Do not require confirmation or an additional click.
- Apply the same duplicate behavior to add-button and drag-and-drop addition.

## Rationale
The queue represents an ordered sequence of playback entries, not a set of unique tracks. Fast queue operations should not require extra dialogs.

## Boundaries
Preserve the current playback state, shared player/queue across navigation, and keyboard-accessible alternatives to drag-and-drop.
