# MusicHub security

Security contract projected from the recorded logs. Only requirements established by accepted decisions appear here; everything else is listed under open questions.

## Trust boundaries

- **Original NAS collection:** MusicHub must not access or scan the user's original music collection. It is out of scope.
- **Managed library:** MusicHub is the sole authoritative manager of its library folder. Music enters only through the designated import location or a UI-based import flow.
- **External devices and services (phones, Google Drive, other synced copies):** they may read or copy library files. Changes made there must not automatically add to, modify or delete the authoritative library (version 1). Two-way sync is not part of version 1.
- **Imported file metadata:** embedded tags, artwork and existing artist/title values are untrusted evidence. They are search hints only and never establish identity.

## Library integrity and acceptance

- Audio whose identification confidence is below the required level must not enter the canonical library. Source files stay available for later identification in the import area or a quarantine area (placement open).
- Medium-confidence imports are allowed only with the uncertainty recorded and visible for review.
- Package downloads are validated per track. Incorrect or insufficiently identified tracks must not enter the canonical library, even when other tracks in the package are accepted.
- Identity confidence and audio quality are separate dimensions. A confidently identified existing recording must not be displaced by a less certain candidate because of better encoding quality.
- Quality upgrades and replacements must preserve the identified recording and version. They must not silently substitute a different mix, performance, remaster or user-selected album edition.
- Superseded audio files are retained, not automatically deleted, so earlier versions remain viewable and revertible.
- Content hashes identify exact file content for storage and deduplication only. They do not establish musical identity.

## Authority of user decisions

- **Wishlist:** the user alone decides what is added. MusicHub never adds artists, albums or tracks on its own. Recommendations and AI-playlist suggestions are not authorization to acquire.
- **Acquisition scope:** automatic searching and acquisition follows the explicitly selected item. A single track does not imply its album, and an artist does not imply their discography. An explicitly added album expands to its tracks, in the user-selected edition.
- **Manual identity confirmation:** it is treated as certain and takes precedence over automated identification. Automation, including autonomous recovery, must not silently overwrite it or other user-controlled decisions. Only a later user correction changes it. Repeated contradicting results raise a visible alert and do not change the identity. The manual provenance is kept separate from machine-generated confidence.

## Provenance, audit and visibility

- Identification outcomes retain provenance: the chosen candidate, supporting evidence, checks performed, confidence, and later user corrections.
- A durable history of identifications that were uncertain is kept, including for tracks already imported.
- The central problem dashboard and its retained problem history make failures, uncertain identifications, manual-identity conflicts and stuck tasks inspectable. The history includes resolved and recurring problems.
- The scheduler shows planned and running tasks, previous results and next runs. Users can trigger tasks manually.

## Configuration and secrets

- MusicHub must be fully configurable through deployment-managed files and/or environment variables, with no required UI step. A UI must not become a separate, conflicting source of configuration truth.
- Secret management is not yet decided.

## Open questions

- Authentication, user accounts, roles, authorization, multi-user or tenant separation, and who may perform wishlist, import, manual-confirmation, task-trigger or problem-resolution actions. No log establishes any of these.
- Access control and exposure of the UI and any upload endpoint, upload validation and format checks.
- Secret and credential handling, including credentials for external search, download, catalog or AI providers and Google Drive export.
- Which problems may be resolved automatically and which need explicit approval.
- Retention and cleanup of quarantined files, uncertain candidates, retained audio versions and problem history.
- Whether manual identity confirmation applies to one file, one recording or equivalent encodings.
- Whether future two-way sync is allowed, and how out-of-band edits to the managed folder are detected or handled.
