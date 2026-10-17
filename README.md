# MusicHub Understanding

This repository captures durable MusicHub understanding through append-only logs and independent projections. Product decisions are recorded in append-only logs; consult `logs/` and the current projections for the latest understanding.

## Start here

AI assistants should read this README and the relevant current projections before discussing or implementing changes. Treat implementation as evidence, not as a source of unquestioned product truth. Discuss uncertainties with the user, then add a new immutable log file to the current session branch. Do not commit discussion logs directly to `main`. Never manually edit projections to record decisions.

A new conversation can begin: `Read the README of vanBassum/musichub-understanding. I want to discuss ...`

## Knowledge loop

Discussion / observation / code evidence → append-only log → independent projections → implementation and review → questions → discussion.

`logs/` holds immutable, timestamped decision and observation entries. The five projections are `model/mental-model.md` (domain semantics), `features/features.md` (approved behavior), `architecture/architecture.md` (durable technical boundaries), `design/design.md` (durable UX and visual rules), and `security/security.md` (security guarantees and trust boundaries). Each projector reads the complete shared log history and edits only its owned directory.


## Recording decisions

Discuss first, record second. A decision log should capture context and trigger, decision and acceptance status, rationale and trade-offs, and relevant decision history. Never invent rationale or promote brainstorming to an accepted contract. Add one coherent item per new `logs/YYYY-MM-DD-HH-MM-SS-description.md`; never edit or delete merged logs. Later decisions supersede earlier ones through new logs. Preserve unresolved questions explicitly.

## Understanding versus delivery

Projections describe the intended target system, not phases, milestones, implementation status or backlog items. Delivery planning belongs in implementation issues. Reviewers should flag significant new or contradictory capabilities, concepts, architecture, design and security requirements that lack supporting understanding, not incidental implementation details.

## Discussion sessions and batching

For an ongoing discussion, create or reuse one dedicated working branch, such as `understanding/session-YYYY-MM-DD-topic`, based on `main`. Add each approved decision as a separate new append-only log file **on that same branch**, not directly to `main`. Continue the discussion without opening a PR or merging after each log. At the end of the session (or when explicitly requested), open one log-only PR to `main`; the existing validator may auto-squash-merge it. One merged PR triggers one centralized projection rebuild. Do not trigger rebuilds for each log entry, each branch commit, or each discussion turn. Multiple conversations can use separate branches. Never edit merged log entries; corrections are new logs.

Changes to README, `.github/workflows/`, `.github/projectors/`, or other non-log paths are mechanism changes and require manual PR merge; do not mix them into log-only auto-merge PRs. The current session branch for this mechanism update is `understanding/session-batching`; create a separate log-only session branch for future decisions.

## Automation

`.github/workflows/project-understanding.yml` validates append-only log-only PRs and auto-merges eligible changes. The merged-PR handler dispatches one centralized rebuild for relevant merged changes (including manual mechanism PRs). Mechanism changes remain manual. `.github/workflows/rebuild-projections.yml` runs five independent projectors on the same `main` snapshot and publishes only when all succeed and `main` has not advanced. Configure `CLAUDE_CODE_OAUTH_TOKEN` and Actions `GITHUB_TOKEN` write permissions.

## Principle

The durable understanding is captured in logs and interpreted into current projections; code is not the ultimate source of truth for MusicHub's intended behavior.
