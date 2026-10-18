# Upload verification, status details, and storage confirmation

Date: 2026-10-18
Status: Accepted
Context: MusicHub upload issues #78, #84 and #85 and implementation PRs #79, #86 and #87 were blocked because the current understanding did not establish upload verification parameters, failure details, or the criteria for confirming a successful MinIO write.

## Decision

- For UI-based file uploads, the client supplies the expected byte length and SHA-256 content digest along with the file. The server validates both against the actual streamed content. Missing, malformed, incomplete or mismatching declarations are rejected; a file must never be marked `Stored` when integrity verification fails.
- `Stored` means the server has sufficiently confirmed that the complete, correct object is durably present in MinIO. A successful storage operation plus appropriate integrity verification qualifies. If the storage client's write call throws after potentially writing the object, the server may independently inspect the object and verify its actual contents and integrity before marking it `Stored`. Mere existence is insufficient without integrity confirmation.
- The implementation may choose an efficient, reliable verification method appropriate to the object store, including reopening/streaming the stored object to compute its SHA-256 if necessary. The user delegates this technical choice to implementation and review; do not assume S3 ETag equals SHA-256.
- Upload registrations retain a concise machine-readable failure reason when unsuccessful, such as `Incomplete`, `Corrupt`, or `StorageError`, and may retain an additional safe human-readable status detail. These fields are persisted and exposed through `GET /api/files` so the UI can explain failures. Do not expose secrets, internal credentials, or unsafe exception details.
- The upload endpoint accepts the declared expected byte length and SHA-256, validates their presence and format, and provides clear HTTP outcomes: `201` only for verified stored files; `400` for invalid/missing declarations; `422` for incomplete or corrupt content, with the file identifier and machine-readable reason when available; `502` for unresolved backend storage failures. Existing size-limit rejection semantics remain in effect.
- Stale unfinished uploads can be expired safely without affecting active uploads; expired/failed records may carry a reason and status detail. Cleanup must avoid deleting valid stored files or racing active uploads.

## Rationale and boundaries

The user approved durable failure diagnostics and client/server integrity verification. An object can exist even when the write client reports an error; the important guarantee is independently verified correct content, not the mere absence of a thrown exception. The precise MinIO verification mechanism is deliberately delegated to Claude and reviewers.

This decision extends and, where needed, supersedes earlier upload contract and lifecycle decisions only on these explicitly described points. Preserve the earlier lifecycle, security, and API behavior otherwise. This log records product decisions, not delivery status.
