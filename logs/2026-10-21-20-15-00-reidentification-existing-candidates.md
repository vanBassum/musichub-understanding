# Re-identification reuses the identification decision workflow

Date: 2026-10-21
Status: Approved

## Context
Catalog reconciliation normally considers Stored files without track links. An explicit full re-identification run must also consider already linked files. A review of implementation PR vanBassum/musichub#184 identified that this behavior was not yet established in the projections.

## Decision
- Default reconciliation continues to process eligible Stored files without a catalog-track link. A user may explicitly request full re-identification, including linked Stored files.
- Re-identification uses the same evidence-based candidate evaluation and decision workflow as initial identification, not a separate Confirmed/Differs decision mechanism.
- An existing automatic track association participates as a candidate alongside newly discovered candidates, with its existing decision evidence/provenance; mere existence of the link is not independent proof of identity.
- The decision engine may automatically replace a previously automatic association only when another candidate has sufficiently stronger identification evidence under the established confidence policy. Otherwise the existing association remains. A re-run must not leave a previously linked file unlinked merely because new evidence is inconclusive.
- Explicit user-confirmed identity remains authoritative and cannot be silently changed by automation. Contradictory evidence is recorded and handled according to the existing manual-confirmation alert contract.
- Persist attempts, candidate evidence, decisions and association changes with provenance, retaining historical decisions. Do not delete the audio object or historical identity evidence as a consequence of re-identification.
- This decision does not introduce new confidence thresholds, an independent conflict state machine, or a new review UI.

## Rationale and trade-offs
This permits autonomous correction of machine-made mistakes while preserving manual authority and avoiding competing decision paths. Existing associations remain eligible for comparison, but do not gain circular confidence simply by having been chosen previously.

## Acceptance
Approved in discussion on 2026-10-21. This clarifies the earlier reconciliation scope and identification/manual-confirmation guarantees; all other open questions remain open.
