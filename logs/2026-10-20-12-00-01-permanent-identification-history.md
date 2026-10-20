# Identification audit history and current file-to-track link

Status: Approved
Date: 2026-10-20

## Context
The current implementation stores FileRecord.TrackId directly and temporary IdentificationOutcome rows tied to Hangfire retention. The owner wants identification attempts and decisions traceable without moving files around MinIO or deriving everyday library queries from a log.

## Decision
- Each physical file stays in its single MinIO storage location. Identification and library state are maintained in the database; no quarantine move or separate storage location is required for uncertain files.
- FileRecord continues to represent storage lifecycle and has a nullable current TrackId link to the catalog Track.
- Keep permanent identification history for a file, including each attempt, methods/evidence/candidates/results and separate applied decisions and their provenance, including manual corrections. An attempt is not itself necessarily an applied decision.
- A successful identification or manual correction writes the audit event and updates the current FileRecord.TrackId atomically in one database transaction.
- Attempts are associated by FileId and chronological order; explicit previous-attempt pointers are unnecessary.
- Manual confirmation must never be silently overwritten by automated identification. Unidentified stored files retain FileStatus.Stored with TrackId null and remain eligible for later review/re-identification.
- Identification history must not be pruned merely because a Hangfire job's retention expires. Storage status is distinct from identification outcome and catalog availability.

## Supersedes
Prior proposals to move low-confidence files to a quarantine area; retention of identification outcomes only for the lifetime of a Hangfire execution.

## Not decided
Exact event/attempt schema and retention on explicit file deletion, confidence thresholds, reprocessing UI and conflict-alert rules.
