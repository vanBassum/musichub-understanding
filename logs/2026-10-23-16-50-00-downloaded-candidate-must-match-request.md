# Acquired file must match requested track

Status: Approved
Date: 2026-10-23

## Context
Soulseek candidates can contain the wrong recording even when their filenames look plausible. Automatically importing unrelated confident matches would not satisfy the user's intended acquisition.

## Decision
Accept a downloaded file for a wanted track only when its confident identity matches the intended track and its specific recording/version (e.g. live, remix, remaster as distinct track identities). A confidently identified different track is not silently imported as a substitute. Reject that candidate for the request, preserve the downloaded source file and record the mismatch so another candidate can be tried.

## Open detail
Exact evidence/scoring for version-specific recording matching remains an implementation/design gap. Do not pretend an identifier lacking version evidence can prove a version match. Use existing approved matching evidence and fail safely when insufficient.
