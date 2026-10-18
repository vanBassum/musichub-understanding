# Bulk deletion of failed files

The Files UI provides an explicit **Delete all failed files** action for technical file registrations in `Failed` status. The user must confirm before the irreversible bulk operation. The button is unavailable when there are no failed files or a deletion is in progress.

The server determines eligible `Failed` records when the operation runs and rechecks status under each file's deletion lock. Files no longer `Failed`, or currently being uploaded, must not be removed by this action. For eligible files, reuse the central FileDeletionService to delete the physical object and remove the FileRecord entirely from the database, without a Deleted tombstone. This does not delete or change catalog entities.

Failures are isolated: one failed removal does not stop other removals. The UI refreshes and reports deleted, skipped and failed counts; failed deletions remain visible/retryable. This is a bulk operation over failed file registrations, not a general-purpose bulk catalog deletion.
