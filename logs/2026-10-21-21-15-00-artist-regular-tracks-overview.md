# Artist overview prioritizes regular songs rather than alternative versions

Date: 2026-10-21
Status: Approved

## Context
In the artist overview, search results currently contain disproportionately many live recordings, remixes and special versions, making the artist's ordinary songs hard to find. The present external metadata integration does not provide reliable popularity/ranking data. The product owner wants a track overview, not an album-grid overview.

## Decision
- An artist overview primarily lists **individual songs/tracks**, including both tracks released as singles and ordinary tracks from studio albums. Do not make full albums the primary units of this overview.
- By default, prioritize ordinary studio versions. Hide identifiable live recordings, remixes, demos and other clearly alternative/special versions from the default list; make them discoverable through an explicit **Show all versions** control.
- While reliable popularity data is unavailable, sort the default track list **alphabetically**. Do not fabricate popularity or imply that alphabetical order is a popularity ranking.
- Keep album and single release associations as contextual track information when available, without duplicating an album as an overview item.
- Do not infer that a remaster is necessarily the same recording, or silently merge versions with ambiguous identity. Remaster grouping, deduplication across single/album appearances and ambiguous classification are **not yet decided**; preserve existing recording identity safeguards.
- If source metadata is insufficient to classify a version confidently, avoid pretending that the classification is certain. Preserve discoverability and do not delete catalog records.
- This is a presentation/search-results decision, not a change to import, canonical recording identity, release selection or acquisition rules.

## Rationale
Users should see recognizable songs first rather than pages dominated by alternative performances. An alphabetical list is predictable and honest in the absence of a reliable popularity signal.

## Open
Exact heuristics/metadata fields for version classification, how to display ambiguous versions, future popularity data source, remaster grouping and duplicate handling.
