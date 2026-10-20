# Persist download history, not search queries or search results

Status: Approved
Date: 2026-10-20

## Context
The proposed acquisition diagram showed permanent search_queries and search_results tables. The owner clarified that search requests/results are transient and may eventually be cached, but should not be persisted now.

## Decision
- Do not create durable search-query or search-result tables for the initial acquisition workflow.
- Search requests and candidate listings are transient operational data. Future caching is a separate undecided design.
- Keep one durable download-history record per attempted/downloaded candidate, including source identity and path where available, status, full-file and audio hashes when available, rejection/acceptance outcome and reason.
- Preserve durable identification attempts and method provenance associated with download history, without introducing persistent search-result entities.
- Successfully imported files continue to use existing canonical FileRecord storage records and track links.

## Open
Specific schema and deduplication constraints; eventual search caching.
