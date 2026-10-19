# Decision: bounded UI upload queue

Status: accepted by owner on 2026-10-19 (previously approved in issue #104).

Context: Unlimited concurrent uploads delay individual completion feedback and make cancellation and status handling harder to reason about.

Decision:
- Uploads use a FIFO bounded parallel queue, default concurrency 5, user-adjustable from 1 to 10 in the UI.
- Starting the next queued file follows release of a running slot. A changed limit affects subsequent starts; active uploads are not destroyed merely because the limit decreases.
- Each file reports its own lifecycle and reaches Stored only after its own server confirmation; out-of-order completion is supported.
- Batch cancellation aborts active uploads and prevents queued ones from starting; files already confirmed Stored remain intact.
- Per-file cancellation affects only that file. Failures release slots and do not stall the batch.
- Reuse existing upload API, records and objects; no speculative deletion or reupload.
- Focused automated tests should cover queue limits, cancellation, failure, out-of-order completion and state transitions. Vitest is approved at an exact compatible devDependency version for these tests.

Rationale: Maintain useful parallel throughput while making progress and cancellation predictable.
