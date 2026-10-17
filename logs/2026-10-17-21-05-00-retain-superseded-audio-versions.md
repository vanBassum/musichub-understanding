# Retain superseded audio versions

## Status
Accepted.

## Context
A quality upgrade can replace the preferred audio file for an existing recording. The user wants the previous file preserved and visible later.

## Decision
- MusicHub retains the previous audio file when a better-quality file becomes the preferred version.
- The user can later view retained versions in an overview, with their qualities, upgrade history and current preferred version.
- Retained versions allow reverting to an earlier audio file.
- MusicHub does not automatically delete superseded files under the current policy.

## Not decided
- Retention periods, storage limits and explicit cleanup controls.
- Exact overview design and metadata fields.
- How restoring a previous version interacts with quality profiles and future upgrade searches.

## History
Extends configurable quality profiles and per-track evaluation of album package downloads.
