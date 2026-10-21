# Contextual status views instead of a Problems page

Date: 2026-10-21
Status: Approved

## Context
The previously approved standalone Problems dashboard duplicates information and actions that belong in Files, Downloads, Library/wishlist and Jobs history. The product owner prefers filtering and counts in the context where the item can be acted upon.

## Decision
- Supersede the dedicated cross-subsystem Problems page/dashboard requirement. No standalone Problems navigation destination is required.
- Files supports filters and result counts for identification states, including unidentified and uncertainly identified files. Identification evidence, provenance, uncertainty and manual confirmation/conflicts remain accessible where relevant.
- Downloads supports status filters and result counts, including failed attempts, with its own download actions.
- Jobs history supports filtering and result counts for failed or stuck executions, and makes reasons, errors and diagnostic history inspectable.
- Library/wishlist supports filtering and counts for wanted or missing music.
- Each contextual view shows the total number of results matching its active filters, with accurate semantics for pagination.
- A future optional Overview page may aggregate counters and link each counter directly to its owning page with the appropriate filters applied. This is a navigation/summary convenience, not a second problem-management subsystem. Its exact counters, layout and timing are not yet approved.
- Retain underlying diagnostic, identification and job history data and existing safety constraints; removing the standalone Problems page does not mean deleting records, suppressing alerts about manual identification conflicts, or eliminating future recovery capability.
- Do not add a new periodic retry/recovery task as part of this UI decision.

## Rationale
Keep one actionable home for each domain and avoid duplicating workflows and inconsistent status across screens.

## Supersedes
Earlier understanding requiring a dedicated central Problems dashboard; domain-specific handling and retained history remain.

## Open
Precise filter taxonomies and overview counter selection; eventual automated recovery rules and scheduling.
