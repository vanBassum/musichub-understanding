# Approve MusicBrainz and AcoustID as identification evidence sources

Date: 2026-10-18
Status: Accepted

## Context
The identification service needs real evidence sources. MusicBrainz candidate search and AcoustID/Chromaprint fingerprint matching are proposed implementations of the existing independent evidence-provider interfaces. Both services may return multiple possible matches. The user explicitly approves their use and the corresponding third-party data exchange.

## Decision
- **MusicBrainz** is approved as an external candidate search source. MusicHub may send artist, title and relevant metadata search hints to MusicBrainz to retrieve candidate recordings and their release associations.
- **AcoustID** is approved as an external audio-fingerprint lookup source. MusicHub may compute an audio fingerprint locally (e.g. with Chromaprint) and send the fingerprint and audio duration to AcoustID. The original audio stream is not sent to AcoustID for this lookup.
- Both providers may yield **multiple candidates**, including source-specific identifiers, scores, references and provenance. Their candidates are evidence, not a final identification. Source scores must not be presented as final MusicHub confidence without resolver evaluation.
- The resolver is responsible for comparing available evidence and deciding on **at most one sufficiently supported exact-version identity, or no identity**. It must not guess when evidence is insufficient or contradictory.
- External integrations must be configurable, including enablement and any credentials. Secrets such as the AcoustID API key must be supplied through deployment-managed configuration or secrets, never committed to source control or logged. Avoid exposing credentials in request URLs or error messages.
- External lookup failures or unavailable dependencies must not be mistaken for a confirmed no-match. Use appropriate timeouts, rate limiting and bounded retries in line with provider requirements.
- The local Chromaprint/fpcalc runtime dependency is approved for fingerprint calculation. Implementation specifics and exact configuration settings remain engineering decisions.

## Rationale and trade-offs
MusicBrainz provides catalog candidates; AcoustID adds evidence based on audio itself. Both are complementary but imperfect and may not distinguish every remaster or edit. Third-party queries disclose the listed metadata or fingerprint-derived information, which is an accepted trade-off for identification. Precise version identity and honest uncertainty remain priorities.

## Relationship to prior decisions
Resolves the previously open choice of the first external catalog and fingerprint sources, associated data egress and secret-handling principle. It does not mandate these as the only future providers, alter the public identification contract, or authorize catalog writes, imports, scheduling or export behavior.
