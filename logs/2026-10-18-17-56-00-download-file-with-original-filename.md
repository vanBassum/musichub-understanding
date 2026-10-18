# Accepted decision: download a stored file using its original uploaded filename

Date: 2026-10-18
Status: Accepted

## Decision
MusicHub allows a user to download a successfully stored file from the managed Files collection through the existing Files API, using its file registration identifier (e.g. `GET /api/files/{id}/download`). The API retrieves the bytes from managed S3-compatible object storage through the existing storage abstraction, not from the user's original NAS and not by exposing a direct MinIO URL.

The download response uses the persisted `OriginalFilename` as the suggested filename (HTTP Content-Disposition attachment, with correct encoding for non-ASCII names). The stored object key or content hash must not become the downloaded filename. Preserve the original file bytes without transcoding or metadata changes.

Only a registration with confirmed `Stored` status can be downloaded. Missing or non-stored registrations return a suitable non-success response. The endpoint follows the same internal-only exposure boundary as the other Files API operations; no new public anonymous access is authorized. Treat the persisted original filename as untrusted when constructing response headers; prevent header injection and path traversal.

## Rationale
A file should remain retrievable as originally uploaded, with a recognizable filename, independently of how MusicHub stores it internally.

## Implementation implications
Extend the existing `FilesController` and storage abstraction as needed; stream downloads without buffering entire objects into memory. This does not imply a catalog, deduplication, transcoding, ZIP export, public share links, or changes to original source files.
