# Accepted decision: verify uploaded bytes against frontend SHA-256

Date: 2026-10-18
Status: Accepted

## Context
The upload endpoint can report a failure even when the full object reached MinIO. We need to distinguish a complete upload from partial or corrupted transfers and from a lost HTTP response.

## Decision
- Before transmitting audio bytes, the frontend computes the file's SHA-256 digest and knows its byte length. It sends the expected SHA-256 and expected byte length as part of the upload request, before the audio stream.
- During that request the API counts bytes actually read and computes SHA-256 over the incoming bytes while streaming. Expected values and intermediate verification state may remain in request-local RAM; they need not be written to the database in advance.
- The API accepts the received content as complete and intact only if the actual byte count equals the expected byte count and the computed digest equals the frontend-provided digest. A short transfer is incomplete; a complete-length transfer with a mismatched digest is invalid/corrupt. Neither may be marked Stored.
- Integrity of bytes received by the API is distinct from proof of durable object storage. Set Stored only after the fully verified content is confirmed in object storage. If the initial storage call throws after the bytes have been received, a subsequent definitive object-store verification may count as storage confirmation, including checking the expected object identity and length and, where necessary, its content digest. Existence alone or an unverified partial object is not enough.
- The frontend's failure to receive an HTTP success response does not invalidate a successfully verified and stored file. It can retrieve the authoritative persisted file status later.

## Rationale and trade-offs
Precomputed SHA-256 plus exact byte count protects against truncated transfers and accidental corruption without buffering the full upload on the API. The frontend must read the file once before upload; show that as preparation progress where useful. SHA-256 establishes agreement between frontend and API, not by itself durable storage or malicious-client trust.

## Prior decision
Refines `2026-10-18-16-35-00-file-upload-lifecycle-status.md`: 'storage backend confirms the write' includes a conclusive post-error verification, not only a successful original PUT response. It does not authorize identification or catalog processing stages.
