# Open questions and evidence requests

No passwords, OTPs, cookies, tokens or unredacted customer content should be placed in repository files. Owner-provided evidence should use a disposable/reference workspace with synthetic data. This is an evidence checklist, not a request to bypass authentication. No owner evidence has been supplied yet.

## Prioritized questions

| ID | Unknown / decision needed | Smallest useful evidence or answer | Blocks |
| --- | --- | --- | --- |
| Q01 | Which authenticated web build and plan is the parity baseline? | Screenshot showing plan and available version/build information, or explicitly state version unavailable. | Final reference baseline; does not stop public discovery. |
| Q02 | Exact per-action workspace/project/group/guest grants; creator vs manager removal; Gantt view delegation. | Advanced permissions and project settings tabs; short owner/admin/member/guest comparison using same resource. | Policy schema and acceptance; WS/PR/GA/MON. |
| Q03 | Personal/group/letter edit/delete rules, admin exceptions, paraph audience and forwarded history. | Send/read then attempt edit/delete with sender and participating admin; show forwarded letter recipient view. | CH/LE authorization. |
| Q04 | One or multiple final approvers; waiting approval, rejection and reopen semantics. | One shared two-person task with final approval: performer ticks, approver finalizes and reopens. | Task state machine and tests. |
| Q05 | Minutes actors, required fields, quorum denominator, absent/external attendees, signature representation and resolution dispatch. | Organizational minutes draft → attendance → request → signatures; include one absent participant and resulting tasks. | ME workflow; legal-signature scope decision. |
| Q06 | Standalone task category vs project category; guest task outside project; customer minutes task project selection. | Categories tab/settings, a category task, and assigned nonmember guest opening a task. | Relational schema and private task grant. |
| Q07 | Resource archive/delete/restore and memberships after recovery; task dispositions. | Both project archive choices plus owner project/task recovery; group/customer recovery screen. | Lifecycle and recovery. |
| Q08 | Calendar view modes, timezone/holiday source, date-only deadlines, recurrence month ends and Gantt phase drag. | Calendar mode picker and recurrence dialog; one month-end schedule and phase drag. | Date adapter and scheduling semantics. |
| Q09 | Preferred stack/team skills and acceptance of architecture proposal; RD weight/variant selection. | Owner decision on Django/React vs alternative and intended maintainers; choose regular RD unless another RD variant intended. | Stack selection; no dependencies installed yet. |
| Q10 | SMS/email/push providers, OTP expiry/resend/lockout, recovery and guest activation security. | Provider availability/deployment restrictions; redacted security/notification dialogs, no codes. | Real onboarding and external delivery. |
| Q11 | Target Debian version, hardware, users/concurrency/workspaces, expected files/data and network model; note scope. | Approximate expected deployment and whether Internet/air-gapped; note behavior across two workspaces. | Sizing, topology, backup/search choices. |
| Q12 | Self-hosted plan/entitlement and billing behavior: full-feature internal deployment or commercial subscriptions? | Owner policy; plan/expiry/capacity screen and redacted invoice flow if commercial parity required. | Entitlement/payment adapter; retained in scope until decided. |
| Q13 | Exact metrics, delays, counts, unread rules, notification channels and presence retention. | Small known fixture and its dashboard/project/member charts; notification preference/history screens. | Reports and event acceptance. |
| Q14 | Forms referenced by tracking-number filters: first-class web module, add-on or integration? Any undocumented menus? | Open filter and linked form screen; screenshot of expanded menus/settings. | Additional module discovery; no form builder assumed. |
| Q15 | Import samples and error/partial/retry behavior; copy field set and task transfer cross-effects. | Empty official CSV/Excel templates, one failed import preview and task/project copy/move dialogs. | Import/copy atomicity and tests. |
| Q16 | File types/quota/limits, forwarding ownership and upload/recording failure behavior. | Upload/forward dialog, current quota screen and oversize response with synthetic file. | Storage API and recovery. |
| Q17 | Search coverage, normalization/ranking, bookmark scope and assistant commands. | One Persian query with mixed Arabic letters/digits plus result opening and command help. | Search/assistant acceptance. |
| Q18 | Poll retraction/closing actors, anonymous result policy, quiz scoring/print and templates. | One anonymous multi-question quiz with respondent and admin results. | Poll correctness and privacy. |
| Q19 | Experimental meeting availability/provider/network/device constraints and guest admission. | Two-browser call with screen sharing and denied-device state; state reference plan/build. | Media service evaluation. |
| Q20 | Gantt dependency cycles, date changes, zoom, phase drag and read-only grants. | Dependent tasks with overlap and cycle attempt; viewer attempts edit. | Gantt domain rules. |
| Q21 | CRM create/edit/print scope, duplicate phone behavior, basic print fields and label logic. | Synthetic customer/representatives, duplicate warning, print and multi-label filter. | CRM validation and ACL. |
| Q22 | Currency/rial/toman, precision, financial void/refund/edit rules, sales stages/close dates and forecast buckets. | One probable/overdue/realized/void document and one opportunity with resulting tables. | Finance/sales calculations. |
| Q23 | Registry numbering actor, independent sequence key, corrections and concurrent behavior. | Incoming/outgoing registration dialogs with two numbering series and duplicate attempt. | Letter numbering and uniqueness. |
| Q24 | Availability/RPO/RTO, backup retention/location, privacy/purge policies and operational owner. | Owner targets and retention decisions, including note purge versus retained backups/presence history. | Production readiness and recovery plan. |

## Minimum request for the next slice

First send **one redacted plan/build screenshot and a 2–3 minute recording of a shared task with final approver**: show project advanced permission settings, performer completion, approver completion and reopen. This resolves Q01/Q04 and part of Q02 using synthetic names. No credentials or access to the owner's account are needed. If recording is unavailable, the equivalent five screenshots are sufficient.

## Follow-up capture checklist (only when its module is next)

1. Workspace settings: member/invite/deleted tabs, guest visibility, feature grants and owner repair dialogs (Q02/Q07/Q12).
2. Project/category: all advanced tabs, task categories, board settings, both calendars, archive modes, copy/import samples (Q06/Q08/Q15).
3. Conversations/assistant: before/after-read actions, voice/file controls, search, mentions/unread, bookmarks, anonymous quiz (Q03/Q16/Q17/Q18).
4. Gantt: view/edit delegation, phases, overlapping dependencies, cycle attempt, phase drag, zoom/print (Q02/Q20).
5. Minutes: role fields, draft/attendance/signing states, absent attendee, task dispatch and template (Q05).
6. CRM/sales/finance: customer members/representatives, call conversion, print, opportunity and each money state with monthly report (Q21/Q22).
7. Letters: unread/read sender/admin actions, paraph recipients/forward, registry numbering and customer link seen by a nonrecipient (Q03/Q23).
8. Monitoring/settings: known-count fixtures, member online history, restricted monitor, notices/mute/sessions/theme and any extra menus (Q10/Q13/Q14).
9. Online meeting: two participants and device denial/screen sharing (Q19).

Record role, plan/build, browser and approximate recording date with each item. Mask real phone numbers and business content; omit login/OTP/password screens. Public tutorial text was reviewed, but video playback was not; an owner recording should resolve current behavior rather than reproduce marketing demonstrations.
