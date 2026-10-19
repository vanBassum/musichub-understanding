# Decision: initial Jobs UI access and execution

Status: accepted by owner on 2026-10-19 (explicitly confirmed for issue #109).

Context: The Hangfire job service is internal-only, while the planned Jobs UI needs HTTP endpoints for listing execution history and manually starting catalog reconciliation. Previous Hangfire execution notes left dashboard exposure and access-control design open.

Decision:
- The initial MusicHub Jobs UI and its API endpoints for listing jobs, viewing execution details/history and manually starting catalog reconciliation are accessible without authentication or authorization, following the current app's unauthenticated Files API convention.
- Do not introduce login, accounts, API keys, role checks, auth middleware or a Hangfire dashboard as part of this feature.
- This is an explicit exception/clarification to earlier open administrative access-control questions for this limited Jobs UI surface; a broader authentication/security design remains open and is not a prerequisite for this delivery.
- Show only real implemented jobs, initially catalog reconciliation; no fake jobs or invented schedule. UI labels follow the existing English-only policy.
- Expose actual Hangfire state/history, stored summary/results and failure information, not invented per-file logs or a parallel logging store. Do not expose stack traces.
- Prevent repeat clicks and refuse concurrent duplicate starts on the server while a run is enqueued or processing.

Rationale: Deliver the agreed local/internal MusicHub workflow now without designing a broader authentication system.

Boundary: This decision does not establish a general authorization policy for other future administrative APIs.
