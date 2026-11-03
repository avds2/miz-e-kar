# Roadmap

**Proposed sequence; no implementation authorized by Phase 0.** Scope remains all 87 requirements, plus any newly evidenced web capability. Dates, staffing and effort are deliberately unset until baseline/access/team/scale decisions are answered. Dependencies describe order, not permission to proceed.

## Phase 0 — evidence and planning (this PR)

Inspect and preserve the repository; research accessible official sources; record requirements, conflicts and unknowns; compare architecture; create project records and reviewable branch/PR. Stop before scaffolding, dependency installation, application implementation or deployment.

Next bounded task: obtain Q01/Q04 and core Q02 evidence, settle Q06 task/category/guest exceptions, and record owner architecture choice. Then a separately authorized P1 slice can begin. Do not wait for all distant-module evidence to design the initial policy boundaries.

## Incremental end-to-end deliveries

Each phase is a milestone composed of bounded PRs, not one giant change. Its requirements can start small and finish later **inside the named milestone**; the matrix must retain all unfinished criteria. Foundation requirements apply to every later flow (e.g., P5 files/notifications inherit P1 security and P3 search). No temporary UI is evidence of behavioral completion.

## P1 — Working core and isolation

Create account/workspace → invite/accept member → create project → assign task → recipient sees it → completes → creator sees result. Include Persian/Jalali/RD foundations, private attachment path, core notifications and negative workspace/role checks. This is the first working slice, not a scope cap.

Dependencies: owner stack decision and verified core policy/data relationships. Use real persistence and two identities; provider-independent adapters may use explicit local test delivery, but that is not accepted SMS/email parity.

Allocated requirements (exhaustive):

- [MK-LOC-001](PARITY-MATRIX.md#mk-loc-001) — Persian browser experience.
- [MK-LOC-002](PARITY-MATRIX.md#mk-loc-002) — Jalali dates and time semantics.
- [MK-LOC-003](PARITY-MATRIX.md#mk-loc-003) — Vazirmatn RD and independent assets.
- [MK-AUTH-001](PARITY-MATRIX.md#mk-auth-001) — Registration and workspace onboarding.
- [MK-AUTH-002](PARITY-MATRIX.md#mk-auth-002) — Login and password recovery.
- [MK-WS-001](PARITY-MATRIX.md#mk-ws-001) — Independent workspaces and switching.
- [MK-WS-003](PARITY-MATRIX.md#mk-ws-003) — Membership invitation, removal and restoration.
- [MK-WS-006](PARITY-MATRIX.md#mk-ws-006) — Feature grants and privacy policy.
- [MK-WS-009](PARITY-MATRIX.md#mk-ws-009) — Dashboard and navigation.
- [MK-PR-001](PARITY-MATRIX.md#mk-pr-001) — Project creation and associated task category.
- [MK-PR-005](PARITY-MATRIX.md#mk-pr-005) — Project task list, filters and output.
- [MK-TA-001](PARITY-MATRIX.md#mk-ta-001) — Create task from all documented contexts.
- [MK-TA-004](PARITY-MATRIX.md#mk-ta-004) — Task completion and partial progress.
- [MK-TA-014](PARITY-MATRIX.md#mk-ta-014) — Personal task trays and daily completions.
- [MK-SYS-001](PARITY-MATRIX.md#mk-sys-001) — Private attachments and aggregate file views.
- [MK-SYS-003](PARITY-MATRIX.md#mk-sys-003) — Notifications, history and muting.
- [MK-OPS-002](PARITY-MATRIX.md#mk-ops-002) — Cross-cutting authorization and durable live updates.

Exit evidence: linked requirement-to-test results, relevant multi-user browser scenarios, persistent reload and negative authorization checks; record all skipped checks and open gaps. No phase is accepted solely from unit tests or a mock screen; update matrix/state/handoff before ending each slice.

## P2 — Task and project rules

Deliver shared/unassigned/final-approved/reopened/recurring tasks, checklists, deadlines/weights/templates, personal/team calendar, board and archive/recovery with policy controls. Complete guest and account security flows.

Dependencies: P1 persistence/access/event contracts and the preceding relevant modules; research the pending questions for this milestone before implementing its rules.

Allocated requirements (exhaustive):

- [MK-AUTH-003](PARITY-MATRIX.md#mk-auth-003) — Account security, sessions and email verification.
- [MK-WS-002](PARITY-MATRIX.md#mk-ws-002) — Workspace settings, ownership and deletion.
- [MK-WS-004](PARITY-MATRIX.md#mk-ws-004) — Guest entry and identity restrictions.
- [MK-WS-005](PARITY-MATRIX.md#mk-ws-005) — Guest module exceptions.
- [MK-PR-002](PARITY-MATRIX.md#mk-pr-002) — Basic project settings and pinning.
- [MK-PR-003](PARITY-MATRIX.md#mk-pr-003) — Advanced project policies and audit.
- [MK-PR-004](PARITY-MATRIX.md#mk-pr-004) — Project grouping.
- [MK-PR-006](PARITY-MATRIX.md#mk-pr-006) — Board columns and templates.
- [MK-PR-007](PARITY-MATRIX.md#mk-pr-007) — Board task movement and completion retention.
- [MK-PR-008](PARITY-MATRIX.md#mk-pr-008) — Project badges and progress.
- [MK-PR-009](PARITY-MATRIX.md#mk-pr-009) — Project archive and recovery modes.
- [MK-TA-002](PARITY-MATRIX.md#mk-ta-002) — Task reports, replies and mentions.
- [MK-TA-003](PARITY-MATRIX.md#mk-ta-003) — Edit, delete and restore task.
- [MK-TA-005](PARITY-MATRIX.md#mk-ta-005) — Shared task and no-assignee behavior.
- [MK-TA-006](PARITY-MATRIX.md#mk-ta-006) — Final approval workflow.
- [MK-TA-007](PARITY-MATRIX.md#mk-ta-007) — Reopen completed task.
- [MK-TA-008](PARITY-MATRIX.md#mk-ta-008) — Reminder, start, deadline and overdue calculation.
- [MK-TA-009](PARITY-MATRIX.md#mk-ta-009) — Checklist completion provenance.
- [MK-TA-010](PARITY-MATRIX.md#mk-ta-010) — Weighted and partial progress calculation.
- [MK-TA-011](PARITY-MATRIX.md#mk-ta-011) — Recurring tasks and calendar projections.
- [MK-TA-012](PARITY-MATRIX.md#mk-ta-012) — Task templates.
- [MK-TA-013](PARITY-MATRIX.md#mk-ta-013) — Copying tasks and shareable links.
- [MK-TA-015](PARITY-MATRIX.md#mk-ta-015) — Personal and team work calendar.
- [MK-TA-016](PARITY-MATRIX.md#mk-ta-016) — Task views, history, transfer and printing.

Exit evidence: linked requirement-to-test results, relevant multi-user browser scenarios, persistent reload and negative authorization checks; record all skipped checks and open gaps. No phase is accepted solely from unit tests or a mock screen; update matrix/state/handoff before ending each slice.

## P3 — Communication and personal productivity

Deliver private/group/channel conversations, receipts and read-locked edits, media/voice, assistant/mentions, polls/quizzes/templates, notes/privacy/purge, search/bookmarks and appearance.

Dependencies: P1 persistence/access/event contracts and the preceding relevant modules; research the pending questions for this milestone before implementing its rules.

Allocated requirements (exhaustive):

- [MK-AUTH-004](PARITY-MATRIX.md#mk-auth-004) — Personal profile and appearance.
- [MK-CH-001](PARITY-MATRIX.md#mk-ch-001) — Conversation directory and private messaging.
- [MK-CH-002](PARITY-MATRIX.md#mk-ch-002) — Groups and channels.
- [MK-CH-003](PARITY-MATRIX.md#mk-ch-003) — Message editing, deleting and receipts.
- [MK-CH-004](PARITY-MATRIX.md#mk-ch-004) — Media and voice messages.
- [MK-CH-005](PARITY-MATRIX.md#mk-ch-005) — Conversation filters and message location.
- [MK-CH-006](PARITY-MATRIX.md#mk-ch-006) — Assistant inbox, commands and mentions.
- [MK-CH-007](PARITY-MATRIX.md#mk-ch-007) — Polls, confidentiality and quiz modes.
- [MK-CH-008](PARITY-MATRIX.md#mk-ch-008) — Poll lifecycle and templates.
- [MK-NO-001](PARITY-MATRIX.md#mk-no-001) — Personal notes and privacy.
- [MK-NO-002](PARITY-MATRIX.md#mk-no-002) — Notes filters and lifecycle.
- [MK-SYS-002](PARITY-MATRIX.md#mk-sys-002) — Workspace search and bookmarks.

Exit evidence: linked requirement-to-test results, relevant multi-user browser scenarios, persistent reload and negative authorization checks; record all skipped checks and open gaps. No phase is accepted solely from unit tests or a mock screen; update matrix/state/handoff before ending each slice.

## P4 — Scheduling and formal meetings

Deliver Gantt phases/dependencies/view delegation/printing and simple/organizational minutes, signatures/quorum, templates and resolution dispatch. Retain unresolved behaviors until evidence settles them.

Dependencies: P1 persistence/access/event contracts and the preceding relevant modules; research the pending questions for this milestone before implementing its rules.

Allocated requirements (exhaustive):

- [MK-ME-001](PARITY-MATRIX.md#mk-me-001) — Simple meeting minutes.
- [MK-ME-002](PARITY-MATRIX.md#mk-me-002) — Organizational minutes lifecycle.
- [MK-ME-003](PARITY-MATRIX.md#mk-me-003) — Minutes signatures and resolution dispatch.
- [MK-ME-004](PARITY-MATRIX.md#mk-me-004) — Minutes templates.
- [MK-GA-001](PARITY-MATRIX.md#mk-ga-001) — Gantt structure and phases.
- [MK-GA-002](PARITY-MATRIX.md#mk-ga-002) — Dependencies and successor notices.
- [MK-GA-003](PARITY-MATRIX.md#mk-ga-003) — Gantt interaction, view grants and print.

Exit evidence: linked requirement-to-test results, relevant multi-user browser scenarios, persistent reload and negative authorization checks; record all skipped checks and open gaps. No phase is accepted solely from unit tests or a mock screen; update matrix/state/handoff before ending each slice.

## P5 — Customer, sales, finance and correspondence

Deliver customer/representative/call → follow-up task flow, opportunity/forecast, money record/report, letter/paraph/registry/customer link. Keep financial and private-letter access boundaries distinct.

Dependencies: P1 persistence/access/event contracts and the preceding relevant modules; research the pending questions for this milestone before implementing its rules.

Allocated requirements (exhaustive):

- [MK-CR-001](PARITY-MATRIX.md#mk-cr-001) — Customer record identity and representatives.
- [MK-CR-002](PARITY-MATRIX.md#mk-cr-002) — Customer resource access and recovery.
- [MK-CR-003](PARITY-MATRIX.md#mk-cr-003) — Customer activity, call reports and follow-ups.
- [MK-CR-004](PARITY-MATRIX.md#mk-cr-004) — Customer tags, filtering, pins and output.
- [MK-CR-006](PARITY-MATRIX.md#mk-cr-006) — Financial records and lifecycle.
- [MK-CR-007](PARITY-MATRIX.md#mk-cr-007) — Sales opportunities.
- [MK-CR-008](PARITY-MATRIX.md#mk-cr-008) — Financial monitoring and arrears dashboard.
- [MK-CR-009](PARITY-MATRIX.md#mk-cr-009) — Sales forecasting and monitoring.
- [MK-LE-001](PARITY-MATRIX.md#mk-le-001) — Letters and personal trays.
- [MK-LE-002](PARITY-MATRIX.md#mk-le-002) — Paraphs, forwarding, receipts and archive.
- [MK-LE-003](PARITY-MATRIX.md#mk-le-003) — Secretariat registration and numbering.
- [MK-LE-004](PARITY-MATRIX.md#mk-le-004) — Read-dependent letter and paraph deletion.
- [MK-LE-005](PARITY-MATRIX.md#mk-le-005) — Customer-linked letters preserve privacy.

Exit evidence: linked requirement-to-test results, relevant multi-user browser scenarios, persistent reload and negative authorization checks; record all skipped checks and open gaps. No phase is accepted solely from unit tests or a mock screen; update matrix/state/handoff before ending each slice.

## P6 — Administration, imports and full reporting

Deliver owner repair/substitution, copying/imports, all monitoring and presence, commercial entitlement decisions, online meetings/screen share and additional authenticated surfaces.

Dependencies: P1 persistence/access/event contracts and the preceding relevant modules; research the pending questions for this milestone before implementing its rules.

Allocated requirements (exhaustive):

- [MK-WS-007](PARITY-MATRIX.md#mk-ws-007) — Owner bulk access repair and substitution.
- [MK-WS-008](PARITY-MATRIX.md#mk-ws-008) — Plan, capacity and subscription administration.
- [MK-PR-010](PARITY-MATRIX.md#mk-pr-010) — Project copying.
- [MK-RT-001](PARITY-MATRIX.md#mk-rt-001) — Online meetings and screen sharing.
- [MK-CR-005](PARITY-MATRIX.md#mk-cr-005) — Customer Excel import.
- [MK-MON-001](PARITY-MATRIX.md#mk-mon-001) — Workspace monitoring overview.
- [MK-MON-002](PARITY-MATRIX.md#mk-mon-002) — Project monitoring.
- [MK-MON-003](PARITY-MATRIX.md#mk-mon-003) — Task monitoring.
- [MK-MON-004](PARITY-MATRIX.md#mk-mon-004) — Customer monitoring.
- [MK-MON-005](PARITY-MATRIX.md#mk-mon-005) — Organizational minutes monitoring.
- [MK-MON-006](PARITY-MATRIX.md#mk-mon-006) — Member analytics and workspace presence.
- [MK-SYS-004](PARITY-MATRIX.md#mk-sys-004) — Task/project imports.
- [MK-SYS-005](PARITY-MATRIX.md#mk-sys-005) — Forms and additional reference surfaces.

Exit evidence: linked requirement-to-test results, relevant multi-user browser scenarios, persistent reload and negative authorization checks; record all skipped checks and open gaps. No phase is accepted solely from unit tests or a mock screen; update matrix/state/handoff before ending each slice.

## P7 — Production qualification and parity reconciliation

Rehearse clean Debian deployment/upgrades/backup/restore; measure representative load and resource limits; reconcile every requirement against current authenticated evidence and browser behavior. No blanket parity sign-off for unresolved or untested criteria.

Dependencies: P1 persistence/access/event contracts and the preceding relevant modules; research the pending questions for this milestone before implementing its rules.

Allocated requirements (exhaustive):

- [MK-OPS-001](PARITY-MATRIX.md#mk-ops-001) — Debian production operation and recovery.

Exit evidence: linked requirement-to-test results, relevant multi-user browser scenarios, persistent reload and negative authorization checks; record all skipped checks and open gaps. Also demonstrate migration failure recovery, attachment-consistent restore, job replay safety and measured operational limits. Complete parity requires closure of every criterion and current reference comparison.

## Scope retention and change rules

- Preserve requirement IDs and all remaining backlog entries after every delivery. Split into child requirements where criteria become too broad; carry parent traceability forward.
- An unavailable paid feature remains a named evidence/implementation gap. Do not replace it with a simpler feature and call it parity.
- Deliberate changes such as secure guest activation, billing treatment or signature semantics need explicit owner decisions and a recorded parity difference. Proposals do not become decisions automatically.
- Before final acceptance, repeat discovery against the chosen plan/build, inspect extra menus and reconcile release differences. A public-document inventory cannot alone establish comprehensive runtime parity.
