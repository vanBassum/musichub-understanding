# Mobile navigation, unified search and responsive lists

Date: 2026-10-19
Status: Approved by product owner

## Context
The phone interface currently exposes too many primary destinations. Player and Queue are conceptually one destination. Mobile lists may overflow horizontally and show more details than are useful on a narrow screen.

## Approved decisions
- The phone's primary navigation has exactly three destinations: Search, Player, More. The UI uses English labels in accordance with the existing language policy; the owner described Search as "Zoeken".
- Search is the central discovery and retrieval interface: one search experience covers both the user's local library/catalog and supported external music sources. The user can distinguish or filter local and external results. Browsing or searching never implicitly adds music to the wishlist or starts acquisition.
- Player includes both Now Playing and Queue, navigable within the single Player destination. Playback remains accessible while navigating elsewhere, consistent with the existing persistent-player decision.
- More houses secondary destinations including Library, Files, Jobs, Artists and Settings, where those features exist. These features remain accessible, and deep links and detail navigation should keep working.
- On phones, lists and tables fit the viewport without horizontal scrolling. Prioritize essential fields, omit secondary columns at narrow widths and make details accessible through item/detail views rather than clipping essential information.
- This decision concerns the mobile navigation and responsive presentation; it does not prescribe the desktop navigation.

## Rationale
Reduce primary navigation complexity and make local and external search feel like one activity while retaining access to management screens.

## Boundaries
No new external search providers, music identification policy, acquisition behavior, playback backend, or settings capabilities are approved by this navigation decision. Exact components, transitions, responsive breakpoints and route implementation belong to UI delivery.
