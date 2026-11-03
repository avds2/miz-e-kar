# P1a — session and workspace foundations

**Status: specification only, 2026-11-03. Not implemented; no commands/tests below exist or have run.** A separate implementation task must authorize this slice. Approved core: Django/DRF + React/TypeScript/Vite + PostgreSQL modular monolith. Channels/Celery/Redis are deferred until a slice needs realtime/jobs. This contract does not approve RLS, production topology, commercial billing or sizing.

## Included flow and data

Start reproducible local services → migrate PostgreSQL → seed synthetic accounts/workspaces/memberships → login → list/select only accessible workspaces → reload and see persisted selection/name → logout and lose authenticated access.

Create a minimal independently designed Persian interface with `lang="fa"`, `dir="rtl"`, keyboard-usable login/workspace selection, mixed-text isolation, loading/empty/error states and local Vazirmatn RD. Bundle only required verified font files with OFL/provenance; no reference logos/backgrounds or external font CDN. Calendar/date widgets are deferred to P1e; Persian/Jalali remains a product requirement.

Limit schema to account, workspace, active/removed membership and database-backed sessions, with versioned migrations and unique user/workspace membership. Use PostgreSQL in development and backend tests, not SQLite or in-memory replacement. Normal HTTP isolation must work without RLS. Selected workspace is stored per server-side session, revalidated on every access; no user-global selection that makes another session switch context. Persist workspace/membership records and session selection across backend restart and browser reload.

Fixture **User A**: owner of **Workspace A**, member of **Workspace B**. Fixture **User B**: owner of B, no membership in A. Use Persian synthetic display names, separate browser contexts and distinct sessions. Seed command is explicit, repeatable and development-only; no public provisioning endpoint or production auto-seed. Read fixture passwords from ignored local environment or a secure prompt; no reusable credentials in Git, logs or screenshots. Re-running seed must not duplicate rows or overwrite unrelated data.

Synthetic identifiers/accounts are test fixtures. They do **not** deliver reference mobile registration, SMS verification/resend, invitation acceptance, password recovery, two-factor authentication, reference lockout timing or account lifecycle parity. MK-AUTH-001 and unfinished MK-AUTH-002 criteria stay open.

## Proposed API contract for this implementation slice

Establish CSRF bootstrap, session login/logout/current-session, membership-filtered workspace list/detail, and workspace selection. Suggested paths: `GET /api/auth/csrf`, `POST /api/auth/login`, `POST /api/auth/logout`, `GET /api/session`, `GET /api/workspaces`, `GET /api/workspaces/{id}`, `POST /api/session/workspace` (workspace ID). Document actual paths if implementation conventions require an equivalent change; preserve these behaviors:

- Django server-side cookie sessions with HttpOnly session cookie, appropriate SameSite and CSRF/origin validation, including login/logout/selection. Production Secure-cookie configuration is explicit; loopback development HTTP configuration is not production readiness.
- Anonymous protected access returns 401; invalid credentials give a generic failure without account disclosure; invalid/missing CSRF or hostile origin on mutations returns 403. Do not claim reference recovery/lockout semantics.
- Authenticated foreign or nonexistent workspace IDs return the same 404 response; no title, member list, count or role leakage. Failed selection leaves prior selection unchanged. Lists contain active memberships only.
- Role alone is not global access: B's owner role in B grants no access to A. Removed membership fails the next protected request, even with a stale selected-workspace session. No create/update/delete workspace, invitation or role-management endpoint in P1a.

<a id="version-preflight"></a>
## Version preflight and reproducibility

During implementation, verify supported compatible versions and licenses from official sources: [Django supported releases](https://www.djangoproject.com/download/#supported-versions), [Django installation compatibility](https://docs.djangoproject.com/en/stable/faq/install/), [DRF requirements](https://www.django-rest-framework.org/#requirements), [React versions](https://react.dev/versions), [Vite guide](https://vite.dev/guide/), [TypeScript releases](https://www.typescriptlang.org/docs/handbook/release-notes/overview.html), [Node releases](https://nodejs.org/en/about/previous-releases), and [PostgreSQL version policy](https://www.postgresql.org/support/versioning/). These are verification targets, not newly accessed sources or version selections in Phase 0.1.

Record selected versions, runtime compatibility (Python/Django/DRF and Node/Vite/React/TypeScript), access dates and source URLs in the implementation record. Pin dependencies/images, commit lockfiles and use deterministic install commands. Establish a development Compose setup (backend/frontend/PostgreSQL, health/readiness and persistent volume), documented prerequisites and `.env.example` with blank secrets. Production Compose/systemd selection remains undecided. No Redis or worker service is necessary for this slice.

Commands to establish in implementation; names are a reviewable proposed interface, not currently runnable commands:

| Command | Required behavior |
| --- | --- |
| `make dev-up` | Deterministically build/install locked dependencies and start local backend/frontend/PostgreSQL with documented ports and readiness checks. |
| `make migrate` | Apply versioned schema to empty or existing development DB; repeat without creating drift. |
| `make seed-dev` | Explicit idempotent synthetic fixture creation; require development mode and ignored local credentials. |
| `make check` | Run PostgreSQL-backed backend business/auth tests, migration drift/system checks, frontend type checks and build; fail nonzero on errors. |
| `make accept` | Run scripted browser acceptance below, including direct HTTP requests, or document exact reproducible browser steps if automation is unavailable. Skipped/unavailable checks do not count as passing. |
| `make dev-down` | Stop services while preserving volumes. No implicit data reset; a destructive reset is separate and explicit. |

A fresh checkout must reproduce setup from the documented prerequisites. Missing Docker/DB/browser capability is an implementation blocker to report with evidence, not permission to silently replace PostgreSQL or skip acceptance.

## Acceptance IDs and parent subsets

All eight slice criteria are **planned/unrun**. These are slice acceptance IDs, not new parent requirement IDs. Keep all 87 parents and their original criteria; passing these subsets alone cannot mark a broad parent complete.

| Slice AC ID | Included parent subset | Check / expected result |
| --- | --- | --- |
| P1A-AC01 | MK-OPS-001 AC1, development reproducibility subset only | Fresh-checkout setup, migration, seed and check commands succeed against PostgreSQL; second migration/seed has no duplicate data/drift. No Debian production-install claim. |
| P1A-AC02 | MK-LOC-001 AC1/AC2 and MK-LOC-003 AC1/AC2, shell-only subsets | Persian fixture names round-trip through DB/API/render/reload; RTL and mixed identifiers remain usable by keyboard at desktop/narrow width. Browser loads local RD, matching provenance/license, with no external font request. Product-wide UI/print/date checks remain open. |
| P1A-AC03 | MK-AUTH-002 AC1/AC2, synthetic session-login subset | Correct fixture credentials authenticate; wrong credentials do not. CSRF/origin tests reject invalid mutations. Logout invalidates server session; replayed old cookie cannot access a protected endpoint. Registration/recovery/OTP/lockout parity excluded. |
| P1A-AC04 | MK-WS-001 AC1/AC2, workspace reads/selection subset | A lists A+B and can select either; B lists B only. B directly requests/selects A via API and receives 404 with no leaked details; prior selection stays B. Project/task views are not present. |
| P1A-AC05 | MK-WS-001 AC2 and MK-WS-006 AC1, membership boundary subset | Anonymous calls fail; owner-in-B is not global owner; test database marks membership removed and stale session loses access on next request. No removal/role-management product UI delivered. |
| P1A-AC06 | MK-OPS-001 migration/persistence and MK-WS-001 selection subsets | Reload and restart backend preserving DB/volume: workspace names/memberships and valid session selection persist. Two browser sessions select independently. This is not backup/restore qualification. |
| P1A-AC07 | MK-OPS-002 AC1 HTTP-only subset | Automated PostgreSQL tests exercise foreign/nonexistent IDs, invalid selection, denied writes, CSRF, logout and removed membership; failed requests cannot change data/session selection. Socket/download/job criteria remain open. |
| P1A-AC08 | MK-LOC-001, MK-AUTH-002 and MK-WS-001 browser subsets | Run two isolated browser contexts for A/B, perform AC02–AC06, and issue unauthorized **direct API requests from B's authenticated context**; reload to prove state. Capture sanitized results for exact commit/browser; a hidden menu or unit tests alone do not pass. |

## Exit evidence and non-goals

Provide exact commit, selected version/support-source ledger, prerequisites/commands, migration results, automated test paths/results, frontend build/type result and sanitized browser/direct-API results for both users and both workspaces. Verify local font loading and Persian/RTL rendering. Record failures/skips honestly; any unperformed included acceptance check leaves P1a unaccepted. Update matrix subset status, PROJECT-STATE.md and HANDOFF.md before stopping; broad parents remain partial/open.

Non-goals: real registration/SMS/recovery/invitations, workspace creation/edit/removal UI, project/task/category schema or flows, guest task access, final approval, calendars/Gantt/minutes/CRM/finance/letters, uploads/search/notifications, sockets/jobs/outbox/RLS, subscription quotas/billing and production deployment/sizing/backup recovery. No owner recording blocks the included slice. Request P1b membership-action evidence when that work is next; keep Q06b/Q06c and all later questions open for their own slices.
