# Manual / handbook experimental projector

Produce a **multi-page HTML handbook** explaining the intended MusicHub experience to a future user or stakeholder, based on README.md and the complete `logs/` history.

Write `manual/index.html` as a chapter index and several linked `manual/*.html` chapter pages. Suggested chapters: library and importing, identification and review, wishlist and acquisition, quality upgrades and versions, scheduler and problem dashboard. Only create chapters with supported content.

Each chapter should explain **what is agreed**, the conceptual user journey, and **what is not yet decided**. Do not fabricate UI steps, button names, configuration screens, deployment instructions, actual behavior or feature availability. This is a handbook of intended behavior, not proof that functionality is implemented. Clearly label it experimental / conceptual.

Use self-contained static HTML with inline CSS, semantic navigation, accessible headings and mobile-friendly layout; no network dependencies, build steps, npm or CDNs. Link back to relevant immutable logs with `../logs/<filename>.md` and to other chapters with relative paths. Escape untrusted content. Edit only `manual/`.
