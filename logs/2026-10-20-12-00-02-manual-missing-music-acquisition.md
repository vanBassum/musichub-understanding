# Manually triggered missing-music acquisition

Status: Approved
Date: 2026-10-20

## Context
The owner clarified that the library's missing-music view, not an explicit wishlist, determines the scope of future search and acquisition. The acquisition workflow should initially resemble the existing manual identification job.

## Decision
- A user-triggered task searches for and attempts to acquire music missing from the catalog's available files.
- Provide a UI button to start this task manually, analogous to the existing identification trigger.
- The task is visible in the existing task/job overview, including progress and results.
- Do not automatically schedule this acquisition task in the current implementation phase.
- Design the task so scheduling may be added later without changing its core behavior.

## Relationship to previous decisions
This supersedes any assumption that automatic recurring acquisition must be implemented immediately. The general long-term intention to support configurable scheduling remains, but is not a requirement for the initial missing-music acquisition delivery.

## Open
Acquisition providers, search strategy, selection and validation rules, retry policy and permissions remain to be specified before implementation.
