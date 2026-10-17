# Autonomous recovery and filterable problem history

## Status
Accepted principle; concrete recovery policies and UI details remain open.

## Context
The user wants MusicHub to operate autonomously, while keeping problems visible and allowing detailed inspection through filters. A temporary download source outage should not necessarily require manual intervention.

## Decision
- MusicHub should autonomously attempt to resolve recoverable problems, such as transient download or task failures.
- Problems may be shown on the dedicated problem dashboard even while automatic recovery is in progress; they need not be hidden until retries are exhausted.
- Distinguish problems currently being recovered, those requiring user action, resolved problems and recurring problems.
- Retain useful problem history so resolved and recurring issues remain inspectable.
- The problem dashboard supports effective filtering to investigate specific situations, including dimensions such as status, problem type, affected music, task, time and severity.
- Autonomous recovery must not override explicit manual identity confirmations or other user-controlled decisions.

## Not decided
- Retry schedules, limits, escalation and notification thresholds.
- Exact status taxonomy, dashboard filters, saved views and history retention.
- Which problems are safe to resolve automatically and which require explicit approval.

## History
Extends the central problem dashboard and scheduler decisions.
