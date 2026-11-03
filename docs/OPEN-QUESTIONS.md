# Open questions and slice gates

Updated 2026-11-03 for Phase 0.1. No authenticated owner recording has been supplied. Core stack approval is recorded in ARCHITECTURE-PROPOSAL.md; it is a decision, not an observation of Mizito. No passwords, OTPs, session cookies or real customer data belong in this repository.

**P1a has no outstanding owner-evidence blocker.** It uses synthetic accounts, seeded memberships and documented independent-workspace behavior. Official dependency compatibility/support verification is an implementation preflight, not a reason to request task/finance/meeting recordings. Unknowns below stay open even when independent work proceeds. “Earliest gate” applies only to the stated action; it does not block an entire phase or its unrelated foundations.

## Q06 split: affiliation, category and access

Q06 remains a grouping/legacy alias; use its independent child questions in requirements and implementation work:

| ID | Question / current evidence | Remaining unknown | Earliest genuine gate |
| --- | --- | --- | --- |
| Q06a | Does a task belong to a project? **D:** H065 explicitly requires a project when creating a task, including customer follow-up. | All hidden creation paths and database cardinality are not observed. No projectless task is established. | P1e may implement the documented project-bound flow; evidence needed before any alternative projectless path or broader schema claim. No P1a gate. |
| Q06b | How does a task category relate to a project? **D:** H042 auto-creates a category with a project; H067 mentions category membership; H069/H024 describe template/settings contexts. | Identity versus grouping, cardinality, independent creation and membership lifecycle remain **U**. “Standalone category” was an unverified interpretation. | P1d category model/automatic creation and later category-aware task access. Capture categories/settings and their project link. No P1a gate. |
| Q06c | Can an assigned guest access a task without project membership? **D:** H114 explicitly permits this assignment. | Exact guest-visible fields/reports, changes after revocation and related project/customer access remain **U**. It does not imply the task lacks a project. | P2 guest task-access slice, before granting related-resource visibility. No P1a/P1d ordinary-member gate. |

Five existing source URLs H042/H065/H067/H069/H114 were re-fetched (HTTP 200) on 2026-11-03; H024 was reread from the prior capture. See the [targeted recheck](REFERENCE-SOURCES.md). This is documentation evidence, not authenticated verification.

## Remaining questions classified by earliest affected slice

| ID | Open issue / current status | Earliest genuine gate; unaffected work | Minimum evidence or decision at that point |
| --- | --- | --- | --- |
| Q01 | Reference authenticated plan/build unknown. | P1b/P1c reference comparison and final P7 parity baseline; does not block P1a engineering acceptance. | Redacted plan/build label, or explicit version-unavailable note. |
| Q02 | Action-specific workspace/project/group/guest policies remain partially unknown. Basic active membership isolation is documented. | P1b invitation/management actors first; project creation in P1d, task actions in P1e, guest/Gantt/monitoring later. No gate on P1a member-only workspace reads. | Capture only the actor/action settings needed by the next slice. |
| Q03 | Read-dependent chat/letter/paraph edit/delete and forward audience. | P3 chat rules; letter-specific part P5. No authentication/workspace gate. | Sender/reader/participating-admin before/after-read results. |
| Q04 | Final approver count, pending/rejection/reopen semantics. | P2 final-approval slice. No P1a or ordinary single-performer P1e gate. | One shared approval task lifecycle when that slice is next. |
| Q05 | Minutes actors/quorum/absentees/external invitees/signature representation. | P4 minutes/signature/resolution dispatch. | One organizational minutes lifecycle and confirmed electorate. |
| Q07 | Archive/delete/restore semantics, including free never-paid workspace deletion. | P2 resource lifecycle/destructive workspace actions; not P1a read/select nor P1b's documented member restoration. | The specific archive/delete/recovery dialog; avoid unrelated resource captures. |
| Q08 | Calendar views/timezone/holidays/date-only/recurrence boundaries. | P1e included scheduling semantics first; P2 recurrence and P4 Gantt afterward. RTL/login shell is independent. | Schedule/date controls for the included flow; boundary fixtures. |
| Q09 | **Core stack choice decided:** Django/DRF + React/TypeScript/Vite + PostgreSQL modular monolith. Versions, licenses, remaining architecture details and maintainer constraints stay open. | P1a engineering preflight verifies official support/compatibility and pins; no further owner stack choice or RD approval is required. RLS/production choices deferred. | Official sources and dated compatibility record; existing verified RD Regular is usable, verify each bundled artifact. |
| Q10 | SMS/email/push providers and OTP/recovery/guest activation details. | P1c real registration/recovery/delivery; P1g external notification channels. Synthetic session login/logout needs none. | Provider availability and challenge/resend/recovery rules, without secrets. |
| Q11 | Target Debian/hardware/load/storage/network model; account-wide vs workspace note scope. | P3 note scope; P7 sizing/topology. Reproducible local P1a PostgreSQL setup does not need production estimates. | Note behavior in two workspaces when relevant; production estimates before sizing. |
| Q12 | Commercial subscriptions, quotas, billing and entitlement policy undecided. | P6 commercial administration or any earlier slice explicitly adding commercial enforcement. Never a gate on advanced functional scope or P1a. | Owner chooses internal full-feature use versus commercial subscriptions; no reference limit becomes a product default automatically. |
| Q13 | Exact event/reminder/count/unread/presence/report semantics. | P1g core events/reminders first; P1h dashboard, later P3/P6 details. No P1a gate. | Known fixture and only the next affected event/panel. |
| Q14 | Form-tracking references may be module/add-on/integration. | P6 additional-surface investigation; no inferred form builder. | Tracking filter and linked screen if present. |
| Q15 | Copy/move/import fields, errors, partial completion and retry semantics. | P2 task copy/move; P6 bulk import/copy. | Specific copy/move dialog or blank import template and failed preview. |
| Q16 | File-type/size/quota/forwarding/error rules. | P1f private attachment flow; later P3 recording/forwarding. No shell/font gate: static licensed font is not a user upload. | One upload/error screen and current limits. |
| Q17 | Search coverage/normalization/ranking/bookmarks/assistant commands. | P3 search/assistant. | One synthetic Persian search and result opening. |
| Q18 | Poll closing/retraction/confidentiality/scoring/templates. | P3 polls/quiz slice. | One anonymous quiz respondent/admin comparison. |
| Q19 | Online meeting availability/media/provider/device/network/guest rules. | P6 media evaluation. | Two-browser call/device denial when relevant. |
| Q20 | Gantt cycles/date propagation/scales/phase drag/view grants. | P4 Gantt. | Dependency and read-only interaction evidence. |
| Q21 | Customer action/print permissions, duplicate phone and filters. | P5 CRM. | Synthetic customer, duplicate warning and print fields. |
| Q22 | Currency/precision/finance states/voids/sales stages/forecast buckets. | P5 finance/sales. No authentication or workspace gate. | One monetary lifecycle and resulting forecast/report. |
| Q23 | Registry numbering actors/series/corrections/concurrency. | P5 registry. | Two series and duplicate registration attempt. |
| Q24 | Recovery/retention/privacy/purge/presence policies and operator targets. | P3 note purge/retention first; P6 presence and P7 recovery qualification. No production sizing gate on P1a dev migrations. | Retention decision for included module; RPO/RTO before production qualification. |

## Evidence checklist for the next affected workflows only

- **P1a:** no owner recording or credentials needed. The implementation agent supplies its own two-user/two-workspace browser and direct-API evidence, dependency verification and migration/reload results. These are Miz-e Kar acceptance checks, not new Mizito observations.
- **Before P1b:** one redacted plan/build image if available; show the actor's member-management role and invite/accept, remove/restore controls for a synthetic regular member. A short recording or equivalent screenshots with actor/action/result is enough. Do not include login, passwords or OTPs.
- **If owner evidence is unavailable:** P1a can proceed under a separate implementation task. Unverified P1b actor boundaries remain open; implement only supported documented behavior or defer the affected action with an explicit gap. Do not guess permissions. Q06b category design waits for its targeted category/project evidence in P1d; Q06c guest visibility waits for P2. No final-approval, finance or minutes capture is requested for P1a.
