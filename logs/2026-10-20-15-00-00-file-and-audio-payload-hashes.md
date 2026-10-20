# Store both full-file and metadata-independent audio hashes

Status: Approved
Date: 2026-10-20

## Context
MP3 metadata changes alter the cryptographic hash of the full file without necessarily changing its audio content. The owner approved storing both forms of identity for downloaded candidates.

## Decision
- For each downloaded candidate, including rejected files, persist a SHA-256 hash of the entire file bytes (including metadata).
- Also persist a metadata-independent hash of the MP3 audio payload, excluding ID3 and other non-audio metadata, using a deterministic, documented extraction algorithm. Record the hash algorithm/extraction version for future reproducibility.
- Use full-file hashes to recognize byte-identical files and audio-payload hashes to recognize identical encoded audio despite metadata changes.
- Neither hash alone proves musical recording identity. Acoustic fingerprints remain a distinct identification method and may recognize equivalent performances across different encodings.
- Retain hashes in durable database records even after temporary files are removed.

## Open
Precise MP3 frame/payload canonicalization, handling malformed files and other codecs, and how duplicate detection incorporates the hashes.
