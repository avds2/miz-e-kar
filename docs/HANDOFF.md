# Handoff

Updated: **2026-11-03**. Stop point: **Phase 0.1 planning only**, existing draft [PR #1](https://github.com/avds2/miz-e-kar/pull/1), branch `docs/phase-0-discovery`. No merge or implementation in this follow-up.

## Current decision and repository state

Read AGENTS.md, PROJECT-STATE.md, OPEN-QUESTIONS.md, the applicable matrix records and [P1A-SPEC.md](P1A-SPEC.md) before implementation. Owner-approved core is Django/DRF + React/TypeScript/Vite + PostgreSQL modular monolith. Channels/Celery/Redis are planned only when a slice requires them. Versions, RLS, detailed architecture, commercial billing/quotas and production sizing remain open; do not ask for core stack approval again.

Pre-edit inspection confirmed clean working tree, no local/remote divergence and head `ceb0dbb38c01e0ec939185fe1aba668a4df30610` on the PR branch. Remote `main` remained `a2f4f8fe0e6da2a5c3808b0c5ef7b974ce1e015c`. Prior discovery commit `95a5d2cdab516e73b461316bea24f856d063f42a` and final Phase 0 handoff commit `ceb0dbb` are preserved. Resolve the Phase 0.1 follow-up hash from Git history/PR head; verify status and remote again before resuming.

## Bounded follow-up completed

- Recorded explicit core approval and separated all remaining proposals; require official support/compatibility/license verification and reproducible dependency pins during implementation.
- Rechecked only five existing task/category/guest sources (HTTP 200); reread H024 from the prior capture. Q06a documents project affiliation, Q06b retains category-model unknowns, Q06c documents nonmember guest task access without implying a projectless task. No authenticated observation was added.
- Classified questions by earliest affected slice/action. No outstanding owner-evidence question blocks P1a. Later approval, finance, minutes, guest/task and commercial unknowns remain open.
- Split P1 into P1a–P1h and added the sole new document P1A-SPEC.md: eight unrun slice acceptance criteria mapped to parent subsets. Preserve all 87 parent IDs, their original criteria and all later backlog. No parent is complete.
- Retained original 114-source/14-category discovery and RD v33.003/OFL provenance. No repeat full discovery, new owner recordings, font bundling or application assets.

## Checks and publication

Phase 0.1 document audit passed: eleven Markdown files with exactly one new specification; all 87 ordered parent IDs and original acceptance criteria retained; every allocation retained and P2–P7 unchanged; 26 classified leaf questions (Q06 retained as grouping alias); eight P1a ACs mapped to valid parent subsets; 114 source identities/URLs/evidence retained; all local links/anchors/reference definitions valid; five targeted HTTP 200 receipts checked. Manual review covered approval boundaries, per-slice gates, guest nonmembership versus task affiliation, fixture limitations and commercial/advanced-scope separation. Git whitespace check passed; no product checks were claimed. Publication uses the existing PR #1 branch; no new PR or merge is needed. Commit and push outcome must be verified against PR/remote head, not inferred from access permissions.

No application commands, dependency installation, scaffolding, migrations, automated product tests, browser acceptance or deployment ran. P1a commands and tests are proposed interfaces/specifications only. Prior reference login observation proves only the unauthenticated form; paid/authenticated behaviors and tutorial playback remain unverified.

## Separate implementation task: P1a only

Implement reproducible local backend/frontend/PostgreSQL services, migrations and explicit development fixtures, independent Persian RTL/local RD shell, database-backed session login/logout and active-membership workspace list/detail/selection. User A belongs to A+B; user B belongs only to B. Enforce direct-API isolation and CSRF, invalidate logout/stale removed membership, and prove reload/backend-restart persistence and independent browser sessions. Establish the documented setup/check/accept commands and verify officially supported compatible versions then.

Exit only after all P1A-AC01–P1A-AC08 checks have recorded paths/commands/results, exact commit/browser and sanitized two-user/two-workspace evidence. Never substitute SQLite, a mock UI or hidden menu for PostgreSQL and authorization acceptance. Report unavailable checks as gaps; update parent subset status and handoff without marking broad parents complete.

Synthetic accounts are fixtures, not registration/SMS/resend/recovery/invitation parity. No project/task/category schema, guests, final approval, finance/meetings, notification infrastructure, RLS or production deployment belongs in P1a. No owner recording or credentials are needed to start it under a new implementation instruction. Before P1b, request only the redacted regular-member management actor/action evidence in OPEN-QUESTIONS.md; keep later questions for their own slices.

Research scratch remains outside Git at `/workspace/work/phase0/` and `/workspace/work/phase01/`; docs and official URLs are sufficient to resume. Do not regenerate documents from old scratch generators: edit current files and preserve concurrent changes.
