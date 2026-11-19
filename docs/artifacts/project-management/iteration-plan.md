## Document Control
- Phase: Survey
- Status: Draft — issued for the end-of-Survey milestone review
- Milestone Target: end of Survey (SBC) — not yet achieved

## Iteration Objectives

Survey is iteration 1 of the sprint zero. It runs on a system nobody here wrote and nobody can ask about: the delivery is a copy of `davidfowl/TodoApp` at `307a1ead`, and `.iari/README.md` records that it carries no requirements, design or architecture document, no database scripts, no manual, no running installation and no reachable authors. This iteration therefore does not build anything — it establishes what the existing system is, at a perimeter the stakeholder will confirm, before any RUP phase plans against it.

| # | Objective | Basis |
|---|---|---|
| 1 | Record the tailoring that governs the sprint zero — the recovered-element rule, the inactive disciplines, the one fired optional. | Development Case, §1–§7 |
| 2 | Draw the perimeter of the existing system from the code: components, external actors, entry points, with the anchor each row was read from. | Development Case DC-D1, DC-D4 |
| 3 | Read the system and record its anomalies — every place the delivery contradicts itself or the documents that describe it — and order the areas Excavation reads in. | System Inventory, Priorities (order 1–8) |
| 4 | Score every anomaly as a project risk, choose a strategy, and put the High-risk acceptances to the stakeholder. | Risk List, all twenty scored |
| 5 | Issue this plan: the cross-iteration roadmap to PR, and this iteration's work items with their owners. | Development Case DC-D1, DC-D7 |

The three stakeholder decisions of 2026-11-19 already taken — external identity-provider sign-in out of scope, the `admin` role as dead code, the self-service identity surface out — are **inputs** to this iteration, not objectives of it. Every one of them is recorded as an exclusion in the System Inventory's Perimeter and carried into R002, R010, R014 and R019.

## Plan and Milestones
### Coarse roadmap — sprint zero then the RUP phases

`6 ± 3` iterations across the project, and this roadmap commits to **8, or 9 if Elaboration needs its second**. The sprint zero adds no milestone of its own to the RUP sequence — it runs before Inception and produces the material Inception builds on. The sequence below is the cross-iteration horizon this plan commits to; nothing beyond the current iteration is planned in detail.

| Order | Phase | Milestone | What the milestone closes | Iterations planned |
|---|---|---|---|---|
| 1 | Survey | **SBC** | The perimeter is drawn and confirmed, the anomalies are recorded, every one scored as a risk, and the tailoring for the sprint zero is issued. | 1 |
| 2 | Excavation | **AR** | The recovered use cases, the recovered architecture, the design model with the persistent schema, and the Deployment Model exist for the priorities Excavation reads first. | 1 |
| 3 | Consolidation | **GHR** | Every entry point of the recovered perimeter has a use case or a recorded exclusion; the Supplementary Specification and the coverage statement complete the set. | 1 |
| 4 | Inception | **LCO** | The declared scope is agreed against the recovered baseline, the candidate architecture exists and the business case is settled. | 1 |
| 5 | Elaboration | **LCA** | The architecture baseline is executable and the first assembled run of the topology has happened; test cases cover it. | 1–2 |
| 6 | Construction | **IOC** | The declared scope is implemented, tested and baselined. | 2 |
| 7 | Transition | **PR** | The product is deployed, acceptance-tested and documented; the release is baselined. | 1 |

`1 + 1 + 1 + 1 + 1–2 + 2 + 1 = 8–9`. The profile is the rubber profile for a small project that is nonetheless **recovery-heavy**, and it bends in exactly two places, each against a named risk:

- **The sprint zero carries three of the eight.** Every requirement, component and table has to be read out of code before Inception can declare anything (R020, R009, R013). This is the whole reason the total sits above the median.
- **Elaboration carries a second iteration, planned rather than optional,** because R020's accepted contingency — the first assembled run as the Integrator's Architecture Build — is the most likely event in the plan to contradict a recovered statement, and the phase must then re-derive the affected elements inside itself. If that run confirms the recovered topology, the second iteration is not spent.
- **Construction is not bent.** Nothing in the Inventory suggests a large declared scope: the recovered product is registration, login, logout and todo list / create / delete, over one aggregate and eight tables. Two iterations are the whole of it.
- **Transition is not compressed either.** It is one iteration with no user training to carry, and the acceptance test is the only thing there that costs a full iteration.

```plantuml
@startgantt
title Project iteration sequence and its human gates (unanchored: no start date, no calendar dates)
skinparam shadowing false

[Sprint zero - Survey SBC] lasts 1 day
[Sprint zero - Excavation AR] lasts 1 day
[Sprint zero - Consolidation GHR] lasts 1 day
[Inception LCO] lasts 1 day
[Elaboration LCA - iteration 1] lasts 1 day
[Elaboration LCA - second iteration if the first assembled run contradicts the recovered topology] lasts 1 day
[Construction IOC - iteration 1] lasts 1 day
[Construction IOC - iteration 2] lasts 1 day
[Transition PR] lasts 1 day
[Stakeholder gate - SBC] lasts 1 day
[Stakeholder gate - AR] lasts 1 day
[Stakeholder gate - GHR] lasts 1 day
[Stakeholder gate - LCO] lasts 1 day
[Stakeholder gate - LCA] lasts 1 day
[Stakeholder gate - IOC] lasts 1 day
[Stakeholder gate - PR] lasts 1 day

[Sprint zero - Excavation AR] starts at [Sprint zero - Survey SBC]'s end
[Sprint zero - Consolidation GHR] starts at [Sprint zero - Excavation AR]'s end
[Inception LCO] starts at [Sprint zero - Consolidation GHR]'s end
[Elaboration LCA - iteration 1] starts at [Inception LCO]'s end
[Elaboration LCA - second iteration if the first assembled run contradicts the recovered topology] starts at [Elaboration LCA - iteration 1]'s end
[Construction IOC - iteration 1] starts at [Elaboration LCA - second iteration if the first assembled run contradicts the recovered topology]'s end
[Construction IOC - iteration 2] starts at [Construction IOC - iteration 1]'s end
[Transition PR] starts at [Construction IOC - iteration 2]'s end

[Stakeholder gate - SBC] starts at [Sprint zero - Survey SBC]'s end
[Stakeholder gate - AR] starts at [Sprint zero - Excavation AR]'s end
[Stakeholder gate - GHR] starts at [Sprint zero - Consolidation GHR]'s end
[Stakeholder gate - LCO] starts at [Inception LCO]'s end
[Stakeholder gate - LCA] starts at [Elaboration LCA - iteration 1]'s end
[Stakeholder gate - IOC] starts at [Construction IOC - iteration 2]'s end
[Stakeholder gate - PR] starts at [Transition PR]'s end

[SBC] happens at [Sprint zero - Survey SBC]'s end
[AR] happens at [Sprint zero - Excavation AR]'s end
[GHR] happens at [Sprint zero - Consolidation GHR]'s end
[LCO] happens at [Inception LCO]'s end
[LCA] happens at [Elaboration LCA - iteration 1]'s end
[IOC] happens at [Construction IOC - iteration 2]'s end
[PR] happens at [Transition PR]'s end

note bottom
  No phase has closed, so no bar length is a forecast of duration and no
  calendar date exists anywhere in this plan. Each iteration ends when its
  exit criteria pass. Each gate is a human wait, carried as days of queue
  time with a ceiling of 14 before the process suspends.
end note
@endgantt
```

### This iteration's fine plan

Work items are the stages the IARI DEVELOPMENT PROCESS runs in Survey, each owned by its role. **No work item carries a size**: nothing has been measured in this system yet, no phase has closed, and a size filled with a human-team unit would be a figure this process cannot produce. Each item ends when its exit condition passes.

| Order | Work item | Owner | Input | Exit condition | Status |
|---|---|---|---|---|---|
| 1 | Development Case — Survey tailoring | Process Engineer | IARI DC baseline, the delivery | Tailoring issued: inactive disciplines, fired optionals, referenced tool configuration | Done — issued |
| 2 | System Inventory — Documentation | Software Archaeologist | The delivered documents, read against the code | Each document's usefulness and currency recorded with its anchor | Done — issued |
| 3 | System Inventory — Perimeter | Software Archaeologist | The solution, its projects, configuration and migrations | Components, external systems and 26 entry points drawn, each with its anchor | Done — issued |
| 4 | System Inventory — Anomalies and Priorities | Software Archaeologist | The reading of 71 of 128 files | Twenty anomalies recorded with evidence; the eight areas ordered for Excavation | Done — issued |
| 5 | Risk List — score, strategy, escalate | Project Manager | The twenty anomalies | Every anomaly a classified risk; the three High acceptances put to the stakeholder and answered | Done — R008, R009 and R020 accepted 2026-11-19 |
| 6 | Iteration Plan — this artifact | Project Manager | System Inventory, Development Case, Risk List | Coarse roadmap and fine plan issued | Done — issued |
| 7 | Stakeholder gate — perimeter confirmation | Stakeholder | System Inventory, Perimeter | The perimeter confirmed as drawn — seven projects, 26 entry points, the external systems and the three exclusions | **Done** — confirmed 2026-11-19 |
| 8 | SBC milestone review | Reviewer → Management Reviewer → Review Coordinator | Every artifact above | Verdict on the SBC milestone | Not started — the reviewers' to give, not this plan's |
| 9 | Iteration Assessment | Project Manager | The SBC verdict | Assessment written *after* the verdict records whether the objectives were met | Not started — blocked on item 8 |

Items 1–7 are complete: the six agent stretches are issued and the one human gate on the iteration is answered. Item 8 is the milestone review, which this plan does not perform and cannot schedule on its own authority; item 9 follows it.

```plantuml
@startgantt
title Survey iteration — stage sequence and human gates (unanchored: no start date, no calendar dates)
skinparam shadowing false

[Development Case — Survey tailoring] lasts 1 day
[System Inventory — Documentation] lasts 1 day
[System Inventory — Perimeter] lasts 1 day
[System Inventory — Anomalies and Priorities] lasts 1 day
[Risk List — score, strategy, escalate] lasts 1 day
[Iteration Plan] lasts 1 day
[Stakeholder gate — perimeter confirmation — answered] lasts 1 day
[SBC milestone review — Reviewer to Management Reviewer to Review Coordinator] lasts 1 day
[Iteration Assessment — written after the verdict] lasts 1 day

[System Inventory — Documentation] starts at [Development Case — Survey tailoring]'s end
[System Inventory — Perimeter] starts at [System Inventory — Documentation]'s end
[System Inventory — Anomalies and Priorities] starts at [System Inventory — Perimeter]'s end
[Risk List — score, strategy, escalate] starts at [System Inventory — Anomalies and Priorities]'s end
[Iteration Plan] starts at [Risk List — score, strategy, escalate]'s end
[Stakeholder gate — perimeter confirmation — answered] starts at [Iteration Plan]'s end
[SBC milestone review — Reviewer to Management Reviewer to Review Coordinator] starts at [Stakeholder gate — perimeter confirmation — answered]'s end
[Iteration Assessment — written after the verdict] starts at [SBC milestone review — Reviewer to Management Reviewer to Review Coordinator]'s end

[SBC] happens at [Stakeholder gate — perimeter confirmation — answered]'s end

note bottom
  Bar length carries ordering only. No stage here has been measured,
  so no bar is a forecast of its duration: each stage ends when its
  exit condition passes.
  The stakeholder gate is answered: the acceptances are in the Risk List,
  the perimeter confirmation in the Evaluation Criteria. It was a human
  wait — days of queue time, ceiling 14.
end note
@endgantt
```

### Measure and forecast

No phase has closed. There is no measured actual, therefore there is no forecast: no token figure, no elapsed figure, and no per-iteration velocity appears in this plan. No declared scope is cut or deferred to fit an estimate.

The budget position was put to the stakeholder in Survey iteration 1 and answered on 2026-11-19:

| What was put | Their answer, verbatim | Recorded |
|---|---|---|
| Whether a token budget has been declared for this project, given that the Development Case records none and the plan commits to 8–9 iterations with R020's contingency able to add one. | "No budget declared — record measured spend at each phase close and forecast from the measured actual, never from an assumption." | 2026-11-19 |

So the project declares **no token budget**: there is no box, no figure was invented for the stakeholder to accept, and nothing is trimmed to fit one. Measured spend is recorded as observed at each phase close, and both clocks are reported apart:

| Clock | What it measures | Where it is recorded | Ceiling |
|---|---|---|---|
| Agent work | Tokens consumed per stage and per role; elapsed agent time | Iteration Assessment, at phase close | No ceiling — measured, not bounded |
| Human gates | Days of queue time waiting for the stakeholder | Risk List, as the gate's trigger indicator | 14 days, then the process suspends; the actual is reported apart |

The two are never added and never converted into one another.

### Critical chain

```plantuml
@startuml
title Survey — critical chain from iteration start to the SBC gate
skinparam shadowing false
skinparam defaultTextAlignment left

|Process Engineer|
start
:Development Case — Survey tailoring;

|Software Archaeologist|
:System Inventory — Documentation;
:System Inventory — Perimeter;
:System Inventory — Anomalies and Priorities;
note right
  Priorities fix the order Excavation reads in.
  They schedule nothing in Survey.
end note

|Project Manager|
:Risk List — score probability and impact,
set strategy, request acceptance for
R008, R009 and R020;
:Iteration Plan — coarse milestone roadmap
and this iteration's work items;

|Stakeholder|
:R008, R009 and R020 accepted — 2026-11-19;
:Perimeter confirmed as drawn — 2026-11-19;
note right
  The gate is answered. Both answers are
  recorded verbatim: the acceptances in the
  Risk List, the perimeter in the Evaluation
  Criteria. It was a human wait of days of
  queue time, ceiling 14.
end note

|Review|
:Reviewer;
:Management Reviewer;
:Review Coordinator — SBC verdict;

|Project Manager|
:Iteration Assessment — after the verdict;
note right
  Every stretch above is a sequential agent
  stretch. No phase has closed, so none
  carries a spend figure: the first measured
  actual replaces every assumed share.
end note
stop
@enduml
```

## Resources

The team is the agents the IARI DC baseline activates, and the plan selects which of them work in this iteration. The roster is not this plan's to change; the Development Case records two roles as silenced by its trigger decisions and neither is scheduled here.

| Role | At work in Survey | Stage it runs | Produces | Notes |
|---|---|---|---|---|
| Process Engineer | Yes | Development Case | Development Case | Environment is High in Survey. Re-prepared at the next Environment phase, not before — no finding or Change Request demands a tailoring change yet. |
| Software Archaeologist | Yes | System Inventory — Documentation, Perimeter, Anomalies and Priorities | System Inventory | Discovery is Critical in Survey. The only role minting `EP-NNN` and `AN-NNN`. |
| Project Manager | Yes | Risk List, Iteration Plan | Risk List, Iteration Plan, Iteration Assessment | Project Management is Medium in Survey. |
| Reviewer | Yes | Milestone review SBC | Review Record | First lens of the SBC review. |
| Management Reviewer | Yes | Milestone review SBC | Review Record | Second lens of the SBC review. |
| Review Coordinator | Yes | Milestone review SBC | Review Record, milestone verdict | Holds the verdict; convenes without the Business Reviewer. |
| Stakeholder | Yes — human gate | Perimeter confirmation and High-risk acceptance | Answer recorded verbatim in the Risk List | The only human in this process. Its wait is quoted in days of queue time, never in the agent clock. |
| Business Process Analyst, Business Reviewer | No | — | — | `business-process-led = false` (Development Case DC-D2). |
| Capsule Designer | No | — | — | `real-time-system = false` (Development Case DC-D3). |
| System Analyst, Software Architect, Designer, Database Designer | Not in Survey | — | — | First at work in Excavation, per the process. Nothing in this plan schedules them earlier. |
| Implementer, Integrator, Test roles, Deployment, Change Control | Not in Survey | — | — | The sprint zero carries no Implementation, Test, Deployment or Change Control stage (Development Case §6). |

**Assignment profile.** Six roles at work, one of them the human gate. That is the whole of Survey — the plan adds no role to accelerate it, because the two stages that dominate its length are sequential by nature: the Inventory must be read before it can be scored, and the verdict cannot precede the reading. Parallelism would buy no clock here and would cost coordination across artifacts that cite each other's labels.

## Use Cases and Scenarios Addressed

**None.** No use case is analysed, designed or implemented in Survey. The system's use cases are recovered from the entry points in Excavation and completed in Consolidation — the Use-Case Model does not exist yet, and no `UC-NNN` has been minted.

Survey's output is the material the recovery is built on: 26 entry points recorded with their anchors, and the three exclusions that decide which of them no use case may be recovered from.

| Recovery input Survey produced | What it fixes for Excavation |
|---|---|
| `EP-001` … `EP-026` with anchors | The set of entry points a use case may be recovered from. |
| `EP-004` … `EP-011`, `EP-020`, `EP-021` excluded by stakeholder decision | Registration, login and logout are recoverable; the self-service identity surface and provider sign-in are not. |
| Priorities, orders 1–8 | The order Excavation reads in: `Todo.Api/Todos` + `Todo.Api/Users` first, the BFF second. |
| `AN-001` … `AN-020` | The anomalies each recovered element must not reproduce — R001 to R020 in the Risk List. |

## Evaluation Criteria
The Survey (SBC) exit criteria. They are what the milestone review judges this iteration against; none is met by assertion, and none is this plan's to declare passed.

| # | Criterion | Evidence it rests on | Status |
|---|---|---|---|
| 1 | The perimeter of the existing system is **confirmed by the stakeholder** — the seven projects, the components, the external systems, and the three exclusions. | System Inventory, Perimeter; the stakeholder's confirmation of 2026-11-19 | Met — confirmed |
| 2 | The **priorities are ordered** for the remaining recovery. | System Inventory, Priorities — eight areas, each with its reason and anchor | Met — recorded |
| 3 | The **unread areas are declared** with the reason each is unread. | System Inventory, Coverage — 71 of 128 files read; the 57 unread named and justified | Met — recorded |
| 4 | Every anomaly the reading recorded is a **classified risk** with a strategy, and the High ones carry the stakeholder's acceptance. | Risk List — 20 anomalies, 20 risks, magnitude by exposure; R008, R009 and R020 accepted by the stakeholder on 2026-11-19, recorded verbatim | Met — recorded |
| 5 | The tailoring governing the sprint zero is issued and its trigger decisions are recorded. | Development Case — §4 decision record DC-D1…DC-D7, §5 optional verdicts | Met — issued |
| 6 | The plan carries the **cross-iteration roadmap** and this iteration's fine plan, with no forecast invented before a measured actual exists. | This artifact, Plan and Milestones | Met — issued |

### Confirmation of the perimeter

Criterion 1 was put to the stakeholder in Survey iteration 1 and answered on 2026-11-19. The proposition put, and the answer received:

| What was put | Their answer, verbatim | Recorded |
|---|---|---|
| The perimeter of the existing system as the System Inventory draws it: the seven projects of `TodoApp.sln` (`Todo.Web.Server`, `Todo.Web.Client`, `Todo.Web.Shared`, `Todo.Api`, `TodoApp.AppHost`, `TodoApp.ServiceDefaults`, `Todo.Api.Tests`) plus the CI workflow; the external systems reached (browser, OTLP collector, container runtime, sqliteweb image, `dotnet-ef` CLI, NuGet feed); 26 entry points; and the three exclusions of 2026-11-19 — external provider sign-in, the admin role, the self-service identity surface. | "Yes" | 2026-11-19 |

That boundary is what Excavation recovers within: a use case comes from an entry point inside it, and a component or table outside it is not recovered at all.

Criterion 1 is met on that answer. All six exit criteria now rest on issued artifacts and recorded stakeholder decisions — whether the artifacts are adequate is the milestone review's judgment, not this plan's claim, and no milestone or iteration is marked complete here.

No criterion was added that the stakeholder did not declare: criteria 1, 2 and 3 are Survey's exit criteria as the process defines them, and 4–6 are the obligations this plan carries to the review. A criterion failing at SBC does not close the milestone — it returns to the next iteration of Survey, whose plan is the Review Record's open findings and the stakeholder's orders.

### Carried forward to the next iteration's plan

Criterion 2 above records that the Inventory's eight priority areas are **ordered**. It does not record that the order settles how much of them the AR milestone must have recovered, and that is the one thing this plan cannot decide for the stakeholder.

The process fixes what AR *produces* — Vision, Use-Case Model, the recovered architecture, the Design Model carrying the persistent schema, and the triggered Deployment Model. Applied to the eight areas it means orders 1–6 are all inside Excavation (the two endpoint groups, the BFF, the cross-cutting mechanisms, the client screens, and the schema and topology), with order 7 (`Todo.Api.Tests`) read as the cross-check on orders 1 and 2 and order 8 (build and tooling) belonging to Inception's Build Environment Setup. The alternative is to split Excavation and let the schema and topology recover in a second iteration.

| Option | AR closes with | Iterations | Cost |
|---|---|---|---|
| A — as planned | Orders 1–6 recovered in one Excavation iteration; 7 as cross-check; 8 at Inception | 8–9, unchanged | The single Excavation iteration carries the whole recovery. R020 and R009 make the BFF half the heaviest reading |
| B — split Excavation | Orders 1–4 at AR; schema and topology in a second Excavation iteration before GHR | 9–10 | One more iteration, against a ceiling of 9 |

The question is open with the stakeholder. Option A is what the roadmap above commits to; option B is one iteration more and stays inside nothing that has been measured. Whichever is answered, it is answered before Excavation is planned — this iteration does not schedule it.

### Excavation scope — decided by the stakeholder

The AR milestone closes with priority areas **1–6 recovered in a single Excavation iteration**, on the order the System Inventory's Priorities fix:

| Order | Area | Where it is recovered |
|---|---|---|
| 1 | `Todo.Api/Todos` + `Todo.Api/Users` | Excavation — the endpoint groups the whole product arrives through |
| 2 | `Todo.Web/Server` — the BFF | Excavation — identity is decided here; AN-009 and AN-013 |
| 3 | `Todo.Api` cross-cutting — authorization, rate limiting, validation, OpenAPI | Excavation — Supplementary Specification mechanisms |
| 4 | `Todo.Web/Client` — the screens | Excavation — AN-008 is a fact about this layer |
| 5 | `Todo.Api/Migrations` and `TodoDbContext` — the schema | Excavation — the Design Model carries it; no Data Model exists |
| 6 | `TodoApp.AppHost` + `TodoApp.ServiceDefaults` — topology | Excavation — the triggered Deployment Model |
| 7 | `Todo.Api.Tests` | Excavation — read as the cross-check on orders 1 and 2 |
| 8 | Build, environment and tooling | Inception — the Integrator's Build Environment Setup |

The proposition put and the answer received:

| What was put | Their answer, verbatim | Recorded |
|---|---|---|
| Excavation closing with areas 1–4 recovered and the schema and AppHost topology recovered in a second Excavation iteration before GHR, at 9–10 iterations total. | "No" | 2026-11-19 |

Option A is therefore the roadmap this plan commits to: **8 iterations, or 9 if Elaboration needs its second.** No second Excavation iteration is planned, and no condition beyond the answer is read into it. The single Excavation iteration carries orders 1–6; order 7 is its cross-check and order 8 opens Inception. Nothing in this iteration schedules that work — it is Excavation's plan to issue.

