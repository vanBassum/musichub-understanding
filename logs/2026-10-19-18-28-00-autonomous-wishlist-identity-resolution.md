# Decision: autonomous matching first, manual review for unresolved identity

Status: accepted by owner on 2026-10-19.

Context: External wishlist selections may resemble existing catalog recordings without sufficient evidence to establish equivalence. The owner wants MusicHub to resolve such cases autonomously where reliable, with manual review as fallback.

Decision:
- On an external track wishlist selection, MusicHub first attempts autonomous evidence-based identity resolution against existing catalog recordings, including additional lookups where useful.
- If evidence establishes the same specific recording/version with sufficient confidence, reuse its catalog identity and wishlist state; never create a duplicate.
- If evidence establishes a genuinely distinct performance/version, it may have a separate catalog identity.
- If uncertainty remains after reasonable autonomous investigation, surface the candidate in a user review list for identity resolution instead of guessing, silently merging, or presenting it as confirmed.
- The review list is a fallback, not a required step for every wishlist action. Manual identity confirmation follows the existing owner-confirmation precedence and provenance rules.

Rationale: Minimize user intervention without sacrificing identity correctness.

Open: Specific evidence thresholds, retry budget and review interaction details; do not infer these from this decision.
