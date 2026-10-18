# Identification as an independent service

Decision: MusicHub provides a standalone identification service via dependency injection. It accepts an audio file and returns a proposed identity, supporting evidence, and an unresolved outcome when identification is not justified. Identification must not write to the database, change tags, enrich metadata, or link/create catalog records. Catalog integration is deliberately deferred. The service contract must remain independent of persistence and catalog structure.

Identification methods are independent tools (file metadata, artist/title searches, audio fingerprints, and future tools). They yield candidates and evidence. Matching a recording does not imply metadata overwriting. Decisions and evidence should be inspectable for future evaluation; no fixed confidence thresholds or weighting formula are mandated now.
