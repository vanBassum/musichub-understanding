# Music-first responsive navigation and information architecture

Date: 2026-10-21
Status: Approved

## Context
Reviewing acceptance UI screenshots, the product owner found the main navigation fragmented and overly technical: Search, Library, Files, Playlists, Artists, Jobs, Downloads and Problems all compete as peers. A proposed visual sitemap was approved as a direction, with an explicit preference for desktop layouts that actually use desktop space rather than enlarged mobile screens. The owner approved placing management under Settings.

## Decision
- Primary navigation emphasizes **Search**, **Library** and **Downloads**. A discoverable **Settings** entry provides access to operational and administrative screens rather than making Management a prominent top-level destination.
- Artist and album detail pages are contextual destinations reached from Search or Library, not permanent top-level navigation tabs. Existing deep links and back navigation should remain usable.
- The Library is the natural home for the user's music and playlists; playlists need not occupy an equally prominent global navigation slot.
- Settings/Management groups the existing Files, background Jobs/Tasks and History, and Problems functionality. These remain distinct capabilities with their established semantics: stored file management, task execution/history, and exceptional-case handling. Grouping them must not hide actionable errors or remove access to their details.
- Downloads remains a user-facing destination showing actual queued, active, completed and failed download requests; sample data is not an acceptable representation of runtime state.
- Responsive design is compositional: desktop uses available width through appropriately dense tables, filters, detail panes and optional playback/queue panels; mobile uses touch-friendly navigation, one-column content and collapsible secondary controls. Desktop must not simply scale up phone-width cards, and mobile must not overflow horizontally.
- Playback and its queue are available across navigation, adapting their presentation to the viewport. The playback queue is distinct from the download queue.
- Preserve current workflows, functionality, data and existing product rules. This decision is about navigation and presentation, not a mandate to rebuild backends or introduce unsupported features.
- Keep the existing English-language UI policy.

## Rationale
Music discovery and listening are the primary tasks. Administrative tools remain accessible without dominating the application. Desktop information density and mobile ergonomics need different arrangements of the same functionality.

## Open
Detailed visual styling, breakpoint values, exact mobile navigation controls, notification treatment for urgent Problems, and precise Settings subsection labels remain implementation/design choices subject to existing accessibility requirements.
