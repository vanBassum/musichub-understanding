# MusicHub features

Catalogue of capabilities established in the logs. Items under "Open" are explicitly undecided and must not be assumed.

## 1. Managed library and import

**Purpose:** MusicHub builds and manages its own music collection, independent of the user's original NAS collection.

- MusicHub manages its library in a user-selected destination folder.
- MusicHub must not access or scan the user's original NAS collection.
- Music enters only through a separate import location (e.g. a designated import folder) or a UI-based import flow; imported music ends up in the library folder.
- MusicHub is the authoritative owner of the library. In version 1 (provisional), external devices/services may read or copy library files, but changes on a phone or synchronized copy must not automatically add, modify or delete library files. Two-way synchronization is not part of version 1.
- Open: import staging folder lifecycle, UI upload mechanics, format validation, duplicate handling, one-way sync/Google Drive integration, detection/repair of out-of-band edits, future two-way sync.

## 2. Canonical track storage and export

- One canonical stored copy per genuinely identical track performance/version; distinct mixes, remixes and other different performances never overwrite each other.
- Physical storage is independent of artist/album/compilation/playlist membership; those groupings are logical references and do not duplicate audio.
- Canonical internal storage uses content hashes/hashed identities, not artist/title paths. Identical file content may be deduplicated by hash. Hash equality is not musical identity; musical duplicate detection belongs to identification.
- MusicHub can generate a separate export with readable artist/title naming and suitable metadata for external devices such as phones. Extra storage use for exports is acceptable. Export metadata/artwork may differ from embedded tags, because recording identity and release relationships are kept in the catalog.
- Open: layout/identifiers, hash algorithm and scope, export structure, sync mechanism, playlist format, filesystem vs S3-compatible storage, selection of artwork among multiple releases, export presets, canonical choice between two different files of the same recording.

## 3. Configuration

- MusicHub must be fully configurable without its UI, via deployment-managed configuration files and/or environment variables (suitable for Docker Compose).
- Any UI must not become an independent, conflicting source of configuration truth.
- Scheduling and task behavior is configurable in the same way.
- Open: configuration layout, precedence, validation, whether the UI shows read-only or editable settings, secrets.

## 4. Track identification

**Purpose:** Identify the exact recording/version of each imported or acquired audio file with minimal manual work, prioritizing correctness.

- Incoming metadata is untrusted evidence; existing artist/title may only serve as search hints.
- Prefer association with the original single release if it genuinely contains the recording, otherwise the appropriate original album release. Never substitute a different recording, mix, remaster or version to satisfy release preference.
- Identification is an ordered, user-configurable workflow of evidence steps contributing to a confidence assessment of candidate identities; costly steps (e.g. fingerprinting) can be skipped once confidence is sufficient.
- Confidence tiers: high → imported automatically; intermediate → imported with recorded, visible uncertainty for later review/correction; very low → not imported as an identified library track.
- Files below the required confidence are not imported into the library; they remain available for later identification in the import area or a quarantine area (placement undecided).
- A durable review/history view lists identifications that have been uncertain, even if already imported. Outcomes retain provenance (chosen candidate, evidence, checks, confidence, user corrections).
- **Manual confirmation:** a user's explicit confirmation counts as 100% certain and overrides automated identification, which must not silently overwrite it. Its provenance is stored separately from machine confidence. If later automated results repeatedly contradict it, a visible alert is raised; the alert does not change the identity, only a user correction does.
- **Existing vs incoming:** identification confidence of both existing and incoming audio is compared; a confidently identified existing recording is not displaced by a less certain candidate merely for better encoding. A candidate with stronger identification evidence may be preferred for further evaluation, subject to thresholds and identity/version checks. Identity confidence and audio quality are separate dimensions. Uncertain candidates may be retained outside the canonical library and shown in a review overview.
- Open: confidence computation/calibration and numeric thresholds (80% was only illustrative), step types and workflow editing UX, remaster vs identical-recording treatment, review queue UI and reprocessing, fingerprint caching, what counts as repeated conflict and where alerts appear, scope of manual confirmation (file/recording/encodings), rules when both are uncertain, retention/cleanup of uncertain candidates.

## 5. Audio quality profiles and upgrades

- Configurable quality profiles define acceptable qualities, their preference order, and an upgrade cutoff. No universal format/bitrate ranking is hardcoded.
- Below the cutoff, MusicHub prefers replacing a file with a better acceptable version of the same recording; at or above the cutoff the track is good enough and need not be upgraded.
- Upgrades must preserve the identified recording/version.
- **Retained versions:** a superseded file is retained, not automatically deleted. The user can view retained versions with their qualities, upgrade history and the current preferred version, and can revert to an earlier file.
- Open: quality attributes/default ranking, profile assignment and coexistence, automatic vs confirmed replacement, retention limits/cleanup, interaction of reverting with profiles and future upgrade searches.

## 6. Wishlist, search and recommendations

- The user decides what is on the wishlist; MusicHub never autonomously adds artists, albums or tracks to it.
- Users search within MusicHub and add chosen results to the wishlist.
- MusicHub may show a Recommended list; suggestions are never automatically added. AI-generated playlists are expected to be a major source of suggestions, including music not yet in the library.
- For items on the wishlist, MusicHub may automatically search, download and upgrade quality within configured rules.
- Scope follows the explicit selection: adding an album resolves its track list and seeks its tracks; adding a track does not request its album; adding an artist does not request the discography.
- When adding an album the user chooses the edition/release. The standard/original release is shown prominently at the top as the default suggestion; other editions are selectable; MusicHub never silently substitutes another edition.
- Open: search sources and result grouping, AI playlist handling of unavailable music and one-click/bulk wishlist adds, recommendation ranking/source, what adding an artist means (if supported), identifying the original release among regional/format editions, ambiguous or missing track listings, whether a default edition needs confirmation.

## 7. Acquisition and album import

- MusicHub periodically searches for missing wanted tracks and for better versions of tracks below their quality cutoff. Missing tracks get higher priority and/or more frequent searches than upgrades. Intervals and priorities are configurable; tracks at cutoff need no further upgrade searches.
- A complete album may be acquired as a package even if some tracks are already present. Each track is then evaluated separately against the canonical library and quality profile: missing tracks are imported; existing tracks are upgraded only if the new file is preferred under the profile and cutoff, otherwise retained. Identity and the chosen edition are respected.
- Package contents are validated per track, not all-or-nothing: tracks meeting acceptance rules are imported immediately even if others fail; incorrect or insufficiently identified tracks never enter the canonical library; tracks still missing remain eligible for future searches.
- Open: default intervals/backoff and scope of settings, provider/rate-limit influence, package vs single-track preference, quality/integrity comparison, staging/cleanup of packages, whether rejected files stay in staging/quarantine, review/reprocessing controls, presentation of partial album completeness.

## 8. Central task scheduler

- A central scheduler runs recurring tasks across workflows (e.g. searching for missing tracks, quality upgrades).
- Users can see planned and running tasks, previous results and next scheduled run, and can trigger a task manually in addition to its schedule.
- Open: task definitions, concurrency, retries, cancellation, logs/history retention, permissions, UI layout/editing, schedule expression format.

## 9. Problem dashboard and autonomous recovery

- A dedicated central dashboard gathers exceptional cases needing attention across subsystems: uncertain recordings, repeated conflicts with manual identification, download/import problems, failed or stuck tasks. It is distinct from the scheduler's general task overview.
- Entries make the affected music or task, reason, severity and available follow-up actions clear; users can address problems or start reprocessing where applicable.
- MusicHub autonomously tries to resolve recoverable problems (e.g. transient download/task failures). Problems may appear while recovery is in progress. The dashboard distinguishes problems being recovered, needing user action, resolved, and recurring.
- Problem history is retained so resolved and recurring issues stay inspectable, with effective filtering (e.g. status, type, affected music, task, time, severity).
- Autonomous recovery must not override manual identity confirmations or other user-controlled decisions.
- Open: severity/status taxonomy, sorting/grouping/saved views, notification rules, retry schedules/limits/escalation, which problems are safe to auto-resolve, suppression/audit/retention, navigation and visual design.

## 10. User interface

- The UI is English only; no multilingual or internationalization support is required.
- The initial UI is a replaceable prototype: a library view with a filter sidebar, a track table and a selected-track details panel, using mock data (no backend integration). Selecting a track shows its details. Controls and filters that are not yet functional are shown as visibly disabled placeholders, not as deceptive interactive elements. This layout is provisional and future redesigns are permitted.
- Open: production visual design, real library data integration, search/filter behavior, playback, broader navigation.
