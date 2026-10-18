## Context
MusicHub file ingestion (#27) needs an HTTP upload contract before implementation. The existing storage-registration decision remains in force. These decisions were explicitly accepted in the 2026-10-18 discussion.

## Accepted decisions
- Expose an initial HTTP upload API for file ingestion, without application authentication, **only within the deployment's internal network**. Public access is forbidden. Deployment/network configuration must enforce the restriction; an unauthenticated endpoint must not be publicly exposed.
- Accept any file type; do not infer music identity or perform audio-format validation during ingestion. Apply technical upload safety checks.
- Configure the maximum size per file through `FileIngestion:MaxUploadSizeBytes`, defaulting to **524288000 bytes (500 MiB)**.
- Stream the request to S3/MinIO without buffering the complete file in memory or on disk, computing SHA-256 during transfer. Support non-seekable HTTP input; the implementation may select the SDK mechanism and should test this behavior.
- `StorageLocation` initially uses the named value `default`, mapped to the existing `FileStorage` configuration.
- `Source` initially permits only `upload`; other sources require future decisions.
- The implementation pipeline may invoke `dotnet ef` to generate EF Core migrations. Generated migrations remain subject to normal PR review.

## Boundaries and trade-offs
This is an intentionally temporary internal-only unauthenticated endpoint, not permission for public unauthenticated uploads. Authentication, public exposure, additional ingestion sources, content-format restrictions, and richer upload mechanics remain future design decisions. No metadata extraction, catalog processing, deduplication or lifecycle processing is introduced by this decision.
