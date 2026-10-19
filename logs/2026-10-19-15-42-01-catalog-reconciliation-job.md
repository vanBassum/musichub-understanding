# Catalog reconciliation from stored files

## Status
Accepted decision.

## Context
Uploaded files and catalog tracks exist as separate concepts. The first useful background job should connect stored audio to the catalog through the existing identification pipeline.

## Decision
- Provide a manually startable catalog reconciliation job as the first Hangfire job.
- It enumerates MusicHub-managed file records confirmed as Stored and not associated with a catalog track; it does not scan the original NAS collection.
- For each eligible file, use the existing identification pipeline and its confidence/evidence policy.
- When identity is sufficiently supported, associate the file with an existing matching recording or create the appropriate catalog track and associate it; avoid duplicates and preserve recording/version distinctions.
- If identification is insufficient or ambiguous, do not create a fabricated catalog identity or change the file's storage status or content. Leave the file unassociated.
- Log each attempt, outcome, reason and error with useful provenance; one file failure must not prevent processing other files.
- The job must be safe to repeat without duplicate tracks or links.
- Start manually initially; the same work may later be invoked periodically or by upload-completion events through Hangfire.

## Rationale
Make the existing Files-to-Catalog pipeline usable without prematurely introducing automatic triggers, while preserving the established conservative identification policy.

## Open
Retry/skip behavior for previously unresolved files, batch limits, concurrent-run controls and detailed operational UI are implementation choices to validate.

## History
Builds on 2026-10-17-20-15-00-import-identification-and-release-metadata, 2026-10-17-20-20-00-configurable-identification-pipeline and 2026-10-17-20-25-00-unidentified-files-and-content-addressed-storage.
