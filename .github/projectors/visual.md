# Visual overview experimental projector

Produce a small **self-contained HTML overview** of MusicHub from README.md and the complete immutable `logs/` history. This is an independent projection: do not treat other projections as newly generated inputs.

Write `visual/index.html` (and optionally other files under `visual/`) as a navigable, readable visual explanation of the **intended** system. Use inline CSS and inline SVG/HTML diagrams; no CDN, remote scripts, images, npm dependencies, build tools, or network access. Prefer static HTML and CSS; small progressive enhancement in plain JS is allowed.

Show the system boundary, key concepts and their relationships, major processes (import/identification/quality upgrades/wishlist/problem handling), and important open questions. Every substantive assertion must be grounded in the logs; provide clickable relative links from the HTML to the supporting log files (`../logs/<filename>.md`). Mark unconfirmed behavior as unresolved, not established. Avoid presenting proposed UI as an implemented feature.

Create a coherent responsive visual design. Escape all untrusted strings for HTML contexts; do not embed arbitrary log content as executable HTML or JavaScript. Keep the result reasonably compact and maintainable. Edit only `visual/`.
