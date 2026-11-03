# Project state

Updated: **2026-11-03**. Current stage: **Phase 0, documentation and discovery**. No application implementation, framework scaffold, dependency installation, schema migration or deployment exists. All 87 parity requirements are not implemented; all proposed acceptance tests are uncreated/unrun.

## Inspected repository and environment

- Repository: `avds2/miz-e-kar`, public; origin `https://github.com/avds2/miz-e-kar.git`.
- Local checkout initially had an unborn `work` branch, no tracked files and no local commits. Remote inspection found `main` at `a2f4f8fe0e6da2a5c3808b0c5ef7b974ce1e015c` (one-line README, first commit). Fetched `main` explicitly because the existing fetch refspec selected only HEAD. Created `docs/phase-0-discovery` from that remote commit; preserved the original README heading and expanded it. No existing application or AGENTS.md was found in the project checkout.
- Research executor: Debian GNU/Linux 13 (trixie), Git 2.52.0, gh 2.46.0, Python 3.12.14, Node 24.22.1, system Chromium 155 and existing Playwright module available. This does not establish target-server OS/resources.
- Managed environment became running/connected; network policy reported **enforced, restricted**, VPN false. Read `/etc/codex/network-policy.json`; official Mizito hosts and GitHub/raw/package hosts were allowed. Actual HTTPS help/font requests and remote Git fetch succeeded. No secrets/environment credential values were read or printed. BeautifulSoup was absent; standard-library parsing was used without installing dependencies.
- Available GitHub connector returned repository access and default branch `main`. CLI Git read access succeeded. Publication results are recorded below only after actual operations.

## Research completed and limitations

Retrieved 14 official help category pages, 114 article/navigation URLs including additional guest documentation, marketing/pricing and five listed release notes. Read tutorial landing text and linked sources; video playback unavailable/unverified. Chromium opened the actual office login form only. No account, paid plan or authenticated resource was accessed. Public docs and directly observed login are distinguished throughout the source register.

Deliverables: the requested ten Markdown files, including 87 stable requirement records with sources/date/evidence, roles/preconditions/flows, fields/transitions, edges, acceptance criteria, questions and proposed delivery phases. Documentation is English; owner reports are Persian. Font RD v33.003 binary availability and OFL license verified in scratch only; no font bundled.

## Decisions versus proposals

**Owner requirements:** complete web parity target, independent brand/assets, Debian, Persian/RTL/BiDi/Jalali/Vazirmatn RD, native apps excluded, Phase 0 only and no merge.

**Proposals only:** Django/DRF + React/TypeScript modular monolith, PostgreSQL, Channels, Celery/Redis; private local file storage; Compose deployment; RLS defense in depth; phases P1–P7. No stack or commercial policy has been approved. No target scale/hardware/RPO/RTO is assumed.

## Checks and publication

Document audit passed: exactly ten Markdown documents, 87 unique requirements with required fields, all 87 phase allocations, 114 source anchors/mappings, 24 valid question IDs and working local links/anchors. All recorded source HTTP receipts were checked as 200. Manual review reconciled major plan/version and privacy conflicts. Publication is pending; see HANDOFF.md for the latest verified results. Application/unit/integration tests are not applicable because no application exists. The reference login browser inspection is not an application acceptance test and proves no authenticated parity.

## Next task and retained scope

Obtain the minimal Q01/Q04/core Q02 reference capture, clarify Q06 data/access exceptions, and record the owner's architecture decision in a bounded discovery follow-up. Then request/receive a new implementation instruction for the P1 core slice. All P2–P7 features remain in the parity matrix and roadmap; unobserved advanced behavior remains explicit, not silently removed.
