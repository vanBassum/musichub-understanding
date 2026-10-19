# Hangfire as central background execution

## Status
Accepted decision.

## Context
The existing central scheduler principle needs a concrete implementation. The user prefers an established .NET scheduler and wants to follow its native model, avoiding a second custom scheduling framework.

## Decision
- Use Hangfire as the central background-job execution and scheduling mechanism for MusicHub, with PostgreSQL persistence in the existing deployment.
- Follow Hangfire's native background/recurring job, scheduling, state and retry concepts. Do not create parallel custom Job/Trigger/Run persistence models duplicating Hangfire.
- Jobs may be manually invoked and later scheduled periodically or enqueued by events.
- Keep domain-specific identification/import outcomes in the MusicHub domain, separate from Hangfire execution metadata.
- Expose useful job progress, history, results and errors, with safe access control for administrative capabilities.
- Keep configuration consistent with the existing file-based configuration principle.

## Rationale
Reuse a maintained scheduler with persistent jobs and retries, avoiding a bespoke scheduling engine.

## Open
Dashboard exposure and authentication design, concurrency limits, retention and retry configuration, and deployment verification remain implementation decisions subject to security review.

## History
Refines 2026-10-17-20-35-00-central-task-scheduling.
