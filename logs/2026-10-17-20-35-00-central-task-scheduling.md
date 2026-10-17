# Central task scheduling

## Status
Accepted principle; scheduler implementation and UI details are open.

## Context
MusicHub will need recurring tasks such as searches for missing tracks and audio-quality upgrades. The user wants visibility and manual control over scheduled work.

## Decision
- MusicHub provides a central scheduler for recurring tasks across different workflows.
- Users can see planned tasks, running tasks, their previous results and next scheduled execution.
- Users can manually trigger a task in addition to its automatic schedule.
- Scheduling and task behavior should be configurable without requiring UI-only configuration, consistent with MusicHub's file-based configuration policy.

## Rationale
Provide predictable, observable and controllable background automation rather than hidden ad hoc jobs.

## Not decided
- Task definitions, concurrency, retry policies, cancellation, logs, history retention and permissions.
- UI layout and editing capabilities.
- Scheduling expression format and deployment topology.

## History
Extends the file-based configuration and quality profile decisions.
