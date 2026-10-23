# Identify downloaded audio before ingestion

Status: Approved
Date: 2026-10-23

## Context
The existing acquisition handoff implementation ingests files without first confirming identity, but the approved rejection policy requires uncertain or failed candidate identities to remain outside managed storage.

## Decision
A downloaded candidate must be identified and validated before it is ingested into managed library storage. A candidate that cannot be confidently identified is rejected for this acquisition attempt; keep the source file intact in the download area, record the reason and allow acquisition to try other candidates. Only a confidently accepted file proceeds through ingestion and durable completion.

## Boundaries
Use existing identification confidence rules; do not invent a new algorithm or assume filename matching is sufficient. Retry transient processing failures separately from identity rejection. Preserve file data and provenance.
