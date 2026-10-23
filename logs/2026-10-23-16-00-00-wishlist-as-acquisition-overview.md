# Wishlist as acquisition overview

Status: Approved
Date: 2026-10-23

## Context
The existing Downloads page only shows transfers, whereas the owner needs to see missing wanted tracks even when no source was found.

## Decision
Use the Downloads page's place in primary navigation for a Wishlist overview of wanted/missing music and its acquisition progress. Missing tracks with no available source remain visible. The overview distinguishes missing, searching, not found, downloading, importing, and available outcomes based on real persisted state, not guessed progress. Users can explicitly trigger a search again for a track. The download queue remains an underlying technical mechanism rather than the sole source of wishlist items. Reuse the catalog/library's existing track identity and wanted/availability model; do not introduce a separate duplicate wishlist catalog.

## Boundaries and open questions
Existing configured automatic searches may continue. Exact inclusion of already-available tracks in the overview was not resolved; do not assume that all available tracks must remain visible. State names are illustrative and must correspond to real lifecycle stages.
