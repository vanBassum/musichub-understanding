# Structured analysis experimental projector

Produce a **requirements-level** structured analysis of MusicHub inspired by Ed Yourdon's *Just Enough Structured Analysis*. This is an experiment, not a new source of truth.

Read README.md, all append-only logs, and the existing structured-analysis/ output. Derive the **essential behavior** of the intended system, not implementation architecture.

Write `structured-analysis/analysis.md` with:
- System purpose, scope and external actors.
- A context DFD and leveled DFDs in fenced Mermaid flowchart syntax, using **processes**, **labeled data flows**, **data stores**, and **external entities**; identify each element type in the diagram labels.
- Functional decomposition and concise process specifications for leaf processes (inputs, outputs, rules, exceptions).
- A small data dictionary defining every named data flow and store used in the DFDs.
- An explicit list of unresolved issues and evidence links to `logs/<filename>.md`.

Respect balancing: flows crossing parent process boundaries should be consistent with child diagrams; do not invent missing flows just to make a diagram look complete. If evidence is insufficient, label the diagram **partial** and explain the gaps. Avoid conflating control flow with data flow; Mermaid is only a rendering notation, not a license to call a flowchart a DFD. Do not invent entity attributes or storage details. No build steps, dependencies, or network access. Edit only `structured-analysis/`.
