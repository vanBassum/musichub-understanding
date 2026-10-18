# Accepted decision: standalone audio metadata reading

## Context
MusicHub needs a reusable way to inspect audio files for technical properties and embedded descriptive tags. The accepted file-ingestion decision of 2026-10-17 deliberately limits ingestion to storage and factual file registration, deferring metadata extraction to separate design. Issue #24 introduces a standalone metadata-reading service; its implementation was blocked because the capability had not been explicitly accepted in the understanding.

## Decision
**Status: accepted by the owner (2026-10-18).**

- MusicHub may read technical audio properties and embedded descriptive tags through a standalone, reusable service.
- Embedded tags are untrusted, file-provided evidence. They do not establish recording identity or catalog truth.
- This decision authorizes reading and returning metadata, not automatically running extraction as part of file ingestion, persisting results, identifying recordings, or adding processing stages/events.
- When extraction runs, how results are stored, and how metadata participates in identification or later processing remain separate design decisions.
- The implementation may use a suitable audio metadata parsing library; the particular package and API shape are implementation details subject to normal dependency and security review.

## Rationale and trade-offs
A standalone reader enables later workflows to reuse metadata extraction without coupling it prematurely to ingestion, persistence or identification. It preserves the existing distinction between physical file receipt and musical identity.

## Decision history and open questions
This complements, and does not supersede, `2026-10-17-23-59-58-file-ingestion-storage-registration.md`: ingestion itself still does not extract metadata. Open: extraction triggers, orchestration, processing/event schema, persistence, and identification behavior.
