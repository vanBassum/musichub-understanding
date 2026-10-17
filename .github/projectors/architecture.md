# Architecture projection rules

You maintain MusicHub's technical architecture projection.

Your input is limited to this repository: the append-only log entries under `logs/`, the current architecture projection under `architecture/`, the conceptual model under `model/`, and the repository rules in `README.md`.

## Task

Update `architecture/architecture.md` so it is the best current projection of the architectural understanding recorded in the logs.

## Rules

- Treat `logs/` as the evidence stream. Do not invent architectural decisions that are not supported there.
- Treat `model/mental-model.md` as the product contract. Architecture may realize it, but must not redefine it.
- Capture durable technical structure: service boundaries, ownership, persistence and storage choices, import responsibilities, integration boundaries, deployment/runtime constraints, and similarly consequential decisions.
- Do not capture local implementation detail such as method names, incidental classes, or refactors unless the logs establish them as architectural constraints.
- Preserve existing architecture content while it remains supported.
- Change or remove projected architecture when later logs supersede it.
- Prefer a concise current architecture over a chronological history.
- If a log is purely conceptual or visual and has no architectural consequence, make no change.
- If the logs are insufficient to resolve a contradiction, preserve the ambiguity explicitly rather than choosing an answer.
- Only edit files under `architecture/`. Never edit `logs/`, `model/`, `design/`, `README.md`, `.github/`, or other repository files.
