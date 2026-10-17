# Configurable confidence-based track identification

## Status
Accepted principles; numerical thresholds and scoring methods are open.

## Context
Track identification may use multiple methods with different costs, including comparatively expensive audio fingerprinting. Some tracks can be imported with qualified uncertainty while very uncertain tracks should not be imported.

## Decision
- Track identification consists of an ordered, configurable workflow of identification/evidence steps, intended to be composable by the user.
- Steps contribute evidence toward a confidence assessment of candidate track identities.
- The workflow can conditionally skip costly steps once confidence is sufficiently high.
- Import policy distinguishes high confidence, intermediate confidence and very low confidence.
- High-confidence matches can be imported automatically.
- Intermediate-confidence matches can also be imported, but their uncertainty must be recorded and remain visible for later review and correction.
- Very low-confidence matches are not imported as identified library tracks.
- MusicHub maintains a durable review/history view of identifications that have been uncertain, even if those tracks were already imported.
- Identification outcomes should retain enough provenance to understand the candidate chosen, supporting evidence, performed checks, confidence and subsequent user corrections.

## Rationale
Minimize manual work and computational expense without concealing uncertain or potentially incorrect identifications.

## Not decided
- Exact confidence computation or calibration, including how correlated evidence is handled.
- Numeric thresholds; 80% was an illustrative example, not an agreed cutoff.
- Workflow editing UX, allowed step types and short-circuit conditions.
- What happens to low-confidence source files pending review.
- Whether fingerprints are generated only on demand or cached.

## History
Refines the earlier import identification policy and its unresolved review queue.
