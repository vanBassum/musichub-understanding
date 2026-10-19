# Decision: track-first wishlist and edition selection in search results

Status: accepted by owner on 2026-10-19.

Context: The user clarified the selection interaction and priority for wishlist and search. Existing understanding requires an explicitly chosen album edition, but leaves open whether a second confirmation step is needed.

Decision:
- Individual tracks are the primary unit of wishlist intent, search/acquisition and quality upgrade. The user can select a single track without selecting or acquiring its album.
- When browsing album search results, different releases/editions are presented as separately identifiable, selectable results.
- Selecting an album result selects that specific edition at the same time. No subsequent mandatory edition-selection step is required.
- Adding that selected album to the wishlist expands the chosen edition into its individual tracks, applying existing per-track presence and quality rules. Do not silently substitute another edition.
- The search and wishlist experience should prioritize efficient individual-track workflows; album selection is a bulk convenience, not a prerequisite for track acquisition.

Rationale: Avoid redundant edition selection and keep the common track workflow simple.

Boundaries: This clarifies target behavior; search-result presentation details, delivery order, mock data and implementation sequencing belong to issues. Existing rules about identity certainty, quality upgrades and package acquisition remain unchanged.
