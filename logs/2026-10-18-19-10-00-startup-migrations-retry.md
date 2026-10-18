# Automatic database migrations during API startup

Status: accepted decision (2026-10-18).

## Context

The acceptance catalog failed with HTTP 500 because a missing migration is suspected. Existing accepted decisions in `logs/2026-10-17-22-00-00-storage-configuration-contract.md` and `logs/2026-10-17-23-59-59-postgresql-health-operations.md` required a separate migration step and prohibited normal startup migrations.

## Decision

This decision supersedes those earlier rules about when database migrations run. On normal API startup, MusicHub applies pending EF Core migrations automatically, before it accepts API requests. A separate deployment migration step is not required. Migration execution must be safe under concurrent instance startup using appropriate database locking, and re-running startup without pending migrations must be safe. Keep any explicit `--migrate` command coherent with the same migration implementation.

When PostgreSQL is temporarily unreachable, retry with exponential backoff beginning at 5 seconds and capped at **60 seconds between attempts** (5, 10, 20, 40, 60, 60, ...), with up to 20% jitter. Continue retrying without a fixed attempt limit; do not retry aggressively. While waiting, readiness stays unhealthy and the API must not serve requests requiring an unmigrated schema. A deterministic schema/SQL migration failure is not transient: stop startup with a clear logged error rather than retry forever. Once migrations succeed, normal service can start.

Migrations remain additive and non-destructive. Do not claim the acceptance HTTP 500 is resolved until checked on the deployed instance.

## Rationale

Keeping the database schema aligned with the deployed application is an application startup responsibility. Bounded retries tolerate temporary database outages without aggressive reconnects, while failing on actual migration errors prevents silently serving an incompatible schema.
