# Engineering instructions

## Start and bound the work

1. Read `docs/PROJECT-STATE.md`, `docs/HANDOFF.md`, `docs/OPEN-QUESTIONS.md`, and the applicable requirements in `docs/PARITY-MATRIX.md` before every task. Inspect branch, status, existing instructions and current files; preserve unrelated work.
2. Work in a bounded end-to-end slice. State the requirement IDs and acceptance criteria included, dependencies, and the remaining scope. An early core delivery never replaces the comprehensive web parity backlog.
3. Phase 0 authorizes documentation and research only. Do not scaffold, install a stack, implement application code or deploy during Phase 0. Architecture and roadmap choices remain proposals until explicitly accepted in a later task. Do not interpret PR merge as stack approval unless the owner says so.

## Evidence and traceability

- Keep repository documents, identifiers and technical work in English; report to the owner in Persian.
- Distinguish documented, directly observed, inferred and unknown behavior. Cite exact official URLs, access date, plan/version context and observation method. Never promote documentation, a screenshot or an inference into an executed reference test.
- Preserve stable requirement IDs. Split requirements with child IDs when necessary and retain the parent mapping. Trace each implemented criterion to test IDs and browser scenarios, file paths, execution results and remaining gaps. Planned test names are not existing tests.
- Inspect relevant release notes and source conflicts before defining a rule. Track unresolved behavior and plan gates explicitly. Do not silently choose a convenient interpretation of conflicting permissions.
- Implement independently. Do not copy Mizito proprietary source, scripts, logos, screenshots, icons, backgrounds or other brand assets into the product. Verify third-party licenses and pin provenance before bundling, including Vazirmatn RD.

## Correctness and acceptance

- Enforce authorization server-side for reads, writes, downloads, searches, reports, exports, jobs and real-time subscriptions. Test workspace isolation and resource permissions using owner, admin, member, guest, removed member and unrelated workspace identities as applicable.
- Test important business rules and transitions: shared-task completion, final approval, recurrence, archive/recovery, read-dependent edit/delete restrictions, minutes quorum, financial calculations and concurrent numbering. Include negative and concurrent cases where relevant; avoid tests that merely duplicate implementation.
- For relevant UI flows, perform browser-based acceptance checks against running software with realistic seeded data and at least two identities when permissions or real-time effects matter. Verify reload/persistence, Persian input, RTL/BiDi, keyboard use and Jalali boundaries. Record the tested commit, browser, scenario and result.
- A mock screen, a screenshot or passing unit tests cannot prove complete functionality or Mizito parity. Do not mark a requirement accepted while its business rules, authorization or browser criteria are untested.
- Report exactly what ran, failed, was skipped or was unavailable and why. Never claim browsing, tests, commits, pushes, deployments or parity without evidence. Do not bypass authentication or store credentials, passwords, OTPs or session recordings containing secrets in the repository.

## Before stopping

Update the parity matrix implementation/test status, open questions, project state and **handoff before stopping**, including files/branch, checks actually run, known failures, next bounded task and retained backlog. Keep proposals separate from approved decisions. Commit only scoped changes on a dedicated branch; open a reviewable PR when supported; do not merge without authorization.
