# Product scope

## Mandate and boundaries

Miz-e Kar is an independently implemented production web application for Debian self-hosting. Full remaining Mizito web scope must survive incremental delivery. This is not a reduced task-manager product. Independent Persian branding, copy and visual design are required; parity concerns observable capability and behavior, not pixel copying.

Included modules are account/security, workspaces and memberships, layered permissions and guests, dashboards, projects and categories, personal/team tasks, list/board/calendar/Gantt, conversations/channels, assistant and mentions, polls/questionnaires/quizzes, online meetings, simple and organizational minutes, customer records/call reports, sales opportunities, financial records and analytics, correspondence/registry, personal notes, attachments, search, bookmarks, notifications, themes, monitoring, imports, print/report output, archive/recovery, and documented plan/capacity administration.

Native Android/iOS builds, biometric login and native sharing/SMS auto-fill are excluded. Responsive browser use, and browser/PWA notification behavior where applicable, remain in the web backlog. Legal validity of signatures is not established by the reference's use of the term digital signature. Mizito's support service, payment account and commercial assets cannot be reused; equivalent product entry points and plan administration remain tracked pending owner decisions.

## Evidence model

Research date: **2026-11-03** (owner context: Asia/Tehran). `D` = public documentation; `O` = directly observed UI; `I` = inference/proposed safeguard; `U` = unknown. D is never O. A requirement can contain D behavior and U error handling. Matrix acceptance criteria are proposed checks, not executed tests or approved design decisions.

The public help landing page, all 14 top-level categories, 108 linked articles, and six additional guest pages were fetched. Seven tutorial landing pages were read; video playback was not verified. Five listed release notes cover Farvardin 1402, Mordad 1402, Dey 1402, Shahrivar 1403 and Tir 1405. These are the versions listed publicly, not proof of the authenticated deployment's version. The public pricing comparison was also read. The reference app was opened in Chromium to the login form only; no account was created or used.

The source register lists exact URLs and inherited access dates. All discovered capabilities map to stable matrix IDs and delivery phases. It is a discovery baseline, not a claim that inaccessible UI has been exhaustively enumerated. New evidence must extend the backlog rather than reduce the target.

## Important behavioral boundaries

- Workspaces are independent. Workspace roles, project/group roles, resource membership, feature grants and plan entitlement are distinct dimensions.
- Owners/admins have broad monitoring powers, but personal chats, personal note content and unnumbered letters have explicit privacy boundaries. Note *counts* can appear in monitoring.
- Board columns do not represent task completion. Shared tasks, copied tasks and final-approval tasks have different completion semantics.
- Recurrence has a completion-gated next instance; calendar future occurrences may be projections rather than already-created tasks.
- Linking a letter to a customer does not grant all customer members access to its content.
- Financial records are a receivables/payables tracking capability; a full accounting ledger, invoicing/tax engine or external banking integration is not evidenced.
- Customer stages can be represented by labels; a separate customizable sales pipeline engine is not verified. Forms are mentioned through tracking-number filters; a form builder has not been established.

## Plan and version reconciliation

| Topic | Public evidence | Treatment before implementation |
| --- | --- | --- |
| Free/base/advanced | Help footer broadly says all features are free; pricing differentiates base/advanced and a free base tier. | Treat footer as promotional; preserve advanced scope. Do not infer entitlements from it. |
| Gantt visibility | H052 says project managers only; H021 and pricing explicitly mention read-only member/guest access. | Keep both manage and view grants; obtain current advanced screen (Q02). |
| Group/project member removal | H040 says creator-only; project settings and H045 describe managers managing members. | Capture action-specific policy; no blanket admin override inferred (Q02). |
| Personal message deletion | H033 contains broad deletion language and a manager-only detail; H034 and tutorial H014 impose read-based restrictions. | Verify personal/group/channel separately (Q03). |
| Final task approver | H079 describes one selected approver; pricing says one or more. | Quorum/count is unresolved; retain approval flow (Q04). |
| Organizational minutes quorum | H054 refers to meeting members; H056 specifies attendees present. | Confirm denominator, abstentions and signatures before automating dispatch (Q05). |
| Task categories | H065 requires a project for each task; H067 and H069 refer to task categories/settings, and H114 allows a guest assignment without project membership. | Establish category ownership and membership schema (Q06). |
| Archive/delete | H040 uses full deletion language; owner tools describe recoverable groups. Project archive retains tasks optionally (Tir 1405). | Per-resource lifecycle, never generic cascading deletion (Q07). |
| Calendar | Marketing mentions day/week/month; detailed project help documents monthly view, due/reminder toggle and no-time tasks. | Month is documented; other view interactions require evidence (Q08). |
| Task templates and mute duration | Older UI placement differs; Tir 1405 moves templates to project/category settings and extends browser mute to 1/2/4/8 hours. | Use release-aware baseline, verify current UI. |
| Paraph deletion | H084 leaves admin exception broad; Tir 1405 limits admin to their own paraphs. | Do not grant deletion of others' paraphs without evidence (Q03). |

## Completion standard

A parity milestone needs dated reference evidence, positive and negative business/authorization tests, browser acceptance against working software, and an explicit gap list. No phase may claim complete parity from documentation, mockups or isolated unit tests. Deployment readiness also needs migration and restore rehearsals, attachment recovery and measured operating limits. Architecture and delivery sequence below are recommendations awaiting owner review.
