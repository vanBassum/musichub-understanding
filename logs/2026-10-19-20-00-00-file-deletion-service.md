# File deletion is a reusable, catalog-preserving operation

## Context and decision status
Accepted in discussion on 2026-10-19. MusicHub has accumulated failed upload registrations, and a manual deletion control is needed before a background task scheduler exists. The user explicitly scoped this decision to **files**, not catalog deletion.

## Accepted behavior
- File deletion is a dedicated, reusable domain operation, independent of a file's current lifecycle status. A central file deletion service implements it; callers do not duplicate storage/database cleanup logic.
- A manual delete action per file is available from the files/upload list, with confirmation. Files with any status may be requested for deletion, including Stored, Failed and Expired; implementation must safely coordinate in-flight uploads to avoid races or resurrection.
- Deletion removes the physical MinIO object and any associated storage remnants under the file's ownership. It must not leave orphaned objects. The deletion operation is retryable and idempotent, and must retain enough durable information to recover if MinIO or database operations fail partway through. A file is not reported as successfully deleted while owned storage remains.
- The file registration remains as a **Deleted** tombstone/status, preserving the fact that deletion was intentional. Related catalog entities remain present; deleting a file must not delete a track, artist, album or other catalog entry.
- The acquisition/download pipeline must respect deliberate deletion and must not automatically download that file again solely because the file is missing. This is distinct from failed upload or temporary storage failure.
- A future cleanup task may select failed/expired files and call the same deletion service. Scheduling, automatic cleanup and catalog deletion are explicitly out of scope for the current delivery.

## Rationale and boundaries
The catalog is authoritative; stored files are subordinate. Reusable deletion semantics avoid tying physical cleanup to a particular upload status or UI workflow. Database and MinIO lack a shared transaction, so robust retry/recovery is essential. The implementation agent may choose the service/API design, deletion-state transitions, storage cleanup and concurrency strategy consistent with these guarantees.

## Explicitly deferred
Catalog-item deletion and its cascade behavior, future scheduling and policy for automatically selecting old/failed files. Historical backups and technical logs are not asserted to be erased by file deletion; the guarantee concerns live application records/references and owned MinIO storage while retaining the deliberate-deletion tombstone.
