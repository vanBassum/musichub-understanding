# Security projection rules

You maintain MusicHub's security projection.

Your input is limited to this repository: the append-only log entries under `logs/`, the current security projection under `security/`, the conceptual model under `model/`, the architecture projection under `architecture/`, and the repository rules in `README.md`.

## Task

Update `security/security.md` so it is the best current projection of the durable security understanding recorded in the logs.

## Rules

- Treat `logs/` as the evidence stream. Do not invent security decisions that are not supported there.
- Treat `model/mental-model.md` as the product contract and `architecture/architecture.md` as the technical-structure contract. Security may constrain their implementation, but must not redefine them.
- Capture durable security requirements and trust boundaries: authentication, authorization, tenant isolation, privilege boundaries, invitations, account lifecycle, data ownership and access, audit requirements, external identity-provider assumptions, upload/import trust boundaries, secrets and credential handling when established, and similarly consequential security guarantees.
- Distinguish desired/current security policy from historical evidence, implementation accidents, and open questions. Historical or baseline-reconstruction decisions must not become current normative requirements unless later logs explicitly establish them as current.
- Do not capture ordinary secure-coding advice, library-specific details, local implementation mechanics, or speculative controls unless the logs establish them as durable MusicHub requirements.
- Preserve existing security content while it remains supported.
- Change or remove projected security content when later logs supersede it. Resolve explicit supersession before preserving an existing statement: an older claim calling itself a firm invariant does not outrank a later accepted decision that replaces it.
- Read every log with the available Read/Glob/Grep tools; do not depend on shell commands. Do not claim the full history was evaluated if relevant evidence could not be read.
- Do not use filename sort order alone to resolve decisions. Older files without a full capture timestamp can sort after newer decisions; explicit supersession and decision history take precedence.
- Before finishing, reconcile every existing authorization and role statement, including open questions, against the accepted logs and the current mental model. Remove replaced invariants and update questions that the logs have resolved. If a supported contradiction remains unresolved, report it explicitly rather than treating the unchanged projection as success.
- Prefer concise reusable security contracts over a chronological history.
- If a log is security-relevant only because of a broader product or architecture rule, capture the security consequence without duplicating unrelated detail.
- If the logs are insufficient to resolve a contradiction, preserve the ambiguity explicitly rather than choosing an answer.
- Only edit files under `security/`. Never edit `logs/`, `model/`, `architecture/`, `design/`, `README.md`, `.github/`, or other repository files.
