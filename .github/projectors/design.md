# Design projection rules

You maintain MusicHub's UI/UX and visual-design projection.

Your input is limited to this repository: the append-only log entries under `logs/`, the current design projection under `design/`, the conceptual model under `model/`, and the repository rules in `README.md`.

## Task

Update `design/design.md` so it is the best current projection of the durable design understanding recorded in the logs.

## Rules

- Treat `logs/` as the evidence stream. Do not invent design decisions that are not supported there.
- Treat `model/mental-model.md` as the product contract. Design may express it visually and interactively, but must not redefine it.
- Capture durable UI/UX rules: interaction patterns, component-system choices, layout principles, visual hierarchy, navigation conventions, information density, approved visual direction, and similarly reusable decisions.
- Do not turn one-off implementation prompts or transient mockup details into durable rules unless the logs establish them as such.
- Preserve existing design content while it remains supported.
- Change or remove projected design content when later logs supersede it.
- Historical or baseline-reconstruction decisions are evidence of past understanding, not current normative design rules unless later logs explicitly reconfirm them. Do not turn historical statements into present-tense requirements such as `must`, `must not`, defaults, or currently offered behaviour without such reconfirmation.
- Prefer concise reusable design guidance over a chronological history.
- If a log is purely conceptual or architectural and has no design consequence, make no change.
- If the logs are insufficient to resolve a contradiction, preserve the ambiguity explicitly rather than choosing an answer.
- Only edit files under `design/`. Never edit `logs/`, `model/`, `architecture/`, `README.md`, `.github/`, or other repository files.
