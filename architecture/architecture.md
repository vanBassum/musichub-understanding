# MusicHub architecture

Durable technical boundaries projected from the decision logs. Items under "Open" are explicitly undecided.

## Library and import boundary
- MusicHub manages its own library in a user-selected destination folder and is its authoritative owner.
- The user's original NAS collection is out of scope; MusicHub must not access or scan it.
- Music enters only through a separate import location or a UI-based import flow, and ends up in the managed library.
- Version 1: external devices and services may read or copy library files, but changes in synchronized copies must never automatically add, modify or delete files in the library. Two-way sync is out of scope for v1.

## Storage
- One canonical stored copy per genuinely identical track performance/version; distinct mixes, remixes and performances never overwrite each other.
- Physical storage is independent of artist, album, compilation and playlist membership; those are logical groupings/references over the canonical audio.
- Internal file storage is content-addressed (hash-based identity, not artist/title paths). Identical content is deduplicated by hash.
- Content-hash equality is not musical identity; musical duplicate detection belongs to the identification pipeline.
- Recording identity and release relationships live in the catalog, independent of embedded file tags.
- Superseded audio versions are retained (not auto-deleted), with quality and upgrade history and the ability to revert to a prior file.
- A separate generated export (readable artist/title names, suitable metadata and release-oriented artwork) serves external devices such as phones; extra storage use is acceptable.

## Configuration and deployment
- MusicHub is a containerized service, fully configurable without its UI through deployment-managed files and/or environment variables (Docker Compose friendly).
- Any UI must not become a separate, conflicting source of configuration truth.
- Scheduling, task behavior, quality profiles, search intervals/priorities and identification workflow are configurable under this policy.

## Delivery pipeline and UI stack
- Pull requests are validated by GitHub Actions (compile/build and lint); failing required checks block merging to main. CI failures are addressed from CI results; implementation agents do not run local builds or test suites.
- After merge to main, the deployable Docker image is built and deployed to acceptation. This post-merge image build is distinct from PR validation; Docker image builds are not duplicated in PR validation.
- The UI is built with React, shadcn/ui components and Tailwind styling; other dependencies require explicit owner approval. The UI is English-only (no i18n framework). Visual layout is provisional and replaceable, not an architectural constraint.
- Whether the current CI workflow already implements this policy is unverified.

## Identification pipeline
- Incoming metadata is untrusted evidence; artist/title serve only as search hints.
- An ordered, user-composable, configurable workflow of evidence steps yields confidence for candidate identities; costly steps (e.g. fingerprinting) may be skipped once confidence is sufficient.
- Confidence bands: high imports automatically; intermediate imports with recorded, visible uncertainty; very low is not imported as an identified library track.
- Below-threshold files stay outside the managed library (import area or a dedicated quarantine; placement undecided) and remain available for later identification.
- Outcomes keep provenance: chosen candidate, evidence, checks performed, confidence, and user corrections. A durable history of uncertain identifications is maintained.
- A manual identity confirmation is treated as certain, stored with provenance distinct from machine confidence, and is never overwritten by automation; repeated contradicting results raise an alert only.
- Identity confidence and audio quality are separate dimensions. A confidently identified existing recording is not displaced by a less certain candidate merely for better encoding. Uncertain candidates may be retained outside the canonical library for review.

## Acquisition and upgrade
- Only user-wishlisted items trigger automatic search/acquisition; discovery, recommendations and AI playlists are suggestions and never authorize acquisition.
- Scope follows the explicit selection: an album (with a user-chosen edition, never silently substituted) expands to its tracks; a track or artist does not expand further.
- Complete album packages may be acquired even when partly present; contents are validated and evaluated per track (not all-or-nothing). Validated missing tracks are imported, qualifying upgrades replace existing ones, failures stay out of the canonical library, and still-missing tracks remain eligible for future searches.
- Configurable audio quality profiles (acceptable qualities, order, cutoff) drive upgrades; upgrades must preserve the identified recording/version. Tracks at cutoff need no upgrade searches.
- Missing tracks get higher search priority/frequency than quality upgrades; intervals and priorities are configurable.

## Scheduling and problem handling
- A central scheduler runs recurring tasks across workflows, exposing planned/running tasks, previous results and next run, with manual triggering.
- A central problem dashboard aggregates exceptions across subsystems (uncertain identifications, manual-identity conflicts, download/import failures, failed or stuck tasks), distinct from the scheduler's task overview.
- MusicHub autonomously retries recoverable problems; problems may be visible during recovery. Status distinguishes recovering, needs user action, resolved and recurring; history is retained and filterable (status, type, music, task, time, severity).
- Autonomous recovery must not override manual identity confirmations or other user decisions.

## Open
- Filesystem vs S3-compatible storage (e.g. MinIO); hash algorithm and scope; canonical layout.
- Quarantine vs import-area retention and lifecycle; staging/cleanup of package downloads.
- Export mechanism (including Google Drive), structure and playlist format; future two-way sync.
- Confidence computation and thresholds; fingerprint caching; search sources and rate limiting.
- Scheduler implementation, concurrency, retry policies, retention; configuration layout and precedence; secrets.
- Retention limits for retained versions and uncertain candidates; replacement policy when both are uncertain.
