# Accepted decision: internal file registration listing

Date: 2026-10-18
Status: Accepted

## Decision
MusicHub provides an internal-only `GET /api/files` endpoint in the existing Files API/controller for listing factual persisted file registrations. This extends the accepted internal upload contract and upload lifecycle decisions. The listing is database-backed and ordered newest first, with deterministic tie-breaking. The standard list response exposes `Id`, `OriginalFilename`, `SizeBytes`, `Status`, and `StartedAt`. Technical `StorageKey` and `ContentHash` are not exposed in the default list response; they remain internal storage details.

The API remains internal-only, with its existing deployment/network exposure boundary; this decision does not authorize public unauthenticated access. The listing is not a music catalog, does not infer tracks, and introduces no metadata-processing lifecycle or event history.

## Rationale
The Files UI must be able to refresh the actual registrations and distinguish storage-confirmed files from incomplete or failed uploads without exposing object identifiers or hashes unnecessarily.

## Implementation implications
Extend the existing `FilesController` and `FileIngestionService` read side. Do not add a separate service or bypass PostgreSQL. The UI only treats a file as successfully stored after the API confirms `Stored`.
