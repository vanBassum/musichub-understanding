# File deletion removes the file record

Decision: The Files area represents received/uploaded physical files, not catalog entities. When a user deletes a file, delete its physical object from object storage and remove its `FileRecord` from the database. The file must disappear from the files list; no `Deleted` file status or persistent file tombstone remains.

Catalog deletion is a separate future concern. Catalog entries may have their own deleted state or lifecycle, but this must not be represented by a `FileRecord` tombstone. The catalog import pipeline does not exist yet, so this file-deletion operation currently has no catalog changes to make.

The file deletion operation remains centralized and reusable, safe for retries and concurrent requests. Avoid reporting successful deletion while the physical object remains; handle partial failures without leaving misleading visible Deleted records. This decision supersedes the earlier file-deletion tombstone requirement in the accepted file-deletion service log; other unaffected service and UI requirements remain in force.
