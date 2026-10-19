# Decision: reuse one catalog identity per specific recording/version when wishlisting

Status: accepted by owner on 2026-10-19.

Context: When an external search result is added to the wishlist, an equivalent recording may already exist in the catalog. The owner confirmed that a specific performance/version is one catalog track, not one track per discovery source or wishlist action.

Decision:
- Each specifically identified recording/performance/version has one logical catalog track identity. External search results and local files referring to that same recording reuse that identity.
- Adding an already known recording to the wishlist changes or preserves the wanted state of its existing catalog track; it never creates a second catalog track or duplicate wishlist entry.
- Different performances, mixes or versions remain separate identities when they genuinely differ.
- Artist/title similarity alone is not sufficient to merge two identities. If evidence is inconclusive, do not silently merge or claim equivalence; preserve the uncertainty for resolution under the identification rules.
- Multiple audio encodings/files and release memberships may reference one catalog recording without multiplying its logical identity.

Rationale: Maintain a coherent single music catalog with idempotent wishlist actions and no accidental identity merges.

Boundary: Exact matching algorithm, uncertain-result workflow and implementation sequencing remain unresolved technical/product details and must not be inferred from this decision.
