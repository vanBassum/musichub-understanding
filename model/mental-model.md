# MusicHub mental model

MusicHub builds and manages its own music library from music the user explicitly wants. It identifies recordings with evidence and confidence, keeps audio quality and identity as separate concerns, and runs largely autonomously while keeping uncertainty and problems visible.

## Library, ownership and import

- MusicHub manages its own library in a user-selected destination folder. It must not access or scan the user's original NAS collection, which is out of scope. (2026-10-17-20-00)
- Music enters through a separate import location or a UI-based import flow, and ends up in the designated library folder.
- MusicHub is the authoritative manager of its library. In version 1, external devices and services may read or copy files. Changes on a phone or other synchronized copy must not automatically add to, modify or delete the authoritative library. Two-way sync is not in version 1 and may be reconsidered. (20-05)
- Open: import staging lifecycle, UI upload mechanics, whether MusicHub detects or repairs out-of-band edits to its managed folder, export/sync mechanism (including Google Drive).

## Tracks, storage and export

- One canonical stored copy exists per genuinely identical track performance/version. Distinct mixes, remixes and other genuinely different performances must not overwrite each other. (20-10)
- Albums, compilations and playlists are logical groupings or references, not reasons to duplicate audio. Physical organization is independent of artist, album or playlist membership.
- Internal physical storage uses content hashes/hashed identities rather than artist/title paths. Identical content can be deduplicated by hash. Hash equality is not musical identity: the same recording in different encodings or with different tags can hash differently, so musical duplicate detection remains the identification pipeline's responsibility. (20-25)
- MusicHub can generate a separate export with readable artist/title naming and suitable metadata for external devices such as phones; the extra storage is acceptable.
- Recording identity and release relationships are kept in the catalog independent of embedded file tags, so exports can choose different release-oriented metadata and artwork. (20-15)
- Open: exact identity matching and dedup algorithm, canonical layout and identifiers, hash algorithm and scope (whole file or normalized audio), filesystem versus S3-compatible storage, export structure and playlist format, canonical selection when two different files represent the same recording.

## Identification

- Incoming metadata is untrusted evidence. Existing artist/title may serve as search hints but do not establish identity. MusicHub aims to identify the exact recording/version of each file. (20-15)
- Prefer associating a recording with its original single release when it genuinely contains that recording, otherwise the appropriate original album release. Never substitute a different recording, mix, remaster or version just to fit the preferred release type.
- Identification is an ordered, user-configurable workflow of evidence steps that contribute to a confidence assessment of candidate identities. Costly steps (such as audio fingerprinting) can be skipped once confidence is sufficient. (20-20)
- Import policy has three bands. High confidence is imported automatically. Intermediate confidence may be imported, with the uncertainty recorded and visible for later review and correction. Very low confidence is not imported as an identified library track.
- Files below the required confidence are not admitted to the library but remain available for later identification, either in the import area or a dedicated quarantine area. (20-25)
- Identification outcomes retain provenance: chosen candidate, evidence, checks performed, confidence and later user corrections. A durable review/history view covers identifications that have been uncertain, even if imported.
- When deciding whether to accept or replace audio, the identification confidence of both the existing recording and the incoming candidate is considered. A confidently identified existing recording is not automatically displaced by a less certain candidate merely because of better encoding quality. A candidate with stronger identification evidence can be preferred for further evaluation, subject to thresholds and identity/version checks. Uncertain candidates may be retained outside the canonical library for later review. Identity confidence and audio quality are separate dimensions and must not be collapsed into one score. (21-15)
- A user's explicit manual identity confirmation is treated as 100% certain and takes precedence over automated identification, which must not silently overwrite it. Its provenance is kept separate from machine-generated confidence. If later automated results repeatedly contradict it, MusicHub raises a visible alert for review; the alert does not change the identity, and only a later user correction can. (21-20)
- Open: confidence computation and calibration (including correlated evidence), numeric thresholds (80% was only an illustration), the remaster-versus-identical-recording distinction, fingerprint caching, fingerprinting and catalog sources, what constitutes "repeated" conflict, whether manual confirmation applies to a file, a recording or equivalent encodings, review and reprocessing workflows, how rejected or low-confidence files are stored and for how long.

## Audio quality

- Configurable audio quality profiles define acceptable qualities, their preference order and an upgrade cutoff. Ranking is configurable, not hardcoded to a format or bitrate. (20-30)
- Below the cutoff, a better acceptable version of the same recording is preferred over the stored file. At or above the cutoff the track is good enough and higher qualities need not trigger replacement.
- Upgrades must preserve the identified recording/version and must not silently substitute a different mix, performance or remaster.
- When a better file becomes preferred, the previous audio file is retained, not automatically deleted. The user can view retained versions with their qualities, upgrade history and current preferred version, and can revert to an earlier one. (21-05)
- Open: default ranking and attributes, profile assignment and coexistence, whether replacement is automatic or confirmed, retention limits and cleanup, how restoring a version interacts with profiles and future upgrade searches.

## Wishlist, discovery and acquisition

- The user decides what goes on the wishlist. MusicHub does not autonomously add artists, albums or tracks to it. Once the user adds an item, MusicHub may search, download and upgrade within configured rules. (20-40)
- Users can search inside MusicHub and add results to the wishlist. MusicHub may show a Recommended list, and AI-generated playlists are expected to be a major source of suggestions, including music not in the library. Suggestions never authorize acquisition on their own unless a later decision changes that. (20-45)
- Acquisition scope follows the explicit selection. Adding an album seeks its constituent tracks; adding a track does not request its album; adding an artist does not request the whole discography. (20-50)
- When adding an album the user chooses the edition. The standard/original release is shown prominently at the top as the default suggestion, other editions remain selectable, and no different edition is silently substituted. (20-55)
- MusicHub may acquire a whole album as a package even if some tracks are already present. Each track is then evaluated separately against the canonical library and quality profile: missing tracks are imported, existing tracks are upgraded only if the new file qualifies, otherwise retained. (21-00)
- Downloaded package contents are validated per track, not all-or-nothing. Tracks meeting the acceptance rules can be imported immediately even if others fail. Incorrect or insufficiently identified tracks must not enter the canonical library, and album tracks still missing remain eligible for future searches. (21-10)
- MusicHub periodically searches for missing wanted tracks and for better versions of tracks below their cutoff. Missing tracks should normally get higher priority and/or more frequent searches than upgrades. Intervals and priorities are configurable, and one uniform cadence is not required. Tracks meeting their cutoff need not keep being searched. (20-36)
- Open: wishlist entry types and input methods, what adding an artist means (if supported), how the authoritative original release is determined, handling of ambiguous albums or missing track lists, search sources and result grouping, how AI playlists reference unavailable music (including one-click or bulk additions), recommendation ranking and source, whole-package versus single-track preference, staging and cleanup of package downloads, default intervals and backoff, scope of priority settings.

## Scheduling, problems and autonomy

- A central scheduler runs recurring tasks across workflows. Users can see planned and running tasks, previous results and next execution, and can trigger tasks manually. (20-35)
- A dedicated central problem dashboard aggregates exceptional cases needing attention: uncertain recordings, repeated conflicts with manual identification, download/import problems, and failed or stuck tasks. Entries convey the affected music or task, reason, severity and available follow-up actions, and users can address problems or trigger reprocessing. It is distinct from the scheduler's general task overview. (21-25)
- MusicHub autonomously attempts to resolve recoverable problems such as transient download or task failures. Problems may appear on the dashboard while recovery is in progress. The model distinguishes problems being recovered, those needing user action, resolved ones and recurring ones. Problem history is retained and the dashboard supports filtering by dimensions such as status, type, affected music, task, time and severity. Autonomous recovery must not override manual identity confirmations or other user-controlled decisions. (21-30)
- Open: task definitions, concurrency, retry policies and limits, cancellation, history retention, permissions, severity and status taxonomy, notification rules, suppression, which problems are safe to resolve automatically.

## Configuration

- MusicHub must be fully configurable without its UI, through deployment-managed files and/or environment variables suitable for Docker Compose. A future UI must not become an independent, conflicting source of configuration truth. Scheduling and task behavior follow the same policy. (20-11, 20-35)
- Open: configuration layout, precedence and validation, whether the UI shows read-only settings or allows any editing, secret management.
