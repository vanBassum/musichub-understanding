# MusicHub design

Durable UX rules supported by the recorded decisions. Visual style, component system, layout and navigation structure are not yet decided.

## Configuration surfaces
- The UI is never required for configuration; it must not become a second, conflicting source of configuration truth. Whether it shows read-only settings or allows editing is open.

## Import
- A UI-based import flow (upload) is one supported way to bring user-supplied files into MusicHub, alongside a designated import folder. Upload mechanics, validation and duplicate handling are open.

## Discovery, search and wishlist
- Users can search inside MusicHub and add chosen results to the wishlist.
- A Recommended list may be shown as suggestions. Suggestions, including AI-playlist items not in the library, are never added to the wishlist automatically; adding is always an explicit user action.
- Adding an album prompts the user to choose a specific edition. The standard/original release is shown prominently at the top as the suggested default; other editions stay selectable. The UI must not silently substitute a different edition.
- Adding a track or artist must not imply the whole album or discography; the scope shown and requested matches the item the user selected.

## Review of identification
- Uncertain identifications remain visible for review and correction, including for tracks already imported, with provenance (candidate chosen, evidence, checks, confidence, user corrections).
- Manual confirmation is presented as user-confirmed, distinct from machine-measured confidence, so the 100% is not mistaken for algorithmic certainty.
- Identity confidence and audio quality are shown as separate dimensions, never merged into one score.
- Uncertain candidates held outside the library can appear in a review overview.
- Repeated contradictions of a manual confirmation surface as a visible alert; the alert does not change the confirmed identity.

## Audio versions
- Users can view retained (superseded) versions of a recording with their qualities, upgrade history and the current preferred version, and can revert to an earlier one.

## Scheduler overview
- A central task overview shows planned tasks, running tasks, previous results and next run, and lets the user trigger a task manually.

## Problem dashboard
- A dedicated central dashboard collects exceptional cases needing attention across subsystems (uncertain recordings, manual-identity conflicts, download/import problems, failed or stuck tasks). It is distinct from the scheduler overview, which shows routine task activity.
- Each entry makes clear the affected music or task, the reason, the severity and the available follow-up actions; users can address problems or trigger reprocessing where applicable.
- Problems stay visible while automatic recovery is in progress. Entries are distinguished as being recovered, needing user action, resolved or recurring.
- Problem history is retained so resolved and recurring issues can be inspected.
- The dashboard supports effective filtering, including by status, problem type, affected music, task, time and severity.

## Open
- Visual direction, navigation, layout, information density and component system.
- Exact dashboard layout, severity taxonomy, saved views and notification rules.
- Review queue workflow, edition presentation and labeling, partial album completeness presentation, and the retained-version overview design.
