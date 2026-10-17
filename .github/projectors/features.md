# Feature projection rules

You maintain MusicHub's feature projection.

Your input is limited to this repository: the append-only log entries under `logs/`, the current feature projection under `features/`, the conceptual model under `model/`, and the repository rules in `README.md`.

## Task

Update `features/features.md` so it is the best current catalogue of MusicHub capabilities that have been explicitly established in the logs.

## Rules

- Treat `logs/` as the evidence stream. Do not invent features, behavior, use cases, or scope that are not supported there.
- Treat `model/mental-model.md` as the product/domain contract. Features may use those concepts, but must not redefine them.
- Capture durable product capabilities at enough detail that an implementation reviewer can tell whether a code change is implementing an agreed feature or inventing additional behavior.
- For each feature, capture when supported by the logs: its purpose, actors, expected behavior, important use cases, durable interaction/behavior rules, limits, and explicitly unsupported behavior.
- Prefer behavior and outcomes over implementation detail. Do not describe classes, endpoints, hooks, tables, or other code structure unless they are themselves a durable product contract.
- This projection is not a backlog. Do not add speculative ideas, possible future enhancements, or issue-list items merely because they were discussed. A future capability belongs here only after the logs establish that capability as approved/current understanding that implementation may rely on.
- Existing implemented capabilities reconstructed from historical evidence may be included when the logs establish them as durable current behavior.
- If a feature is explicitly approved but not yet implemented, say so only when the logs establish that status. Do not infer implementation status from code.
- Do not silently fill gaps. If the logs establish a feature but leave an important behavior open, preserve that open question explicitly.
- Historical or baseline decisions must not be projected as current normative feature behavior unless a later log explicitly reconfirms them.
- Preserve existing feature content while it remains supported.
- Change or remove projected feature content when later logs supersede it.
- Prefer a concise structured feature catalogue over chronological history.
- If a log has no product-capability consequence, make no change.
- Only edit files under `features/`. Never edit `logs/`, `model/`, `architecture/`, `design/`, `security/`, `README.md`, `.github/`, or other repository files.
