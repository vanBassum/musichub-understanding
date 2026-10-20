# Initial acquisition uses MP3; quality profiles deferred

Status: Approved
Date: 2026-10-20

## Context
The owner reports that slskd has been added to the deployment stack (deployment connectivity and runtime remain unverified). The autonomous missing-music acquisition workflow needs an initial file-format preference without prematurely designing a full quality policy.

## Decision
- For the initial autonomous missing-music acquisition workflow, search for and download MP3 audio files.
- A configurable quality-profile system is desired later; its schema, thresholds, ranking, upgrade rules and user interface are not decided now.
- Do not assume that the initial MP3 choice defines the library's permanent format restriction or future quality strategy.

## Open
Minimum acceptable MP3 bitrate, candidate ranking, whether to retain multiple versions, and future quality profile semantics.
