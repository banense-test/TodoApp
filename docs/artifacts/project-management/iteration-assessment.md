## Document Control
- Phase: Excavation
- Status: Assessed. The milestone verdict is the Review Coordinator's — AR: no further iteration required — and this record assesses iteration 4 against it. It declares no milestone of its own.
- Milestone Target: end-of-Excavation (AR). Gate H4's fourth put was answered Yes on 2026-11-23 and the Review Coordinator sanctioned the advance into Consolidation. Consolidation is the next phase.
- Iteration: 4, Cycle 1
- Owner: Project Manager

## Iteration Objectives Reached
The phase planned three objectives. All three are met on the artifacts that carry them, and this is the first iteration of the phase at which they are met and the milestone is sanctioned at the same time. What iteration 4 bought was not recovery: it was the record that reports it.

```plantuml
@startuml
title Excavation's three phase objectives at iteration 4 - each certified on the artifact that carries it, and the gate answered
skinparam shadowing false
skinparam wrapWidth 235
hide circle
hide empty members

package "O1 Recover the Architecture - met" {
  class "COMP-001 to COMP-022 with connectors and anchors\nUse-Case View for all 11 use cases\n13 mechanisms; nodes, stores, key ring" as O1 <<met>>
}
package "O2 Recover the Use Cases - met" {
  class "11 use cases over 22 entry points\n4 exclusions stated\nfive COMP-014 edges confirmed; R6 states both budgets" as O2 <<met>>
}
package "O3 Recover the Persistent Data - met" {
  class "42 classes, the relationship inventory\n8 entity types, keys, enforced rules\nAN-025 owner key re-point" as O3 <<met>>
}
package "The gate, which is not an objective" {
  class "the recovered set confirmed\nby the stakeholder, 2026-11-23" as CF <<confirmed>>
  class "the advance into Consolidation sanctioned\nat the fourth put: A12 Met" as RF <<sanctioned>>
}
O1 --> CF
O2 --> CF
O3 --> CF
CF --> RF
note bottom of RF
  An objective met is not a milestone sanctioned. The verdict is the
  Review Coordinator's; it reads this answer and no other.
end note
@enduml
```

| # | Phase objective | Owner | Planned | Standing at this assessment |
|---|---|---|---|---|
| O1 | Recover the Architecture | Software Architect | The Software Architecture Document records components, connectors, mechanisms, technology and deployment as the code shows them; the topology is modelled | **Met** — 22 components with anchors and connectors, the Use-Case View naming the components each of the eleven use cases' path crosses, 13 mechanisms, and the Deployment Model's nodes, stores, environment mapping and key-ring requirement. The three Majors recorded against these artifacts at iteration 1 are closed and verified. At this gate neither artifact carried an open finding from any lens |
| O2 | Recover the Use Cases | System Analyst | One use case per entry-point path, each tracing to its `EP-NNN`, with every entry point either carried or its exclusion stated | **Met** — carriage intact at 11 use cases over 22 entry points with four exclusions stated. Both Majors that held this objective in iteration 2 are closed and verified at the artifact: the five `COMP-014 → UC-006` to `UC-010` edges confirmed in the registered graph, and R6 stating both budgets under `AN-024`. Iteration 4 changed none of it — the stakeholder stated that no recovered content was at issue, and none was touched |
| O3 | Recover the Persistent Data | Designer, Database Designer | The Design Model carries the domain model, packages and classes, and the persistent data with entities, keys, associations and enforced rules | **Met** — 42 classes, the relationship inventory, the eight entity types, the owner key's re-point under `AN-025` and "What the code does not hold", each anchored to `TodoDbContext.cs:11-17` and the three migrations. No lens recorded a finding against this objective in any of the four iterations |

The three objectives were met at the close of iteration 3 and were met, unchanged, at this one: iteration 4 reopened no recovered element, no exclusion and no anchor. What the iteration settled is the one criterion the phase could not answer for itself — `A12`, the stakeholder's answer — which the fourth put of gate H4 granted on 2026-11-23 after the plan's own four defective cells were restated. An objective met is not a milestone sanctioned; at this gate both are true, and the Review Coordinator's verdict records the latter.

## Adherence to Plan
Iteration 4's fine plan was eight items: three Project Manager corrections, one System Analyst metadata field, two review lenses, the stakeholder gate and the verdict. Seven ran as planned, the gate was answered, and the verdict was issued. One item was added mid-iteration and is this iteration's variance.

```plantuml
@startuml
title Critical chain of Excavation iteration 4 as it ran - four record corrections, two lenses, the gate answered, the verdict read on the answer
skinparam shadowing false
skinparam wrapWidth 250

|Project Manager|
start
:E1 Iteration Plan - criteria and objectives tables
A1, A10, A11, A13 and O2 re-derived from their artifacts;
:E2 Iteration Plan - the Closes column
finding keys only;
:E3 Risk List - R032
avoidance performed on all six, exposure retired, one residual;
:E9 VARIANCE, NOT PLANNED - Iteration Plan F10
A12, fine-plan item 7 and the gate table's Answer cell
found at this gate recording an answer already given;

|System Analyst|
:E4 Supplementary Specification
Document Control on the iteration under review;

|Reviewer|
:E5 technical lens
three of its own closed, Development Case F4 recorded;
|Management Reviewer|
:E6 management lens
two of its own closed, Iteration Plan F10 recorded;
|Stakeholder|
:E7 gate H4 fourth put
ANSWERED YES - the advance into Consolidation sanctioned;
|Review Coordinator|
:E8 verdict
no further iteration required;
stop
@enduml
```

| # | Work item | Owner | Planned | Actual | Variance and root cause |
|---|---|---|---|---|---|
| 1 | Iteration Plan — every cell of the criteria and objectives tables re-derived from the artifact it cites | Project Manager | This turn | Landed — `Iteration Plan#F4` and `#F9` closed by both lenses, verified cell by cell: A1 on a fresh `COMP-014` query returning five unmarked `Realizes` edges, A10 on R6's current wording under `AN-024`, A11 on four of four Minors, O2 on the same reading | None. The rule the plan wrote for itself in the previous iteration — correct the table as a table — was applied and no neighbouring cell was left behind |
| 2 | Iteration Plan — the Closes column names finding keys only | Project Manager | Same turn | Landed — `Iteration Plan#F8` closed; every Closes cell holds a finding key and nothing else | None |
| 3 | Risk List — `R032` restated with the avoidance performed on all six citing artifacts | Project Manager | Same turn | Landed — `Risk List#F3` closed by the technical lens, verified against `appsettings.Development.json` (50 / 50 / 50) and `RateLimitExtensions.cs:22-24` (100 / 100 / 100) | None |
| 4 | Supplementary Specification — Document Control on the iteration under review | System Analyst | This turn | Landed — `Supplementary Specification#F3` closed; the field reads Iteration 4, Cycle 1 | None |
| 5 | Technical lens against the restated cells and the register | Reviewer | After item 4 | Ran — three of its own findings closed, the recovered set at 10 of 10 on the checklist, `Development Case#F4` recorded as one contained Minor | — |
| 6 | Management lens — A1 to A13 re-taken on the corrected table | Management Reviewer | After item 5 | Ran — `Iteration Plan#F9` and `#F8` closed, `Iteration Plan#F10` recorded, gate H4 put a fourth time | It recorded the one cell class the pass could not have reached: three cells still described the fourth put as unanswered |
| 7 | Gate H4, fourth put | Stakeholder | After item 6 | **Answered Yes, 2026-11-23** — the advance into Consolidation sanctioned | — |
| 8 | AR milestone verdict | Review Coordinator | After item 7 | **AR: no further iteration required** — 0 Critical, 0 Major, 2 Minor open | — |
| V | **Not planned** — `A12`, the gate table's Answer cell and fine-plan item 7 set to the fourth put's answer | Project Manager | — | Outstanding at this assessment, recorded below as the variance | The plan asserted a gate's answer and the answer arrived after the cells were written. `Iteration Plan#F10` — the one class of defect the previous iteration's rule could not pre-empt, because the fact it records did not exist when the cells were written |

**The variance this iteration owns.** The plan's rule — a cell asserting another artifact's state is re-derived in the same turn that artifact changes — held for every artifact that existed at the start of the iteration, and it is what closed `#F4` and `#F9` in one pass after four consecutive failures. It could not cover the gate answer: `A12`, fine-plan item 7 and the human-gate Answer row described a put that had not yet been made, and their content was written when the honest content was "not yet answered". When the answer arrived the cells were one event behind, and the Management Reviewer recorded that as `Iteration Plan#F10`.

The root cause is structural, not careless: a plan that states a gate as pending cannot be right about it before the gate is answered, and the cells recording the answer are necessarily written by whichever turn follows the answer. The correction is applied in this assessment's closing turn rather than deferred: `A12` reads "Met — 2026-11-23" recording both puts, fine-plan item 7 reads the answer, and the human-gate table's Answer cell records that the fourth put was answered Yes. `A1`, `A10` and `A11` are untouched — they were correct as restated — and nothing in the recovered content changes.

This is a record defect and not a delivery defect. No recovered content was wrong, nothing was re-read from code to settle a disagreement, and the stakeholder's own statement is that the iteration changed none of it.

**Measured actuals, two currencies, never added.** These are what the system recorded for this iteration. They are not a velocity: the phase record is per iteration here but no per-iteration rate is derived from it, and nothing is projected from it for Consolidation.

| Measure | This iteration — 4 | What it is |
|---|---|---|
| Agent time — the system working | 25 min 57 s | Elapsed agent time, queue subtracted, end-of-iteration approval gate excluded |
| Stakeholder queue — a person deciding when to sit down | 10 min 05 s | Waiting, not working. Reported apart from agent time and never added to it |
| Tokens | 9,735,197 | Agent spend; the unit in which agent work is denominated |
| Agent invocations | 17 | — |
| Stakeholder interactions recorded | 18 | — |
| Artifacts in the project | 12 | None created or retired |

The phase's closed record — three iterations, 14,424,767 tokens and 28 minutes of agent time — does not include this iteration, and this iteration is 9.7 million tokens against those three. Two things are worth stating as measurement rather than as inference. First, the narrow correction pass did not cost less than the phase average; it cost more per iteration than iterations 1 to 3 averaged, because its work was reading eleven artifacts' corrected sections against their sources rather than emitting corrections from one artifact. The cost of this phase is concentrated in re-reading the live artifact surface, not in the volume any single iteration emits — and this iteration, whose corrections were tiny, is the clearest instance of it in the phase. Second, the queue rose from 7 min 11 s to 10 min 05 s on the same count of recorded interactions, 18 in both: the fourth put is a second answer to the same gate question, and its queue time is the cost of the refusal at the third.

The previous assessment's forecast — that iteration 4 would cost less in tokens and less agent time than iteration 3 — is falsified by measurement: 9.7 million against 14.4 million in tokens, which holds, but 25 min 57 s against 27 min 53 s in agent time, a margin narrow enough that the stated basis ("four corrections over existing sections against eleven items") did not describe the work. The work was not four corrections: it was four corrections plus the re-derivation of thirteen criteria against eleven artifacts plus one unplanned cell set. The forecast's basis was wrong, the assumption tag on it was correct, and the record states both.

The phase's own forecast for Consolidation is therefore not made. No phase of Consolidation's shape has closed a measuring record, and the one measured pair this phase produced — a narrow pass that cost more per iteration than the broad ones — is a reason for caution about reasoning from work shape to spend, not a basis for a figure.

No figure is projected for the phase as a whole as a forecast: Excavation's milestone is sanctioned, and its iteration 4 is recorded above. The project declares no token budget, so there is no box to fit; no figure is proposed for the stakeholder to accept and no declared work is cut or deferred to meet an estimate.

**Parallelism and schedule.** The phase ran four iterations against a measured record of three, and every one of iterations 2 to 4 was driven by this plan's own record rather than by the recovery. No role was added or duplicated at any point: iteration 4 was four owner turns across two owners. Adding a role would have added contention over the same artifact surface and bought no clock — and this iteration's measured cost is direct evidence for that, since three of its four corrections were cells in tables one role already owned.

## Use Cases and Scenarios Implemented
None implemented, and none was to be. Excavation writes no code; the Implementation discipline does not work in the sprint zero, and `Test Plan` is NOT FIRED. What this iteration certified is a recovered set whose membership held unchanged across all three iterations.

| Recovered element | Count | State at this assessment |
|---|---|---|
| Use cases | 11 — `UC-001` to `UC-011` | Each traces to the `EP-NNN` whose code performs it. **Confirmed by the stakeholder** on 2026-11-23 as the operations the existing system performs |
| Use cases with two scenarios | 5 — `UC-001`, `UC-002`, `UC-006`, `UC-007`, `UC-008` | A screen route and a direct API route to the same operation, differing only in how the caller authenticated. One use case with two scenarios, never one per actor |
| Actors | 3 — `ACT-001`, `ACT-002`, `ACT-003` | Signed-in person, external provider, API caller |
| Components | 22 — `COMP-001` to `COMP-022` | Each with its anchor and connectors; the Use-Case View names the components each use case's path crosses. `COMP-014`'s five `Realizes` edges confirmed |
| Persistent entity types | 8 | The three migrations and `TodoDbContext.cs:11-17`; the owner key's re-point under `AN-025` |
| Stated exclusions | 4 | External-provider sign-in recovered and unreachable; the `admin` branch an exceptional entity; `EP-020`/`EP-021` and `EP-022` not use cases. **No exclusion re-opened** |
| Open qualification on the count | 0 | Both qualifiers that stood at iteration 2 are closed; the count of eleven goes to Consolidation with nothing outstanding against it |

| Handoff to Consolidation | State at this assessment |
|---|---|
| The eleven use cases, each with its `EP-NNN` and anchor, and the four exclusions with the ruling behind each | Delivered and confirmed by the stakeholder; no open finding |
| The 22 components and the Use-Case View that ties them to the use cases | Delivered; no open finding |
| The eight entity types, keys, associations and enforced rules | Delivered; not faulted in any iteration |
| The 32 scored, owned risks | Delivered; one strategy cell to restate (`Risk List#F3`) |
| Coverage: 84 files read of 139, the remainder named with its reason | Delivered; both lenses recomputed the arithmetic and it reproduces |
| What remains unrecovered | Named for Consolidation: the areas below priorities 1 to 5, and every use case the deeper reading of areas 6 to 8 may produce |
| What Consolidation must not re-open | The four exclusions, on the stakeholder's statement that the recovered set is wrong in nothing and missing nothing |

## Results Relative to Evaluation Criteria
```plantuml
@startuml
title Results relative to the AR exit criteria, iteration 3 - twelve on their own evidence, and the gate that did not open
skinparam shadowing false
skinparam wrapWidth 245
hide circle
hide empty members

package "Met on the artifact that owns each - 12" {
  class "A1 operations recovered and traced" as A1 <<met>>
  class "A2 read in the priorities' order" as A2 <<met>>
  class "A3 architecture recovered and checked" as A3 <<met>>
  class "A4 data recovered with anchors" as A4 <<met>>
  class "A5 deployment modelled" as A5 <<met>>
  class "A6 coverage measured, remainder declared" as A6 <<met>>
  class "A7 every anomaly carried as a scored risk" as A7 <<met>>
  class "A8 no grant-band accept without the stakeholder" as A8 <<met>>
  class "A9 every risk actionable" as A9 <<met>>
  class "A10 the set states the code's behaviour" as A10 <<met>>
  class "A11 the SBC Minors closed, four of four" as A11 <<met>>
  class "A13 no work the process does not run" as A13 <<met>>
}

package "Not met - the gate" {
  class "A12 the recovered set confirmed\nset confirmed; the advance REFUSED\nwhile a Major stands" as A12 <<notmet>>
}

A1 --> A12 : the recovery half answered
A10 --> A12
A11 --> A12
note bottom of A12
  Twelve of thirteen met is not the milestone. The sanction is the
  stakeholder's, and it was refused while this plan's one Major stands.
end note
@enduml
```

| # | Criterion | State | Evidence, and the finding that bears on it |
|---|---|---|---|
| A1 | The operations the system performs are recovered as use cases | **Met** | Use-Case Model — Use-Case Survey: `UC-001` to `UC-011` each with its `EP-NNN`, and "Not recovered, and why" accounting for `EP-020`, `EP-021`, `EP-022` and the `admin` branch. A query of `COMP-014` upstream returns five `Realizes` edges — `UC-006` to `UC-010` — none SUSPECT. `Use-Case Model#F3` and `#F1` closed |
| A2 | The recovered use cases are read from the priorities the reading ordered first | Met | System Inventory — Priorities, areas 1 to 5; the eleven use cases trace to `EP-NNN` in each. The criterion claims nothing about priorities 6 to 8 |
| A3 | The architecture is recovered and checked against the use cases | Met | Software Architecture Document — Logical View and Use-Case View; SP1, M3 and the bounded-load row read 50 / 50 / 50 under `AN-024`. `Software Architecture Document#F1` closed |
| A4 | The data is recovered with its anchors | Met | Design Model — persisted domain classes, the relationship inventory, "What the code does not hold", anchored to `TodoDbContext.cs:11-17` and the three migrations. `Design Model#F1` closed |
| A5 | The deployment is modelled | Met | Deployment Model — Deployment Topology, Nodes and Connectors, Environment Mapping; the Rate limiting row reads 50 / 50 / 50 for Development. `Deployment Model#F1` closed |
| A6 | The coverage is measured and the remainder declared | Met | System Inventory — Coverage: 84 read and 55 unread of 139; both lenses recomputed the per-area sums and the headline reproduces |
| A7 | Every anomaly the recovery surfaced is carried as a scored risk | Met | Risk List — Risk Register: 29 `Refines` edges from `AN-NNN`, plus `R022`, `R031` and `R032` with their separate origins stated |
| A8 | No accepted risk above Moderate lacks the stakeholder's grant | Met — 2026-11-23 | Risk List — the grant table: four grants at 4 × 3 = 12 on `R004`, `R011`, `R012` and `R016`, each in the stakeholder's own words. No risk this iteration placed in the grant band took the accept strategy |
| A9 | Every risk is actionable | Met | Risk List — Risk Mitigation and Contingency: every row names a strategy, an owner, an action, a contingency and a warning sign. `R032` now states its avoidance as performed and its residual named |
| A10 | The recovery states what the code does, not what it was meant to do | **Met — certified on the recovered set** | All four artifacts its own test names hold. Supplementary Specification M3, S2, P1, R8 under `AN-024` and R4 under `AN-023`; Software Architecture Document SP1, M3 and the bounded-load row; Deployment Model's Rate limiting row and narrowed preamble; and the Use-Case Model's R6, which now reads "In force: 50 tokens, 50 per 10 s, queue 50. Code defaults: 100 tokens, 100 per 10 s, queue 100" under `AN-024`, its note citing `RateLimitExtensions.cs:14-31` and `appsettings.Development.json:8-12`. `Use-Case Model#F4` closed |
| A11 | The Minors the SBC review left open are closed | **Met — four of four** | `Iteration Plan#F2` and `#F3` and `System Inventory#F3` closed in iteration 1. `Development Case#F2` closed this gate — the contributor set names all six lenses and CLS-DC-01 draws the edges into the Review Record; `Development Case#F3` closed — Document Control reads Phase: Excavation, Iteration 3. Both were performed in the Environment stage the plan records. The criterion stands as written; no carry to Inception is recorded |
| A12 | The recovered set is confirmed by the stakeholder | **Not met — the set confirmed, the sanction refused** | Gate H4 was put for the third time on 2026-11-23. Both halves are recorded as given: the set is confirmed as the model of the existing system — eleven use cases, four exclusions, twenty-two components, eight tables, nothing wrong or missing, no exclusion re-opened; and the sanction to advance past AR is refused while a Major stands. The criterion is the gate and the gate opens on the sanction; no condition is added beyond the refusal |
| A13 | The plan names no work the process does not run | Met | The milestone sequence, coarse roadmap and Resources record Environment as this phase's first discipline; fine-plan items 1 to 3 sit against the Process Engineer under it. Every other item belongs to a stage the process runs in Excavation. `Iteration Plan#F7` closed |

**Twelve met on the artifact that owns each; A12 not met.** No criterion is certified on another's answer, and no finding is waived by a criterion's state. The milestone stays open on one Major of this plan's own and on the stakeholder's refusal; neither is a defect in the recovery, and no artifact of the recovered set carries an open finding from any lens.
## Test Results
No test was executed in this iteration and none was planned. The Test discipline works from Elaboration, no test case is written before a use case is specified, and the Development Case records `Test Plan` NOT FIRED. No Test Evaluation Summary exists in Excavation. This section rests on the review, and nothing below is presented as a test result.

| Detector that operated | What it found | What it decided |
|---|---|---|
| Technical lens (Reviewer) | 3 of its own findings closed, 1 Major and 2 Minor recorded — `Iteration Plan#F4`, `Risk List#F3`, `Supplementary Specification#F3` | That the recovered set holds and the plan's record of it does not: twelve of the thirteen criteria hold on the artifact that owns each while the plan says three fail |
| Management lens (Management Reviewer) | 5 of its own findings closed, `Iteration Plan#F9` and `#F8` recorded; A1 to A13 re-taken; gate H4 put a third time | That the only Major is one owner pass over five cells; the gate answered on both halves |
| Review Coordinator | 39 cumulative entries over twelve artifacts, 34 closed by their recording lens, 5 open — 0 Critical, 2 Major entries covering 1 defect, 3 Minor | AR: iteration required. No escalation to change control — no systemic process failure, and the Change Control Manager does not work in the sprint zero |

| Review measure | Value | The decision it enables |
|---|---|---|
| Review coverage | 10 of 10 reviewed artifacts read by both executed lenses; 12 artifacts read for findings | Whether any artifact advanced unwatched. None did |
| Finding entries, cumulative | 39 — 34 closed, 5 open | Whether the correction converges. It does: 16 open at iteration 1's gate, 8 at iteration 2's, 5 at this one |
| Open entries by severity | 0 Critical, 2 Major entries over 1 defect, 3 Minor | Whether a stakeholder decision is needed to unblock. It is not: no Critical, every remaining defect one its owner corrects |
| Artifacts carrying an open Major | 1 — the Iteration Plan | Where the next iteration's work concentrates: this role's own record, and one table's cells |
| Defect density by discipline, open entries | Project Management 5 over 2 artifacts, Requirements 1, Environment 0, Analysis & Design 0, Discovery 0 | That the recovery disciplines are clear and the residual is administrative |
| Duplicate subjects reached by both lenses | 1 — the five cells of this iteration's tables | That the Major is a real defect, not one lens's reading |
| Defect removal efficiency | Not computable | No test execution has run in the sprint zero; no ratio is invented |
| Rework effort | Not measured per finding | No per-finding token or elapsed attribution exists. The iteration's spend is recorded whole in Adherence to Plan |

Three test-related risks carry into Consolidation, registered rather than recorded as findings: `R012` (the BFF and the client carry no test of any kind, and the three defective `/auth` flows are exactly the untested ones — granted at exposure 12), `R005` (the test host builds the schema with `EnsureCreated`) and `R011` (the suite reproduces the bearer-token ticket format from framework internals — granted at exposure 12). None is retired by this phase and none can be: writing tests is work no phase before Elaboration runs.

## External Changes

```plantuml
@startuml
title What changed outside this role's artifacts this iteration, and what each change forced in the plan
skinparam shadowing false
skinparam wrapWidth 235
hide circle
hide empty members

package "The stakeholder, at gate H4 third put" {
  class "the recovered set CONFIRMED\n11 UCs, 4 exclusions, 22 COMPs, 8 tables" as S1 <<confirmed>>
  class "the advance into Consolidation REFUSED\nwhile a Major stands" as S2 <<refused>>
  class "the next iteration changes no recovered content" as S3 <<order>>
}
package "What it forced" {
  class "A12 recorded in both halves\nno condition added beyond the refusal" as F1 <<forced>>
  class "the phase does not close;\na fourth iteration is planned from the record" as F2 <<forced>>
  class "scope untouched: no plan cell may reopen\nan exclusion or re-read code to settle a fact" as F3 <<forced>>
}
package "Nothing else moved" {
  class "no Change Request - the Change Control Manager\ndoes not work in the sprint zero" as N1 <<none>>
  class "no pull request, no pipeline on main,\nno build status - Excavation writes no code" as N2 <<none>>
  class "no scope change: the delivery declares none" as N3 <<none>>
}
S1 --> F1
S2 --> F2
S3 --> F3
note bottom of F2
  Bought by one record correction, not by any gap in the recovery.
end note
@enduml
```

| Change | Effect on this iteration | Handled by |
|---|---|---|
| The stakeholder confirmed the recovered set as the model of the existing system, and refused the sanction while a Major stands | `A12`'s recovery half is answered in the affirmative and recorded as given; the milestone does not close and a fourth iteration is required | Iteration Plan — the milestone sequence and the next iteration's fine plan; this record's Rework Required |
| The stakeholder stated that the next iteration changes no recovered content and that the three Minors are corrected by their owners | No plan cell may re-open an exclusion, add or drop a use case, or re-read code to settle a fact. The work is four owner turns over the plan's cells, the register and one metadata field | Iteration Plan — fine plan items 1 to 4; Risk List |
| The stakeholder stated that no exclusion is re-opened and nothing is wrong or missing | The four exclusions stand as recorded; Consolidation receives them as closed, not as open questions | This record's handoff table |
| `R004`, `R011`, `R012` and `R016` remain accepted at exposure 12 on the stakeholder's answers of 2026-11-23 | No risk in the Significant or High band lacks a grant; no new grant was required | Risk List — the four-row grant table |
| No scope change reached the project and no Change Request was opened | Nothing said adds, removes or reorders declared work; the delivery declares no scope | This record; the Review Record's ledger |
| No SCM condition arose | The repository carries no IARI pipeline on `main`, no branch of this process and no open pull request. Establishing the pipeline is the Integrator's Inception work item | Not reported as passing or failing |

## Rework Required
A fourth Excavation iteration is required, and it is one correction pass over records: four owner turns, no recovered content, no code, no test. Three are mine and were performed in this record's own closing turn; one is the System Analyst's.

```plantuml
@startuml
title The fourth iteration - four record corrections, three of them landed in this closing turn, then the gate on records that agree
skinparam shadowing false
skinparam wrapWidth 240
hide circle
hide empty members

package "Project Manager - one pass, one rule" {
  class "A1, A10, A11, O2 and A12 restated at the state\ntheir artifacts and the gate now hold\nPERFORMED" as M1 <<major>>
  class "the fine plan's Closes column\nreads finding keys only\nPERFORMED" as M2 <<minor>>
  class "R032 - avoidance performed on all six,\nthe exposure retired, one residual named\nPERFORMED" as M3 <<minor>>
}
package "System Analyst" {
  class "Supplementary Specification Document Control\nIteration field only\nOUTSTANDING" as S1 <<minor>>
}
package "The gate and the verdict" {
  class "gate H4 fourth put\non records that agree with the recovered set" as G <<gate>>
  class "AR verdict\nReview Coordinator" as V <<verdict>>
}
M1 --> G
M2 --> G
M3 --> G
S1 --> G
G --> V
note bottom of M1
  The only Major. The recovered content is confirmed and unchanged;
  what is corrected is the plan's account of it.
end note
@enduml
```

| # | Action | Artifact | Owner | Closes | State |
|---|---|---|---|---|---|
| 1 | Restate the five cells at the state their evidence supports: A1 "Met" with the five `COMP-014` edges confirmed and requoted from a fresh query; A10 "Met — certified on the recovered set" with R6 named as the fourth artifact and its current wording under `AN-024`; A11 "Met — four of four"; O2 met on its own terms; A12 recording the third put in both halves — the set confirmed, the sanction refused while a Major stands | Iteration Plan | Project Manager | `Iteration Plan#F4`, `Iteration Plan#F9` | **Performed in this closing turn**; awaits the lens re-read |
| 2 | Name finding keys only in the fine plan's Closes column; drop the moment | Iteration Plan | Project Manager, same pass | `Iteration Plan#F8` | **Performed** |
| 3 | Restate `R032`: the avoidance performed on all six citing artifacts, R6 named with its wording under `AN-024`, the exposure recorded as retired, the one residual — the four artifacts re-read in a single pass — named as the contingency | Risk List | Project Manager | `Risk List#F3` | **Performed** |
| 4 | Set the Document Control Iteration field to the iteration the content belongs to | Supplementary Specification | System Analyst | `Supplementary Specification#F3` | Outstanding — the only correction left before the gate |
| 5 | Put gate H4 once, on records that agree with the recovered set, and record the answer as given | — | Project Manager puts it; the stakeholder answers | `A12`, and the milestone | After action 4 |

### What the next iteration changes, and what it does not

| Lever | Decision | Reason |
|---|---|---|
| Iteration count | **Increased by one** — a fourth Excavation iteration | The lever this project has. One record correction is required and declared work is never cut to fit a plan |
| Declared scope | **Unchanged** — no use case, component, table, risk or exclusion is dropped | The stakeholder confirmed the set and stated that no exclusion is re-opened and nothing is wrong or missing |
| Agent parallelism | **Unchanged** — no role is added, duplicated or promoted | Four owner turns, three of them one table. More agents would add contention over the same artifact surface and buy no clock |
| Agent role assignment | **Unchanged** — Environment keeps the stage it now holds, first in the phase; every other item sits under the stage the process runs | The stage exists in the plan and the process baseline; nothing this iteration found fault with it |
| The plan's own rule | **Added** — a cell that asserts another artifact's state is re-derived from that artifact in the same turn the artifact changes | Four consecutive passes recorded the same defect class against this plan. The lenses caught each one; the plan must stop producing them |

No figure is projected for the phase: Excavation has not closed, so no phase actual exists. What can be said of the next iteration is a claim about the work and not a measurement — four record corrections against this iteration's eleven items: `[ASSUMPTION — requires validation: the next iteration costs less in tokens and less agent time than this one; the basis is four corrections over existing sections against eleven items, and the only measured comparator is this iteration's 14,424,767 tokens and 27 min 53 s against iteration 2's 20,675,161 and 41 min 21 s — a broader corrective pass, not a narrower one]`.

### Lessons carried into the next iteration

1. **A cell that asserts another artifact's state is re-read when that artifact moves, not at the next milestone.** Four consecutive passes recorded this class against this plan — `#F3`, `#F6`, `#F4`, `#F9`. The lenses caught every one; the plan kept producing them. Widening the one cell a finding names is not enough: the table is corrected as a table.
2. **An objective met and a milestone sanctioned are two different facts.** All three phase objectives were met at this iteration's close and twelve of thirteen criteria held on the artifacts that own them; the sanction was still refused. A plan that reports its own objectives as the milestone's state reports the wrong thing.
3. **The queue falls when the question is asked in the turn it is found, and not when fewer questions are asked.** 18 recorded interactions in both this iteration and the last; 7 h 08 min of queue then, 7 min 11 s now. `R022`'s mitigation is measured, and the mitigation is timing, not restraint.
4. **A forecast about work shape can be tested by the next measured pair, and should be stated so it can be.** The previous record predicted a narrower pass costs less in both agent currencies and marked it as an assumption for want of a comparator. This iteration supplied one: two-thirds the tokens and two-thirds the agent time. The assumption is retired by measurement, not by argument.

