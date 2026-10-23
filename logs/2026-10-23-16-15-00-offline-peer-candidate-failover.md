# Candidate failover when Soulseek peers are offline

Status: Approved
Date: 2026-10-23

## Context
Soulseek search candidates can become stale before transfer. The slskd enqueue API can report an offline peer. Repeatedly retrying the same offline peer prevents acquisition even when alternative candidates may exist.

## Decision
Keep discovery and transfer as separately scheduled processes, but coordinate them as one acquisition workflow. When a candidate's peer is confirmed offline, do not repeatedly retry that same peer in the immediate attempt. Mark the source temporarily unusable, try the next eligible candidate, and if none remain, schedule a fresh search. The wanted track remains missing/eligible for future acquisition until a valid file is ingested. Track the attempted candidates and reason for failover in acquisition activity history.

## Constraints
Recognize offline-peer failures from slskd's actual error semantics, not from any HTTP 500 or 404 in isolation. Preserve candidate quality/identity constraints, idempotency, retry safety, provider rate limits and provenance. No requirement to collapse searching and downloading into a single synchronous job. Sharing zero files is a separate possible rejection concern, not proof of the observed offline error.
