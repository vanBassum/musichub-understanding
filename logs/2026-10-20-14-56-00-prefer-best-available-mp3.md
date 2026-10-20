# Prefer best available MP3, allow lower-quality fallback

Status: Approved
Date: 2026-10-20

## Context
The initial missing-music acquisition workflow is restricted to MP3 for now. The owner clarified how quality should affect autonomous result selection.

## Decision
- Prefer the highest-quality available MP3 candidate for a missing recording.
- If a higher-quality MP3 is unavailable, lower-quality MP3 is acceptable; quality alone must not prevent acquisition.
- This preference does not bypass correct recording identification or other safety checks.
- Quality profiles, minimum bitrate settings, upgrade behavior and user overrides remain future work.

## Open
Precise quality ranking when bitrates/encodings differ, how to verify reported bitrate, and the policy for replacing an existing lower-quality file.
