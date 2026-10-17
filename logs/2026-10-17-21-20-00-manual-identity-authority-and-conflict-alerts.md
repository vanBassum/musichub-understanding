# Manual identification authority and recurring conflict alerts

## Status
Accepted.

## Context
Users can review uncertain recordings and manually confirm their identity. Automated identification may later disagree with that decision.

## Decision
- A user's explicit manual identity confirmation is treated as 100% certain and takes precedence over automated identification.
- Automated identification must not silently overwrite a manually confirmed identity.
- If subsequent identification results repeatedly contradict the manual confirmation, MusicHub should surface a visible notification or alert for review.
- Such alerts do not change the confirmed identity; only a subsequent user correction may do that.
- Preserve the provenance of manual confirmation separately from machine-generated confidence so the displayed 100% is not mistaken for independently measured algorithmic certainty.

## Not decided
- What constitutes repeated conflicting evidence and where the alert is displayed.
- Alert dismissal, recurrence and review workflow.
- Whether manual confirmation applies to one file, one recording, or multiple equivalent encodings.

## History
Refines confidence-aware candidate evaluation and review.
