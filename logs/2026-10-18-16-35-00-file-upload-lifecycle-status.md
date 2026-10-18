# Accepted decision: upload lifecycle on file registration

Date: 2026-10-18
Status: Accepted
Context: MusicHub issue vanBassum/musichub#38, following completed ingestion issue #27.

## Decision
This decision refines and narrowly supersedes the prohibition on processing statuses in `2026-10-17-23-59-58-file-ingestion-storage-registration.md` **only for the upload/storage lifecycle**.

The factual `Files` registration may persist a minimal `Status` with exactly four values: `Pending`, `Uploading`, `Stored`, and `Failed`. It may also persist nullable `SizeBytes`, representing bytes actually streamed and confirmed stored.

`FileIngestionService` owns these status transitions. Create the record before ingestion, mark it `Uploading` while streaming, and set `Stored` only after the storage backend confirms the write. Persist `ContentHash` and `SizeBytes` only after that confirmation. For handled failures, persist `Failed` when possible. Cancellation or process termination may leave `Pending` or `Uploading`; neither implies successful storage.

The existing `FileStorageService` remains responsible only for object storage operations. This decision does **not** authorize metadata extraction state, identification state, catalog or track processing state, `CompletedAt`, an event log, or event sourcing. The earlier prohibition on processing stages and histories remains in force outside this narrowly defined upload lifecycle.

## Rationale and tradeoffs
A persisted upload lifecycle lets the UI distinguish incomplete and failed transfers from storage-confirmed files without mistaking transfer progress for durable storage. Four states and an optional byte count are sufficient for this purpose; a broader processing workflow or event history would add complexity and mix unrelated responsibilities into the factual Files record.

## Implementation implications
Issue #38 extends the existing ingestion service and Files registration, not a new processing service. Existing records require conservative migration semantics: only confirmed stored objects should appear as `Stored`; a nullable hash alone is not proof of an incomplete object.
