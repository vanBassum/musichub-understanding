# Persist rejected acquisition candidates and defer cleanup

Status: Approved
Date: 2026-10-20

## Context
Autonomous Soulseek acquisition may download a candidate whose recording identity cannot be sufficiently verified. Such files should not be imported into the managed library, and repeat searches should not repeatedly download the same rejected candidate.

## Decision
- Download candidates to temporary disk storage outside the managed MinIO library, not RAM.
- Validate the candidate's recording identity before library import. A candidate that fails validation or is too uncertain is not imported into MinIO.
- Persist rejected-candidate records in the database, including rejection outcome and enough stable source/file identity information to avoid downloading the same rejected file again.
- Keep rejected files temporarily in the download area so they can be reconsidered; they are not part of the library.
- Plan a separate cleanup task later; do not implement or schedule automatic cleanup as part of this decision.
- Temporary retention duration and cleanup policy remain undecided. A seven-day duration was discussed as a possible future policy, not an automatic deletion mandate.

## Open
Stable candidate identity across provider listings and reuploads, retry policy when evidence improves, treatment of removed temporary files, and cleanup-task behavior.
