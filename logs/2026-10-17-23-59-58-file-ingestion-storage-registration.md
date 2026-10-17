# Accepted decision: file ingestion is storage and factual registration only

## Context
MusicHub receives audio files through a UI upload or by scanning a designated import folder. The owner distinguishes receipt/storage of bytes from later metadata extraction, identification and catalog processing. A file can be present without its musical identity being known. Earlier understanding called for content-addressed physical storage; this decision supersedes that **physical naming rule**, while retaining content hashing as a factual property and for potential future deduplication.

## Decision
**Status: accepted by the owner (2026-10-17).**

- **Ingestion scope:** "Import" means copying the source file into MusicHub-managed storage and recording factual information about the received file. It does **not** extract audio metadata, identify music, update catalog identities, or perform any later processing. Those activities will be designed separately, including an event-sourcing-like processing/event table. Do not add processing stages or statuses to the factual file record.
- **Source:** Both UI uploads and import-folder scans copy files to managed storage. Scanning an import folder does not require deleting or moving the original; source cleanup policy remains undecided.
- **Initial backend:** Use an S3-compatible storage interface, with MinIO as the initial provider. Other S3-compatible services should work through configuration. Filesystem and FTP backends are possible future extensions, not required now.
- **Storage abstraction:** Each file registration references a named `StorageLocation`, resolved from deployment-managed app settings. The storage backend type, endpoint, bucket/root and credentials belong to that configuration, not in the file record. `StorageKey` is a relative object key/path within the configured location; do not store a full S3 URL or backend-specific JSON in the file record.
- **Key layout:** Generate a random UUID for the stored object's name, distinct from the database primary key. Use a dedicated `library/` prefix, followed by a two-character prefix derived from the UUID, then the UUID itself, e.g. `library/5f/5f8a2c91-7b43-4c90-a831-1d23e4567890`. The key is **not** derived from the content hash. Other bucket prefixes remain available for future purposes.
- **Factual file registration:** A `Files` table uses an integer primary key `Id`, original filename, named `StorageLocation`, `StorageKey`, nullable SHA-256 `ContentHash`, and `StartedAt` timestamp. The source of ingestion may be retained as a factual property; no process state or processing history belongs here. `FinishedAt` is not required.
- **Write order:** Create the database record before streaming to S3. Stream directly to the UUID-based key while calculating the content hash. Populate `ContentHash` only after successful storage confirmation. A null hash means completion has **not been confirmed**; it does not prove that a partial object exists. Do not buffer the entire file in RAM or rename/copy objects solely to achieve hash-based naming.
- **Duplicates:** No deduplication behavior is established in this decision. Keep hash recording, but defer policy and implementation for detecting, reconciling or deleting duplicate content and for repeated import registrations. Do not silently discard duplicate uploads.
- **Future storage copies:** Multiple locations per logical file may be designed later; do not introduce an additional locations table or JSON schema preemptively.

## Rationale and trade-offs
A UUID key is available before bytes arrive, allowing one-pass streaming to S3 and SHA-256 calculation without temporary local buffering or S3 copy/rename. Storage-location indirection keeps physical deployment addresses out of file records. A factual record created before the upload permits later reconciliation of interrupted transfers. File existence and musical identification are independent. This intentionally trades immediate deduplication for a simpler ingestion boundary.

## Decision history and open questions
This supersedes earlier statements that canonical physical object names must be derived from the content hash; content hashes remain relevant for integrity and future duplicate detection. The earlier acceptance rule for *identified library tracks* is not changed: storing raw bytes under `library/` does not itself assert a validated musical identity or catalog entry.

Open: duplicate handling, incomplete upload reconciliation/cleanup, import-folder source retention/deletion, future non-S3 adapters, multiple stored copies, event/processing schema, and any transaction/retry mechanics beyond the agreed write order.
