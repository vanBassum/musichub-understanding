# Per-track acquisition activity history

Status: Approved
Date: 2026-10-23

## Context
A single current download status cannot explain what has been attempted or why a wanted track remains missing.

## Decision
Each Wishlist track row can expand to show a persistent, chronological, user-readable activity history, with timestamps and meaningful acquisition milestones such as search started, number of results found, candidate evaluation, download started/completed, import started/completed, and errors. The collapsed row stays compact and shows status and recent activity. Errors may expose further technical detail on demand. The history remains available across application restarts and retries and must be derived from actual workflow events, never invented UI steps.

## Boundaries
Retain provenance and truthful counts; avoid secrets, sensitive filesystem paths and excessive raw log output. Exact retention policy is not yet decided.
