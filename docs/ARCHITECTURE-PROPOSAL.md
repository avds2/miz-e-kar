# Architecture proposal

**Status: proposed, not approved or installed.** The owner approved comprehensive web scope and Debian deployment, not a framework. No application source or scaffold exists. Deployment scale, concurrency, attachment growth, hardware, budget and recovery objectives remain Q11/Q24.

## Realistic options

| Option | Fit and strengths | Costs / tradeoffs |
| --- | --- | --- |
| Django + Django REST Framework + React/TypeScript | Mature relational/domain model, transactions, migrations, authentication and administrative tooling; React suits calendars, boards, chat and Gantt. Channels supports session-authenticated sockets. | Python and TypeScript toolchains; object authorization and socket revocation must be designed explicitly; administrative UI cannot substitute for product flows. |
| Laravel + Vue/TypeScript + Reverb/queues | Coherent full-stack conventions, policies, migrations, jobs and broadcasting; viable Debian operation. | Still requires careful resource policies and rich-client components; PHP expertise and broadcasting operations need confirmation. |
| NestJS + React/TypeScript + PostgreSQL | One language family and natural event/socket interfaces; useful with an experienced TypeScript team. | More assembly for authorization, admin, relational migrations and durable workflows; shared TypeScript types do not validate business rules. |

**Recommendation:** a Django modular monolith with REST APIs, React/TypeScript built with Vite, PostgreSQL, Channels, and Celery/Redis. Use one origin for browser assets, HTTP API and sockets. Select supported/pinned versions and verify library licenses during the first authorized implementation slice. This balances the relational workflows and rich interactions without distributed-service complexity. Team expertise could justify Laravel instead (Q09). No performance superiority is claimed; no benchmark ran.

## Domain boundaries and relationships

Keep identity, workspaces/access, projects/tasks, conversations, meetings, customers/sales/finance, correspondence, notes, notifications/search and operations as modules in one backend and database. Route mutations through explicit domain services/policies and transactions; prevent arbitrary cross-module table writes. Start with one frontend and cohesive API contracts, not multiple applications or microservices.

| Relationship | Proposed model / unresolved constraint |
| --- | --- |
| User ↔ Workspace | Many-to-many Membership with owner/admin/member/guest role, invitation/removal state and workspace job title. Global account/profile/sessions separate from membership. Exactly one owner per workspace; transactional transfer. |
| Workspace → Project | Project members/managers, settings revisions, project groups (many-to-many), board columns and activity feed. Project-linked task category initially; standalone categories require Q06. |
| Project → Task | Task has nullable-many assignees, creator, optional approval policy, checklist items, reports/replies, labels, reminder/start/due, progress/weight, attachment links and receipts. A guest may receive a task without joining the project: task-specific access must not reveal project feed. |
| Task → Recurrence / Gantt | Rule plus real occurrences and computed projections; occurrence uniqueness. Gantt phases/order and directed dependencies refer to original tasks, not duplicated task records. Board position is independent of completion. |
| Conversation → Message | Explicit type: private/group/channel/project/customer/assistant; typed content and read receipts. A single activity envelope may reference task/minutes/poll events; canonical domain records remain authoritative. |
| Meeting → Resolution / Signature | Separate minutes revision, electorate/attendance snapshot, roles, signatures and resolution links; approval dispatch is transactional and idempotent. Signature representation awaits Q05. |
| Customer → Related records | Multiple phones/representatives and resource ACL; call reports, tasks, minutes, documents, opportunities and financial records. Scope labels by module, not a universal unrestricted label table. |
| Letter ↔ Customer / Task | Explicit links do not broaden either resource's ACL. Letter recipients/paraph audience and registered status determine read access. Outgoing sequence uses locked counter plus unique constraint; incoming numbers need not be unique. |
| Note / Attachment | Note content owner-only; account vs workspace note scope awaits Q11. Attachments use resource links with authorization, not public paths or unrestricted polymorphic IDs. |

Use database foreign keys, unique constraints and same-workspace composite relationships where practical. Keep original authorship/history after member removal and substitution. Use explicit per-resource lifecycles: task deletion/recovery, project archive modes, recoverable conversation/customer removal, note trash with purge. Do not implement a generic cascade-delete policy. Financial amounts use exact decimal or integer minor units plus a currency/unit; never floating point. Rial/toman semantics remain unresolved.

## Isolation and server-side authorization

Resolve workspace context from authenticated membership and validate it against each resource; never trust a client-supplied workspace ID. Central policy combines membership state, plan entitlement, action grant, resource membership/role, record state and private-content exceptions. Default deny for unspecified permissions until clarified. “Owner” is not a universal content-reader.

Apply the same policy to queries, aggregates/counts, imports, prints, file downloads, bookmarks, notification rendering and socket subscriptions. Preserve explicit guest-deny rules and task-specific grants. Commands recheck policy inside the transaction; membership revocation removes subscriptions and invalidates caches. Test concurrent revoke/write/read races and inaccessible foreign keys.

Proposed defense in depth: PostgreSQL row-level workspace policies for workspace-owned tables with a non-owner, non-superuser runtime role; transaction-local context reset with pooled connections; separate migration role. RLS does not replace action/private-resource policy. Prototype and test the context contract before depending on it; table owners/superusers can bypass ordinary RLS. Explicitly scoped worker/admin jobs need the same boundaries. See [PostgreSQL RLS documentation](https://www.postgresql.org/docs/current/ddl-rowsecurity.html), accessed 2026-11-03.

## Durable events, live updates and jobs

Commit state, audit and outbox event in one PostgreSQL transaction. A worker drains the outbox to Channels and notification jobs. Redis is transport/cache, not the record of tasks or business state. Clients use entity versions and a cursor/refetch path after disconnection; sockets validate origin, session and current membership on subscribe and sensitive dispatch. Never broadcast a whole private record to a workspace room. Authentication middleware alone is not resource authorization ([Channels authentication](https://channels.readthedocs.io/en/stable/topics/authentication.html), accessed 2026-11-03).

Celery jobs handle reminders, SMS/email/browser push, recurrence progression, imports/copies, thumbnails and note purge. One scheduler enqueues due work; durable database timestamps and unique operation keys make worker restarts safe. Bound retries with backoff/timeouts; retain actionable failure status and safe operator replay. Workers recheck recipient permissions before delivery. Do not promise exactly-once provider delivery: idempotent effects and deduplication are required because work can be retried ([Celery task guidance](https://docs.celeryq.dev/en/stable/userguide/tasks.html), accessed 2026-11-03).

Recurrence creates a successor only on verified completion; calendar projections must not trigger notifications prematurely. Approval, minutes dispatch and letter numbering need locked/conditional writes to prevent duplicate finalization. Audit actor/time and prior/new state for privileged changes without logging secrets.

## Attachments and search

Initially store private files outside the web root on a backed-up Debian volume, behind an attachment storage interface. Retain original filename/media type/size/checksum and resource ACL. Serve authorized downloads through the backend or internal reverse-proxy redirect. Stage uploads with limits, verified content type, safe filenames, quota reservations, scanning and cleanup; protect inline previews from active content. Restore bytes and metadata together. Add S3-compatible storage only if operations/scale require it; do not provision a separate object-store cluster speculatively.

Start with PostgreSQL text/trigram indexes over normalized search fields (Persian/Arabic yeh/kaf, whitespace and digit handling), preserving original text. Benchmark Persian substrings/tokenization, rank and ACL filtering on representative fixtures. Authorize candidates before exposing snippets/counts; recheck live ACL on open. Search filenames and authorized module content; file-content OCR/search is not documented. Add an external engine only if measured needs justify its indexing/recovery burden.

## Persian, time and frontend

Use semantic HTML, logical CSS properties, RTL by default and explicit BiDi isolation for mixed identifiers. Build reusable accessible dialogs, forms and date/number adapters; independently design visuals. Browser checks cover keyboard/focus, narrow desktop/mobile-browser widths, Persian editing and print output. Calendar/Gantt libraries need license and RTL/Jalali interaction verification before selection.

Store instants as timezone-aware UTC timestamps; store date-only business dates separately. Keep IANA timezone and original recurrence calendar/rule so month-end/yearly Jalali schedules are not approximated by fixed UTC intervals. Display and input Jalali via a tested adapter with Gregorian API representation explicitly documented; imports use documented Gregorian dates. No assumption that every product user is in Tehran; the owner's chat timezone is not a deployment-wide setting. Test Esfand leap days, Nowruz, midnight, date-only deadlines and clients in different zones.

Self-host pinned Vazirmatn RD files after selection; preserve OFL notices and provenance. Font availability/license verification is recorded in the source register. No font or branded assets are bundled in Phase 0.

## Debian deployment, migrations and recovery

Propose a small Docker Compose deployment on a supported Debian release: TLS reverse proxy, built frontend + production ASGI service, worker/scheduler, PostgreSQL and Redis, with private persistent volumes. No Kubernetes, service mesh or managed-cloud requirement. A systemd-managed equivalent remains viable if the operator prefers it (Q11). The research machine being Debian 13 does not establish the target server version or capacity.

Use non-root application processes, least-privilege DB roles, same-origin secure HttpOnly session cookies, CSRF/origin protections, bounded login/OTP attempts, encrypted transport and secrets outside Git. Disable debug, configure hosts and run production framework checks; use a production ASGI server ([Django deployment checklist](https://docs.djangoproject.com/en/5.2/howto/deployment/checklist/), accessed 2026-11-03). SMTP/SMS/push providers and outbound connectivity are open questions. A documented one-time guest invitation flow should replace sending reusable plaintext credentials if approved; record that deliberate behavior difference rather than claiming identical parity.

Version migrations with schema/data constraints and reversible/forward-repair strategy. Use expand/backfill/contract for risky changes; dry-run migration against a restored copy, take a pre-change recovery point and record release/image/schema compatibility. A code rollback cannot automatically undo a destructive data migration. No migrations were created in this phase.

Back up database, attachment bytes/metadata, configuration and required encryption material with a consistent manifest/checkpoint; encrypt and keep an off-host copy with retention/access monitoring. Start with scheduled logical backups; assess base backups/WAL point-in-time recovery when RPO/data volume is known. Never treat a successful backup command as proof of recovery. Rehearse restore into an isolated machine, validate row/attachment checksums and ACL fixtures, rebuild search, reconcile outbox/reminders without resending completed effects, and measure achieved RPO/RTO. Alert on failed backups, disk/quota pressure, queue age, failed jobs, server errors and restore-test age. Target numbers await Q24.

Video conferencing is retained for P6. Evaluate a maintained self-hostable media service/SFU and TURN deployment then; a ten-person media call changes bandwidth/CPU/network requirements substantially. Do not add media infrastructure to P1 or assume Mizito's provider is reusable.
