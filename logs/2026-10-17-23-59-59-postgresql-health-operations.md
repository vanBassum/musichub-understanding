# Accepted decision: PostgreSQL persistence and operational health checks

## Context
MusicHub needs durable catalog persistence and operational signals for container deployment. The PostgreSQL foundation implementation in musichub issue #19 / PR #23 exposed gaps between an already accepted storage configuration decision and the current architecture/security projections. This entry clarifies and extends that decision; it does not change the library's musical identity model or the file-storage decision.

## Decision
**Status: accepted by the owner (2026-10-17).**

- **Relational persistence:** PostgreSQL is MusicHub's database for durable application/catalog data. Entity Framework Core is the chosen .NET ORM and migration mechanism.
- **Schema lifecycle:** Database migrations are run as a separate, explicit deployment/maintenance operation. Normal application startup does not apply migrations automatically.
- **Deployment configuration:** Database connection settings and credentials are supplied by deployment-managed configuration or environment variables, consistently with MusicHub's existing configuration policy. Do not commit credentials or expose them in logs, errors or health responses. This decision does not prescribe a secret manager.
- **Health monitoring:** MusicHub provides health checks suitable for Docker/container orchestration and operational monitoring. Distinguish process liveness from dependency readiness: an unavailable PostgreSQL database must be reflected in readiness, but must not by itself cause liveness to fail or prevent the process from starting.
- **Information disclosure:** Health checks expose only minimal operational status. They must not reveal credentials, connection strings, internal exception details or sensitive configuration. Any public endpoint must obey this restriction.
- **Implementation freedom:** Specific HTTP paths, response representation, health-check library, dependency timeouts and migration command syntax are implementation choices, not durable domain decisions. No authentication policy or broader exposure of application data is authorized by this entry.

## Rationale and trade-offs
PostgreSQL and EF Core establish a consistent persistence boundary and migration strategy. Explicit migrations make schema changes a controlled deployment step rather than a side effect of restarting containers. Separate liveness and readiness let infrastructure distinguish a running application from an unavailable dependency, without restart loops caused solely by database outages. Minimal health responses limit information disclosure.

## Decision history and remaining questions
The previously accepted storage configuration contract already selected PostgreSQL, EF Core, deployment-supplied configuration and separate migrations. This entry confirms those choices and explicitly establishes operational health monitoring and its disclosure boundary. Existing projections may lag behind accepted logs and should be rebuilt from the complete log history.

Authentication, endpoint access-control policy, choice of secret manager, and exact health endpoint routes remain open; this decision does not settle them.
