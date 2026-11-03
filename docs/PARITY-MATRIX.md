# Parity matrix

## Reading this register

All source access dates are **2026-11-03**, inherited by every record below. `[Hnnn]` links resolve to the exact official source URL at the end of this file and are described in [Reference sources](REFERENCE-SOURCES.md). OWNER means the owner's task mandate; OFFICE is the unauthenticated login observation; FONT is the upstream font verification. The date is the access date, not the source publication date.

D = documented; O = directly observed; I = inferred/proposed engineering behavior; U = unknown. **No authenticated reference behavior is directly observed.** D applies to stated behavior, not unstated actor/error details. “Actor” combines actor, permission and preconditions; “Flow” contains action and observable result; “Edges” includes unresolved error behavior and cross-module effects. Acceptance criteria (AC) are proposed checks. Unknown policies require evidence before accepting implementation.

**Every requirement is `Not implemented`; every test is `Planned, not created or run`.** These two fields apply to every record without exception. Stable test namespace: `TEST-<requirement-ID>-AC<n>`; split criteria into child IDs when implementing. Record actual test/browser paths, commit, results and remaining gaps here in future slices. Delivery phases are planned starting milestones, mapped in [Roadmap](ROADMAP.md); P1 foundations apply to every later phase. Broad parents span multiple slices and later module entry points. No item is deferred out of the full parity target.

## Phase 0.1 slice traceability

All **87 parent IDs and acceptance criteria remain in the backlog**. [P1a](P1A-SPEC.md) defines eight slice acceptance IDs, mapped to explicit parent subsets; these are not new parent requirements or claims of reference observation. Completing a subset never completes its parent. At implementation, append actual test paths/results to that mapping; nothing is implemented or tested yet.

P1a covers only locale/font display, synthetic session login/logout, workspace selection/membership isolation, PostgreSQL migrations/persistence and reproducible setup. Registration/SMS/recovery (MK-AUTH-001 and the remaining MK-AUTH-002 criteria), invitations, projects/tasks, files, notifications and realtime/job checks remain unfinished. Q06a/Q06b/Q06c, Q04, Q05, Q12 and Q22 do not block P1a. See [slice-specific question classification](OPEN-QUESTIONS.md).

## LOC

<a id="mk-loc-001"></a>

### MK-LOC-001 — Persian browser experience

Evidence: **D/I** · Sources: [OWNER] [H049] · Reference plan: All · Delivery: **P1**.

- **Actor / preconditions:** All permitted users; supported browser.
- **Flow / observable result:** Enter Persian and mixed Latin text across the working core; display and edit without directional corruption.
- **Fields / states / transitions:** Persian UI; RTL layout; BiDi isolation for identifiers, phone numbers, URLs and numbers.
- **Errors / edges / cross-effects:** Keyboard navigation, long text, narrow screens, print; later phases inherit this criterion.
- **Acceptance criteria:** AC1: Persian round-trip survives reload. AC2: mixed URL/phone content and keyboard focus remain usable in RTL.
- **Open questions:** Q08; unspecified validation, permission details and failures remain U.

<a id="mk-loc-002"></a>

### MK-LOC-002 — Jalali dates and time semantics

Evidence: **D/I** · Sources: [OWNER] [H049] [H073] · Reference plan: All; advanced due dates · Delivery: **P1**.

- **Actor / preconditions:** User permitted to schedule a task.
- **Flow / observable result:** Select a Jalali date/time; view the same intended local schedule in lists and calendars.
- **Fields / states / transitions:** Reminder, start, due, local date, timezone, recurrence. Proposed UTC instants and separate date-only values.
- **Errors / edges / cross-effects:** Leap Esfand, month-end, midnight and different client zones; Gregorian import dates.
- **Acceptance criteria:** AC1: Jalali/Gregorian round-trip works across year boundaries. AC2: no day shift for date-only values.
- **Open questions:** Q08; unspecified validation, permission details and failures remain U.

<a id="mk-loc-003"></a>

### MK-LOC-003 — Vazirmatn RD and independent assets

Evidence: **D/I** · Sources: [OWNER] [FONT] · Reference plan: All · Delivery: **P1**.

- **Actor / preconditions:** Maintainer preparing frontend assets.
- **Flow / observable result:** Use verified upstream RD files and independent product identity in a later implementation.
- **Fields / states / transitions:** v33.003; family Vazirmatn RD; OFL 1.1; provenance/checksum.
- **Errors / edges / cross-effects:** No Mizito assets; preserve font notices; recheck modified-font terms before modification.
- **Acceptance criteria:** AC1: deployed font is RD and loads without external CDN. AC2: license/provenance shipped with the selected files.
- **Open questions:** Q09; unspecified validation, permission details and failures remain U.

## AUTH

<a id="mk-auth-001"></a>

### MK-AUTH-001 — Registration and workspace onboarding

Evidence: **D** · Sources: [H004] · Reference plan: All · Delivery: **P1**.

- **Actor / preconditions:** Unauthenticated person with accessible mobile number.
- **Flow / observable result:** Submit number, verify SMS code, enter name/team/password confirmation and accept terms; account and workspace become available.
- **Fields / states / transitions:** OTP challenge, resend, expired code, profile name, workspace title.
- **Errors / edges / cross-effects:** Wrong number, delayed/expired code; actual expiry/rate limits unknown.
- **Acceptance criteria:** AC1: valid verified onboarding creates one owner workspace. AC2: invalid/expired code cannot create one.
- **Open questions:** Q10; unspecified validation, permission details and failures remain U.

<a id="mk-auth-002"></a>

### MK-AUTH-002 — Login and password recovery

Evidence: **D/O** · Sources: [H005] [H006] [OFFICE] · Reference plan: All · Delivery: **P1**.

- **Actor / preconditions:** Registered person; valid credentials or verified recovery challenge.
- **Flow / observable result:** Login with mobile/password; reset via SMS code when forgotten. Login form directly observed; success paths documented only.
- **Fields / states / transitions:** Phone, password, reset code; temporary login restriction after failures.
- **Errors / edges / cross-effects:** Help says restriction lasts at least one hour; exact threshold/reset session effects unknown.
- **Acceptance criteria:** AC1: valid login and recovery restore access. AC2: bad credentials/code do not authenticate; restriction/resend are testable.
- **Open questions:** Q10; unspecified validation, permission details and failures remain U.

<a id="mk-auth-003"></a>

### MK-AUTH-003 — Account security, sessions and email verification

Evidence: **D** · Sources: [H030] · Reference plan: Both documented · Delivery: **P2**.

- **Actor / preconditions:** Account holder; current password where requested.
- **Flow / observable result:** Change password/phone, enable SMS second factor, verify email for notices; inspect/revoke one or all other sessions.
- **Fields / states / transitions:** Old/new phone, verification code, password confirmation, successful/failed login history.
- **Errors / edges / cross-effects:** Revoked session must lose protected access; provider failure/recovery needs specification.
- **Acceptance criteria:** AC1: phone change requires current password and new-number verification. AC2: revoked sessions fail next protected request. AC3: failed/successful logins are visible.
- **Open questions:** Q10; unspecified validation, permission details and failures remain U.

<a id="mk-auth-004"></a>

### MK-AUTH-004 — Personal profile and appearance

Evidence: **D** · Sources: [H030] [H024] · Reference plan: Both; status/job title advanced per pricing · Delivery: **P3**.

- **Actor / preconditions:** Account holder; workspace role for job title assignment.
- **Flow / observable result:** Edit name/avatar/birthday; select light/dark/system and independently sourced background; set personal status.
- **Fields / states / transitions:** Profile, birthday marker, status text/color, theme preference.
- **Errors / edges / cross-effects:** Birthday shown across member workspaces; no reference background images copied.
- **Acceptance criteria:** AC1: profile/theme persist. AC2: birthday/status respect member visibility and guest identity rules.
- **Open questions:** Q08; unspecified validation, permission details and failures remain U.

## WS

<a id="mk-ws-001"></a>

### MK-WS-001 — Independent workspaces and switching

Evidence: **D** · Sources: [H025] [H004] · Reference plan: All · Delivery: **P1**.

- **Actor / preconditions:** Authenticated owner/member of selected workspace.
- **Flow / observable result:** Create another workspace or switch among owned/joined workspaces; all resource context follows selection.
- **Fields / states / transitions:** Workspace, membership, active context.
- **Errors / edges / cross-effects:** No cross-workspace relationships documented; user profile may span workspaces.
- **Acceptance criteria:** AC1: switching changes visible projects/tasks. AC2: forged IDs from another workspace fail reads and writes.
- **Open questions:** Q11; unspecified validation, permission details and failures remain U.

<a id="mk-ws-002"></a>

### MK-WS-002 — Workspace settings, ownership and deletion

Evidence: **D** · Sources: [H026] · Reference plan: Both documented · Delivery: **P2**.

- **Actor / preconditions:** Owner/admin for general settings; only owner for transfer; recipient already admin.
- **Flow / observable result:** Edit title/activity; inspect storage/plan; owner transfers to existing admin; free never-paid workspaces expose a deletion option.
- **Fields / states / transitions:** Title, activity sector, owner, storage; free/previously-paid flag; deletion lifecycle unknown.
- **Errors / edges / cross-effects:** No data loss on transfer; concurrent transfer/removal and rollback unknown.
- **Acceptance criteria:** AC1: member cannot edit settings. AC2: non-admin target rejected; after transfer exactly one owner remains. AC3: deletion option follows free/never-paid eligibility; deletion actor and recovery require evidence.
- **Open questions:** Q02; unspecified validation, permission details and failures remain U.

<a id="mk-ws-003"></a>

### MK-WS-003 — Membership invitation, removal and restoration

Evidence: **D** · Sources: [H027] · Reference plan: Both; guest advanced · Delivery: **P1**.

- **Actor / preconditions:** Owner/admin; workspace invitation capacity available.
- **Flow / observable result:** Invite phone number; resend/cancel pending invitation; set role/job title; remove and restore members.
- **Fields / states / transitions:** Pending/accepted/removed; admin/member role; title; member and guest capacity.
- **Errors / edges / cross-effects:** Existing accounts receive in-app invitation; removal keeps history; restoration restores prior tasks/projects.
- **Acceptance criteria:** AC1: pending invitation can be canceled. AC2: removed user immediately loses access without deleting history; restoration is verified.
- **Open questions:** Q02; unspecified validation, permission details and failures remain U.

<a id="mk-ws-004"></a>

### MK-WS-004 — Guest entry and identity restrictions

Evidence: **D** · Sources: [H012] [H110] [H112] [H113] · Reference plan: Advanced · Delivery: **P2**.

- **Actor / preconditions:** Owner/admin invites guest; named regular members placed in guest visibility list.
- **Flow / observable result:** Guest accepts invitation and participates only within allowed resources; ordinary identities hidden unless explicitly introduced.
- **Fields / states / transitions:** Guest membership; visible-member list; invite status.
- **Errors / edges / cross-effects:** No monitoring/print; no group/channel creation; invitation transport for new users is documented with credentials, requiring independent security design review.
- **Acceptance criteria:** AC1: guest cannot enumerate hidden identities or monitoring. AC2: changing visibility grants changes rendered identities.
- **Open questions:** Q02 Q10; unspecified validation, permission details and failures remain U.

<a id="mk-ws-005"></a>

### MK-WS-005 — Guest module exceptions

Evidence: **D** · Sources: [H111] [H114] [H065] · Reference plan: Advanced · Delivery: **P2**.

- **Actor / preconditions:** Guest with per-resource membership/grants.
- **Flow / observable result:** Collaborate in invited projects/customer records, receive assigned tasks/letters, use personal notes.
- **Fields / states / transitions:** Guest can receive a project-associated task without project membership (H065/H114; exact access details U); CRM/sales/finance grants; no label creation anywhere or labels on notes; no message details/edit/forward/seen-list/copy/share controls.
- **Errors / edges / cross-effects:** No private chats with guests even for owner; guest cannot create customers; guest activity can be monitored by authorized managers.
- **Acceptance criteria:** AC1: guest DM and print routes deny access. AC2: assigned task is accessible without exposing the project. AC3: message-metadata/edit/forward/share and label actions unavailable. Guest letters preserve hidden sender identity unless introduced.
- **Open questions:** Q02 Q06a Q06c; unspecified validation, permission details and failures remain U.

<a id="mk-ws-006"></a>

### MK-WS-006 — Feature grants and privacy policy

Evidence: **D** · Sources: [H029] [H012] · Reference plan: Base + advanced policy controls · Delivery: **P1**.

- **Actor / preconditions:** Owner/admin configures grants; active membership required.
- **Flow / observable result:** Configure creation, CRM visibility/print/sales/finance, monitoring, guest-visible identities and secretariat access.
- **Fields / states / transitions:** Workspace grant plus resource role/membership; hide latest-task activity in coworker list.
- **Errors / edges / cross-effects:** Private chats, personal note content and unnumbered letters remain private from broad admin privileges.
- **Acceptance criteria:** AC1: deny via API as well as UI. AC2: search/export/realtime do not leak protected content. AC3: coworker hiding removes task details.
- **Open questions:** Q02; unspecified validation, permission details and failures remain U.

<a id="mk-ws-007"></a>

### MK-WS-007 — Owner bulk access repair and substitution

Evidence: **D** · Sources: [H031] [H012] · Reference plan: Advanced per pricing · Delivery: **P6**.

- **Actor / preconditions:** Workspace owner exclusively; selected source/target members and resources.
- **Flow / observable result:** Bulk grant/revoke CRM/project/group access for multiple users; filter by archived state/grouping; restore resources; substitute departed worker.
- **Fields / states / transitions:** Selected projects/groups/customers; incomplete tasks; old/new member.
- **Errors / edges / cross-effects:** Content/history retained; restored groups need members added again; historical release calls this admin access, current role article says owner.
- **Acceptance criteria:** AC1: admin/member attempts denied. AC2: selected incomplete tasks/access move without rewriting prior authorship.
- **Open questions:** Q02 Q07; unspecified validation, permission details and failures remain U.

<a id="mk-ws-008"></a>

### MK-WS-008 — Plan, capacity and subscription administration

Evidence: **D** · Sources: [H028] [H026] [PRICE] · Reference plan: Free/base/advanced reference variants · Delivery: **P6**.

- **Actor / preconditions:** Owner/admin; workspace context.
- **Flow / observable result:** Inspect current plan/remaining term and capacity; request trial, upgrade/renew and invoice/payment flow.
- **Fields / states / transitions:** Trial seven days; activity-sector gift 15 days; free five users/150 MB; CRM base 2,000 vs advanced 10,000; expiry/invoice/discount/payment status.
- **Errors / edges / cross-effects:** Advanced-to-base downgrade timing documented; provider/account/proration and self-host commercial model unresolved. No payment purchase attempted.
- **Acceptance criteria:** AC1: plan transition retains data. AC2: capacity denial is explicit and consistent server-side. AC3: failed/unconfirmed payment cannot activate entitlement.
- **Open questions:** Q12; unspecified validation, permission details and failures remain U.

<a id="mk-ws-009"></a>

### MK-WS-009 — Dashboard and navigation

Evidence: **D** · Sources: [H025] [H013] [H024] [H108] · Reference plan: All; privileged panels gated · Delivery: **P1**.

- **Actor / preconditions:** Active workspace member; dashboard metrics require matching grants.
- **Flow / observable result:** Open my work/follow-ups, coworkers, project progress, help/support links and financial arrears panel when authorized.
- **Fields / states / transitions:** Today/delayed/follow-up counts, latest work, online/status, project progress; hidden amount toggle.
- **Errors / edges / cross-effects:** Guest omitted from coworkers; note counts may be monitored but not content; independent support destination needed.
- **Acceptance criteria:** AC1: core task changes update correct counts. AC2: guest/unauthorized identities see no privileged panel or hidden activity.
- **Open questions:** Q13; unspecified validation, permission details and failures remain U.

## PR

<a id="mk-pr-001"></a>

### MK-PR-001 — Project creation and associated task category

Evidence: **D** · Sources: [H041] [H042] [H008] [H065] [H114] · Reference plan: All; advanced creation policy · Delivery: **P1**.

- **Actor / preconditions:** Member permitted to create projects; selected workspace users/guests.
- **Flow / observable result:** Set title/color/avatar and members; create project and automatic task category.
- **Fields / states / transitions:** Project, resource membership/manager role, category, activity feed.
- **Errors / edges / cross-effects:** H065 documents project affiliation. H042 documents automatic category creation; category independence/cardinality remains Q06b. H114 is an access exception only, not projectless-task evidence.
- **Acceptance criteria:** AC1: project/category created atomically and visible after reload. AC2: user without creation grant cannot create through API.
- **Open questions:** Q06a Q06b; unspecified validation, permission details and failures remain U.

<a id="mk-pr-002"></a>

### MK-PR-002 — Basic project settings and pinning

Evidence: **D** · Sources: [H044] · Reference plan: Base; also advanced · Delivery: **P2**.

- **Actor / preconditions:** Project manager; exact member-removal actor disputed.
- **Flow / observable result:** Edit title/image/color, members/managers, grouping, notification preference and pin project.
- **Fields / states / transitions:** Project role, notification setting, pin; max three pins.
- **Errors / edges / cross-effects:** Owner-only archive recovery; workspace admins control group labels; creator-only rule conflicts with manager membership editing.
- **Acceptance criteria:** AC1: settings persist for allowed actor. AC2: fourth pin has explicit handling. AC3: denied member action cannot mutate settings.
- **Open questions:** Q02; unspecified validation, permission details and failures remain U.

<a id="mk-pr-003"></a>

### MK-PR-003 — Advanced project policies and audit

Evidence: **D** · Sources: [H045] [H024] · Reference plan: Advanced · Delivery: **P2**.

- **Actor / preconditions:** Project manager with advanced settings access.
- **Flow / observable result:** Toggle advanced mode; configure create/edit rights, reminder extension, deadlines, weights, board approval and monitoring delegates; review/save changes.
- **Fields / states / transitions:** Settings/task-template/modules tabs; Gantt and organizational minutes modules; settings history.
- **Errors / edges / cross-effects:** Policy changes must invalidate stale clients; disabling modules must not destroy data (proposed safeguard).
- **Acceptance criteria:** AC1: member restrictions enforced through every entry point. AC2: saved changes appear in settings audit.
- **Open questions:** Q02; unspecified validation, permission details and failures remain U.

<a id="mk-pr-004"></a>

### MK-PR-004 — Project grouping

Evidence: **D** · Sources: [H063] [H046] [H044] · Reference plan: Both · Delivery: **P2**.

- **Actor / preconditions:** Workspace admin creates/edits group names; project actor assigns existing groups as permitted.
- **Flow / observable result:** Assign project to one or more groups; select groups to filter project list and reports.
- **Fields / states / transitions:** Group title/color if evidenced later; project-group many-to-many; per-group counts.
- **Errors / edges / cross-effects:** Not the same as project conversation or task category; grouping affects bulk access/report filtering.
- **Acceptance criteria:** AC1: multi-group project appears under either matching group. AC2: ordinary actor cannot rename group titles.
- **Open questions:** Q06b; unspecified validation, permission details and failures remain U.

<a id="mk-pr-005"></a>

### MK-PR-005 — Project task list, filters and output

Evidence: **D** · Sources: [H047] [H022] · Reference plan: Both; some fields advanced · Delivery: **P1**.

- **Actor / preconditions:** Project viewer; create/print according to applicable grants.
- **Flow / observable result:** View mine/others/unassigned/done/delayed/timed/untimed; combine filters, sort and print table.
- **Fields / states / transitions:** Text, creator, assignee, status, tags, board list, customer, time range, form tracking number; created/updated/due/reminder sort.
- **Errors / edges / cross-effects:** Task attachments separate from conversation files; forms capability not established.
- **Acceptance criteria:** AC1: combined filters return correct fixtures. AC2: printed rows match authorized filtered results, including dates and delay.
- **Open questions:** Q06b Q14; unspecified validation, permission details and failures remain U.

<a id="mk-pr-006"></a>

### MK-PR-006 — Board columns and templates

Evidence: **D** · Sources: [H048] [H020] [PRICE] · Reference plan: Both · Delivery: **P2**.

- **Actor / preconditions:** Project member; manager for column sorting; other edit permissions need confirmation.
- **Flow / observable result:** Initialize columns from Kanban, departments, users, weekdays or custom; add/rename/color/remove columns; sort asc/desc.
- **Fields / states / transitions:** Column title, order, color; creation/reminder/update sorting.
- **Errors / edges / cross-effects:** Removing column is not evidence for deleting tasks; compact cards documented in pricing.
- **Acceptance criteria:** AC1: configured columns persist. AC2: column removal preserves original tasks. AC3: unauthorized column mutation fails.
- **Open questions:** Q02 Q07; unspecified validation, permission details and failures remain U.

<a id="mk-pr-007"></a>

### MK-PR-007 — Board task movement and completion retention

Evidence: **D** · Sources: [H048] [H045] · Reference plan: Both; manager retention advanced · Delivery: **P2**.

- **Actor / preconditions:** Permitted project actor; manager for completion approval.
- **Flow / observable result:** Create task in column, move cards, view column progress; retain completed cards until manager approval when configured.
- **Fields / states / transitions:** Column assignment/order independent from task status; chart toggle; completed-retained/removed-from-board.
- **Errors / edges / cross-effects:** Do not automatically complete by dropping into a Done-named column.
- **Acceptance criteria:** AC1: move changes column without completing task. AC2: manager-only retention release is enforced.
- **Open questions:** Q02; unspecified validation, permission details and failures remain U.

<a id="mk-pr-008"></a>

### MK-PR-008 — Project badges and progress

Evidence: **D** · Sources: [H051] [H043] [H072] · Reference plan: Both; weighted advanced · Delivery: **P2**.

- **Actor / preconditions:** Authorized project viewer; changes since their last visit.
- **Flow / observable result:** View unread-change badge, overall/mine/others and per-board progress with recent completion metrics.
- **Fields / states / transitions:** Done/delayed/timed/untimed; count/weighted calculation; per-user seen cursor.
- **Errors / edges / cross-effects:** No-task/zero-weight rounding undefined; unread cursor scope must be verified.
- **Acceptance criteria:** AC1: two users have independent unread counts. AC2: known weighted fixture gives expected partial/completed progress.
- **Open questions:** Q13; unspecified validation, permission details and failures remain U.

<a id="mk-pr-009"></a>

### MK-PR-009 — Project archive and recovery modes

Evidence: **D** · Sources: [H053] [H024] · Reference plan: Both; recovery owner · Delivery: **P2**.

- **Actor / preconditions:** Project manager archives; owner recovers.
- **Flow / observable result:** Choose project-only archive or archive plus remove tasks from trays; recover project or archived tasks independently.
- **Fields / states / transitions:** Active/archived project; task visibility/archive; memberships.
- **Errors / edges / cross-effects:** Project-only leaves tasks in personal trays while project access stops; article also asks that task statuses be settled.
- **Acceptance criteria:** AC1: both archive modes preserve history and differ in tray visibility. AC2: only owner can recover.
- **Open questions:** Q07; unspecified validation, permission details and failures remain U.

<a id="mk-pr-010"></a>

### MK-PR-010 — Project copying

Evidence: **D** · Sources: [H058] [H020] · Reference plan: Advanced · Delivery: **P6**.

- **Actor / preconditions:** Actor with project-copy permission, exact role to verify; access to source.
- **Flow / observable result:** Choose destination name and tasks; confirm; create separate project with settings/members/board/Gantt.
- **Fields / states / transitions:** Selected task set, copied phases/dependencies; new IDs.
- **Errors / edges / cross-effects:** Reports/history excluded; omitted tasks omitted from copied Gantt; failure/partial-copy behavior unknown.
- **Acceptance criteria:** AC1: source remains unchanged. AC2: copied tasks lack prior reports/history; excluded tasks absent in all views.
- **Open questions:** Q07 Q15; unspecified validation, permission details and failures remain U.

## TA

<a id="mk-ta-001"></a>

### MK-TA-001 — Create task from all documented contexts

Evidence: **D** · Sources: [H065] [H009] · Reference plan: Both; advanced fields gated · Delivery: **P1**.

- **Actor / preconditions:** Permitted task creator; existing project required in documented creation flow. A guest assignee can lack project membership; that does not remove task-project affiliation.
- **Flow / observable result:** Create through tray, project feed/list/board/calendar/Gantt, minutes, letter or customer; same task becomes visible in linked contexts.
- **Fields / states / transitions:** Title, description, tags, checklist, attachments, reminder, assignees, project, board; optional publish-to-feed.
- **Errors / edges / cross-effects:** Context supplies project or requires selection; no silent cross-workspace assignment. Later entry points delivered with their modules.
- **Acceptance criteria:** AC1: initial project-to-assignee flow survives reload. AC2: linked entry points retain correct project and permissions.
- **Open questions:** Q06a Q06b; unspecified validation, permission details and failures remain U.

<a id="mk-ta-002"></a>

### MK-TA-002 — Task reports, replies and mentions

Evidence: **D** · Sources: [H071] [H080] [H020] · Reference plan: Both; mentions advanced · Delivery: **P2**.

- **Actor / preconditions:** Task participant allowed to report; mention recipient authorization to verify.
- **Flow / observable result:** Add progress report/file, reply to report, mention one or more users and inspect dated activity.
- **Fields / states / transitions:** Report body, author/time, attachments, parent reply, mentions/read state.
- **Errors / edges / cross-effects:** Mention opens task via assistant; must not grant unintended resource access.
- **Acceptance criteria:** AC1: reply points to correct report. AC2: mention reaches permitted recipient with link and read transition. AC3: audit preserves author/time.
- **Open questions:** Q02; unspecified validation, permission details and failures remain U.

<a id="mk-ta-003"></a>

### MK-TA-003 — Edit, delete and restore task

Evidence: **D** · Sources: [H067] · Reference plan: Both; advanced editing policy · Delivery: **P2**.

- **Actor / preconditions:** Simple project assignee; advanced project manager/permitted assignee; category rules differ.
- **Flow / observable result:** Edit fields or delete from task menu; find removed task in feed and restore.
- **Fields / states / transitions:** Editable fields; deleted/restored; membership in task category.
- **Errors / edges / cross-effects:** Category creator/assignee/admin deletion rule; assignee needs category membership; recovery actor unclear.
- **Acceptance criteria:** AC1: restricted editor denied. AC2: delete removes active item; authorized restore returns same task/history.
- **Open questions:** Q02 Q06b Q07; unspecified validation, permission details and failures remain U.

<a id="mk-ta-004"></a>

### MK-TA-004 — Task completion and partial progress

Evidence: **D** · Sources: [H066] [H075] · Reference plan: Both · Delivery: **P1**.

- **Actor / preconditions:** Assigned performer; permitted to act on task.
- **Flow / observable result:** Tick completion, finish checklist and confirm, or set 100 percent and confirm; task becomes done.
- **Fields / states / transitions:** Progress 0–100, completion time/user; active/done.
- **Errors / edges / cross-effects:** Non-assignee cannot complete; moving columns has no completion effect; approval tasks route to pending approval.
- **Acceptance criteria:** AC1: assignee completion updates trays/project. AC2: non-assignee rejected; canceling checklist prompt leaves task active.
- **Open questions:** Q04; unspecified validation, permission details and failures remain U.

<a id="mk-ta-005"></a>

### MK-TA-005 — Shared task and no-assignee behavior

Evidence: **D** · Sources: [H077] [H078] · Reference plan: Both · Delivery: **P2**.

- **Actor / preconditions:** Permitted creator/editor; performers are selected workspace users.
- **Flow / observable result:** Assign several people to one task or clear assignee; later assign unclaimed task.
- **Fields / states / transitions:** One task with many assignees; no-assignee state; completed-by.
- **Errors / edges / cross-effects:** Any performer completes shared task for all unless final approval enabled; unassigned tasks only in project.
- **Acceptance criteria:** AC1: any shared performer completion removes same task from all trays. AC2: unassigned task enters tray only after assignment.
- **Open questions:** Q04; unspecified validation, permission details and failures remain U.

<a id="mk-ta-006"></a>

### MK-TA-006 — Final approval workflow

Evidence: **D** · Sources: [H079] [H077] · Reference plan: Both · Delivery: **P2**.

- **Actor / preconditions:** Creator selects final approver from multiple selected performers; approver controls final completion.
- **Flow / observable result:** Performer ticks done; task becomes waiting approval; designated approver completes or leaves pending with report.
- **Fields / states / transitions:** Active → waiting approval → done; performer ticks and approval identity.
- **Errors / edges / cross-effects:** Board/feed reflect final state; number of approvers disputed; no invented rejection transition.
- **Acceptance criteria:** AC1: performer alone cannot finalize approved task. AC2: approver completes once; all views show same state.
- **Open questions:** Q04; unspecified validation, permission details and failures remain U.

<a id="mk-ta-007"></a>

### MK-TA-007 — Reopen completed task

Evidence: **D** · Sources: [H068] · Reference plan: Advanced · Delivery: **P2**.

- **Actor / preconditions:** Manager for ordinary task; final approver exclusively for final-approval task.
- **Flow / observable result:** Find completed task in project filter or daily completion list; confirm reopening.
- **Fields / states / transitions:** Done → active; open tray visibility.
- **Errors / edges / cross-effects:** Other members cannot reopen final-approved task, including blanket manager override.
- **Acceptance criteria:** AC1: reopened task returns to performer tray/project. AC2: wrong actor cannot reopen.
- **Open questions:** Q04; unspecified validation, permission details and failures remain U.

<a id="mk-ta-008"></a>

### MK-TA-008 — Reminder, start, deadline and overdue calculation

Evidence: **D** · Sources: [H074] [H065] · Reference plan: Reminder both; start/deadline advanced · Delivery: **P2**.

- **Actor / preconditions:** Creator/editor subject to project scheduling policy.
- **Flow / observable result:** Set reminder and optional start/due; system classifies current/future/overdue and sends reminder.
- **Fields / states / transitions:** Independent reminder/due; deadline-based delay when due present.
- **Errors / edges / cross-effects:** No due: exact reminder-to-overdue boundary unknown; extension policy; date inversion/timezone errors.
- **Acceptance criteria:** AC1: due-bearing task uses due for delay. AC2: denied extension rejected. AC3: one reminder despite retry.
- **Open questions:** Q08; unspecified validation, permission details and failures remain U.

<a id="mk-ta-009"></a>

### MK-TA-009 — Checklist completion provenance

Evidence: **D** · Sources: [H075] [H020] · Reference plan: Both · Delivery: **P2**.

- **Actor / preconditions:** Task actor can tick items; managers control completed item changes per release.
- **Flow / observable result:** Add/reorder checklist; tick items; view who/when; confirm completing whole task.
- **Fields / states / transitions:** Item order/text, checked-by/time; completed item locked except manager edit/uncheck.
- **Errors / edges / cross-effects:** Shared task may finish before every item; provenance survives reload.
- **Acceptance criteria:** AC1: item shows correct performer/time. AC2: nonmanager cannot edit/uncheck locked completed item.
- **Open questions:** Q02; unspecified validation, permission details and failures remain U.

<a id="mk-ta-010"></a>

### MK-TA-010 — Weighted and partial progress calculation

Evidence: **D/I** · Sources: [H072] · Reference plan: Advanced · Delivery: **P2**.

- **Actor / preconditions:** Manager enables weight and weighted charts; task editor records weight/progress.
- **Flow / observable result:** Set weight; show project progress proportional to weight and partial progress.
- **Fields / states / transitions:** Weight units configurable meaning; sum(weight × progress)/sum(weight) inferred formula from example.
- **Errors / edges / cross-effects:** Zero/missing/negative weights and rounding unknown; charts include overdue remainder.
- **Acceptance criteria:** AC1: weight 30 of total 50 yields 60 percent at completion and 30 percent at half progress. AC2: invalid weights handled explicitly.
- **Open questions:** Q13; unspecified validation, permission details and failures remain U.

<a id="mk-ta-011"></a>

### MK-TA-011 — Recurring tasks and calendar projections

Evidence: **D** · Sources: [H076] [H073] [H024] · Reference plan: Both; custom patterns updated Tir 1405 · Delivery: **P2**.

- **Actor / preconditions:** Permitted task scheduler.
- **Flow / observable result:** Choose daily/weekly/monthly/yearly/custom recurrence and never/count/date end; complete instance to generate next; cancel recurrence.
- **Fields / states / transitions:** Series rule, next instance, projection, completion gate; selected weekdays/month-day patterns.
- **Errors / edges / cross-effects:** Future dates visible in calendar while next real instance waits for completion; shifting first instance reschedules future projections.
- **Acceptance criteria:** AC1: no completion means no next real task. AC2: duplicate completion/job retry produces one successor. AC3: cancellation stops future generation.
- **Open questions:** Q08; unspecified validation, permission details and failures remain U.

<a id="mk-ta-012"></a>

### MK-TA-012 — Task templates

Evidence: **D** · Sources: [H069] [H024] · Reference plan: Advanced · Delivery: **P2**.

- **Actor / preconditions:** Project manager maintains templates; eligible members use them in their joined projects.
- **Flow / observable result:** Create/search/edit/activate/deactivate/delete template in project/category settings; instantiate editable new task.
- **Fields / states / transitions:** Template fields, source project/category, active flag, new task ID.
- **Errors / edges / cross-effects:** Current placement differs from old help; cross-project eligibility requires source membership.
- **Acceptance criteria:** AC1: disabled template cannot be selected. AC2: instance edits do not mutate template. AC3: nonmember cannot use private-source template.
- **Open questions:** Q06b; unspecified validation, permission details and failures remain U.

<a id="mk-ta-013"></a>

### MK-TA-013 — Copying tasks and shareable links

Evidence: **D** · Sources: [H070] [H022] · Reference plan: Both; per-person bulk copies advanced · Delivery: **P2**.

- **Actor / preconditions:** Actor who can access source and create destination task.
- **Flow / observable result:** Copy task to another customer/context or separately for selected users; copy link and open task.
- **Fields / states / transitions:** Independent new task versus shared task; URL identifier.
- **Errors / edges / cross-effects:** Copied history/attachments fields and actor rules need evidence; links convey no public permission.
- **Acceptance criteria:** AC1: copies have independent completion states. AC2: unauthorized link visitor denied.
- **Open questions:** Q15; unspecified validation, permission details and failures remain U.

<a id="mk-ta-014"></a>

### MK-TA-014 — Personal task trays and daily completions

Evidence: **D** · Sources: [H064] [H016] · Reference plan: Both · Delivery: **P1**.

- **Actor / preconditions:** Member sees own tasks and tasks they follow; broader monitoring requires grants.
- **Flow / observable result:** Use my work/follow-ups/daily done/category/tag tabs; sort and filter; print results.
- **Fields / states / transitions:** Today/delayed/current/untimed/future; creator/status/customer/time filters; daily grouping.
- **Errors / edges / cross-effects:** Daily result timezone and visibility scope need verification.
- **Acceptance criteria:** AC1: assigned and delegated fixtures appear in correct tabs. AC2: unauthorized coworkers do not leak through filters or print.
- **Open questions:** Q06b Q08; unspecified validation, permission details and failures remain U.

<a id="mk-ta-015"></a>

### MK-TA-015 — Personal and team work calendar

Evidence: **D** · Sources: [H073] · Reference plan: Both; all-user view advanced grant · Delivery: **P2**.

- **Actor / preconditions:** Member for own tasks; delegated monitoring grant for team view.
- **Flow / observable result:** Navigate months/today; filter, show no-time tasks/full titles, create on date and move first recurring instance.
- **Fields / states / transitions:** Member filters project/category/tags; privileged creator/assignee filters; future occurrence projection.
- **Errors / edges / cross-effects:** No-time scheduling must respect edit rules; narrow viewport browser requirements need confirmation.
- **Acceptance criteria:** AC1: member cannot request another user calendar. AC2: all-user mode needs grant and shows authorized fixtures only.
- **Open questions:** Q08; unspecified validation, permission details and failures remain U.

<a id="mk-ta-016"></a>

### MK-TA-016 — Task views, history, transfer and printing

Evidence: **D** · Sources: [H071] [H022] [PRICE] · Reference plan: Both · Delivery: **P2**.

- **Actor / preconditions:** Authorized task viewer/editor; destination project membership for moves proposed.
- **Flow / observable result:** Inspect task change history and view receipts; move between projects; print task with reports.
- **Fields / states / transitions:** Viewed-by/time, history entries, destination project, printable reports.
- **Errors / edges / cross-effects:** Receipts apply to tasks created after release activation; move/Gantt/customer effects unknown.
- **Acceptance criteria:** AC1: dated history and viewer receipts match actions. AC2: move cannot cross workspace and preserves authorized history.
- **Open questions:** Q15; unspecified validation, permission details and failures remain U.

## CH

<a id="mk-ch-001"></a>

### MK-CH-001 — Conversation directory and private messaging

Evidence: **D** · Sources: [H032] [H033] [H114] · Reference plan: Both · Delivery: **P3**.

- **Actor / preconditions:** Workspace members allowed to communicate; guests have no private chats.
- **Flow / observable result:** Open all/groups/people tabs, search names, start private conversation or message invited person before acceptance.
- **Fields / states / transitions:** Workspace-scoped conversation; invited marker; messages available after acceptance.
- **Errors / edges / cross-effects:** Admin is not automatically a participant; no cross-workspace DM link.
- **Acceptance criteria:** AC1: accepted invite exposes prior intended messages. AC2: outsider/admin nonparticipant cannot read chat; guest DM denied.
- **Open questions:** Q03; unspecified validation, permission details and failures remain U.

<a id="mk-ch-002"></a>

### MK-CH-002 — Groups and channels

Evidence: **D** · Sources: [H034] [H035] [H040] · Reference plan: Both; restricted visibility advanced · Delivery: **P3**.

- **Actor / preconditions:** User with creation grant; group/channel admin manages allowed settings.
- **Flow / observable result:** Create title/image and public/selected membership; manage roles, notifications and up to three pinned conversations.
- **Fields / states / transitions:** Group vs one-way channel; admin/member; archive/delete terminology disputed.
- **Errors / edges / cross-effects:** Channel posting only creator/admin; member removal creator-only claim conflicts with other manager rules.
- **Acceptance criteria:** AC1: nonadmin channel post rejected. AC2: private group excluded from directory/search for outsider.
- **Open questions:** Q02 Q07; unspecified validation, permission details and failures remain U.

<a id="mk-ch-003"></a>

### MK-CH-003 — Message editing, deleting and receipts

Evidence: **D** · Sources: [H033] [H034] [H024] · Reference plan: Both · Delivery: **P3**.

- **Actor / preconditions:** Message author before read; workspace manager exception requires participation.
- **Flow / observable result:** Send/reply/copy/format/pin messages; inspect read times; edit unread message with Up Arrow; delete under permitted rule.
- **Fields / states / transitions:** Sent/read receipts; author; reply target; bold/italic text; pinned-message marker.
- **Errors / edges / cross-effects:** Read/edit race; personal deletion language conflicts; no broad manager access to private chats inferred.
- **Acceptance criteria:** AC1: unread edit succeeds, read edit fails for ordinary author. AC2: unauthorized delete and stale-client edit rejected.
- **Open questions:** Q03; unspecified validation, permission details and failures remain U.

<a id="mk-ch-004"></a>

### MK-CH-004 — Media and voice messages

Evidence: **D** · Sources: [H033] [H036] [H024] · Reference plan: Files both; private voice advanced · Delivery: **P3**.

- **Actor / preconditions:** Permitted conversation sender; microphone permission for recording.
- **Flow / observable result:** Upload/drag/paste files/images; choose compressed image or original file; caption/forward; browse gallery, rotate/zoom and play audio; record/stop/resume/send/discard voice.
- **Fields / states / transitions:** Documented per-file ceiling 100 MB; recording; gallery; attachment type.
- **Errors / edges / cross-effects:** No microphone/device, denied permission, interrupted upload; forwarding needs destination rights.
- **Acceptance criteria:** AC1: original-file mode preserves bytes. AC2: forbidden destination/oversize rejected. AC3: recording cancel does not send.
- **Open questions:** Q16; unspecified validation, permission details and failures remain U.

<a id="mk-ch-005"></a>

### MK-CH-005 — Conversation filters and message location

Evidence: **D** · Sources: [H037] [H020] [H024] · Reference plan: Both · Delivery: **P3**.

- **Actor / preconditions:** Authorized conversation viewer.
- **Flow / observable result:** Combine text/date/user/content-type filters; search filename; open result in original context and clear filter.
- **Fields / states / transitions:** Images/videos/files/polls; voice only private chat; tasks/minutes in project context.
- **Errors / edges / cross-effects:** No search result snippets from inaccessible content; exact matching/tokenization unknown.
- **Acceptance criteria:** AC1: filtered result opens correct message location. AC2: user/resource removal removes results and download access.
- **Open questions:** Q17; unspecified validation, permission details and failures remain U.

<a id="mk-ch-006"></a>

### MK-CH-006 — Assistant inbox, commands and mentions

Evidence: **D** · Sources: [H038] [H062] [H080] [H023] [H024] · Reference plan: Core reminders both; mentions advanced · Delivery: **P3**.

- **Actor / preconditions:** Member receiving own assistant events; authorized source context.
- **Flow / observable result:** Request today/tomorrow/overdue/delegated work and help; receive reminders, invitations, mentions, dependency and signature notices; open source and return.
- **Fields / states / transitions:** Mention all/unread filters; read/unread reset; dated assistant search; minutes filter.
- **Errors / edges / cross-effects:** This is documented command/event behavior, not evidence of generative AI; canceled reminders and removed access handled.
- **Acceptance criteria:** AC1: commands return correct authorized tasks. AC2: opening mention marks read; mark-unread and return preserve navigation.
- **Open questions:** Q13 Q17; unspecified validation, permission details and failures remain U.

<a id="mk-ch-007"></a>

### MK-CH-007 — Polls, confidentiality and quiz modes

Evidence: **D** · Sources: [H039] [H020] · Reference plan: Both per comparison · Delivery: **P3**.

- **Actor / preconditions:** Group/channel manager; project/customer creation role to verify; eligible participants.
- **Flow / observable result:** Create choices, multi-select, multi-question, quiz or combined quiz; vote and inspect permitted results.
- **Fields / states / transitions:** Question/options, correct answer; public, manager-visible identities or anonymous aggregate.
- **Errors / edges / cross-effects:** Anonymous vote identities must not leak to managers; sequential question result reveal timing documented.
- **Acceptance criteria:** AC1: visibility modes pass distinct API/browser checks. AC2: quiz reveals correctness after answer and multi-question score is accurate.
- **Open questions:** Q18; unspecified validation, permission details and failures remain U.

<a id="mk-ch-008"></a>

### MK-CH-008 — Poll lifecycle and templates

Evidence: **D** · Sources: [H039] [PRICE] · Reference plan: Both per comparison · Delivery: **P3**.

- **Actor / preconditions:** Poll creator/authorized manager; eligible respondent.
- **Flow / observable result:** End poll, retract permitted vote; define/reuse/remove template; print quiz results as documented in comparison.
- **Fields / states / transitions:** Open/closed; response; template; aggregate/result output.
- **Errors / edges / cross-effects:** Exact retraction actor/window, ties, edit behavior and template scope unknown.
- **Acceptance criteria:** AC1: closing prevents later voting. AC2: template creates independent poll. AC3: prints obey confidentiality.
- **Open questions:** Q18; unspecified validation, permission details and failures remain U.

## RT

<a id="mk-rt-001"></a>

### MK-RT-001 — Online meetings and screen sharing

Evidence: **D** · Sources: [H050] [H033] [H014] · Reference plan: Advanced; experimental · Delivery: **P6**.

- **Actor / preconditions:** Permitted project/group/private-chat participants; media-capable browser.
- **Flow / observable result:** Select up to ten participants, start/join call with mic/camera off, toggle devices, share screen, enlarge participant and end.
- **Fields / states / transitions:** Invitation/participant list; media state; call lifecycle.
- **Errors / edges / cross-effects:** Help denies participation without mic/camera; actual failure modes, provider/TURN/firewall and guest admission unknown.
- **Acceptance criteria:** AC1: allowed peers join and denied peers cannot. AC2: device permission failure is visible; end releases media.
- **Open questions:** Q19; unspecified validation, permission details and failures remain U.

## ME

<a id="mk-me-001"></a>

### MK-ME-001 — Simple meeting minutes

Evidence: **D** · Sources: [H054] [H055] [H097] · Reference plan: Both · Delivery: **P4**.

- **Actor / preconditions:** Project actor creates; project manager edits/prints/history; customer context also documented.
- **Flow / observable result:** Record date/time/location/subject/text/files and resolutions; publish; edit content, inspect history and restore version.
- **Fields / states / transitions:** Minutes and linked resolution tasks; immutable prior revisions.
- **Errors / edges / cross-effects:** Editing minutes does not edit resolution tasks; creation in customer conflicts with project-only wording.
- **Acceptance criteria:** AC1: resolution becomes correctly assigned project task. AC2: content rollback preserves separately edited task.
- **Open questions:** Q05 Q06a Q06b; unspecified validation, permission details and failures remain U.

<a id="mk-me-002"></a>

### MK-ME-002 — Organizational minutes lifecycle

Evidence: **D** · Sources: [H056] · Reference plan: Advanced; module enabled · Delivery: **P4**.

- **Actor / preconditions:** Authorized meeting organizer; assigned chair/secretary/expert/execution observer.
- **Flow / observable result:** Draft schedule/agenda/members/external invitees; invite by SMS; record attendance/text/resolutions; request signatures; print/update before signature request.
- **Fields / states / transitions:** Draft → forming → awaiting signature → signed; required fields; meeting labels; absence reason.
- **Errors / edges / cross-effects:** Text required before signature request; editing locked after request; notify time/place change/cancel/remind.
- **Acceptance criteria:** AC1: missing required text blocks request. AC2: after signature request content edit denied. AC3: invitations and status changes remain consistent under failed SMS.
- **Open questions:** Q05 Q10; unspecified validation, permission details and failures remain U.

<a id="mk-me-003"></a>

### MK-ME-003 — Minutes signatures and resolution dispatch

Evidence: **D** · Sources: [H054] [H056] · Reference plan: Advanced · Delivery: **P4**.

- **Actor / preconditions:** Eligible attendee/signatory; quorum rules require owner evidence.
- **Flow / observable result:** Receive signature request in assistant; sign; dispatch resolution tasks once majority is reached.
- **Fields / states / transitions:** Signature identity/time, eligible-voter snapshot, quorum, resolution/task link.
- **Errors / edges / cross-effects:** Members vs present-attendees denominator disputed; legal/certificate signature meaning unknown; absent/external guests and duplicate vote handling unresolved.
- **Acceptance criteria:** AC1: for verified electorate of five, fewer than three signatures cannot dispatch; third dispatches once. AC2: retry/signature replay cannot duplicate tasks.
- **Open questions:** Q05; unspecified validation, permission details and failures remain U.

<a id="mk-me-004"></a>

### MK-ME-004 — Minutes templates

Evidence: **D** · Sources: [H057] · Reference plan: Simple + organizational variants · Delivery: **P4**.

- **Actor / preconditions:** Workspace admin creates; template source project membership required for use.
- **Flow / observable result:** Define/remove template from minutes and reuse; edits to source simple minutes update template.
- **Fields / states / transitions:** Simple template content; organizational template only meeting information and members.
- **Errors / edges / cross-effects:** Do not copy signing/attendance/execution states into new organizational minutes.
- **Acceptance criteria:** AC1: nonmember cannot use private-source template. AC2: new organizational minutes starts unsigned/draft with only allowed copied fields.
- **Open questions:** Q05; unspecified validation, permission details and failures remain U.

## GA

<a id="mk-ga-001"></a>

### MK-GA-001 — Gantt structure and phases

Evidence: **D** · Sources: [H052] · Reference plan: Advanced; module enabled · Delivery: **P4**.

- **Actor / preconditions:** Project manager; read-only delegation separately evidenced.
- **Flow / observable result:** Create/reorder/rename/delete phases; add existing/new/standalone tasks; move tasks across phases; remove task from Gantt.
- **Fields / states / transitions:** Phase/task hierarchy, task bars, phase bounds from earliest/latest tasks; today/progress states.
- **Errors / edges / cross-effects:** Removing from Gantt does not delete project task; phase deletion removes structure, not underlying work.
- **Acceptance criteria:** AC1: task remains after Gantt removal. AC2: phase bounds follow member task dates.
- **Open questions:** Q02 Q08; unspecified validation, permission details and failures remain U.

<a id="mk-ga-002"></a>

### MK-GA-002 — Dependencies and successor notices

Evidence: **D** · Sources: [H052] [H023] · Reference plan: Advanced · Delivery: **P4**.

- **Actor / preconditions:** Gantt editor; successors have authorized assignees.
- **Flow / observable result:** Connect multiple predecessor/successor tasks; visualize invalid overlapping dates; complete prerequisite and notify successor assignees.
- **Fields / states / transitions:** Directed dependency; valid/invalid overlap marker.
- **Errors / edges / cross-effects:** Source shows invalid links in red; rejection/automatic rescheduling/cycle behavior not verified.
- **Acceptance criteria:** AC1: overlap rendered invalid without silently rewriting dates. AC2: prerequisite completion sends one correct successor notice.
- **Open questions:** Q20; unspecified validation, permission details and failures remain U.

<a id="mk-ga-003"></a>

### MK-GA-003 — Gantt interaction, view grants and print

Evidence: **D** · Sources: [H052] [H021] [PRICE] · Reference plan: Advanced · Delivery: **P4**.

- **Actor / preconditions:** Project manager edits; delegated member/guest read-only per release.
- **Flow / observable result:** Drag phase/task schedule, jump to start, zoom timeline and print chart.
- **Fields / states / transitions:** Time scale, print range, viewer/editor grant.
- **Errors / edges / cross-effects:** Help and release disagree on viewer access and scale names; effect of phase drag on tasks needs observation.
- **Acceptance criteria:** AC1: viewer cannot change dates via API or drag. AC2: printed authorized chart matches selected range.
- **Open questions:** Q02 Q08 Q20; unspecified validation, permission details and failures remain U.

## CR

<a id="mk-cr-001"></a>

### MK-CR-001 — Customer record identity and representatives

Evidence: **D** · Sources: [H095] [H022] · Reference plan: Both · Delivery: **P5**.

- **Actor / preconditions:** Member with CRM menu/resource/create grants.
- **Flow / observable result:** Create/edit photo, personal/business names, multiple titled phones/mobile/address; expand legal info and representatives.
- **Fields / states / transitions:** Postal code, web/email/fax, national/economic IDs, notes; representative name/role/mobile/landline.
- **Errors / edges / cross-effects:** Duplicate-phone warning documented; block vs warn and normalization unknown.
- **Acceptance criteria:** AC1: fields/representatives persist. AC2: duplicate phone produces warning; inaccessible records do not leak through warning.
- **Open questions:** Q21; unspecified validation, permission details and failures remain U.

<a id="mk-cr-002"></a>

### MK-CR-002 — Customer resource access and recovery

Evidence: **D** · Sources: [H093] [H100] [H031] · Reference plan: Both; guest gated · Delivery: **P5**.

- **Actor / preconditions:** CRM-granted member plus record membership; manager edits permitted settings; owner repairs bulk access.
- **Flow / observable result:** Add/remove members/managers; edit title/image, mute notifications; remove/archive group and restore via owner tools.
- **Fields / states / transitions:** Record membership, role, lifecycle and conversation.
- **Errors / edges / cross-effects:** Removing group cuts all members access; true data deletion not established; other record members do not automatically see linked private letters.
- **Acceptance criteria:** AC1: CRM menu grant alone does not expose unrelated records. AC2: removed member loses search/files/realtime.
- **Open questions:** Q02 Q07; unspecified validation, permission details and failures remain U.

<a id="mk-cr-003"></a>

### MK-CR-003 — Customer activity, call reports and follow-ups

Evidence: **D** · Sources: [H096] [H097] [H022] · Reference plan: Both; feature grants apply · Delivery: **P5**.

- **Actor / preconditions:** Record participant; project membership for follow-up tasks unless specific exception applies.
- **Flow / observable result:** Chat/upload/mention/poll; record inbound/outbound call date/time/text; convert call report to task; record minutes/resolutions.
- **Fields / states / transitions:** Activity feed, call direction/time, related project/task/minutes, reports unread/read.
- **Errors / edges / cross-effects:** Call text editable only until read; guest activities constrained to visible identities; minutes project association unclear.
- **Acceptance criteria:** AC1: call report conversion preserves text and links correct task/project. AC2: read report cannot be edited by ordinary author.
- **Open questions:** Q06a Q06b Q21; unspecified validation, permission details and failures remain U.

<a id="mk-cr-004"></a>

### MK-CR-004 — Customer tags, filtering, pins and output

Evidence: **D** · Sources: [H094] [H099] [H029] · Reference plan: Both · Delivery: **P5**.

- **Actor / preconditions:** Authorized CRM viewer; separate CRM print grant; no guest print.
- **Flow / observable result:** Search name/business/text, include/exclude labels, count results, pin up to three, print base-data table.
- **Fields / states / transitions:** Customer labels distinct from finance/opportunity labels; filtered row count.
- **Errors / edges / cross-effects:** Print excludes some fields per help; exact fields and multi-label AND/OR behavior unknown.
- **Acceptance criteria:** AC1: filtered count matches rows. AC2: print denied without grant and contains only approved basic fields.
- **Open questions:** Q21; unspecified validation, permission details and failures remain U.

<a id="mk-cr-005"></a>

### MK-CR-005 — Customer Excel import

Evidence: **D** · Sources: [H098] · Reference plan: Advanced per pricing · Delivery: **P6**.

- **Actor / preconditions:** Workspace admin with customer import rights.
- **Flow / observable result:** Download sample; upload Excel; map nonstandard columns, select record members/tags, preview and confirm.
- **Fields / states / transitions:** Up to 5,000 records per import; field mapping; empty/ignored columns.
- **Errors / edges / cross-effects:** Invalid headings need manual mapping; retry/duplicate/partial-import semantics unknown.
- **Acceptance criteria:** AC1: 5,001-record boundary produces explicit handling. AC2: preview mapped fixture and resulting memberships agree; ordinary member denied.
- **Open questions:** Q15; unspecified validation, permission details and failures remain U.

<a id="mk-cr-006"></a>

### MK-CR-006 — Financial records and lifecycle

Evidence: **D** · Sources: [H101] [H029] · Reference plan: Advanced · Delivery: **P5**.

- **Actor / preconditions:** Record participant with financial-create grant.
- **Flow / observable result:** Enter amount/date/incoming-or-outgoing/cashed state/method/description/tags/files; void or record realization.
- **Fields / states / transitions:** Cash, cheque, probable, void; received/paid; due date; record-specific financial labels.
- **Errors / edges / cross-effects:** Overdue uncashed receivables; currency/unit, negative/refund/edit/audit rules unknown.
- **Acceptance criteria:** AC1: recording/voiding preserves auditable record and correct category. AC2: user without finance grant cannot mutate via API.
- **Open questions:** Q22; unspecified validation, permission details and failures remain U.

<a id="mk-cr-007"></a>

### MK-CR-007 — Sales opportunities

Evidence: **D** · Sources: [H102] [H029] [PRICE] · Reference plan: Advanced · Delivery: **P5**.

- **Actor / preconditions:** Record participant with opportunity-create/view grant.
- **Flow / observable result:** Record title, nominal value, probability, description, follow-up owner, tags and attachment; track negotiation/success/failure.
- **Fields / states / transitions:** Probability 0–100; weighted value; opportunity-specific labels; linked customer.
- **Errors / edges / cross-effects:** Pipeline transition rules and close-date requiredness unknown; not a verified generic CRM automation engine.
- **Acceptance criteria:** AC1: value 1,000 at 25 percent yields weighted 250. AC2: unauthorized opportunity access denied.
- **Open questions:** Q22; unspecified validation, permission details and failures remain U.

<a id="mk-cr-008"></a>

### MK-CR-008 — Financial monitoring and arrears dashboard

Evidence: **D** · Sources: [H101] [H024] [H029] · Reference plan: Advanced · Delivery: **P5**.

- **Actor / preconditions:** Financial-monitoring grantee; dashboard visibility restricted.
- **Flow / observable result:** Filter labels; inspect confirmed receipts/payments, overdue/probable receipts/payments, monthly/yearly table and charts; drill into documents.
- **Fields / states / transitions:** Time buckets; totals; overdue uncashed cheque/probable receipt; dashboard amount visibility.
- **Errors / edges / cross-effects:** Do not expose totals through general workspace monitoring without financial grant; rounding/currency/month boundaries unknown.
- **Acceptance criteria:** AC1: cash/uncashed/void/due fixtures reconcile across tables/charts/dashboard. AC2: revoked grant removes aggregates.
- **Open questions:** Q22; unspecified validation, permission details and failures remain U.

<a id="mk-cr-009"></a>

### MK-CR-009 — Sales forecasting and monitoring

Evidence: **D** · Sources: [H102] [H094] · Reference plan: Advanced · Delivery: **P5**.

- **Actor / preconditions:** Sales-monitoring grantee.
- **Flow / observable result:** View successful/failed/negotiating opportunities, filter probability, inspect nominal/weighted totals and open details.
- **Fields / states / transitions:** Weighted value = nominal × probability/100; aggregate forecast.
- **Errors / edges / cross-effects:** Status/probability interaction and future-month grouping needs evidence.
- **Acceptance criteria:** AC1: forecast equals sum of eligible weighted opportunities. AC2: filters and detail access obey same sales policy.
- **Open questions:** Q22; unspecified validation, permission details and failures remain U.

## LE

<a id="mk-le-001"></a>

### MK-LE-001 — Letters and personal trays

Evidence: **D** · Sources: [H081] [H082] · Reference plan: Both · Delivery: **P5**.

- **Actor / preconditions:** Workspace sender; selected recipients include permitted guests.
- **Flow / observable result:** Compose subject/rich text/multiple recipients/labels; attach file or project task; send; view inbox/outbox/my paraphs.
- **Fields / states / transitions:** Text formatting/lists/links; recipients; attached task; 100 MB file limit.
- **Errors / edges / cross-effects:** Task attachment requires relevant project membership; private unnumbered letters not visible to broad admins.
- **Acceptance criteria:** AC1: recipients receive same letter, outsider/admin nonrecipient cannot read it. AC2: attached task cannot bypass project rights.
- **Open questions:** Q03 Q06a; unspecified validation, permission details and failures remain U.

<a id="mk-le-002"></a>

### MK-LE-002 — Paraphs, forwarding, receipts and archive

Evidence: **D** · Sources: [H083] [H086] · Reference plan: Both · Delivery: **P5**.

- **Actor / preconditions:** Letter participant; forwarding actor rule to verify.
- **Flow / observable result:** Reply to specific paraph/all recipients; forward with text/files to new recipients; inspect seen times; label/archive/filter/print.
- **Fields / states / transitions:** Reply chain, recipient set/read times; incoming archive; text/sender/recipient/read/attachment/tag/customer/date filters.
- **Errors / edges / cross-effects:** Forwarded history visibility and archive personal/global scope unresolved.
- **Acceptance criteria:** AC1: specific reply points to target paraph. AC2: recipients/read receipts match permissions and print never widens access.
- **Open questions:** Q03; unspecified validation, permission details and failures remain U.

<a id="mk-le-003"></a>

### MK-LE-003 — Secretariat registration and numbering

Evidence: **D** · Sources: [H085] [H029] · Reference plan: Advanced · Delivery: **P5**.

- **Actor / preconditions:** Owner/admin or secretariat grantee for registered letters; exact numbering actor to verify.
- **Flow / observable result:** Register outgoing with date/prefix/start/suffix or incoming with provided number; inspect dedicated trays and search by number/date.
- **Fields / states / transitions:** Independent outgoing sequences, increment/uniqueness; incoming may duplicate; registration paraph.
- **Errors / edges / cross-effects:** Unnumbered letter stays private; numbering expands visibility to authorized registry users.
- **Acceptance criteria:** AC1: concurrent outgoing registrations cannot duplicate number. AC2: incoming duplicate allowed. AC3: nonparticipant cannot see letter before registration.
- **Open questions:** Q23; unspecified validation, permission details and failures remain U.

<a id="mk-le-004"></a>

### MK-LE-004 — Read-dependent letter and paraph deletion

Evidence: **D** · Sources: [H084] [H024] · Reference plan: Both per current release · Delivery: **P5**.

- **Actor / preconditions:** Original sender for letter; paraph author for paraph; admin own-content exception.
- **Flow / observable result:** Delete own unread letter with paraphs or own unread paraph; apply documented manager exception after read.
- **Fields / states / transitions:** Deleted letter/paraph; viewed-by/time guard.
- **Errors / edges / cross-effects:** Admin exception for others disputed; Tir 1405 limits exception to own content; no inferred restore behavior.
- **Acceptance criteria:** AC1: read letter blocks ordinary sender delete. AC2: admin can delete own read letter/paraph; cannot delete others pending clarified policy.
- **Open questions:** Q03; unspecified validation, permission details and failures remain U.

<a id="mk-le-005"></a>

### MK-LE-005 — Customer-linked letters preserve privacy

Evidence: **D** · Sources: [H087] [H020] · Reference plan: Advanced per pricing · Delivery: **P5**.

- **Actor / preconditions:** Letter participant with access to target customer records.
- **Flow / observable result:** Connect letter to one or more customers; filter letters by customer; open linked letter through its own permission checks.
- **Fields / states / transitions:** Letter-customer many-to-many; letter ACL remains authoritative.
- **Errors / edges / cross-effects:** Customer membership alone does not grant private letter content; numbered letter registry exception applies.
- **Acceptance criteria:** AC1: customer member lacking letter access cannot read content or attachment. AC2: authorized participant can open from both contexts.
- **Open questions:** Q03; unspecified validation, permission details and failures remain U.

## NO

<a id="mk-no-001"></a>

### MK-NO-001 — Personal notes and privacy

Evidence: **D** · Sources: [H088] [H089] [H114] · Reference plan: Both; guests cannot label notes · Delivery: **P3**.

- **Actor / preconditions:** Account holder only.
- **Flow / observable result:** Create/edit title/text/checklist/image/color/pin/labels and copy content.
- **Fields / states / transitions:** Private note, checklist/order, image and personal label; guest label exception.
- **Errors / edges / cross-effects:** Workspace admins may see counts only; account-wide vs workspace-local note scope unresolved.
- **Acceptance criteria:** AC1: owner edits survive reload. AC2: any other user including workspace owner cannot fetch content/image; guest cannot label.
- **Open questions:** Q11; unspecified validation, permission details and failures remain U.

<a id="mk-no-002"></a>

### MK-NO-002 — Notes filters and lifecycle

Evidence: **D** · Sources: [H090] [H091] [H092] [H023] · Reference plan: Both · Delivery: **P3**.

- **Actor / preconditions:** Note owner.
- **Flow / observable result:** Search note text; filter all/label/archived/deleted; archive/delete/restore; permanently purge after 30 days in trash.
- **Fields / states / transitions:** Active/archived/deleted/purged; label rename/color.
- **Errors / edges / cross-effects:** Archive does not start deletion retention; purge boundary and backup-retention implications need definition.
- **Acceptance criteria:** AC1: archived/deleted notes restore correctly before purge. AC2: note deleted 30 days ago becomes unrecoverable through application.
- **Open questions:** Q24; unspecified validation, permission details and failures remain U.

## MON

<a id="mk-mon-001"></a>

### MK-MON-001 — Workspace monitoring overview

Evidence: **D** · Sources: [H103] [H029] · Reference plan: Mixed; detailed controls vary · Delivery: **P6**.

- **Actor / preconditions:** Monitoring grantee; admins automatically receive broad workspace monitoring per help.
- **Flow / observable result:** Inspect workspace owner/age/membership/storage and 30-day activity charts.
- **Fields / states / transitions:** Conversation/letter/task/customer/note counts; task completion distribution.
- **Errors / edges / cross-effects:** Counts do not authorize private content; exact exclusions and date buckets unverified.
- **Acceptance criteria:** AC1: fixture counts reconcile by period without exposing private content. AC2: guest/ordinary non-grantee denied.
- **Open questions:** Q13; unspecified validation, permission details and failures remain U.

<a id="mk-mon-002"></a>

### MK-MON-002 — Project monitoring

Evidence: **D** · Sources: [H104] [H022] [H024] · Reference plan: Advanced detailed monitoring · Delivery: **P6**.

- **Actor / preconditions:** Workspace monitor or limited project monitoring delegate.
- **Flow / observable result:** Filter groups/name/archive state; sort by latest completion/delay/done count; inspect 30-day shares, delay/workload and print.
- **Fields / states / transitions:** Project progress, largest delay, largest tray; authorized project set.
- **Errors / edges / cross-effects:** Limited grants differ from broad workspace view; chart labels/rounding unknown.
- **Acceptance criteria:** AC1: delegated monitor sees allowed project set. AC2: archive filter and printed totals match seeded data.
- **Open questions:** Q02 Q13; unspecified validation, permission details and failures remain U.

<a id="mk-mon-003"></a>

### MK-MON-003 — Task monitoring

Evidence: **D** · Sources: [H105] [H029] · Reference plan: Advanced detailed monitoring · Delivery: **P6**.

- **Actor / preconditions:** Workspace/task-tray monitoring grantee.
- **Flow / observable result:** Filter text/creator/assignee/status/overdue/tags/group/category/customer/time/form tracking; sort and print tasks.
- **Fields / states / transitions:** Created/reminder/start/due/done date ranges; result list.
- **Errors / edges / cross-effects:** Form builder is not evidenced by filter alone; privilege must apply to result counts too.
- **Acceptance criteria:** AC1: combined fixtures match filters and print. AC2: unauthorized team tray queries denied.
- **Open questions:** Q13 Q14; unspecified validation, permission details and failures remain U.

<a id="mk-mon-004"></a>

### MK-MON-004 — Customer monitoring

Evidence: **D** · Sources: [H106] · Reference plan: Both per pricing; grant required · Delivery: **P6**.

- **Actor / preconditions:** Authorized customer-monitoring actor.
- **Flow / observable result:** Filter labels/absence of labels/access/nonaccess/creator/created range; print reusable table.
- **Fields / states / transitions:** Record counts, effective ACL filters, customer details.
- **Errors / edges / cross-effects:** Global-monitoring versus resource membership visibility needs current reference capture.
- **Acceptance criteria:** AC1: access filters reflect actual membership changes. AC2: private fields follow defined report policy.
- **Open questions:** Q02 Q21; unspecified validation, permission details and failures remain U.

<a id="mk-mon-005"></a>

### MK-MON-005 — Organizational minutes monitoring

Evidence: **D** · Sources: [H107] [H024] · Reference plan: Advanced · Delivery: **P6**.

- **Actor / preconditions:** Authorized minutes-monitoring actor.
- **Flow / observable result:** Search title/text and filter expert/chair/observer/attendees/labels/project/status; see meeting time/location and unresolved resolutions.
- **Fields / states / transitions:** Draft/forming/waiting signature/signed/uncompleted resolutions; time/place.
- **Errors / edges / cross-effects:** Overlapping statuses and simple minutes inclusion unknown.
- **Acceptance criteria:** AC1: each fixture appears under correct lifecycle/status filter. AC2: linked resolution completion updates monitoring.
- **Open questions:** Q05 Q13; unspecified validation, permission details and failures remain U.

<a id="mk-mon-006"></a>

### MK-MON-006 — Member analytics and workspace presence

Evidence: **D** · Sources: [H108] · Reference plan: Advanced · Delivery: **P6**.

- **Actor / preconditions:** Authorized member monitor; guest activity included, guests cannot monitor.
- **Flow / observable result:** View per-person activity counts, tray, project share/30-day completions, and online-history chart/table by selected day.
- **Fields / states / transitions:** Role/title/invitation status/last online; note counts; per-workspace presence.
- **Errors / edges / cross-effects:** Online in one workspace is not presence in all workspaces; note content remains private; retention/heartbeat semantics unknown.
- **Acceptance criteria:** AC1: switching active workspace affects only its presence history. AC2: private note content inaccessible from analytics.
- **Open questions:** Q13 Q24; unspecified validation, permission details and failures remain U.

## SYS

<a id="mk-sys-001"></a>

### MK-SYS-001 — Private attachments and aggregate file views

Evidence: **D** · Sources: [H036] [H047] [H096] [H024] · Reference plan: Both; shared across later modules · Delivery: **P1**.

- **Actor / preconditions:** Actor authorized on source and destination resources.
- **Flow / observable result:** Upload/download attachment; view project task attachments separately from conversation files; search filename and type.
- **Fields / states / transitions:** Attachment metadata, private bytes, original filename, owner resource; 100 MB documented per-file ceiling.
- **Errors / edges / cross-effects:** Authorization after removal/forwarding, failed upload/quota and deletion/restore must be coherent; scanning proposed safeguard.
- **Acceptance criteria:** AC1: unauthorized direct URL download denied. AC2: oversize/quota interruption leaves no visible broken attachment.
- **Open questions:** Q16; unspecified validation, permission details and failures remain U.

<a id="mk-sys-002"></a>

### MK-SYS-002 — Workspace search and bookmarks

Evidence: **D** · Sources: [H024] [H023] · Reference plan: Both · Delivery: **P3**.

- **Actor / preconditions:** Active member with permission to matched content.
- **Flow / observable result:** Search across allowed modules/filenames; bookmark task/letter/message and reopen through dashboard.
- **Fields / states / transitions:** Query, result type/source, bookmark per user.
- **Errors / edges / cross-effects:** Exact search coverage/ranking and bookmark behavior after access loss unknown; deleted items cannot leak snippets.
- **Acceptance criteria:** AC1: protected fixture never appears in search, counts or bookmarks to unauthorized user. AC2: bookmark survives reload and rechecks access.
- **Open questions:** Q17; unspecified validation, permission details and failures remain U.

<a id="mk-sys-003"></a>

### MK-SYS-003 — Notifications, history and muting

Evidence: **D** · Sources: [H030] [H024] [H023] · Reference plan: Both; provider setup required · Delivery: **P1**.

- **Actor / preconditions:** Event recipient; browser/email permission and verified address where required.
- **Flow / observable result:** Receive task/invite/update/reminder events, inspect history; set project/group/customer notifications and browser mute 1/2/4/8 hours.
- **Fields / states / transitions:** Delivery/read history; mute-until; user/resource preference; email verification; browser/PWA subscription.
- **Errors / edges / cross-effects:** Denied browser permission/offline/revoked access/provider outage; exact channels and event policy unknown.
- **Acceptance criteria:** AC1: core event reaches correct recipient once. AC2: mute suppresses browser display then expires, without leaking revoked content.
- **Open questions:** Q10 Q13; unspecified validation, permission details and failures remain U.

<a id="mk-sys-004"></a>

### MK-SYS-004 — Task/project imports

Evidence: **D** · Sources: [H059] [H060] [H061] · Reference plan: Advanced per pricing; workspace admin · Delivery: **P6**.

- **Actor / preconditions:** Workspace admin; valid Trello JSON/CSV/Excel.
- **Flow / observable result:** Download sample; upload/map users/tags/columns, preview, choose Trello done column, confirm new project.
- **Fields / states / transitions:** Gregorian dates with hyphens; Persian-comma multi-tags; missing headings/title validation.
- **Errors / edges / cross-effects:** Untitled rows not imported; optional unmapped columns blank; Trello done column explicitly determines completion.
- **Acceptance criteria:** AC1: mapped done-column tasks imported completed. AC2: malformed headings/title/date yield actionable row/mapping feedback; retry behavior defined.
- **Open questions:** Q15; unspecified validation, permission details and failures remain U.

<a id="mk-sys-005"></a>

### MK-SYS-005 — Forms and additional reference surfaces

Evidence: **D/U** · Sources: [H047] [H105] [H024] · Reference plan: Unknown · Delivery: **P6**.

- **Actor / preconditions:** Unknown actor; only form tracking-number filter documented.
- **Flow / observable result:** Retain investigation of form references plus help/support/new-features entry points; inventory additional authenticated menus.
- **Fields / states / transitions:** Form tracking number; support destinations; new-feature notices.
- **Errors / edges / cross-effects:** No verified form builder, API, automation, time tracker or custom-field engine; do not fabricate them or silently declare excluded.
- **Acceptance criteria:** AC1: owner evidence resolves whether forms are separate module/integration. AC2: every newly found capability gains a requirement/phase before parity review.
- **Open questions:** Q14; unspecified validation, permission details and failures remain U.

## OPS

<a id="mk-ops-001"></a>

### MK-OPS-001 — Debian production operation and recovery

Evidence: **D/I** · Sources: [OWNER] [PRICE] · Reference plan: Deployment requirement · Delivery: **P7**.

- **Actor / preconditions:** Operator with deployment/backup permissions.
- **Flow / observable result:** Deploy pinned releases, migrate, monitor health/jobs/storage, back up and rehearse restore of database and attachments.
- **Fields / states / transitions:** Release/migration version; backup manifest; recovery checkpoint; measured limits.
- **Errors / edges / cross-effects:** RPO/RTO/scale/hardware unknown; failed migration/restore rollback planned; no deploy performed in Phase 0.
- **Acceptance criteria:** AC1: clean Debian install passes smoke/browser checks. AC2: independent restore reproduces data/attachments and ACLs; record actual recovery time.
- **Open questions:** Q11 Q24; unspecified validation, permission details and failures remain U.

<a id="mk-ops-002"></a>

### MK-OPS-002 — Cross-cutting authorization and durable live updates

Evidence: **I** · Sources: [OWNER] [H029] [H012] · Reference plan: All · Delivery: **P1**.

- **Actor / preconditions:** Every user/API/job/socket action; current membership and resource policy.
- **Flow / observable result:** Persist mutation and audit/event transactionally, deliver to authorized recipients, recover missed events on reconnect.
- **Fields / states / transitions:** Workspace scope, policy decision, event cursor, job idempotency key.
- **Errors / edges / cross-effects:** Concurrent revoke/write, stale socket, duplicate job, deleted resource and search index lag; proposed implementation contract.
- **Acceptance criteria:** AC1: two-workspace API/socket/download negative suite passes. AC2: reconnect recovers durable state; revoked peer receives no later protected payload.
- **Open questions:** Q02 Q11; unspecified validation, permission details and failures remain U.

## Source URL definitions

[H004]: https://help.mizito.ir/article/69aeaae517f243f6a25b8e77/%D8%A7%DB%8C%D8%AC%D8%A7%D8%AF-%D8%AD%D8%B3%D8%A7%D8%A8-%DA%A9%D8%A7%D8%B1%D8%A8%D8%B1%DB%8C-(%D8%A7%DB%8C%D8%AC%D8%A7%D8%AF-%D9%85%DB%8C%D8%B2%DA%A9%D8%A7%D8%B1)
[H005]: https://help.mizito.ir/article/69aeaceb17f243f6a25b8fba/%D9%86%D8%AD%D9%88%D9%87-%D9%88%D8%B1%D9%88%D8%AF-%D8%A8%D9%87-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88
[H006]: https://help.mizito.ir/article/69aeabf117f243f6a25b8f10/%D8%B1%D9%81%D8%B9-%D9%85%D8%B4%DA%A9%D9%84%D8%A7%D8%AA-%D9%88%D8%B1%D9%88%D8%AF-%D8%A8%D9%87-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88
[H008]: https://help.mizito.ir/article/69a6b4a749f9f8d00252affa/%D8%A7%DB%8C%D8%AC%D8%A7%D8%AF-%D8%A7%D9%88%D9%84%DB%8C%D9%86-%D9%BE%D8%B1%D9%88%DA%98%D9%87-%D8%AF%D8%B1-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88
[H009]: https://help.mizito.ir/article/69a6b56949f9f8d00252b058/%D8%A7%DB%8C%D8%AC%D8%A7%D8%AF-%D8%A7%D9%88%D9%84%DB%8C%D9%86-%D9%88%D8%B8%DB%8C%D9%81%D9%87-(%D8%AA%D8%B3%DA%A9)-%D8%AF%D8%B1-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88
[H012]: https://help.mizito.ir/article/6a76f5b446cee20012bcd8f4/%D8%A7%D9%86%D9%88%D8%A7%D8%B9-%DA%A9%D8%A7%D8%B1%D8%A8%D8%B1-%D8%AF%D8%B1-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88
[H013]: https://help.mizito.ir/article/6a8ab0b447a120003ca6ea12/%D9%85%D8%AD%DB%8C%D8%B7-%D9%85%DB%8C%D8%B2%DA%A9%D8%A7%D8%B1-%D8%AF%D8%B1-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88
[H014]: https://help.mizito.ir/article/6a8ad7e9888c8a0012184870/%DA%AF%D9%81%D8%AA%DA%AF%D9%88-%D9%88-%D8%AC%D9%84%D8%B3%D8%A7%D8%AA-%D8%A2%D9%86%D9%84%D8%A7%DB%8C%D9%86-%D8%AF%D8%B1-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88
[H016]: https://help.mizito.ir/article/6a8ad8f8888c8a001218492d/%D9%85%D8%AF%DB%8C%D8%B1%DB%8C%D8%AA-%D9%88%D8%B8%D8%A7%DB%8C%D9%81-%D8%AF%D8%B1-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88
[H020]: https://help.mizito.ir/article/6a77099c46cee20012bcdb17/%D8%A2%D9%BE%D8%AF%DB%8C%D8%AA-%D9%81%D8%B1%D9%88%D8%B1%D8%AF%DB%8C%D9%86-%DB%B1%DB%B4%DB%B0%DB%B2
[H021]: https://help.mizito.ir/article/6a7719f24fc55f001274900d/%D8%A2%D9%BE%D8%AF%DB%8C%D8%AA-%D9%85%D8%B1%D8%AF%D8%A7%D8%AF%D9%85%D8%A7%D9%87-%DB%B1%DB%B4%DB%B0%DB%B2
[H022]: https://help.mizito.ir/article/6a771a2e4fc55f001274901b/%D8%A2%D9%BE%D8%AF%DB%8C%D8%AA-%D8%AF%DB%8C-%D9%85%D8%A7%D9%87-%DB%B1%DB%B4%DB%B0%DB%B2
[H023]: https://help.mizito.ir/article/6a771a6b8d44a80012a1d152/%D8%A2%D9%BE%D8%AF%DB%8C%D8%AA-%D8%B4%D9%87%D8%B1%DB%8C%D9%88%D8%B1%D9%85%D8%A7%D9%87-%DB%B1%DB%B4%DB%B0%DB%B3
[H024]: https://help.mizito.ir/article/6a771ada4fc55f0012749024/%D8%A2%D9%BE%D8%AF%DB%8C%D8%AA-%D8%AA%DB%8C%D8%B1%D9%85%D8%A7%D9%87-%DB%B1%DB%B4%DB%B0%DB%B5
[H025]: https://help.mizito.ir/article/69772e7346b3767096d47e6f/%D9%85%D9%81%D9%87%D9%88%D9%85-%D9%85%DB%8C%D8%B2%DA%A9%D8%A7%D8%B1
[H026]: https://help.mizito.ir/article/6978667946b3767096d47e7a/%D8%AA%D9%86%D8%B8%DB%8C%D9%85%D8%A7%D8%AA-%D9%85%DB%8C%D8%B2%DA%A9%D8%A7%D8%B1-(%D8%A7%D8%B7%D9%84%D8%A7%D8%B9%D8%A7%D8%AA-%D9%85%DB%8C%D8%B2%DA%A9%D8%A7%D8%B1)
[H027]: https://help.mizito.ir/article/69786a8246b3767096d47e7e/%D8%AA%D9%86%D8%B8%DB%8C%D9%85%D8%A7%D8%AA-%D9%85%DB%8C%D8%B2%DA%A9%D8%A7%D8%B1-(%D8%B3%D8%B1%D8%A8%D8%B1%DA%AF-%D8%A7%D8%B9%D8%B6%D8%A7)
[H028]: https://help.mizito.ir/article/6978761d46b3767096d47e82/%D8%AA%D9%86%D8%B8%DB%8C%D9%85%D8%A7%D8%AA-%D9%85%DB%8C%D8%B2%DA%A9%D8%A7%D8%B1-(%D8%B3%D8%B1%D8%A8%D8%B1%DA%AF-%D9%85%D8%A7%D9%84%DB%8C)
[H029]: https://help.mizito.ir/article/6978872c46b3767096d47e89/%D8%AA%D9%86%D8%B8%DB%8C%D9%85%D8%A7%D8%AA-%D9%85%DB%8C%D8%B2%DA%A9%D8%A7%D8%B1-(%D8%B3%D8%B1%D8%A8%D8%B1%DA%AF-%D9%85%D8%AC%D9%88%D8%B2%D9%87%D8%A7)
[H030]: https://help.mizito.ir/article/6979d7ff99b384d46b6a478b/%D9%85%D8%AD%DB%8C%D8%B7-%D9%85%DB%8C%D8%B2%DA%A9%D8%A7%D8%B1-(%D8%AA%D9%86%D8%B8%DB%8C%D9%85%D8%A7%D8%AA-%D9%BE%D8%B1%D9%88%D9%81%D8%A7%DB%8C%D9%84)
[H031]: https://help.mizito.ir/article/6979b61199b384d46b6a4782/%D9%85%D8%AC%D9%88%D8%B2%D9%87%D8%A7%DB%8C-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88-(%D8%AA%D9%86%D8%B8%DB%8C%D9%85%D8%A7%D8%AA-%D8%A7%D8%AE%D8%AA%D8%B5%D8%A7%D8%B5%DB%8C-%D9%85%D8%A7%D9%84%DA%A9-%D9%85%DB%8C%D8%B2%DA%A9%D8%A7%D8%B1)
[H032]: https://help.mizito.ir/article/698881861d8eb1045ca36100/%D9%85%D8%B9%D8%B1%D9%81%DB%8C-%D9%81%D8%B6%D8%A7%DB%8C-%DA%AF%D9%81%D8%AA%DA%AF%D9%88-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88
[H033]: https://help.mizito.ir/article/698883e41d8eb1045ca36103/%D8%A7%D8%B1%D8%B3%D8%A7%D9%84-%D9%BE%DB%8C%D8%A7%D9%85-%D8%B4%D8%AE%D8%B5%DB%8C-%D8%AF%D8%B1-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88
[H034]: https://help.mizito.ir/article/698aeb041d8eb1045ca3610b/%D8%A7%DB%8C%D8%AC%D8%A7%D8%AF-%DA%AF%D8%B1%D9%88%D9%87-%DA%AF%D9%81%D8%AA%DA%AF%D9%88-%D8%AF%D8%B1-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88
[H035]: https://help.mizito.ir/article/698aecdf1d8eb1045ca3610f/%D8%A7%DB%8C%D8%AC%D8%A7%D8%AF-%DA%A9%D8%A7%D9%86%D8%A7%D9%84-%D8%AF%D8%B1-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88
[H036]: https://help.mizito.ir/article/698b11c01d8eb1045ca36115/%D8%A7%D8%B1%D8%B3%D8%A7%D9%84-%D9%BE%DB%8C%D8%A7%D9%85-%D8%BA%DB%8C%D8%B1%D9%85%D8%AA%D9%86%DB%8C
[H037]: https://help.mizito.ir/article/698b12de1d8eb1045ca36119/%D9%81%DB%8C%D9%84%D8%AA%D8%B1-%D9%BE%DB%8C%D8%A7%D9%85-%D9%87%D8%A7
[H038]: https://help.mizito.ir/article/6991aa2ce69ec52d915511d3/%D8%A2%D8%B4%D9%86%D8%A7%DB%8C%DB%8C-%D8%A8%D8%A7-%D8%AF%D8%B3%D8%AA%DB%8C%D8%A7%D8%B1-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88
[H039]: https://help.mizito.ir/article/6991abc1e69ec52d91551223/%D9%86%D8%B8%D8%B1%D8%B3%D9%86%D8%AC%DB%8C-%D8%AF%D8%B1-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88
[H040]: https://help.mizito.ir/article/6a65b3e553fe69001202032e/%D8%AA%D9%86%D8%B8%DB%8C%D9%85%D8%A7%D8%AA-%DA%AF%D8%B1%D9%88%D9%87-%DA%AF%D9%81%D8%AA%DA%AF%D9%88-%D9%88-%DA%A9%D8%A7%D9%86%D8%A7%D9%84
[H041]: https://help.mizito.ir/article/697da5f399b384d46b6a4793/%D8%A2%D8%B4%D9%86%D8%A7%DB%8C%DB%8C-%D8%A8%D8%A7-%D9%85%D9%81%D9%87%D9%88%D9%85-%D9%BE%D8%B1%D9%88%DA%98%D9%87
[H042]: https://help.mizito.ir/article/697da77799b384d46b6a4798/%D8%A7%DB%8C%D8%AC%D8%A7%D8%AF-%D9%BE%D8%B1%D9%88%DA%98%D9%87-%D8%AC%D8%AF%DB%8C%D8%AF
[H043]: https://help.mizito.ir/article/697da9b899b384d46b6a479c/%D8%A2%D8%B4%D9%86%D8%A7%DB%8C%DB%8C-%D8%A7%D9%88%D9%84%DB%8C%D9%87-%D8%A8%D8%A7-%D8%A7%D9%85%DA%A9%D8%A7%D9%86%D8%A7%D8%AA-%D9%BE%D8%B1%D9%88%DA%98%D9%87
[H044]: https://help.mizito.ir/article/697daf3499b384d46b6a479f/%D8%AA%D9%86%D8%B8%DB%8C%D9%85%D8%A7%D8%AA-%D9%BE%D8%B1%D9%88%DA%98%D9%87-%D8%B3%D8%A7%D8%AF%D9%87:-(%D9%86%D8%B3%D8%AE%D9%87-%D9%BE%D8%A7%DB%8C%D9%87)
[H045]: https://help.mizito.ir/article/697db2a699b384d46b6a47a3/%D8%AA%D9%86%D8%B8%DB%8C%D9%85%D8%A7%D8%AA-%D9%BE%D8%B1%D9%88%DA%98%D9%87-%D9%BE%DB%8C%D8%B4%D8%B1%D9%81%D8%AA%D9%87
[H046]: https://help.mizito.ir/article/697dc19b99b384d46b6a47a6/%DA%AF%D8%B1%D9%88%D9%87-%D9%BE%D8%B1%D9%88%DA%98%D9%87
[H047]: https://help.mizito.ir/article/697dc44299b384d46b6a47aa/%D8%B3%D8%B1%D8%A8%D8%B1%DA%AF-%D9%88%D8%B8%D8%A7%DB%8C%D9%81
[H048]: https://help.mizito.ir/article/697dc94b99b384d46b6a47ae/%D8%A8%D9%88%D8%B1%D8%AF-%D9%BE%D8%B1%D9%88%DA%98%D9%87
[H049]: https://help.mizito.ir/article/697ddbc099b384d46b6a47b2/%D8%B3%D8%B1%D8%A8%D8%B1%DA%AF-%D8%AA%D9%82%D9%88%DB%8C%D9%85
[H050]: https://help.mizito.ir/article/697dddfc99b384d46b6a47b6/%D8%AC%D9%84%D8%B3%D9%87-%D8%A2%D9%86%D9%84%D8%A7%DB%8C%D9%86
[H051]: https://help.mizito.ir/article/697ddfed99b384d46b6a47bb/%D8%A8%D8%AC-(badge)-%D9%88-%D9%86%D9%85%D9%88%D8%AF%D8%A7%D8%B1%D9%87%D8%A7
[H052]: https://help.mizito.ir/article/698082b71d8eb1045ca360b9/%DA%AF%D8%A7%D9%86%D8%AA-%DA%86%D8%A7%D8%B1%D8%AA
[H053]: https://help.mizito.ir/article/6986f0cb1d8eb1045ca360cc/%D8%A2%D8%B1%D8%B4%DB%8C%D9%88-%D9%BE%D8%B1%D9%88%DA%98%D9%87
[H054]: https://help.mizito.ir/article/6986f3551d8eb1045ca360ce/%D8%B5%D9%88%D8%B1%D8%AA%D8%AC%D9%84%D8%B3%D9%87-%D9%88-%D8%A7%D9%86%D9%88%D8%A7%D8%B9-%D8%A2%D9%86
[H055]: https://help.mizito.ir/article/6986f4b41d8eb1045ca360d2/%D8%B5%D9%88%D8%B1%D8%AA%D8%AC%D9%84%D8%B3%D9%87-%D8%B3%D8%A7%D8%AF%D9%87
[H056]: https://help.mizito.ir/article/698717511d8eb1045ca360d8/%D8%B5%D9%88%D8%B1%D8%AA%D8%AC%D9%84%D8%B3%D9%87-%D8%B3%D8%A7%D8%B2%D9%85%D8%A7%D9%86%DB%8C-(%D9%BE%DB%8C%D8%B4%D8%B1%D9%81%D8%AA%D9%87)
[H057]: https://help.mizito.ir/article/698732121d8eb1045ca360dd/%D8%A7%D9%84%DA%AF%D9%88%DB%8C-%D8%B5%D9%88%D8%B1%D8%AA%D8%AC%D9%84%D8%B3%D9%87
[H058]: https://help.mizito.ir/article/698734691d8eb1045ca360e0/%DA%A9%D9%BE%DB%8C-%DA%A9%D8%B1%D8%AF%D9%86-%D9%BE%D8%B1%D9%88%DA%98%D9%87
[H059]: https://help.mizito.ir/article/6988385b1d8eb1045ca360e8/%D8%A7%D9%86%D8%AA%D9%82%D8%A7%D9%84-%D9%BE%D8%B1%D9%88%DA%98%D9%87-%D8%A7%D8%B2-%D8%AA%D8%B1%D9%84%D9%88-(Trello)-%D8%A8%D9%87-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88
[H060]: https://help.mizito.ir/article/698851b71d8eb1045ca360ed/%D8%A7%D9%86%D8%AA%D9%82%D8%A7%D9%84-%D9%88%D8%B8%D8%A7%DB%8C%D9%81-%D8%A8%D9%87-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88-%D8%A7%D8%B2-%D8%B7%D8%B1%DB%8C%D9%82-%D9%81%D8%A7%DB%8C%D9%84-CSV
[H061]: https://help.mizito.ir/article/69885a2c1d8eb1045ca360f2/%D8%A7%D9%86%D8%AA%D9%82%D8%A7%D9%84-%D9%88%D8%B8%D8%A7%DB%8C%D9%81-%D8%A8%D9%87-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88-%D8%A7%D8%B2-%D8%B7%D8%B1%DB%8C%D9%82-%D9%81%D8%A7%DB%8C%D9%84-%D8%A7%DA%A9%D8%B3%D9%84-(Excel)
[H062]: https://help.mizito.ir/article/698865e91d8eb1045ca360f5/%D9%85%D9%86%D8%B4%D9%86-%D8%AF%D8%B1-%DA%AF%D8%B1%D9%88%D9%87-%D9%BE%D8%B1%D9%88%DA%98%D9%87
[H063]: https://help.mizito.ir/article/69887d941d8eb1045ca360f9/%DA%AF%D8%B1%D9%88%D9%87--%D8%A8%D9%86%D8%AF%DB%8C-%D9%BE%D8%B1%D9%88%DA%98%D9%87-%D9%87%D8%A7
[H064]: https://help.mizito.ir/article/6991afcde69ec52d9155129e/%D8%A2%D8%B4%D9%86%D8%A7%DB%8C%DB%8C-%D8%A8%D8%A7-%D8%A8%D8%AE%D8%B4-%D9%88%D8%B8%D8%A7%DB%8C%D9%81
[H065]: https://help.mizito.ir/article/6991b368e69ec52d91551385/%D8%A7%DB%8C%D8%AC%D8%A7%D8%AF-%D9%88%D8%B8%DB%8C%D9%81%D9%87
[H066]: https://help.mizito.ir/article/6991c032a0f86e7782e69d7f/%D8%B1%D9%88%D8%B4-%D9%87%D8%A7%DB%8C-%D8%A7%D9%86%D8%AC%D8%A7%D9%85-%D9%88%D8%B8%DB%8C%D9%81%D9%87
[H067]: https://help.mizito.ir/article/6991b8a9e69ec52d915513b5/%D9%88%DB%8C%D8%B1%D8%A7%DB%8C%D8%B4-%D9%88-%D8%AD%D8%B0%D9%81-%D9%88%D8%B8%DB%8C%D9%81%D9%87
[H068]: https://help.mizito.ir/article/699417d7763dc3b82e37f86d/%D8%AA%D8%A8%D8%AF%DB%8C%D9%84-%D9%88%D8%B8%DB%8C%D9%81%D9%87-%D8%AA%DA%A9%D9%85%DB%8C%D9%84-%D8%B4%D8%AF%D9%87-%D8%A8%D9%87-%D8%AF%D8%B1-%D8%AD%D8%A7%D9%84-%D8%A7%D9%86%D8%AC%D8%A7%D9%85
[H069]: https://help.mizito.ir/article/6991ba23e69ec52d915513e5/%D8%A7%D9%84%DA%AF%D9%88%DB%8C-%D9%88%D8%B8%DB%8C%D9%81%D9%87-%D9%88-%D8%AA%D9%86%D8%B8%DB%8C%D9%85%D8%A7%D8%AA-%D8%A2%D9%86
[H070]: https://help.mizito.ir/article/6a815f948d44a80012a1dd31/%DA%A9%D9%BE%DB%8C-%D9%88%D8%B8%DB%8C%D9%81%D9%87
[H071]: https://help.mizito.ir/article/6994123d763dc3b82e37f82f/%D8%B3%D8%A7%D8%A8%D9%82%D9%87-%D8%AA%D8%BA%DB%8C%DB%8C%D8%B1%D8%A7%D8%AA-%D8%AF%D8%B1-%D9%88%D8%B8%DB%8C%D9%81%D9%87
[H072]: https://help.mizito.ir/article/69809f651d8eb1045ca360c3/%D9%88%D8%B2%D9%86-%D9%88%D8%B8%DB%8C%D9%81%D9%87
[H073]: https://help.mizito.ir/article/69940dd7763dc3b82e37f7ec/%D8%AA%D9%82%D9%88%DB%8C%D9%85
[H074]: https://help.mizito.ir/article/6994189e763dc3b82e37f895/%D9%85%D9%87%D9%84%D8%AA-%D8%A7%D9%86%D8%AC%D8%A7%D9%85-%D9%88%D8%B8%DB%8C%D9%81%D9%87
[H075]: https://help.mizito.ir/article/699418fc763dc3b82e37f8ce/%D9%85%D9%81%D9%87%D9%88%D9%85-%D9%88-%DA%A9%D8%A7%D8%B1%D8%A8%D8%B1%D8%AF-%DA%86%DA%A9--%D9%84%DB%8C%D8%B3%D8%AA-%D9%88%D8%B8%DB%8C%D9%81%D9%87
[H076]: https://help.mizito.ir/article/699420e5763dc3b82e37f947/%D9%88%D8%B8%DB%8C%D9%81%D9%87-%D8%AA%DA%A9%D8%B1%D8%A7%D8%B1-%D8%B4%D9%88%D9%86%D8%AF%D9%87
[H077]: https://help.mizito.ir/article/69942281763dc3b82e37f977/%D8%A7%D8%B1%D8%AC%D8%A7%D8%B9-%D9%88%D8%B8%DB%8C%D9%81%D9%87-%D8%A8%D9%87-%DA%86%D9%86%D8%AF-%D9%86%D9%81%D8%B1-%D9%88-%DA%A9%D8%A7%D8%B1%D8%A8%D8%B1%D8%AF-%D8%A2%D9%86
[H078]: https://help.mizito.ir/article/699422f7763dc3b82e37f9a7/%D9%88%D8%B8%DB%8C%D9%81%D9%87-%D8%A8%D8%AF%D9%88%D9%86-%D8%A7%D9%86%D8%AC%D8%A7%D9%85-%D8%AF%D9%87%D9%86%D8%AF%D9%87
[H079]: https://help.mizito.ir/article/6994243e763dc3b82e37f9d8/%D8%A7%DB%8C%D8%AC%D8%A7%D8%AF-%D9%88%D8%B8%DB%8C%D9%81%D9%87-%D8%A8%D8%A7-%D8%AA%D8%A7%DB%8C%DB%8C%D8%AF-%DA%A9%D9%86%D9%86%D8%AF%D9%87-%D9%86%D9%87%D8%A7%DB%8C%DB%8C
[H080]: https://help.mizito.ir/article/69942633763dc3b82e37fa00/%D9%85%D9%86%D8%B4%D9%86-%D8%AF%D8%B1-%D9%88%D8%B8%DB%8C%D9%81%D9%87
[H081]: https://help.mizito.ir/article/69995e6c763dc3b82e37fc39/%D9%85%D9%81%D9%87%D9%88%D9%85-%D9%86%D8%A7%D9%85%D9%87
[H082]: https://help.mizito.ir/article/69995ed9763dc3b82e37fc47/%D8%B1%D9%88%D8%B4-%D8%A7%DB%8C%D8%AC%D8%A7%D8%AF-%D9%86%D8%A7%D9%85%D9%87
[H083]: https://help.mizito.ir/article/69995f37763dc3b82e37fc54/%D8%AC%D8%B2%D8%A6%DB%8C%D8%A7%D8%AA-%D9%86%D8%A7%D9%85%D9%87-(%D9%BE%D8%A7%D8%B3%D8%AE%D8%8C-%D8%A7%D8%B1%D8%AC%D8%A7%D8%B9-%D9%88-%D8%A2%D8%B1%D8%B4%DB%8C%D9%88-%D9%86%D8%A7%D9%85%D9%87-)
[H084]: https://help.mizito.ir/article/6a36725d4fc55f0012745bda/%D8%AD%D8%B0%D9%81-%D9%86%D8%A7%D9%85%D9%87-
[H085]: https://help.mizito.ir/article/69995f70763dc3b82e37fc61/%D9%85%D9%81%D9%87%D9%88%D9%85-%D8%AF%D8%A8%DB%8C%D8%B1%D8%AE%D8%A7%D9%86%D9%87
[H086]: https://help.mizito.ir/article/69995f9c763dc3b82e37fc6e/%D9%81%DB%8C%D9%84%D8%AA%D8%B1-%D9%86%D8%A7%D9%85%D9%87-%D9%87%D8%A7
[H087]: https://help.mizito.ir/article/69995fca763dc3b82e37fc7b/%D8%A7%D8%AA%D8%B5%D8%A7%D9%84-%D9%86%D8%A7%D9%85%D9%87-%D8%A8%D9%87-%D9%BE%D8%B1%D9%88%D9%86%D8%AF%D9%87-%D9%85%D8%B4%D8%AA%D8%B1%DB%8C%D8%A7%D9%86
[H088]: https://help.mizito.ir/article/69996028763dc3b82e37fcba/%D9%85%D9%81%D9%87%D9%88%D9%85-%DB%8C%D8%A7%D8%AF%D8%AF%D8%A7%D8%B4%D8%AA-%D9%87%D8%A7
[H089]: https://help.mizito.ir/article/6999605f763dc3b82e37fcc7/%D8%A7%DB%8C%D8%AC%D8%A7%D8%AF-%DB%8C%D8%A7%D8%AF%D8%AF%D8%A7%D8%B4%D8%AA-%D8%AF%D8%B1-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88
[H090]: https://help.mizito.ir/article/6999608e763dc3b82e37fcd4/%D9%81%DB%8C%D9%84%D8%AA%D8%B1-%DB%8C%D8%A7%D8%AF%D8%AF%D8%A7%D8%B4%D8%AA-%D9%87%D8%A7
[H091]: https://help.mizito.ir/article/699960d8763dc3b82e37fce8/%D9%88%DB%8C%D8%B1%D8%A7%DB%8C%D8%B4-%DB%8C%D8%A7%D8%AF%D8%AF%D8%A7%D8%B4%D8%AA
[H092]: https://help.mizito.ir/article/69996109763dc3b82e37fcf5/%D8%AD%D8%B0%D9%81-%D9%88-%D8%A2%D8%B1%D8%B4%DB%8C%D9%88-%DB%8C%D8%A7%D8%AF%D8%AF%D8%A7%D8%B4%D8%AA
[H093]: https://help.mizito.ir/article/69a6813f49f9f8d00252adb2/%D9%85%D9%81%D9%87%D9%88%D9%85-%D9%BE%D8%B1%D9%88%D9%86%D8%AF%D9%87-%D9%85%D8%B4%D8%AA%D8%B1%DB%8C%D8%A7%D9%86-%D9%88-%D9%86%D8%AD%D9%88%D9%87-%D8%AF%D8%B3%D8%AA%D8%B1%D8%B3%DB%8C-%D8%A8%D9%87-%D8%A2%D9%86
[H094]: https://help.mizito.ir/article/69a68ef049f9f8d00252ae23/%D8%A8%D8%AE%D8%B4-%D9%87%D8%A7%DB%8C-%D9%BE%D8%B1%D9%88%D9%86%D8%AF%D9%87-%D9%85%D8%B4%D8%AA%D8%B1%DB%8C%D8%A7%D9%86-(%D8%B3%D8%B1%D8%A8%D8%B1%DA%AF-%D9%87%D8%A7)
[H095]: https://help.mizito.ir/article/69d778d717f243f6a25be763/%D8%AB%D8%A8%D8%AA-%D8%A7%D8%B7%D9%84%D8%A7%D8%B9%D8%A7%D8%AA-%D9%85%D8%B4%D8%AA%D8%B1%DB%8C-%D8%AC%D8%AF%DB%8C%D8%AF
[H096]: https://help.mizito.ir/article/69a6a75849f9f8d00252aece/%D8%AC%D8%B2%D8%A6%DB%8C%D8%A7%D8%AA-%D9%BE%D8%B1%D9%88%D9%86%D8%AF%D9%87-%D9%85%D8%B4%D8%AA%D8%B1%DB%8C
[H097]: https://help.mizito.ir/article/69a67eb949f9f8d00252ad82/%D8%A7%D8%B1%D8%B3%D8%A7%D9%84-%D9%BE%DB%8C%D8%A7%D9%85-%D8%BA%DB%8C%D8%B1-%D9%85%D8%AA%D9%86%DB%8C-%D8%AF%D8%B1-%D9%BE%D8%B1%D9%88%D9%86%D8%AF%D9%87-%D9%85%D8%B4%D8%AA%D8%B1%DB%8C%D8%A7%D9%86
[H098]: https://help.mizito.ir/article/69a68d0149f9f8d00252adeb/%D8%A7%D9%86%D8%AA%D9%82%D8%A7%D9%84-%D9%BE%D8%B1%D9%88%D9%86%D8%AF%D9%87-%D9%85%D8%B4%D8%AA%D8%B1%DB%8C%D8%A7%D9%86-%D8%A7%D8%B2-%D9%81%D8%A7%DB%8C%D9%84-%D8%A7%DA%A9%D8%B3%D9%84-%D8%A8%D9%87-%D9%85%DB%8C%D8%B2%DB%8C%D8%AA%D9%88
[H099]: https://help.mizito.ir/article/69a6b02f49f9f8d00252af3e/%D9%81%DB%8C%D9%84%D8%AA%D8%B1%D9%87%D8%A7%DB%8C-%D9%BE%D8%B1%D9%88%D9%86%D8%AF%D9%87-%D9%85%D8%B4%D8%AA%D8%B1%DB%8C%D8%A7%D9%86
[H100]: https://help.mizito.ir/article/69a68f7a49f9f8d00252ae53/%D8%AA%D9%86%D8%B8%DB%8C%D9%85%D8%A7%D8%AA-%DA%AF%D8%B1%D9%88%D9%87-%D9%BE%D8%B1%D9%88%D9%86%D8%AF%D9%87-%D9%85%D8%B4%D8%AA%D8%B1%DB%8C
[H101]: https://help.mizito.ir/article/69a6901449f9f8d00252ae73/%D8%AB%D8%A8%D8%AA-%D8%B3%D9%86%D8%AF-%D9%85%D8%A7%D9%84%DB%8C
[H102]: https://help.mizito.ir/article/69a6aae249f9f8d00252af0e/%D9%81%D8%B1%D8%B5%D8%AA-%D9%81%D8%B1%D9%88%D8%B4
[H103]: https://help.mizito.ir/article/69a6baec49f9f8d00252b102/%D9%85%D9%81%D9%87%D9%88%D9%85-%D9%85%D8%A7%D9%86%DB%8C%D8%AA%D9%88%D8%B1%DB%8C%D9%86%DA%AF
[H104]: https://help.mizito.ir/article/69a6c95449f9f8d00252b15a/%D9%85%D8%A7%D9%86%DB%8C%D8%AA%D9%88%D8%B1%DB%8C%D9%86%DA%AF-%D9%BE%D8%B1%D9%88%DA%98%D9%87-%D9%87%D8%A7
[H105]: https://help.mizito.ir/article/69d4ef3e17f243f6a25bdb9d/%D9%85%D8%A7%D9%86%DB%8C%D8%AA%D9%88%D8%B1%DB%8C%D9%86%DA%AF-%D9%88%D8%B8%D8%A7%DB%8C%D9%81
[H106]: https://help.mizito.ir/article/69a6cb2249f9f8d00252b1e1/%D9%85%D8%A7%D9%86%DB%8C%D8%AA%D9%88%D8%B1%DB%8C%D9%86%DA%AF-%D9%BE%D8%B1%D9%88%D9%86%D8%AF%D9%87-%D9%85%D8%B4%D8%AA%D8%B1%DB%8C%D8%A7%D9%86
[H107]: https://help.mizito.ir/article/69a6ca0149f9f8d00252b192/%D9%85%D8%A7%D9%86%DB%8C%D8%AA%D9%88%D8%B1%DB%8C%D9%86%DA%AF-%D8%B5%D9%88%D8%B1%D8%AA%D8%AC%D9%84%D8%B3%D8%A7%D8%AA
[H108]: https://help.mizito.ir/article/69a6c90d49f9f8d00252b132/%D9%85%D8%A7%D9%86%DB%8C%D8%AA%D9%88%D8%B1%DB%8C%D9%86%DA%AF-%D8%A7%D8%B9%D8%B6%D8%A7%DB%8C-%D8%AA%DB%8C%D9%85
[H110]: https://help.mizito.ir/article/6a76f95446cee20012bcda1c/%D9%85%D9%81%D9%87%D9%88%D9%85-%D9%88-%D8%AA%D8%B9%D8%B1%DB%8C%D9%81-%DA%A9%D8%A7%D8%B1%D8%A8%D8%B1-%D9%85%D9%87%D9%85%D8%A7%D9%86
[H111]: https://help.mizito.ir/article/6a76facd4fc55f0012748ede/%D9%85%D8%AC%D9%88%D8%B2%D9%87%D8%A7%DB%8C-%DA%A9%D8%A7%D8%B1%D8%A8%D8%B1-%D9%85%D9%87%D9%85%D8%A7%D9%86
[H112]: https://help.mizito.ir/article/6a76f9ce46cee20012bcda3f/%D8%A7%D8%B6%D8%A7%D9%81%D9%87-%DA%A9%D8%B1%D8%AF%D9%86-%DA%A9%D8%A7%D8%B1%D8%A8%D8%B1-%D9%85%D9%87%D9%85%D8%A7%D9%86-%D8%A8%D9%87-%D9%85%DB%8C%D8%B2%DA%A9%D8%A7%D8%B1
[H113]: https://help.mizito.ir/article/6a76fa204fc55f0012748e91/%D8%A7%D8%B1%D8%AA%D8%A8%D8%A7%D8%B7-%DA%A9%D8%A7%D8%B1%D8%A8%D8%B1-%D9%85%D9%87%D9%85%D8%A7%D9%86-%D8%A8%D8%A7-%D8%A7%D8%B9%D8%B6%D8%A7
[H114]: https://help.mizito.ir/article/6a76fa758d44a80012a1d031/%DA%A9%D8%A7%D8%B1%D8%A8%D8%B1-%D9%85%D9%87%D9%85%D8%A7%D9%86-%D8%AF%D8%B1-%D8%A8%D8%AE%D8%B4-%D9%87%D8%A7%DB%8C-%D9%85%D8%AE%D8%AA%D9%84%D9%81
[PRICE]: https://www.mizito.ir/pricing
[OFFICE]: https://office.mizito.ir/#/lg/login
[FONT]: https://github.com/rastikerdar/vazirmatn/tree/v33.003/Round-Dots
[OWNER]: PRODUCT-SCOPE.md
