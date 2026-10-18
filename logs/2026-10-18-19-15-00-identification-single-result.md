# Identification service returns one identity or none

Date: 2026-10-18
Status: Accepted

## Context
MusicHub has an independent identification service with evidence providers and interchangeable rule-based/AI resolver strategies. The user wants a simple functional boundary rather than exposing the internal candidate search and decision process to callers. Import, catalog persistence and scheduling are separate future concerns.

## Decision
- A caller supplies audio to the identification service.
- The service independently gathers evidence and resolves it to **at most one** identified recording identity.
- When it cannot establish a sufficiently reliable identity, returning **no identity** is a valid and expected outcome. It must not force a guess.
- Candidate comparisons, alternative candidates, evidence collection and resolver decisions remain internal responsibilities; the caller is not required to choose among candidates.
- This is a functional contract, not a prescribed method signature, nullability representation or error-handling implementation. Technical design is left to the implementation.
- Future UI controls may influence identification internally without changing the principle of a single-or-no-identity outcome.

## Rationale and boundaries
The caller should not need to orchestrate identification or decide which candidate is correct. Reliability takes precedence over always returning a match. This decision does not authorize automatic library import, persistence, scheduler tasks or user-facing review workflows.

## Relationship to prior decisions
Clarifies the existing identification workflow and confidence-band decisions: uncertainty and evidence provenance remain meaningful internally, while the service's primary functional result is one identity or no identity. It does not resolve confidence thresholds or the technical representation of diagnostics and errors.
