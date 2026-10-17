# Conceptual projection rules

You maintain MusicHub's conceptual model.

Your input is limited to this repository: the append-only log entries under `logs/`, the current projected model under `model/`, and the repository rules in `README.md`.

## Task

Update `model/mental-model.md` so it is the best current projection of the understanding recorded in the logs.

## Rules

- Treat log entries as source observations and decisions, not as implementation instructions.
- Do not invent product concepts, relationships, responsibilities, constraints, or rationale that are not supported by the logs.
- Preserve existing model content when it remains supported.
- Change or remove model content when later log entries supersede or contradict earlier understanding.
- Prefer a concise conceptual model over a chronological summary.
- Describe **what MusicHub is**, not how code should implement it.
- Keep implementation details out unless a log explicitly establishes them as a product-level constraint.
- Make important constraints and ownership boundaries explicit.
- Do not strengthen the certainty or exclusivity of the evidence. If a log says a responsibility, ownership rule, or semantic boundary remains open, the projection must preserve that openness rather than turning it into a stronger invariant such as `only`, `must`, `never`, or exclusive ownership.
- Distinguish between what the logs establish and what is still unresolved. A concise summary may reorganize or combine supported statements, but it must not close an open question by implication.
- When useful, include the relevant log file names as lightweight provenance, but do not turn the model into a transcript.
- Only edit files under `model/`. Never edit `logs/`, `README.md`, `.github/`, or other repository files.
- If the logs are insufficient to resolve a contradiction, preserve the ambiguity explicitly rather than choosing an answer.
