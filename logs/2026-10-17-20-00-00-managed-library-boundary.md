# Managed music library and import boundary

## Status
Accepted decision, discussed 2026-10-17.

## Context
MusicHub needs to build and manage its own music collection. An existing NAS collection exists, but it must remain outside MusicHub's scope. The user may manually supply files for import, including by copying them into a designated import folder or uploading through the UI.

## Decision
- MusicHub manages its own music library in a user-selected destination folder.
- MusicHub must not access or scan the user's original NAS music collection.
- Music enters MusicHub through a separate import location or a UI-based import flow.
- Imported music is ultimately stored in MusicHub's designated library folder.

## Rationale
Keep the original collection independent and out of scope. Give MusicHub a clearly bounded destination for the music it manages, with explicit user-controlled import.

## Not decided
- Import staging folder configuration and lifecycle.
- UI upload mechanisms, format validation, duplicate handling and file organization.
- Database, metadata storage, download workflows and other implementation details.

## History
Initial decision. No earlier MusicHub Understanding log superseded.
