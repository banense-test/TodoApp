## Document Control
- Phase: Consolidation
- Status: Draft — the plan for this phase's current iteration, produced for the end-of-Consolidation (GHR) milestone review
- Milestone Target: end-of-Consolidation (GHR) — not yet achieved
- Iteration: 2, Cycle 1
- Owner: Project Manager

## Iteration Objectives
Consolidation is the sprint zero's third and last phase. It does not recover anything: the recovered set — eleven use cases, four stated exclusions, twenty-two components, eight tables — was confirmed by the stakeholder as the model of the existing system at gate H4's third put and the advance into this phase was sanctioned at the fourth. What this phase does is **complete that set, count what rests on it, and hand it forward as the starting point of the declared change**. Nothing the stakeholder declares is worked here.

The phase's objectives, and each one's standing on the artifact that carries it:

```plantuml
@startuml
title Consolidation's three phase objectives - each certified on the artifact that carries it, none of them on the gate
skinparam shadowing false
skinparam wrapWidth 240
hide circle
hide empty members

package "O1 Complete the set - every artifact of the set present" {
  class "Use-Case Model: UC-001 to UC-011,\n4 exclusions stated\nSupplementary Specification: mechanisms with anchors\nSoftware Architecture Document: COMP-001 to COMP-022,\nUse-Case View for all 11" as O1 <<standing>>
  class "Design Model: 42 classes, 8 tables,\nkeys, associations, enforced rules\nDeployment Model: nodes, stores, environment mapping" as O1B <<standing>>
}
package "O2 Count the coverage - and say what stays unread" {
  class "System Inventory: 84 of the 94 own-tree files\nopened, 89.4 per cent; 67 anchored, 71.3 per cent;\nthe 45 vendored Bootstrap files named as excluded" as O2 <<standing>>
  class "one reading named as incomplete:\nthe model snapshot's product version, R034\nits action performed in the persistent-data description" as O2B <<standing>>
}
package "O3 Hand the set forward - the register and the plan" {
  class "Risk List: 34 risks, 29 Refines edges,\nno accept above Moderate without a grant" as O3 <<standing>>
  class "this plan: coarse roadmap, fine plan,\nGHR exit criteria" as O3B <<standing>>
}
package "The gate, which is not an objective" {
  class "gate H5 - refused at the first put,\nre-put at this iteration's close" as CF <<open>>
}
O1 --> CF
O2 --> CF
O3 --> CF
note bottom of CF
  An objective met is not a milestone sanctioned. Gate H5 was put and
  refused on 2026-11-23 and is re-put now. The verdict is the Review
  Coordinator's and reads this answer alone.
end note
@enduml
```

| # | Objective | Satisfied when | Owner | Standing |
|---|---|---|---|---|
| O1 | Complete the set the stakeholder confirmed | Every artifact of the recovered set stands at this phase, each element anchored to the file it was read from, and no recovered element has been reopened | System Analyst, Software Architect, Designer, Database Designer | **Standing, not certified** — the six artifacts are present at this phase and iteration, and this iteration reopened no element. This plan does not certify its own phase's artifacts; that is the lenses' work at the GHR review |
| O2 | Count the coverage and declare what stays unread | Coverage of the delivery's own files is counted, every file of that tree is either opened or named with the reason it was not, the headline figure reproduces from the per-area table, and any reading left incomplete is named | Software Archaeologist | **Standing** — the coverage reads 84 of the 94 own-tree files opened (89.4 per cent), 67 anchored (71.3 per cent), with the 45 vendored Bootstrap files named as one excluded third-party distribution and the raw 84 of 139 stated beside it. The one reading handed forward incomplete is named: the model snapshot's product version, carried as `R034` |
| O3 | Leave the phase a register and a plan, not a set of notes | Every open anomaly is a scored risk with an owner and an action, no accepted risk above Moderate lacks the stakeholder's grant, and every work item of this phase belongs to a stage the process runs here | Project Manager | **Standing** — 34 risks, 29 `Refines` edges, four grants at exposure 12, and the two exposures this phase adds (`R033`, `R034`) carried with owners this plan schedules |

The stakeholder confirmed the recovered content at gate H4 and sanctioned the advance into this phase. Nothing in this phase reopens it, and the objectives above add nothing to it: they complete, count and hand forward.

### What the two exposures this phase adds now stand at

`R034`'s action is performed: the persistent-data description records the snapshot's `ProductVersion` `8.0.0` against the build's `net9.0` and its EF Core 9.x packages, so no role scaffolds a migration against it unread. The incompatibility itself is not corrected — the snapshot is the delivery's file and this process records the system as it is.

`R033`'s action is performed. At the first put the graph returned all four edges marked `SUSPECT`; queried again in this iteration at each of the four ends it returns `CLS-001` → `TBL-001`, `CLS-007` → `TBL-002`, `CLS-020` → `UC-007` and `CLS-020` → `UC-010` unmarked. Each owner cleared its own end on the evidence the Design Model already stated, and `G7` now reads Standing on that act rather than on the strategy word the register carries.

## Plan and Milestones
The plan is two-level. The **coarse roadmap** fixes the milestone sequence across the project and what each milestone is judged on. The **fine plan** is this iteration's work items with their owners, bounded to Consolidation. What a completed iteration delivered and what it cost belongs in the Iteration Assessment, not here.

### Coarse roadmap — the milestone sequence

```plantuml
@startgantt
title Consolidation (GHR) in the milestone sequence - unanchored, no project start date, no projected calendar span

[SBC - Survey, 2 iterations] lasts 1 day
[SBC - Survey, 2 iterations] is colored in Gray
[Gate H2 - perimeter confirmed] lasts 1 day
[Gate H2 - perimeter confirmed] starts at [SBC - Survey, 2 iterations]'s end
[Gate H2 - perimeter confirmed] is colored in Green
[AR - Excavation, 4 iterations] lasts 1 day
[AR - Excavation, 4 iterations] starts at [Gate H2 - perimeter confirmed]'s end
[AR - Excavation, 4 iterations] is colored in Gray
[Gate H4 - advance into Consolidation granted] lasts 1 day
[Gate H4 - advance into Consolidation granted] starts at [AR - Excavation, 4 iterations]'s end
[Gate H4 - advance into Consolidation granted] is colored in Green
[Consolidation iteration 1 - the set completed and counted] lasts 1 day
[Consolidation iteration 1 - the set completed and counted] starts at [Gate H4 - advance into Consolidation granted]'s end
[Consolidation iteration 1 - the set completed and counted] is colored in Gray
[Consolidation iteration 2 - the nine open findings cleared] lasts 1 day
[Consolidation iteration 2 - the nine open findings cleared] starts at [Consolidation iteration 1 - the set completed and counted]'s end
[GHR review, second pass] lasts 1 day
[GHR review, second pass] starts at [Consolidation iteration 2 - the nine open findings cleared]'s end
[GHR review, second pass] is colored in Salmon
[Gate H5 - the set accepted as the starting point] lasts 1 day
[Gate H5 - the set accepted as the starting point] starts at [GHR review, second pass]'s end
[Gate H5 - the set accepted as the starting point] is colored in Crimson
[GHR verdict] lasts 1 day
[GHR verdict] starts at [Gate H5 - the set accepted as the starting point]'s end
[GHR verdict] is colored in Crimson
[Inception - LCO] lasts 1 day
[Inception - LCO] starts at [GHR verdict]'s end
[Inception - LCO] is colored in Gray
[LCO review] happens at [Inception - LCO]'s end
[LCO review] is colored in Salmon
[Elaboration - LCA] lasts 1 day
[Elaboration - LCA] starts at [LCO review]'s end
[LCA review] happens at [Elaboration - LCA]'s end
[LCA review] is colored in Salmon
[Construction - IOC] lasts 1 day
[Construction - IOC] starts at [LCA review]'s end
[IOC review] happens at [Construction - IOC]'s end
[IOC review] is colored in Salmon
[Transition - PR] lasts 1 day
[Transition - PR] starts at [IOC review]'s end
[PR review] happens at [Transition - PR]'s end
[PR review] is colored in Salmon
@endgantt
```

No bar carries an absolute date or a projected calendar span. The one-day lengths are the diagram's sequencing device, not durations claimed for the work: spend is measured in the two currencies — tokens and agent time, kept apart from stakeholder queue time — and never as a span. `Crimson` marks the two stretches not yet reached: gate H5, at its second put, and the GHR verdict that reads it.

| Order | Phase | Milestone | Discipline intensity | Risks this milestone confronts | What the milestone is judged on |
|---|---|---|---|---|---|
| 1 | Survey | SBC — passed at the re-take, 2 iterations | Environment High, Discovery Critical, Project Management Medium | R001 to R021 carried into the register; R016, R012, R004 and R011 granted for the sprint zero | The perimeter and its priorities stated and the anomalies carried as scored risks |
| 2 | Excavation | AR — passed at gate H4's fourth put, 4 iterations | Environment Low, Requirements High, Analysis & Design Critical, Discovery Critical, Project Management Medium | R001, R004, R019, R020, R021, R023, R028, R030 (System Analyst); R002, R009, R010, R017, R024, R025, R015 (Software Architect); R003, R018, R027 (Designer); R026, R029 (Database Designer); R031 and R032 (the plan's own) | The set recovered on anchors, the coverage measured, and the stakeholder's confirmation of the recovered content as the model of their system |
| 3 | Consolidation | **GHR — this phase, iteration 2** | Environment Low, Requirements High, Analysis & Design Medium, Discovery Critical, Project Management Medium | **R033** (an edge left suspect at the phase close; its avoidance performed this iteration, all four ends cleared); **R032** (one fact transcribed inconsistently — the OpenAPI gating was its seventh instance and is settled at all three artifacts); **R034** (the snapshot's product version, recorded where it is read); R003, R010, R018, R024, R025, R027 confirmed against the completed set; R030's statement read again only if the session surface moved, and it has not | **The complete set present and anchored, the coverage counted over the delivery's own tree, and the stakeholder's acceptance of the set as the starting point for the declared change** |
| 4 | Inception | LCO | Environment High, Requirements Critical, Project Management High, Analysis & Design Medium, Implementation Medium, Test Low, Deployment Low, CM Medium | R007, R013, R014 (Integrator, Build Environment Setup); R016's grant expires with the sprint zero and the declared change becomes the thing to check against | The declared change is scoped, a candidate architecture exists, the CM strategy is set, the Change Request ledger is opened |
| 5 | Elaboration | LCA | Environment Medium, Analysis & Design Critical, Requirements High, Implementation Medium, Test Medium, Project Management Medium, CM Medium, Deployment Low | R012, R011, R005 (Test Manager and Test Designer); R006, R029 (the test project is next touched here) | The architecture baseline is accepted and an executable architecture is built |
| 6 | Construction | IOC | Environment Low, Implementation Critical, Test Critical, Requirements Medium, Analysis & Design High, Project Management High, Deployment Medium, CM High, Business Modeling Low | Completes R012's coverage of the client's todo flow; R008 (Technical Writer); R027 and R024 corrected in the implementation they constrain | The declared scope is implemented and its test evaluation is recorded |
| 7 | Transition | PR | Environment Low, Deployment Critical, Test High, Project Management Medium, Implementation Medium, Requirements Low, Analysis & Design Low, CM Medium | R011's contingency is taken only if a deliberate upgrade lands before the release; R026 becomes a release-blocking conversion if a pre-existing database is in the release's path | The release build is baselined and acceptance-tested; the Change Requests are closed |

**Sequencing is driven by the Risk List, not by convenience.** The first put of this gate was refused on six Major findings, and the order this iteration works in is the Review Coordinator's, confirmed by the stakeholder without a ranking among them: the coverage restatement and the OpenAPI gating first, because the plan's own cells cite both, and the plan's cells last. `R033`'s four edges were cleared by the owners the graph marks before the lenses could read them again. `R034` was written before any role read the persistence description.

No plan here schedules work a later phase performs — the build risks (`R007`, `R013`, `R014`) wait for Inception because that is the first phase the Integrator works, and the test risks (`R005`, `R011`, `R012`) wait for Elaboration and Construction because no test case exists before a use case is specified.

### This iteration's fine plan

Every item below belongs to a stage the IARI process runs in Consolidation: Environment, Requirements, Analysis & Design, Discovery, Project Management, and the milestone review's three lenses. Nothing is scheduled that a later phase performs. Nine findings held the first put — six Major, three Minor, none Critical — and all nine were corrections their owners could make inside this phase; the stakeholder ordered all six Major cleared here rather than carried into Inception.

**One rule governs every state cell.** A state cell is re-derived from the artifact it describes in the turn this plan is written, never carried from the turn before. Every correction below was read at its artifact in this iteration, and the four trace edges were queried at the graph.

```plantuml
@startuml
title Critical chain of Consolidation iteration 2 - the nine open findings cleared, then the gate re-put
skinparam shadowing false
skinparam wrapWidth 250

|Software Archaeologist|
start
:C1 System Inventory#F4
coverage restated over the delivery's own 94 files
84 opened 89.4 per cent, 67 anchored 71.3 per cent
the 45 vendored Bootstrap files named as one excluded distribution;
:no count and no per-area row changed
the arithmetic reproduces;

|System Analyst|
:C2 Supplementary Specification#F4
S8 and S18 corrected against Todo.Api/Program.cs:44,49-58,62
M12 states the gating, F13 carries the constraint
Vision#F2 settled in the same pass;
:CLS-020 to UC-007 and CLS-020 to UC-010
cleared at the System Analyst's end;

|Designer|
:C3 CLS-001 to TBL-001 and CLS-007 to TBL-002
cleared at the Designer's end;

|Software Architect|
:C4 Software Architecture Document#F2
one configuration binding against the Deployment Model's two
the count reconciled and said so;

|Project Manager|
:C5 Risk List#F4
R033 and R031 at probability 5, exposure 20, High band;
:C6 this plan
G4's threshold written, G3 names both causes,
G6 decided on the act and not on the strategy label;

|Reviewer|
:C7 GHR technical lens, second pass;

|Management Reviewer|
:C8 GHR management lens, second pass;

|Stakeholder|
:C9 Gate H5 re-put
the complete set asked to be accepted as the
starting point of the declared change;

|Review Coordinator|
:C10 GHR verdict;

|Project Manager|
:C11 Iteration Assessment
written on the verdict;
stop
@enduml
```

| # | Work item | Discipline / stage | Owner | State | Closes |
|---|---|---|---|---|---|
| 1 | Development Case made current for Consolidation; ACT-DC-01's phase partitions each name every discipline the canonical matrix schedules in them, Project Management included | Environment — Development Case | Process Engineer | Done — ACT-DC-01 names Project Management in every phase it draws, at the intensity the matrix gives it, Survey through Transition | `Development Case#F4` |
| 2 | System Inventory: the coverage restated over the 94 files of the delivery's own tree — 84 opened (89.4 per cent), 67 anchored (71.3 per cent) — with the 45 vendored Bootstrap files named as one excluded third-party distribution and the raw 84 of 139 stated beside it | Discovery — System Inventory | Software Archaeologist | **Done — landed this iteration.** No count and no per-area row changed; the Files column sums to 139 and the Read column to 84 | `System Inventory#F4` |
| 3 | Supplementary Specification: S8 and S18 corrected against `Todo.Api/Program.cs:44,49-58,62` — the reference UI and both health endpoints are Development-only, the OpenAPI document is mapped unconditionally and is the one diagnostic surface an operating instance publishes, the logging stage runs in every environment with its field set gated. `M12` states the same gating, `F13` carries it as a constraint on later phases | Requirements — Supplementary Specification | System Analyst | **Done — landed this iteration**, cross-referenced to SAD `M12` and the Deployment Model's Environment Mapping on the same anchors | `Supplementary Specification#F4` |
| 4 | Vision: the Constraints row corrected to the gating the code has — the OpenAPI document served in every environment, the reference UI and both health endpoints Development-only | Requirements — Vision | System Analyst | **Done — landed this iteration**, on the same correction as item 3 | `Vision#F2` |
| 5 | Clear the two `CLS-020` edges at the System Analyst's end: `CLS-020` → `UC-007` and `CLS-020` → `UC-010` | Requirements — the owner's own stage | System Analyst | **Done — both cleared.** The graph was queried in this turn and returns neither marked. The reading that keeps them is the Design Model's: `CLS-012` attaches the filter to `/todos` naming `typeof(TodoItem)` at `TodoApi.cs:22`, so both the create and the change operation carry it | `Design Model#F2` |
| 6 | Clear the two `Specifies` edges at the Designer's end: `CLS-001` → `TBL-001` and `CLS-007` → `TBL-002` | Analysis & Design — the owner's own stage | Designer | **Done — both cleared.** The graph was queried in this turn and returns neither marked. The reading that keeps them is the model's: `CLS-001` is four properties in four columns of `Todos`, and `CLS-007` adds no member while `AspNetUsers` stores all fifteen it inherits | `Design Model#F2` |
| 7 | Software Architecture Document: the Deployment View's count reconciled with the Deployment Model's — one configuration binding and a gated surface set, two differences and not one | Analysis & Design — Software Architecture Document | Software Architect | **Done — landed this iteration.** The Deployment View states the same two the Deployment Model counts and says so | `Software Architecture Document#F2` |
| 8 | Risk List: `R033`'s probability restated at 5 on the basis its own evidence states — the warning sign firing on all four edges — carrying exposure 20, and `R031` tested the same way | Project Management — Risk List | Project Manager | **Done — landed this iteration.** Both rows read 5 × 4 = 20 in the High band, each with the basis the evidence states | `Risk List#F4` |
| 9 | Iteration Plan: `G4`'s threshold written into the criterion and both ratios in its evidence cell; `G3`'s evidence naming both causes; `G6` decided on the act performed rather than on the strategy label | Project Management — Iteration Plan | Project Manager | **Done — this document**, in the Evaluation Criteria section | `Iteration Plan#F11`, `#F12`, `#F13` |
| 10 | Use-Case Model, Software Architecture Document, Design Model and Deployment Model confirmed against the completed set | Requirements, Analysis & Design | System Analyst, Software Architect, Designer | Present at this phase and iteration, unchanged: the recovered content was confirmed at gate H4 and this iteration reopened no element | `R003`, `R010`, `R018`, `R024`, `R025`, `R027` |
| 11 | GHR technical lens, second pass | Review | Reviewer | Not yet run | — |
| 12 | GHR management lens, second pass | Review | Management Reviewer | Not yet run | — |
| 13 | Gate H5 re-put — the complete set accepted by the stakeholder as the starting point of the declared change | Gate | Stakeholder | **Re-put at this iteration's close. Refused at the first put on 2026-11-23; no answer to the second put exists** | `G2` |
| 14 | GHR milestone verdict | Review | Review Coordinator | Not yet run | The milestone |
| 15 | Iteration Assessment, written on the verdict | Project Management — Iteration Assessment | Project Manager | Not yet written — it cannot describe an iteration still under review | — |

**Items 2 to 9 are the nine findings the first put left open, and all nine are closed at their own artifacts.** The order they were worked in is the one the Review Coordinator set and the stakeholder confirmed: coverage and the OpenAPI gating first, because item 9's criterion cells cite both, and the plan's cells last. That dependency is why `G4` could not be restated before the Inventory held its ratio, and why `G3` could not name its second cause before the Specification held the gating.

**The one item this plan can assign but not perform is the gate.** `G2` opens on the stakeholder's answer alone. The process waits inside the bound `R022` sets — a ceiling of 14 days of queue time, with the process suspending rather than auto-filling on expiry — and this plan records no answer it has not received.

**Two currencies, never summed.** Items 1 to 12 and 14 are agent work, quoted in tokens and measured elapsed agent time. Item 13 is a human gate — waiting, not working — quoted only in queue time. Item 15 is written after the verdict and costs agent work.

**Nothing is added and nothing is cut.** No recovered element changes, no declared work exists in this phase to cut, and no agent role is duplicated: the roles that hold an open item are the roles the process schedules here for their own disciplines.

### Measured actuals and what this plan is sized from

Measured, not estimated, and quoted as the closed phases deliver them. Agent work and stakeholder queue are two clocks and are never added.

| Closed phase | Iterations | Agent time | Stakeholder queue | Tokens | Agent runs | Artifacts |
|---|---|---|---|---|---|---|
| Survey | 2 | 29 min | 5 min | 8,995,433 | 10 | 6 |
| Excavation (at 3 iterations) | 3 | 28 min | 7 min | 14,424,767 | 17 | 12 |
| Excavation (at close) | 4 | 26 min | 10 min | 9,735,197 | 17 | 12 |

The two Excavation rows are the same phase measured at two iteration counts; the four-iteration row is the record it closed on, and it is the one that carries forward. No per-iteration figure is quoted and none is derived: the record is per phase, and a number obtained by dividing it would be a velocity this system does not measure.

**Consolidation carries no figure of its own.** No phase of its shape has closed, so there is nothing comparable to size it from, and its own spend is being incurred now and closes only when its exit criteria pass. The project declares no token budget, so there is no box to fit: no figure is proposed for the stakeholder to accept, no declared work is cut or deferred to meet an estimate, and no calendar date is projected from any of the figures above. The one figure named anywhere in this plan that is not a measured actual is the 80 per cent coverage bar, and it is a criterion's threshold, not an estimate of spend.

The chain is sequential at its load-bearing points and parallelism would buy no clock: items 2 to 9 are corrections at six different artifacts, each owed to the role that owns it, and adding a second role to any of them would add contention over one artifact surface rather than shorten it. This phase needed a second iteration because the first left nine findings open, and the lever that took it there was **another iteration planned from the Review Record** — not more agents, and not less scope. If the second put is refused again, that is the lever again.

| Human gate | Who | What the iteration waits for | Bound | Answer |
|---|---|---|---|---|
| H5 | Stakeholder | The complete recovered set — eleven use cases, four stated exclusions, twenty-two components, eight tables — accepted as the starting point for the declared change | `R022` — ceiling 14 days of queue time; on expiry the process suspends and nothing is auto-filled | **Put once and refused on 2026-11-23; re-put at this iteration's close, and no answer to the second put exists.** The refusal ordered this iteration: six Major findings cleared here and the gate put again. The sprint zero's gates were put six times in all and the four puts at gate H4 cost a measured 10 min of queue time across Excavation, reported apart from agent time and never added to it |

## Resources
The roles are the 26-role roster of the IARI DC baseline, minus the two the Development Case records as not working in this project. No role is added, merged or renamed.

| Role | Discipline | Works this iteration | Stage it holds here, and why |
|---|---|---|---|
| Process Engineer | Environment | Yes | Development Case, at Low intensity as the phase's first discipline. ACT-DC-01 names Project Management in every one of its seven phase partitions, at the intensity the canonical matrix gives it, so `Development Case#F4` is closed |
| System Analyst | Requirements | Yes | Use-Case Model, Supplementary Specification and Vision; and two of the four suspect edges, `CLS-020` → `UC-007` and `CLS-020` → `UC-010`, cleared at its end |
| Software Architect | Analysis & Design | Yes | Software Architecture Document — components, mechanisms, the use-case view and the Deployment View, at Medium intensity |
| Designer | Analysis & Design | Yes | Design Model — domain model and package classes; and two of the four suspect edges, `CLS-001` → `TBL-001` and `CLS-007` → `TBL-002`, cleared at its end |
| Database Designer | Analysis & Design | Yes | Design Model's persistent data — entities, keys and associations, the enforced rules, and the snapshot's product version that `R034` records |
| Software Archaeologist | Discovery | Yes | System Inventory, at Critical intensity: the coverage counted over the delivery's own tree and every unread file named |
| Project Manager | Project Management | Yes | Risk List and Iteration Plan, and the Iteration Assessment after the verdict |
| Reviewer | Review | Yes | GHR technical lens, second pass |
| Management Reviewer | Review | Yes | GHR management lens, second pass, and the gate re-put |
| Review Coordinator | Review | Yes | GHR milestone verdict |
| Requirements Specifier | Requirements | No — Elaboration | Use-case detail and NFR thresholds are written against a declared scope; the delivery declares none, and this phase completes the recovered set rather than specifying a new one |
| User Interface Designer | Analysis & Design | No — Elaboration | Storyboards and the navigation map follow a use-case specification |
| Business Process Analyst | Business Modeling | No — inactive | `business-process-led = false` |
| Capsule Designer | Analysis & Design | No — inactive | `real-time-system = false` |
| Integrator | Implementation | No — Inception | No build environment is set up in the sprint zero; `R007` waits on Inception |
| Implementer, Code Reviewer | Implementation | No — Elaboration | No code is written in the sprint zero |
| Test Manager, Test Designer, Tester, Test Analyst | Test | No — Inception at the earliest | No Test Plan is triggered and no test case is written before a use case is specified |
| Deployment Manager, Technical Writer | Deployment | No — Inception, Construction | The Deployment Model is recovered, not planned; user documentation follows an implementation |
| Configuration Manager, Change Control Manager | Configuration & Change Management | No — Inception | No baseline exists and the Change Request ledger is opened at LCO |

The stakeholder is not an agent role: they are the only human in the process, and their work is gate H5.

**The profile is ten roles, and it is the shape of the phase rather than a cost decision.** Six of them hold a stage here because one of the nine findings this iteration clears sits in an artifact they own: the System Inventory, the Supplementary Specification and the Vision (System Analyst), the Software Architecture Document (Software Architect), the Design Model (Designer), the Risk List and this plan (Project Manager). A profile with the record-keepers alone would leave each of those findings to be recorded as a Major at the lens, which is the defect `R031` cost this project two iterations to learn.

## Use Cases and Scenarios Addressed
Consolidation recovers no use case and adds none. What this phase does is complete the set the stakeholder confirmed and hand it to Inception as that phase's baseline. The set below is the complete recovered model — every use case with the entry points it was read from, and every entry-point group that carries none, with the reason.

**This is the baseline Inception starts from.** No use case in it is qualified: every row's recovery is certified on the Use-Case Model, and the four exclusions are the stakeholder's own rulings of 2026-11-23.

```plantuml
@startuml
title The eleven recovered use cases Consolidation hands forward, the entry points each was read from, and what carries no use case
skinparam shadowing false
skinparam wrapWidth 210
left to right direction
skinparam componentStyle rectangle

package "Recovered - 11 use cases over 22 entry points" {
  component "UC-001 Create an account\nEP-002, EP-004, EP-015" as U1
  component "UC-002 Sign in with email and password\nEP-002, EP-005, EP-015" as U2
  component "UC-003 Sign in with an external provider\nEP-007, EP-008, EP-016\nrecovered and unreachable" as U3
  component "UC-004 Sign out\nEP-006" as U4
  component "UC-005 Maintain one's own account\nEP-015" as U5
  component "UC-006 See one's own tasks\nEP-001, EP-003, EP-009, EP-010" as U6
  component "UC-007 Add a task\nEP-003, EP-009, EP-012" as U7
  component "UC-008 Remove a task\nEP-003, EP-009, EP-014" as U8
  component "UC-009 Read one task by id\nEP-011" as U9
  component "UC-010 Change a task, including complete\nEP-013" as U10
  component "UC-011 Consult the API reference\nEP-017, EP-018, EP-019" as U11
}

package "Not recovered, each exclusion the stakeholder ruled" {
  component "EP-020 readiness, EP-021 liveness\nplatform mechanism, no actor's goal" as X1
  component "EP-022 migration platform event\na component's start-up step" as X2
  component "the admin branch of EP-011,\nEP-013, EP-014\nexceptional entity - nothing grants the role" as X3
}

U1 --> X1 : not a use case
U3 --> X3 : the provider path is unreachable,\nthe admin branch is not a use case
note bottom of U1
  Five use cases carry two scenarios rather than one - UC-001,
  UC-002, UC-006, UC-007, UC-008 - each a screen route and a
  direct API route on the same operation. One use case with two
  scenarios, never one use case per actor.
end note
note bottom of X3
  Stakeholder ruling, 2026-11-23. Recorded in the System
  Inventory's Perimeter and in AN-004.
end note
@enduml
```

| Use case | Primary actor | Recovered from | Scenarios | What the recovery may not claim, and where that is carried |
|---|---|---|---|---|
| `UC-001` Create an account | ACT-001, ACT-003 | `EP-002`, `EP-004`, `EP-015` | Screen route, direct API route | That a refusal names its cause: every authentication failure reaches the person as one 401 with no body (`AN-021`, `AN-020`) |
| `UC-002` Sign in with email and password | ACT-001, ACT-003 | `EP-002`, `EP-005`, `EP-015` | Screen route, direct API route | That a failed sign-in distinguishes a wrong password from a locked or absent account, and that lockout ends the access a token already holds (`AN-021`, `AN-022`) |
| `UC-003` Sign in with an external provider | ACT-001, with ACT-002 authenticating | `EP-007`, `EP-008`, `EP-016` | Screen route | That it is reachable: no provider is registered in the delivered configuration. Also that the callback reports its outcome (`AN-020`) or checks the scheme (`AN-019`) |
| `UC-004` Sign out | ACT-001 | `EP-006` | Screen route | That the provider's own session ends: one call signs the local cookie scheme out and nothing else |
| `UC-005` Maintain one's own account | ACT-003 | `EP-015` | Direct API route | That a screen reaches it: the client's six operations contain no account-maintenance call |
| `UC-006` See one's own tasks | ACT-001, ACT-003 | `EP-001`, `EP-003`, `EP-009`, `EP-010` | Screen route, direct API route | That the list honours the `admin` role (`AN-018`), or that an unreachable API is distinguishable from an empty list (`AN-026`) |
| `UC-007` Add a task | ACT-001, ACT-003 | `EP-003`, `EP-009`, `EP-012` | Screen route, direct API route | That a create body can set a row complete: the insert copies the title alone |
| `UC-008` Remove a task | ACT-001, ACT-003 | `EP-003`, `EP-009`, `EP-014` | Screen route, direct API route | That another person's row is distinguished from one that does not exist: both answer 404 |
| `UC-009` Read one task by id | ACT-003 | `EP-011` | Direct API route | That a screen reaches it: none does. Its `admin` branch is the exceptional entity `AN-004` records |
| `UC-010` Change a task, including marking it complete | ACT-003 | `EP-013` | Direct API route | That a user-facing path completes a task: the client makes no update call (`AN-001`) |
| `UC-011` Consult the API reference | ACT-003 | `EP-017`, `EP-018`, `EP-019` | Direct API route | That a Swagger UI is mounted as the README states (`AN-008`), or that the root redirect resolves outside Development (`AN-017`) |

Three entry-point groups carry no use case and the Use-Case Model says why: `EP-020` and `EP-021` are a platform mechanism with no actor the delivery names, `EP-022` is a component's start-up step, and the `admin` branch of `EP-011`, `EP-013` and `EP-014` is an exceptional entity no running caller can enter — the stakeholder's ruling of 2026-11-23, recorded in the System Inventory's Perimeter and in `AN-004`. The provider sign-in path is the fourth exclusion and is carried, not dropped: `UC-003` exists and is marked unreachable in the delivered configuration.

## Evaluation Criteria
The exit criteria for Consolidation's milestone (GHR). Each is decided on the evidence the artifact it cites records, re-derived from that artifact in the turn this plan is written. The three families below are the milestone's purpose and nothing beyond it is added to them: the set is **complete**, what rests on it is **counted**, and the stakeholder **accepts it as the starting point**. A criterion about an artifact is certified on that artifact's own text, never on an adjacent artifact's answer.

```plantuml
@startuml
title GHR exit criteria at Consolidation iteration 2 - eight, each decided on the evidence the artifact it cites records
skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam wrapWidth 250
hide circle
hide empty members

package "The set is complete - 3" {
  class "G1 Every artifact of the set present\nUC-001 to UC-011, 4 exclusions,\nCOMP-001 to COMP-022, 8 tables" as G1 <<standing>>
  class "G2 The stakeholder accepts the set as the\nstarting point of the declared change" as G2 <<refused, re-put>>
  class "G3 No recovered element reopened\nnor contradicted between artifacts" as G3 <<standing>>
}

package "What rests on it is counted - 2" {
  class "G4 The coverage counted over the delivery's\nown tree, 80 per cent or more" as G4 <<standing>>
  class "G5 Every reading left incomplete is named" as G5 <<standing>>
}

package "The phase's own obligations - 3" {
  class "G6 Every open anomaly is a scored risk\nand no accept above Moderate lacks a grant" as G6 <<standing>>
  class "G7 No suspect trace open at the phase close" as G7 <<standing>>
  class "G8 No work the process does not run here" as G8 <<standing>>
}

G1 --> G2
G3 --> G2
G4 --> G2
G7 --> G2

note bottom of G2
  Put and refused on 2026-11-23. The criterion opens on the answer
  alone: no Yes is recorded that has not been given, and this plan
  certifies nothing on the stakeholder's behalf.
end note
note bottom of G4
  The bar is in the criterion's text. The ratio it is measured on is
  84 of the 94 files of the delivery's own tree - 89.4 per cent. The
  raw 84 of 139, 60.4 per cent, sits beside it and is not the figure.
end note
note bottom of G7
  Four edges the graph returned marked at the first put. Queried this
  turn, all four return unmarked, each cleared at the end its owner holds.
end note
@enduml
```

| # | Criterion | Met when | State | Evidence |
|---|---|---|---|---|
| G1 | Every artifact of the recovered set is present at this phase | The Use-Case Model, the Supplementary Specification, the Software Architecture Document, the Design Model and the Deployment Model each stand at this phase and iteration, with every element anchored to the file it was read from | Standing — not certified | Each artifact's Document Control names Phase Consolidation. The Designer's model carries `CLS-001` to `CLS-042` and `TBL-001` to `TBL-008`; the Architect's carries `COMP-001` to `COMP-022`; the System Analyst's carries `UC-001` to `UC-011` with the four exclusions. The Deployment Model is present under the one optional trigger the Development Case reports fired. What this criterion needs is the lenses reading each, not this plan asserting it |
| G2 | The stakeholder accepts the complete set as the starting point of the declared change | Gate H5 answered Yes | **Not met — refused at the first put, re-put at this iteration's close** | No Yes exists. The stakeholder refused the sanction on 2026-11-23 and ordered the six Major findings cleared in this phase with the gate put again. `R022` bounds the re-put at a ceiling of 14 days of queue time, with the process suspending rather than auto-filling on expiry. This plan records no answer it has not received |
| G3 | No recovered element is reopened or contradicted | The eleven use cases, four exclusions, twenty-two components and eight tables stand as confirmed, and no artifact states a fact another contradicts | Standing | The recovered content is unchanged since the confirmation at gate H4, and this iteration reopened no element. **Two causes could fail this criterion and both are now settled at their own artifacts.** First, the four edges marked `SUSPECT` at the first put — `CLS-001` → `TBL-001` and `CLS-007` → `TBL-002` (Designer), `CLS-020` → `UC-007` and `CLS-020` → `UC-010` (System Analyst): an edge nobody confirmed is a link no artifact can be certified against. Both owners cleared their ends and the graph returns all four unmarked. Second, the one code fact the set stated two ways — the Supplementary Specification's S8 and S18 placing the OpenAPI document among the Development-only surfaces, against `Todo.Api/Program.cs:58` where `app.MapOpenApi()` is called outside the Development block at 49-56 and against the SAD's `M12` and the Deployment Model's Environment Mapping. S8, S18 and the Specification's `F13` now state the same gating as those two artifacts on the same anchors. `R034`'s fact is recorded in the persistent-data description, so the snapshot's product version does not stand as an uncontradicted reading |
| G4 | The coverage is counted over the delivery's own tree and reaches the bar | Coverage of the delivery's own files is **80 per cent or more**, with every file of that tree either opened or named with the reason it was not, and the headline figure reproducing from the per-area table | Standing | System Inventory — Coverage: **84 of the 94 files of the delivery's own tree opened, 89.4 per cent**, against the 80 per cent bar; 67 of the 94 anchored, 71.3 per cent. The raw repository count is stated beside it and is not the figure the criterion is measured on: **84 of 139, 60.4 per cent**. The 45 files excluded from the denominator are the vendored Bootstrap 5 distribution under `Todo.Web/Client/wwwroot/bootstrap/`, named as one third-party release the contribution contract forbids editing, which the stakeholder ruled on 2026-11-23 is not their system. The 10 own-tree files never opened are each named with the reason; the Files column sums to 139 and the Read column to 84, so the figure reproduces from the table |
| G5 | Every reading this phase leaves incomplete is named | Where the count found a reading the phase could not complete, it is handed forward by name rather than left to be discovered | Standing | The Inventory names the model snapshot as that reading; the persistent-data description records the version it declares against the build's, and `R034` carries the exposure with a named owner and action |
| G6 | Every open anomaly is a scored risk, and no accept above Moderate lacks a grant | No anomaly maps to no risk, every score reproduces from the one published mapping, and no risk in the High or Significant band is accepted on the Project Manager's authority — **decided on the action performed, never on the strategy word a cell carries** | Standing | Risk List — 29 `Refines` edges from `AN-001` to `AN-029`; `R022`, `R031`, `R032`, `R033` and `R034` with their origins stated; four grants at 4 × 3 = 12, each quoting the stakeholder's own answer; no risk above Moderate accepted on this role's authority. `R031` and `R033` sit in the High band at 5 × 4 = 20 and take the avoid strategy, which is this role's authority at any band — **and both cells are decided on the act, not on the label.** `R031`'s contingency was taken and performed: the Environment stage now runs in Excavation as its first discipline and both Development Case Minors are corrected. `R033`'s avoidance has been performed: all four edges were cleared at the end their owner holds, and a graph query made in this turn returns `CLS-001 → TBL-001`, `CLS-007 → TBL-002`, `CLS-020 → UC-007` and `CLS-020 → UC-010` unmarked. An avoidance whose action has not been performed is not a retirement; these two have been performed, and the evidence is the act |
| G7 | No suspect trace is open at the phase close | Every edge the graph returns marked SUSPECT has been cleared by the role that owns its far end, with the reading stated, or retired and re-registered | Standing | At the first put the graph returned four marked, and this plan recorded the criterion open rather than certifying it on the owners' behalf. In this turn the graph was queried again at each of the four ends and returns all four unmarked: `CLS-001` → `TBL-001` (`Specifies`), `CLS-007` → `TBL-002` (`Specifies`), `CLS-020` → `UC-007` and `CLS-020` → `UC-010` (`Realizes`). The Design Model's Traceability section states the reading that keeps each edge, so the clearance rested on the model's own evidence and needed no re-reading of the code |
| G8 | The plan names no work the process does not run | Every work item belongs to a stage the IARI process runs in Consolidation, and no item schedules work a later phase performs | Standing | Decided on this plan's own table above. Every item belongs to Environment, Requirements, Analysis & Design, Discovery, Project Management, the Review lenses, the gate or the verdict. No item schedules implementation, build, test-design or configuration-management work: those belong to Inception, Elaboration and Construction |

The denominator `G4` is measured on, and the two ratios that measure two different things:

```plantuml
@startuml
title G4 - the denominator the coverage criterion is measured on
skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam wrapWidth 230
hide circle
hide empty members

class "Repository tree\n139 files" as ALL

class "The delivery's own tree\n94 files\ncoverage denominator" as OWN
class "Vendored Bootstrap 5\nTodo.Web/Client/wwwroot/bootstrap\n45 files" as VEND

class "Opened\n84 files - 89.4 per cent\nagainst the 80 per cent bar" as OPEN
class "Anchored by a recovered artifact\n67 files - 71.3 per cent" as ANCH
class "Never opened\n10 files, each named with its reason" as UO

class "Raw ratio\n84 of 139 - 60.4 per cent" as RAW

ALL *-- OWN
ALL *-- VEND
OWN *-- OPEN
OWN *-- ANCH
OWN *-- UO
ALL ..> RAW : the same reading over a\ndenominator that mixes in\nthe bundle

note right of VEND
  Excluded from the denominator by the stakeholder's
  ruling of 2026-11-23: a third-party release the
  contribution contract forbids editing, and not the
  system. Named as one distribution, never file by file.
end note
note bottom of RAW
  Stated beside the count so the arithmetic reproduces,
  and not the figure coverage is measured on. The two
  ratios measure two things and neither substitutes
  for the other.
end note
@enduml
```

**One criterion is the gate and it opens on the answer alone.** `G2` was put and refused at the first put of this gate; it is re-put at this iteration's close, and this plan records no answer it has not received. The gate record of the sprint zero is carried in the coarse roadmap: H2 sanctioned at its second put, H4 at its fourth. None of it is read for more than it says.

**Seven criteria stand and one does not, and the one that does not is the stakeholder's to move.** Six of the seven standing were certified on corrections performed in this iteration at their own artifacts; the seventh, `G7`, could only be certified on its owners' act and that act has been performed, verified at the graph in this turn. Nothing here is certified on an owner's behalf. The lever on `G2` is not another reading of the code, another agent, or a narrower criterion — it is the stakeholder's answer, and if the answer is No again the lever is another iteration planned from the Review Record.

