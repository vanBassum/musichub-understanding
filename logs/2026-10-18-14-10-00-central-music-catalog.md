# Central music catalog and initial delivery scope

Date: 2026-10-18
Status: Accepted in discussion

## Context
Before designing the central scheduler, the user chose to establish the music catalog as the authoritative source of music identity and availability. Work scheduling is deferred.

## Decisions
- MusicHub has one authoritative catalog of known music, including tracks without audio files. Wishlist, library and future workflows are views or relationships over that catalog, not independent competing music inventories.
- A track represents one specific recording/performance/version. Remixes, live performances and remakes are distinct tracks.
- Artists are independent entities with many-to-many relationships to tracks, including roles; albums can also relate to artists.
- Albums, compilations and playlists conceptually share an ordered collection of track references, with distinct types and metadata. Tracks can belong to multiple collections without duplicating audio.
- Playlists may reference unavailable tracks. AI may suggest unavailable tracks, but suggestions never authorize wishlist additions or acquisition without user approval.
- Audio files are independent entities; tracks may have zero or multiple files, and files may exist without an identified track. For the initial scope, a file is linked to at most one track. Identification and cleanup are separate concerns.
- Initial delivery focuses on a catalog data model, API and functioning UI, including manually registering tracks and viewing/searching them. Albums/playlist management, wishlist behavior, and scheduler are deferred. Existing upload, storage and metadata-extraction work remains separate.
- A generic mutable track status field is not yet approved: availability, desire, and processing can coexist and should not be forced into one exclusive state.

## Rationale and trade-offs
A central catalog prevents duplicate inventories and makes work discovery derivable from domain facts. Separating track identity from physical files supports unavailable music, multiple encodings, uncertain imports, and later cleanup. Avoid designing the scheduler before catalog semantics are established.

## Open
Exact schema, endpoint names, UI interaction details, status representation, collection implementation, file association workflow, event sourcing, and scheduler design remain implementation/design questions. No event-sourcing requirement was decided.
