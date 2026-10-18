# Correction: delivery pipeline statements are not MusicHub architecture

Date: 2026-10-18
Status: Accepted

## Context
The current architecture projection contains a section titled "Delivery pipeline and UI stack". Its first two bullets describe GitHub Actions PR validation, whether agents run builds and tests, merge blocking, and post-merge image building and deployment to acceptation. Its final sentence says that implementation of the CI policy is unverified. These statements were previously recorded as architecture understanding but concern the development and delivery process, not the intended MusicHub system.

## Correction
Withdraw those delivery-process statements as MusicHub architecture decisions. In particular, no MusicHub understanding contract specifies whether implementation agents run local builds or tests, how PR checks or merges operate, or when CI builds or deploys an image. The statement about CI verification is also withdrawn.

This correction does **not** withdraw the product's containerized deployment/configuration requirements, nor the React, shadcn/ui, Tailwind, UI language, dependency-approval and provisional-layout decisions currently grouped alongside the delivery statements. Those remain unchanged.

## Rationale
The withdrawn statements describe the tooling and process used to deliver MusicHub, rather than properties or guarantees of MusicHub itself. Their presence wrongly makes a change in automation appear to require a product-architecture decision.

## History
Supersedes only the delivery-process portions of the earlier decisions reflected in `architecture/architecture.md` under "Delivery pipeline and UI stack". No projection is edited by this log.
