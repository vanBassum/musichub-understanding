# Simplify Files page filtering and actions

Status: Approved
Date: 2026-10-23

## Context
The Files page displays many separate status and identification filter buttons plus administration controls, making the top of the page visually cluttered. The owner approved a compact dark-mode mockup.

## Decision
Use one compact Files toolbar: prominent Upload files action, text search, a status dropdown, an identification dropdown, and a secondary menu for less frequent controls such as simultaneous-upload settings and bulk failed-file deletion. Filters can be combined; relevant counts remain available inside filter options. The file table, pagination, file statuses and per-file actions remain accessible. Show errors contextually instead of leaving stale generic error banners in the main layout.

## Constraints
Keep current upload, filtering, identification and deletion semantics; no new backend feature. The mockup is a visual direction, not a mandate for exact icons, counts, filenames or values. Preserve responsive and accessible behavior.
