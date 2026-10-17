# File-based configuration as the authoritative configuration interface

## Status
Accepted principle; UI configuration behavior remains open.

## Context
MusicHub is deployed as a containerized service. The user's stack and service configuration is managed externally through files and automation, rather than through manual UI setup.

## Decision
- MusicHub must be fully configurable without using its UI.
- Configuration must be expressible through deployment-managed configuration files and/or environment variables, suitable for Docker Compose.
- A future UI, if provided, must not become an independent conflicting source of configuration truth.

## Rationale
Enable repeatable, externally managed deployment and configuration with no required manual UI steps.

## Not decided
- Precise .NET configuration layout (for example appsettings.json), precedence and validation.
- Whether the UI exposes read-only settings or supports any editing.
- Exact settings, storage backend options, and secret management.

## History
Initial configuration policy decision.
