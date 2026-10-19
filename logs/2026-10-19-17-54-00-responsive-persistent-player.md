# Decision: responsive persistent playback presentation

Status: accepted by owner on 2026-10-19.

Context: Playback controls should remain accessible while browsing any MusicHub screen, without consuming excessive space on narrow displays.

Decision:
- Playback UI is part of the shared application shell and remains available across navigation, independent of the active page.
- On sufficiently wide desktop viewports, show the full player persistently docked on the right beside the main content.
- On intermediate/tablet-sized viewports, replace the full panel with a compact persistent player exposing basic playback controls and current track context.
- On narrow/mobile viewports, use a compact persistent mini-player near the bottom, coordinated with mobile navigation.
- From either compact presentation, activating the player opens an expanded full-player overlay above the current page. Closing the overlay returns to the same page and context.
- Responsive presentation follows available viewport space, not device type. Exact breakpoint values and placement are UI implementation details, provided content remains usable.
- The shared playback state should survive route changes, overlay transitions and viewport changes without interruption when real playback is implemented.

Rationale: Provide consistent access to playback while prioritizing browsing space on tablet and mobile.

Boundaries: This establishes the intended UI behavior, not an audio engine or playback backend. The first delivery may use simple placeholder data and controls; real playback wiring is separate work. The three-viewport concept image is illustrative rather than pixel-perfect specification.
