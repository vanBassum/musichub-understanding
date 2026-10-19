# Identification diagnostics visible in job execution details

Date: 2026-10-19
Status: Approved by product owner

## Context
A manually started catalog reconciliation job completed after examining 35 Stored files, linking none and reporting 35 unidentified. The aggregate result does not explain which identification strategies were attempted or why each file remained unresolved.

## Decision
- Each attempted file identification has one consolidated, structured diagnostic outcome, associated with the specific job execution and file. Avoid a stream of separate log messages for each evidence step.
- That outcome shows which identification methods were attempted, skipped or failed; their meaningful results and confidence/evidence where available; and the final identification decision with a comprehensible reason.
- Users can inspect these per-file outcomes from the existing Jobs page, within the relevant execution's details. Aggregate job totals remain available.
- The presentation must distinguish no match, insufficient confidence, skipped/unconfigured methods and technical failures, without suggesting that job completion implies successful identification.
- Diagnostic outcomes must not invent identification evidence or change identification decisions. Repeated job executions retain distinguishable results.
- Implementation format, storage, API structure and exact UI presentation are left to the implementation team, respecting existing architecture and retention/security conventions.

## Rationale
Enable diagnosis of unsuccessful catalog reconciliation without flooding operational logs, and make the outcome inspectable without server-log access.

## Boundaries
No changes to confidence thresholds, identification strategies, file storage, automatic scheduling or catalog semantics are approved here. Existing provenance/review requirements remain applicable.
