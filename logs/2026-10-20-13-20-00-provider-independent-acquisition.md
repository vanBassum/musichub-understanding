# Provider-independent acquisition with slskd first

Status: Approved
Date: 2026-10-20

## Context
The initial missing-music acquisition task is manually triggered. The owner selected Soulseek through its Docker-hosted slskd client, while requiring preparation for multiple acquisition providers.

## Decision
- Separate MusicHub's search, result evaluation, download orchestration, identification and import responsibilities from provider-specific communication.
- Support interchangeable acquisition/search providers rather than coupling the workflow to Soulseek.
- Implement slskd, the Docker-hosted Soulseek client with an HTTP API, as the first provider.
- Other providers may be added later without replacing the core acquisition workflow.

## Open
Provider-specific configuration, authentication, file handoff and download limits, additional providers and search strategies.
