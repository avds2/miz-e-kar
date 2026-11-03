# Project state

Updated: **2026-11-03**. Current stage: **Phase 0.1, bounded planning follow-up on PR #1**. No application implementation, framework scaffold, dependency installation, schema migration or deployment exists. All 87 parity requirements are not implemented; all proposed acceptance tests are uncreated/unrun.

## Inspected repository and environment

- Repository: `avds2/miz-e-kar`, public; origin `https://github.com/avds2/miz-e-kar.git`.
- Local checkout initially had an unborn `work` branch, no tracked files and no local commits. Remote inspection found `main` at `a2f4f8fe0e6da2a5c3808b0c5ef7b974ce1e015c` (one-line README, first commit). Fetched `main` explicitly because the existing fetch refspec selected only HEAD. Created `docs/phase-0-discovery` from that remote commit; preserved the original README heading and expanded it. No existing application or AGENTS.md was found in the project checkout.
- Research executor: Debian GNU/Linux 13 (trixie), Git 2.52.0, gh 2.46.0, Python 3.12.14, Node 24.22.1, system Chromium 155 and existing Playwright module available. This does not establish target-server OS/resources.
- Managed environment became running/connected; network policy reported **enforced, restricted**, VPN false. Read `/etc/codex/network-policy.json`; official Mizito hosts and GitHub/raw/package hosts were allowed. Actual HTTPS help/font requests and remote Git fetch succeeded. No secrets/environment credential values were read or printed. BeautifulSoup was absent; standard-library parsing was used without installing dependencies.
- Available GitHub connector returned repository access and default branch `main`. CLI Git read access succeeded. Publication results are recorded below only after actual operations.

## Research completed and limitations

Retrieved 14 official help category pages, 114 article/navigation URLs including additional guest documentation, marketing/pricing and five listed release notes. Read tutorial landing text and linked sources; video playback unavailable/unverified. Chromium opened the actual office login form only. No account, paid plan or authenticated resource was accessed. Public docs and directly observed login are distinguished throughout the source register.

Phase 0 deliverables: the requested ten Markdown files, including 87 stable requirement records with sources/date/evidence, roles/preconditions/flows, fields/transitions, edges, acceptance criteria, questions and proposed delivery phases. Documentation is English; owner reports are Persian. Font RD v33.003 binary availability and OFL license verified in scratch only; no font bundled.

## Decisions versus proposals

**Owner requirements:** complete web parity target, independent brand/assets, Debian, Persian/RTL/BiDi/Jalali/Vazirmatn RD, native apps excluded, Phase 0 only and no merge.

**Owner decision, 2026-11-03:** Django/DRF + React/TypeScript with Vite + PostgreSQL, as a modular monolith. Channels and Celery/Redis are planned components introduced only when an implemented slice requires them. This approves neither every architecture detail nor implementation in this follow-up.

**Still proposals/unresolved:** dependency versions (verify official support/compatibility during implementation), schema/API details, RLS, outbox, storage/search, production topology, commercial billing/subscription/quotas, hardware/load and recovery objectives. Advanced functional scope is retained independently of commercial policy. Development setup and acceptance are specified in P1A-SPEC.md, not implemented.

## Checks and publication

Historical Phase 0 audit passed: exactly ten Markdown documents, 87 unique requirements with required fields, all 87 phase allocations, 114 source anchors/mappings, 24 valid question IDs and working local links/anchors. All recorded source HTTP receipts were checked as 200. Manual review reconciled major plan/version and privacy conflicts. Full staged whitespace check passed. Discovery commit `95a5d2cdab516e73b461316bea24f856d063f42a` was pushed successfully on `docs/phase-0-discovery`. Draft [PR #1](https://github.com/avds2/miz-e-kar/pull/1) is open against `main`, unmerged. A documentation follow-up records publication and final edge-case review; resolve the final branch head with `git rev-parse HEAD`. Application/unit/integration tests are not applicable because no application exists. The reference login browser inspection is not an application acceptance test and proves no authenticated parity.

## Phase 0.1 inspection and changes

Before editing: branch `docs/phase-0-discovery`, local and remote head both `ceb0dbb38c01e0ec939185fe1aba668a4df30610`, clean working tree and zero divergence after explicit fetch. `main` remained `a2f4f8fe0e6da2a5c3808b0c5ef7b974ce1e015c`; PR #1 was open/draft/unmerged at the same head. No concurrent changes were present at inspection; preserve any new work encountered before publishing.

Rechecked only H042/H065/H067/H069/H114 (all HTTP 200), plus reread H024's existing capture. Q06a documents task-project affiliation; Q06b keeps category relationship unresolved; Q06c documents assigned-guest nonmember access with exact visibility still unknown. No source establishes projectless tasks from guest nonmembership. No authenticated reference observation was added.

P1 now has bounded slices P1a–P1h. Added one specification, P1A-SPEC.md, with eight planned slice AC IDs and parent-subset mappings. All 87 parent requirement IDs and all P2–P7 allocations remain; no parent or slice is implemented/accepted. Q06 is a legacy grouping with three child questions, not a combined prerequisite. All question gates are classified by earliest affected action/slice. P1a has no owner-recording blocker; version/tool verification is implementation preflight.

Phase 0.1 validation results are recorded in HANDOFF.md. The documentation follow-up belongs on the existing PR branch; Git history supplies its final commit identifier. No application scaffold, dependency installation, code, migration or deployment was performed.

## Next task and retained scope

Under a separate implementation task, implement only [P1a](P1A-SPEC.md): reproducible backend/frontend/PostgreSQL setup, local RD/Persian RTL shell, synthetic-account session login/logout and membership-isolated workspace selection with real persistence/migrations. Prove eight slice criteria with meaningful PostgreSQL tests and two-user/two-workspace browser/direct-API/reload evidence. Broad parents remain partial/open even after that subset passes.

No need to wait for Q04 final approval, Q05 meetings, Q06b category modeling, Q06c guest task visibility, Q12 commercial policy or Q22 finance to start P1a. Keep those questions open for their affected slices. Registration/SMS/recovery/invitations, project/task flows and all later modules remain in the complete parity backlog. Before P1b, request only its regular-member management evidence.
