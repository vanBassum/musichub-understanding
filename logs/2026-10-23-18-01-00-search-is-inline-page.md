# Search results replace page content inline

Status: approved by product owner, 2026-10-23.

Context: The owner dislikes a popup/overlay result list, particularly on mobile.

Decision: Search is a full page. Typing into the top search field updates the page's own results in place rather than opening a popup or dialog. Show browsable album, track and artist result categories with the ability to focus a category. Mobile-first usability matters; navigating to an album exposes editions and the selected edition's tracklist before adding it to the wishlist. Keep empty/loading/error states within the page.

Rationale: Browsable search is easier to scan and supports albums and compilations, not just quick suggestions.

Open: Final visual design, ranking and exact debounce/pagination behavior.
