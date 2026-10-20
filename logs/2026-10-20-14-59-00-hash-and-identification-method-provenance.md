# Retain file hash and method provenance for acquisition candidates

Status: Approved
Date: 2026-10-20

## Context
Rejected acquisition candidates should be eligible for later re-evaluation as identification methods improve. The owner wants to know which methods were already attempted and always retain the file hash.

## Decision
- Calculate and durably retain a cryptographic content hash for every downloaded candidate, including rejected candidates, independent of whether the temporary file remains available.
- Record every identification attempt as durable history, including the methods executed, their versions where available, evidence/results, conclusion, reason and timestamp.
- Preserve prior attempts when retrying identification; new methods or changed methods can re-evaluate a previously rejected candidate.
- When the temporary file is still present, re-identify it without redownloading.
- Use hash equality to recognize byte-identical files, but never equate identical content hash with correct recording identity. Before downloading, use available provider/source identity and rejection history; content hash can only be verified once bytes are available unless supplied by a trustworthy source.

## Open
Exact hash algorithm and schema, method-version granularity, rules for triggering re-evaluation and treatment of metadata-only source matches.
