# Decision: persistent acquisition download queue

Date: 2026-10-21
Status: approved by product owner

## Context
The recurring Search for Missing Music task currently attempts slskd downloads within its own execution. Downloads can outlive a search job and repeated executions can attempt the same music again. The user wants a basic separate Downloads page to inspect current transfers and statuses.

## Decision
- MusicHub owns a durable download queue in PostgreSQL. slskd remains the transfer provider, not the source of truth for MusicHub's acquisition intent.
- Searching for missing wishlist music discovers and evaluates candidates, then enqueues eligible download requests; it does not wait for transfers to finish.
- An application service exposed through dependency injection manages queue operations, persistence and duplicate active-request prevention. A separate background worker processes queued downloads through slskd, tracks progress, recovers after restarts and hands completed files to the existing identification/import workflow.
- These are components of the existing MusicHub application, not new containers or microservices.
- A basic separate Downloads UI shows current and historical requests, track/artist, status, progress and errors. Use the existing React/shadcn UI stack.
- Job history reports search/enqueue work separately from ongoing download lifetime. A later search run must not blindly duplicate an active transfer.
- Download attempts and outcomes remain durable and inspectable across job executions and restarts. Preserve existing files and acquisition provenance.

## Boundaries and open details
Exact state-machine names, retry intervals, API shapes, scheduling and concurrency mechanisms are implementation details to define consistently across delivery issues. Do not assume user controls for pause/cancel/retry, manual candidate selection, or download priority are approved. Do not bypass identification or import safety checks. No independent configuration UI or separate service deployment.

## Delivery
Four independently reviewable issues: queue/persistence and contracts; worker/slskd integration; search decoupling and downstream import; Downloads UI. Parallel implementation may use agreed contracts or mocks; integrate in dependency order.
