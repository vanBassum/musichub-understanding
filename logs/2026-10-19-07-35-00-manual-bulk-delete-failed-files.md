# Manual bulk deletion of failed files

Users may manually delete all Failed file registrations in the Files interface in one action, after an explicit confirmation that the operation is irreversible. This is not automatic or scheduled cleanup.

At execution time, the API selects Failed files and rechecks each file's status under its deletion lock. Files no longer Failed or currently uploading are skipped and kept. Eligible files are removed using the shared FileDeletionService: delete the physical object and then remove its FileRecord, without a Deleted tombstone. Catalog tracks, artists, and albums are unaffected.

One file's deletion failure does not stop the remaining files. The operation reports deleted, skipped, and failed results. The Files UI refreshes afterward; failures remain visible for individual retry. The bulk action is unavailable if there are no Failed files or while it is running.
