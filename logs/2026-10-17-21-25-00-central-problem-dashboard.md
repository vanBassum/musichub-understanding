# Central problem dashboard

## Status
Accepted principle; exact dashboard layout and workflows remain open.

## Context
MusicHub can encounter uncertain identifications, contradictions with manual decisions, download or import failures, and scheduled task errors. The user wants these problems collected separately rather than dispersed across features.

## Decision
- MusicHub has a dedicated, central problem dashboard for exceptional cases requiring attention.
- It aggregates problems across subsystems, including uncertain recordings, repeated conflicts with manual identification, download/import problems and failed or stuck tasks.
- Entries should make the affected music or task, reason, severity and available follow-up actions understandable.
- Users should be able to address problems or initiate reprocessing where applicable.
- The scheduler's general task overview remains distinct: it displays planned/running task activity, whereas the problem dashboard focuses on exceptions.

## Not decided
- Specific severity taxonomy, sorting, filters, grouping, and notification rules.
- Resolution workflows, assignment, suppression, retention and audit history.
- Exact navigation and visual design.

## History
Extends central task scheduling, confidence-aware review, and manual identity conflict alerts.
