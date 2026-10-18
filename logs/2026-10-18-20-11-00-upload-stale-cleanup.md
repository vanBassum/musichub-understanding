# Accepted decision: recover and expire unfinished uploads

Date: 2026-10-18
Status: Accepted

## Context
File registrations are created before an upload is finished. A browser disconnect, process crash or lost response can leave an unfinished status in the database, even when object storage may contain bytes.

## Decision
- Preserve the existing factual Files registration, created before receiving the complete upload, with its start/creation timestamp and an upload lifecycle status. Do not introduce a separate durable upload session or database table merely for the expected byte count and client SHA-256; those verification inputs can remain in request-local memory.
- The upload request may transition to Stored only after full byte-count, SHA-256 and durable-storage verification. Known upload errors are recorded as Failed when possible; unfinished uploads remain identifiable from their persisted status and creation time.
- Extend the minimal upload status vocabulary to distinguish a stale unfinished upload with `Expired`. This narrowly supersedes the exactly-four-status restriction in `2026-10-18-16-35-00-file-upload-lifecycle-status.md`; do not introduce broader processing stages or an event-sourcing history. A separately persisted `Corrupted` or `Incomplete` status is not required: these are failure reasons, not additional durable lifecycle stages.
- A future cleanup task may inspect nonterminal upload records older than one hour and resolve them. Before expiring or deleting anything, it must ensure the upload is no longer actively running and verify the object-store state, so a successful upload with a lost response is not marked failed. Inconclusive verification must not result in false Stored or unsafe deletion. Incomplete/unconfirmed stale uploads may be marked Expired and eligible temporary objects cleaned up safely.
- The one-hour threshold is a starting default for detecting stale uploads, not a guarantee that every upload finishes within one hour. Implementations must avoid racing an active large upload, e.g. with bounded upload lifetime or active-operation awareness.
- The database remains the authoritative source of the final upload status, which the frontend can retrieve after a disconnect.

## Rationale and trade-offs
This keeps temporary request verification state out of PostgreSQL, uses the existing file record for durable recovery and enables eventual cleanup without confusing upload transfer status with library processing. Cleanup scheduling and operational implementation are deferred to an implementation issue.

## Prior decision
Supersedes the four-value restriction only to add Expired; keeps the narrow upload/storage lifecycle boundary and the prohibition on unrelated processing statuses.
