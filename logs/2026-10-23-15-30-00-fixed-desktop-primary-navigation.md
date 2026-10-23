# Fixed desktop primary navigation

Status: Approved
Date: 2026-10-23

## Context
The current application mixes a horizontal top navigation with a second navigation inside Settings (Files and Jobs). The owner approved a desktop design mockup replacing these with one coherent navigation rail.

## Decision
On desktop, MusicHub uses one persistent, non-collapsible left sidebar for primary navigation. It includes Search, Library, Downloads, Files, Jobs and Settings. Files and Jobs are first-class destinations, not Settings subpages; Settings contains actual configuration. The redundant top-level horizontal navigation is removed. The current playlist/player can remain as a right-side panel. On mobile, the same destinations remain accessible via responsive menu navigation rather than an always-visible desktop sidebar.

## Constraints
Preserve current routes where feasible, file management, jobs, playback/queue state, keyboard accessibility and responsive behavior. This is information architecture/UI work, not a backend feature. The approved desktop mockup is visual guidance, not an exact pixel specification.
