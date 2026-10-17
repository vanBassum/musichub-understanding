# PostgreSQL and S3-compatible storage configuration contract

Date: 2026-10-17
Status: Accepted by product owner

## Context

MusicHub currently has a UI shell but no configured database or object storage. Its acceptation stack needs to be prepared before the library data model, imports and playback are implemented. The owner wants to follow the same broad environment-variable configuration approach used for Parklr, while leaving service topology to the stack.

## Accepted decisions

- Use **PostgreSQL** for MusicHub's relational persistence and **MinIO / S3-compatible object storage** for managed files.
- The application consumes configuration and connects to these services. The deployment stack decides whether to run dedicated or shared PostgreSQL/MinIO instances, and owns service networking, persistent volumes, credentials, database/user provisioning and bucket provisioning.
- Keep application configuration in ASP.NET Core's standard configuration system, allowing environment variables to override appsettings. Do not hardcode deployment-specific endpoints or secrets or commit secrets to Git.
- Adopt the following **proposed application configuration keys as the agreed implementation contract**. The API does not support them yet; implementation issues must introduce them:
  - `Database__Host` (example `postgres`)
  - `Database__Port` (example `5432`)
  - `Database__Database` (example `musichub`)
  - `Database__Username` (example `musichub`)
  - `Database__Password` (secret)
  - `FileStorage__Endpoint` (example `http://minio:9000`)
  - `FileStorage__Bucket` (example `musichub`)
  - `FileStorage__AccessKey` (secret)
  - `FileStorage__SecretKey` (secret)
- The deployment may supply secrets through environment substitution (for example `MUSICHUB_DB_PASSWORD`, `MUSICHUB_MINIO_ACCESS_KEY`, `MUSICHUB_MINIO_SECRET_KEY`); those are stack-side example variable names, not additional application configuration keys.
- Keep the database private, and keep MinIO's application-facing S3 endpoint private to the deployment network.
- Use EF Core and a **separate database migration step invoked by the stack**. Do not automatically apply schema migrations on normal API startup. This separates schema changes from serving traffic.
- Introduce database integration and object storage integration as separate implementation steps before designing the library domain schema and import pipeline. Storage integration must not imply permission to touch the original NAS collection; MusicHub's managed library remains separate.

## Deliberately delegated or undecided

- Whether PostgreSQL/MinIO instances are shared or dedicated, their image versions, credentials, volume paths, backup implementation and network names are stack decisions.
- The exact invocation interface for the separate EF Core migration step must be defined in the implementation issue and documented for the stack. No specific migration CLI/container entrypoint has been accepted yet.
- No track/album schema, import process, or playback functionality is approved by this entry alone.

## Rationale

Stable environment-variable keys allow the stack to be prepared independently of application development. Independent database and object-storage integration keeps failures isolated, and explicit migration execution avoids surprise schema changes on API startup.
