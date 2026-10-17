# Import identification and release metadata policy

## Status
Accepted product principle; matching algorithms and thresholds remain undecided.

## Context
Imported MP3s often originate from compilation albums. Their embedded album, artwork and other metadata may reflect the compilation rather than the original track release. The user wants accurate identification with minimal manual work.

## Decision
- Treat incoming metadata as untrusted evidence, not authoritative catalog truth.
- Existing artist and title values may be used as initial search hints; they do not establish identity on their own.
- MusicHub aims to identify the exact recording or version represented by each imported audio file.
- Prefer association with the original single release when it genuinely contains that recording; otherwise prefer the appropriate original album release.
- Do not substitute a different recording, mix, remaster or version merely to satisfy the preferred release type.
- Tracks that cannot be confidently identified remain available in a separate unresolved review queue, without fabricated identification.
- Keep recording identity and release relationships in the catalog independently of embedded file tags, so exports can choose different release-oriented metadata and artwork presentations.
- Minimize manual work while prioritizing correctness.

## Rationale
Compilation-derived tags and artwork are often unsuitable for a canonical track catalog. Identifying the actual recording and its release relationships enables accurate metadata and flexible exports.

## Not decided
- Audio fingerprinting, external catalog sources, confidence thresholds and conflict resolution.
- Exact distinction and treatment of remasters versus otherwise identical recordings.
- Review queue UI, timing and user workflow.
- Export presets and selection of artwork when multiple releases exist.

## History
Builds on the canonical-track and export separation decisions.
