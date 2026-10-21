# Manual retry and removal of download attempts

Date: 2026-10-21
Status: Approved

## Context
The Downloads page shows failed attempts but offers no direct action. The product owner wants manual control over the download queue during this early phase. Automatic periodic recovery/cleanup was discussed but explicitly deferred.

## Decision
- The Downloads page offers **Retry** for failed download attempts, allowing a user to explicitly request another attempt through the existing download pipeline.
- The page offers **Remove** to remove a download attempt from the visible queue. Removal must not delete the corresponding wishlist entry, alter desired catalog membership, or delete already stored audio/files.
- Wishlist intent and download attempt lifecycle are independent. A wanted but missing track remains wanted after a download attempt is removed; a future separately initiated search may discover it again.
- Avoid duplicate concurrent attempts or unsafe reprocessing. Actions must clearly report failures and reflect actual persisted queue state.
- Do not introduce a new scheduled or periodic download-recovery/cleanup task as part of this change. Future automatic retries, retry policies and cleanup scheduling are separate decisions.
- Preserve existing operational diagnostics/history where applicable; removing an entry from the active queue is not authorization to erase unrelated history or evidence.

## Rationale
Simple explicit actions solve the immediate usability problem while the product owner retains control over when recovery happens.

## Open
Exact future automated recovery policy, retry limits/backoff, and retention duration for completed/failed attempts.
