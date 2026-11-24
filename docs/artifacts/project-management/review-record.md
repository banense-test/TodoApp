## Document Control
### Reviewer lens
<!-- review: Consolidation I2 -->

- Phase: Consolidation
- Status: Draft — the GHR technical lens, taken before the milestone verdict; 0 Critical, 1 Major, 0 Minor open from this lens
- Milestone Target: end-of-Consolidation (GHR) — not yet achieved
- Iteration: 2, Cycle 1
- Review point: Lifecycle Milestone Review, exit-criteria lens
- Review type: formal inspection against checklist
- Reviewer: Reviewer
- Artifacts reviewed: 12 of 12
- Prior findings of this lens: 5 open at the start of this turn, 5 closed this turn, 0 re-recorded
- Disposition: Approved with Changes

### Management Reviewer lens
<!-- review: Consolidation I1 -->

<!-- review: Consolidation I1 -->

- Review type: Lifecycle Milestone Review — end-of-Consolidation (GHR)
- Milestone target: end-of-Consolidation (GHR) — not achieved at this put
- Iteration: Consolidation iteration 1, cycle 1
- Lens: Management Reviewer
- Verdict: No-Go

### Review Coordinator lens
<!-- review: Consolidation I1 -->

<!-- review: Consolidation I1 -->

- Phase: Consolidation
- Status: Draft — produced for the end-of-Consolidation (GHR) milestone review
- Milestone Target: end-of-Consolidation (GHR) — not yet achieved
- Iteration: 1, Cycle 1
- Owner: Review Coordinator
- Review event: GHR — Greenfield Handoff Ready; gate H5 put 2026-11-23
- Lenses executed: Reviewer (technical), ManagementReviewer (management)
- Lens inactive: BusinessReviewer — did not evaluate this review
- Milestone verdict: phase scope incomplete — six Major findings carried into Consolidation iteration 2

## Review Scope and Criteria
### Reviewer lens
<!-- review: Consolidation I1 -->

The GHR asks one question: do the artifacts collectively satisfy the conditions for the set to be handed forward as the starting point of the declared change. This lens answers it on the technical artifacts — is every element anchored to the code it cites, does every trace the set declares hold in the graph, and does the set agree with itself. It does not ask whether the stakeholder accepts the set; that is gate H5's question and the Management Reviewer's to put.

#### Checklist applied

| # | Checklist item | Applied to | Where it is decided |
|---|---|---|---|
| C1 | Every artifact of the recovered set is present at this phase and iteration | All 12 | Every artifact's Document Control names Phase Consolidation, Iteration 1, Cycle 1 |
| C2 | Every declared element cites the anchor it was read from — a file and lines, or `Source: EP-NNN` for a recovered use case | Use-Case Model, SAD, Design Model, Supplementary Specification | Sampled at the code: the OpenAPI gating in `Todo.Api/Program.cs`, the eight tables against their migrations, the rate-limit override against `appsettings.Development.json` |
| C3 | Every trace edge the artifact's Traceability table declares is carried by the registered graph, unmarked | Use-Case Model, SAD, Design Model, System Inventory | RTM query, whole project, 317 links |
| C4 | No suspect trace is open at the phase close | Design Model | RTM: four edges return `SUSPECT` → Major, `Design Model#F2` |
| C5 | No cross-cutting technical mechanism is modelled as a use case; one declared process is one use case with several scenarios | Use-Case Model, Vision | Eleven use cases; `EP-020`/`EP-021`/`EP-022` and the `admin` branch are exclusions with stated reasons |
| C6 | The Development Case does not redefine the baseline: roster, CORE ownership, CORE omission, the CORE + OPTIONAL universe, use-case enumeration | Development Case | Deltas only; two roles inactive with the triggers that justify each; six optional verdicts re-evaluated; `docs/CONTRIBUTING.md` present |
| C7 | Every OPTIONAL artifact the Development Case declares fired has its §5.2 condition genuinely holding | Development Case, Deployment Model | Deployment Model: distributed topology, four processes, a proxy hop, per-project settings pairs — the condition holds |
| C8 | No artifact states a behaviour the code contradicts | Supplementary Specification, SAD, Deployment Model, Vision, Design Model | Sampled at `Todo.Api/Program.cs`; one defect found → Major, `Supplementary Specification#F4`; its two echoes → Minor at `Vision#F2`, `SAD#F2` |
| C9 | Every target value in the Supplementary Specification is a value the system has, not a value it is meant to have | Supplementary Specification | Both rate-limit budgets stated under `AN-024`; `R4` states the two hops apart under `AN-023` |
| C10 | The System Inventory's coverage is counted, every unread area carries its reason, and the headline reproduces from the per-area table | System Inventory | Arithmetic reproduces (84 + 55 = 139). The ratio it reports fails the bar → Major, `System Inventory#F4` |
| C11 | A value or a count with no anchor and no stakeholder answer behind it | All 12 | None found; the four accepted grants cite the stakeholder's answers, and no quantitative claim is unsourced |
| C12 | No work item in the plan belongs to a phase that does not run it | Iteration Plan | Every item sits in Environment, Requirements, Analysis & Design, Discovery, Project Management, the lenses, the gate or the verdict |
| C13 | Every artifact carries UML, and each diagram is formally well-formed | All 12 | Every artifact carries at least one validated diagram; stereotypes, multiplicities and object lifelines are used as the notation requires |
| C14 | The set agrees with itself — no two artifacts state one fact differently | Whole set | Two disagreements found → `Supplementary Specification#F4` against the SAD and the Deployment Model; `SAD#F2` against the Deployment Model |

#### Scope of this lens, stated so it is not mistaken for the whole review

This lens reads the artifacts. It does not read the plan's schedule against a calendar, the register's strategy choices against the Project Manager's authority, or the recovered set against what the stakeholder wants — those are the Management Reviewer's and the gate's. Where this lens records a Major, it is because another role builds on the defect or an exit criterion fails, not because a document reads badly.

#### SCM evidence

No pull request exists in the repository and none is open — the sprint zero writes artifacts, not code, and the Implementation Model is the delivery's own tree, unchanged since `307a1ea`. The repository carries no IARI pipeline (`ci.yml` does not exist), so there is no build status to report for `main` and this lens claims none. Neither absence is a finding: the sprint zero produces no code, and no role in this phase is charged with establishing a build.

### Management Reviewer lens
<!-- review: Consolidation I1 -->

<!-- review: Consolidation I1 -->

This lens decides the milestone: whether the recovered set is complete, whether what rests on it is counted, and whether the organization may hand it forward as the starting point of the declared change. The question is exit criteria, not completion and not feasibility — the iteration's artifacts are read as the evidence each criterion cites.

Ten artifacts read at source: Development Case, System Inventory, Risk List, Iteration Plan, Vision, Use-Case Model, Supplementary Specification, Software Architecture Document, Deployment Model, Design Model. Trace state was queried against the registered graph rather than taken from any artifact's word: `CLS-001`, `CLS-020` and the business-level RTM covering all 315 links.

```plantuml
@startuml
title GHR exit criteria - eight, each decided on the artifact it cites
skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam wrapWidth 240
hide circle
hide empty members

package "Met on the evidence this review read - 3" {
  class "G1  Every artifact of the recovered set is present\nUC-001 to UC-011, COMP-001 to COMP-022,\nTBL-001 to TBL-008, all at Consolidation iteration 1" as G1 <<Met>>
  class "G5  A reading left incomplete is named\nR034: the snapshot names ProductVersion 8.0.0\nagainst a net9.0 build, recorded where it is read" as G5 <<Met>>
  class "G8  No work the process does not run here\n10 roles at work, each in a stage Consolidation runs" as G8 <<Met>>
}

package "Not met as the plan states it - 2" {
  class "G4  Coverage counted and the remainder declared\ncites 84 of 139 = 60.4 per cent, below the\n80 per cent bar; 84 of the 94 own-tree files\nis 89.4 per cent and is stated nowhere" as G4 <<Not-met>>
  class "G6  No accept above Moderate lacks a grant\nR033 sits at 16 in the High band, its action\nunperformed, and no grant is recorded" as G6 <<Not-met>>
}

package "Failing the criterion outright - 2" {
  class "G3  No recovered element contradicted\nSupplementary Specification#F4 states the\nOpenAPI document as Development-only" as G3 <<Not-met>>
  class "G7  No suspect trace open at the phase close\nall four edges still carry SUSPECT" as G7 <<Not-met>>
}

package "The gate itself - 1" {
  class "G2  Stakeholder accepts the set as the start\nGate H5 put 2026-11-23 and refused" as G2 <<Not-met>>
}

G4 --> G2
G6 --> G2
G3 --> G2
G7 --> G2

note bottom of G2
  A criterion met is not the milestone sanctioned. Six Majors
  stand at this put and no Critical does.
end note
note bottom of G7
  CLS-001 to TBL-001 and CLS-007 to TBL-002 marked for the
  Designer; CLS-020 to UC-007 and UC-010 for the System Analyst.
  Both roles hold a stage in this phase; neither act is done.
end note

@enduml
```

**What was checked beyond the eight criteria.** The Development Case against the IARI baseline: two roles inactive, each carrying the trigger that justifies it, no CORE artifact omitted or reassigned, no artifact outside the CORE + OPTIONAL universe named, and one optional trigger fired whose §5.2 condition genuinely holds against a four-process topology with a per-process settings pair. All six optional verdicts audited one by one rather than accepted as a table. The coverage arithmetic recomputed from the per-area table: its Files column sums to 139 and its Read column to 84, so the count reproduces and only the denominator is at issue. The register's grants read against the band each exposure falls in: four accepts at 4 × 3 = 12 each quote the stakeholder's own answer, and no risk above Moderate accepts on the Project Manager's authority.

**What was deliberately not judged.** `Iteration Assessment` is the Project Manager's Assess touchpoint and runs after this review; at review time it cannot describe the iteration under review, so its absence is not a defect and not a gate condition. `Change Request` is not opened in the sprint zero, where no Change Control Manager works. Neither is a finding.

### Review Coordinator lens
<!-- review: Consolidation I1 -->

<!-- review: Consolidation I1 -->

**Review type:** Milestone review at phase exit — the Greenfield Handoff Ready (GHR) review, which sanctions (or refuses) the transition from Consolidation into Inception. Per decision heuristic 1 it is a milestone review and nothing substitutes for it; the Iteration Evaluation Criteria Review and the Iteration Acceptance Review for this iteration are folded into it, because the iteration and the phase close on the same boundary in the sprint zero.

**Trigger:** Consolidation iteration 1's artifacts in their target state and the Iteration Plan's GHR criteria `G1` to `G8` written. Not a calendar date, and not decoupled from the plan: if the iteration's artifacts slip, this review slips with them.

**Scope:** twelve artifacts read — the eight CORE artifacts this phase produces, the System Inventory, and the Review Record itself.

| Artifact | Owner | Why it is in scope at GHR |
|---|---|---|
| Development Case | Process Engineer | The tailoring that governs every discipline's floor this milestone |
| System Inventory | Software Archaeologist | The coverage this phase exists to count |
| Risk List | Project Manager | The register the phase's exposures are carried on |
| Iteration Plan | Project Manager | The criteria the GHR verdict is read on |
| Vision | System Analyst | The stakeholder-facing statement of the recovered set |
| Use-Case Model | System Analyst | The 11 use cases and 4 stated exclusions |
| Supplementary Specification | System Analyst | The mechanisms the use cases include |
| Software Architecture Document | Software Architect | The 22-component architecture |
| Deployment Model | Software Architect | The fired optional trigger's artifact |
| Design Model | Designer | 42 classes, 8 tables, the edge set |
| Review Record | Reviewer / Management Reviewer / Review Coordinator | This record |
| Iteration Assessment | Project Manager | Not judged here — it is written on the verdict (see Disposition) |

**Lens participation — authoritative, not inferred from the artifact.**

| Lens | Status | Entries recorded | Open | What it contributes to the verdict |
|---|---|---|---|---|
| Technical / Reviewer | EXECUTED | 30 | 5 — 3 Major, 2 Minor | Twelve artifacts read; the artifact-level defect set across Requirements, Analysis & Design, Discovery and Environment |
| Management / ManagementReviewer | EXECUTED | 21 | 4 — 3 Major, 1 Minor | Twelve artifacts read; the criteria-table defects the milestone verdict is decided on, plus the gate H5 put and the stakeholder's answer |
| Business / BusinessReviewer | **INACTIVE — did not evaluate this review** | 0 | — | Nothing. Business Modeling is inactive for this project (`business-process-led = false`, Development Case); the lens is not counted as Approved, not counted as a pass, and no part of the milestone decision rests on it |
| Review Coordinator | Executing (this role) | — | — | The ledger, the cross-lens reconciliation, the action priorities, the calendar, the metrics and the verdict |

**Entry criteria — enforced before the review began.**

| Criterion | State at entry |
|---|---|
| The artifacts reviewed are in target state, not draft-for-review | Met — each artifact's Document Control names Consolidation iteration 1 |
| Reviewers assigned with matching expertise | Met — architecture and design artifacts to the technical lens, the tailoring and coverage artifacts to both lenses, the sanction question reserved to the stakeholder |
| Agenda and evaluation criteria distributed in advance | Met — the Iteration Plan's `G1` to `G8` state the criteria before the artifact set is read |
| The tailoring exists and is current | Met — Development Case made current for Consolidation |

**Exit criteria — enforced before the verdict.**

| Criterion | State at the close |
|---|---|
| Every Critical and Major finding has an owner and a deadline | Met — all nine open entries carry an owner and are scheduled in Consolidation iteration 2 |
| The Review Record is signed and archived | Met — this record, committed to the SCM repository |
| No open Critical and no open Major at the milestone | **Not met — 6 Major open.** This is why the milestone is not sanctioned |
| The stakeholder sanction is recorded | Met as recorded — gate H5 was put and **REFUSED**; a refusal is a recorded answer and admits no Conditional Go |
| Coverage counted at the bar the milestone is reviewed against | **Not met on the figure the artifacts state** — see `System Inventory#F4` and `Iteration Plan#F11` |

## Findings
### Reviewer lens
<!-- review: Consolidation I1 -->

```plantuml
@startuml
title COMPLIANCE-GHR-01 Technical lens - checklist item by artifact, Pass / Fail

skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam wrapWidth 260
hide circle
hide empty members

package "Pass - nothing defects this artifact from this lens" {
  class "Development Case" as DC <<Pass>> {
    dc-baseline conformance : Pass
    six optional triggers audited one by one : Pass
    Document Control names phase and iteration : Pass
    ACT-DC-01 against the intensity table : Pass
    use-case enumeration rules untouched : Pass
  }
  class "Use-Case Model" as UCM <<Pass>> {
    11 use cases over 22 entry points : Pass
    cross-cutting mechanism not a use case : Pass
    one declared process, two scenarios : Pass
    anchors cite the code they were read from : Pass
    Traceability rows against the graph : Pass
  }
  class "Risk List" as RL <<Pass>> {
    every anomaly of the reading is a risk : Pass
    every score reproduces from one mapping : Pass
    no accept above Moderate without a grant : Pass
    R033 and R034 carried with owner and action : Pass
  }
  class "Iteration Plan" as IP <<Pass>> {
    G7 recorded open, not certified on the owners' behalf : Pass
    no work item of a later phase : Pass
    tokens and elapsed time kept apart : Pass
    state cells re-derived from their artifacts : Pass
  }
  class "Deployment Model" as DPM <<Pass>> {
    5.2 trigger genuinely holds for this topology : Pass
    environment mapping against the code : Pass
    Document Control : Pass
  }
}

package "Fail - finding recorded this milestone" {
  class "Design Model" as DM <<Fail>> {
    CLS-020 to UC-007 and UC-010 : Fail
    CLS-001 to TBL-001 and CLS-007 to TBL-002 : Fail
    Design Model#F2 trace-gap, Major
  }
  class "Supplementary Specification" as SS <<Fail>> {
    S8 names the OpenAPI document Development-only : Fail
    S18 concludes no diagnostic surface exists : Fail
    Supplementary Specification#F4 consumed-defect, Major
  }
  class "System Inventory" as SI <<Fail>> {
    84 of 139 opened is 60.4 per cent : Fail
    67 of 139 anchored is 48.2 per cent : Fail
    System Inventory#F4 exit-criterion-unmet, Major
  }
  class "Vision" as VIS <<Fail>> {
    Constraints row repeats the OpenAPI gating : Fail
    Vision#F2 contained-defect, Minor
  }
  class "Software Architecture Document" as SAD <<Fail>> {
    one setting separates the environments : Fail
    Deployment Model states two : Fail
    Software Architecture Document#F2 contained-defect, Minor
  }
}

UCM --> DM : each class in it realizes a use case
SAD --> DPM : the deployment view answers to the topology
SS --> VIS : the same sentence, one authority
@enduml
```

```plantuml
@startuml
title DEFECT-GHR-01 Finding count by severity across the artifact, this milestone

skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam wrapWidth 230
hide circle
hide empty members

package "3 Major - the artifact is reworked before any role consumes it again" {
  class "Design Model\nfinding F2" as M1 <<Major>> {
    trace-gap
    4 suspect edges open at the phase close
    owner : Designer 2, System Analyst 2
  }
  class "Supplementary Specification\nfinding F4" as M2 <<Major>> {
    consumed-defect
    OpenAPI document stated Development-only
    consumed by the Deployment Manager and the Technical Writer
  }
  class "System Inventory\nfinding F4" as M3 <<Major>> {
    exit-criterion-unmet
    coverage 60.4 per cent against a bar of 80
    certified Standing by G4 without a denominator
  }
}

package "2 Minor - fixed by the owner's next turn, holds no milestone" {
  class "Vision\nfinding F2" as m1 <<Minor>> {
    contained-defect
    the same OpenAPI sentence at a supporting artifact
  }
  class "Software Architecture Document\nfinding F2" as m2 <<Minor>> {
    contained-defect
    one setting against the Deployment Model's two
  }
}

package "0 Critical - no defect needs a decision only the stakeholder can take" {
  class "none" as C <<none>> {
    no undeclared scope
    no contradiction in what the stakeholder declared
    no risk only they may accept
  }
}

package "Closed this milestone" {
  class "Development Case\nfinding F4" as X <<Resolved>> {
    ACT-DC-01 omits Project Management
    corrected in every phase partition
  }
}

M1 --> C : no escalation
M2 --> C : no escalation
M3 --> C : no escalation
m1 --> C
m2 --> C

note bottom of M1
  The one exit criterion the phase has not moved: G7 reads
  "Open - the phase's live criterion" and R033 sits at
  exposure 16. Both owners hold a stage this iteration, so
  the clearance needs no new reading of the code.
end note

note bottom of M3
  The reading itself is sound - every unopened file is named
  with its reason and 45 of the 55 are one vendored Bootstrap
  distribution. The defect is the denominator, not the count.
end note

note bottom of M2
  Two artifacts already state the correct gating and one of
  them names this artifact as the owner of the correction.
  The disagreement is inside the set, not against the code.
end note
@enduml
```

#### Development Case

Approved from this lens. `Development Case#F4` is closed and verified: ACT-DC-01 now names Project Management in every phase partition it draws, at the intensity the canonical matrix gives it, so the diagram and the intensity table agree.

The baseline is not redefined. Two roles are inactive and each carries the trigger that justifies it (`business-process-led = false`, `real-time-system = false`); no CORE artifact is omitted or reassigned; no artifact outside the CORE + OPTIONAL universe is listed; the use-case enumeration rules are stated as the baseline states them. The six optional verdicts were re-evaluated this iteration against the recovered set, and the one FIRED trigger — the Deployment Model — holds on this project's real facts: four processes, a browser bundle, a separate REST service, SQLite, a YARP proxy hop, and a settings pair per serving project. That is a distributed, multi-environment topology by any reading of §5.2. The five NOT FIRED verdicts each name the condition that does not hold, and each holds up: eight entity types is below the >10 threshold, no regulated vocabulary is in play, no phase before Elaboration runs a proof of concept, no formal delivery consumes test reporting, and no UX-critical decision waits on validation.

#### System Inventory

**Major — `System Inventory#F4`, criterion `exit-criterion-unmet`.** The coverage this phase exists to count is stated at 84 of 139 files — 60.4% — and 67 of 139 anchored — 48.2%. Neither reaches the 80% bar this milestone is reviewed against, and the Iteration Plan certifies `G4` as Standing on that figure. The reading behind the count is sound and candid: every unopened file is named, 45 of the 55 are one vendored Bootstrap 5 distribution, and six more carry no perimeter fact. The defect is the denominator — 45 of those 139 are a third-party bundle the contribution contract forbids editing, and the ratio over the 94 files that are the delivery's own tree (84 opened, 89.4%) appears nowhere. A milestone cannot certify a coverage criterion on a ratio that fails its bar, nor on a ratio whose denominator hides the fact that it would pass.

Traceability checked and clean: the AN rows against the registered graph agree — `AN-021` names `EP-004`, `EP-005`, `EP-007`, which is what the diagram and the graph both carry; every entry point resolves to a use case or to a stated exclusion.

#### Use-Case Model

Approved from this lens. Eleven use cases over 22 entry points, each anchored to the entry point whose code performs it; `EP-020`, `EP-021`, `EP-022` and the `admin` branch are exclusions with a stated reason, three of them the stakeholder's own rulings. No cross-cutting mechanism is modelled as a use case: the session, the bucket, the validation filter and the schema migration are mechanisms in the Supplementary Specification, not ellipses here. The five use cases with two routes in are one use case each with two scenarios, not one per actor — `ACT-001` and `ACT-003` are the same person on two authentication routes, and the artifact says so and says why. The Traceability table's eleven rows match the graph: every `EP-NNN → UC-NNN` edge it declares is carried, unmarked.

The two entry-point lists are reconciled and the rule is stated in the artifact: the Survey's Source column names the entry point whose code performs the use case, the actor-goal matrix names the entry point the actor acts through. That distinction is the correct reading of this code — the screen is `EP-003` and the operation it becomes is `EP-012` — and it is no longer two unlabelled lists that disagree.

#### Supplementary Specification

**Major — `Supplementary Specification#F4`, criterion `consumed-defect`.** S8 states that the OpenAPI document exists in Development only, and S18 concludes that "a non-Development run exposes no readiness probe and no diagnostic surface at all". Both are wrong against `Todo.Api/Program.cs`: `app.MapOpenApi()` is called at line 58, outside the `if (app.Environment.IsDevelopment())` block at 49-56. The document is served in every environment and is the one diagnostic surface an operating instance does publish.

This is a consumed defect, not a stale note. The Software Architecture Document's group-answer table names this artifact as the owner of the correction — "the specification's S8 and S18 state the document among the Development-only surfaces; the code maps it unconditionally and the code is recorded" — while its own mechanism M12 and the Deployment Model's Environment Mapping both state the opposite gating correctly. So the set a milestone certifies carries two answers to one question, and the requirements artifact carries the wrong one. The Deployment Manager and the Technical Writer read this artifact to write a runbook and a release note; both would document a diagnostic surface as absent that is in fact present.

Everything else in this artifact holds, and three parts of it are the best work in the set: both rate-limit budgets are stated under `AN-024` in M3, P1 and R8 rather than one figure; R4 states the BFF's two outbound hops apart under `AN-023`; and the twelve "behaviours the recovered use cases must not overstate" are the constraint the Use-Case Model's flows actually obey.

#### Software Architecture Document

**Minor — `SAD#F2`, criterion `contained-defect`.** The Deployment View closes "One setting separates Development from any other environment: the request budget", while the Deployment Model opens its Environment Mapping conclusion "Two settings separate the environments, not one". Both artifacts have the facts right and their facts agree; only the count is stated twice with two answers, using the same word for different things without saying so. Contained: the SAD is the architecture record, the Deployment Model is the artifact the fired trigger commissions for this question, and no role builds a decision on which of the two counts is right.

The rest of the architecture holds on the anchors. The component view is 22 components with every use case's path crossing named components, and its own Traceability table reports 77 `Realizes` edges read back from the graph, cross-checked from either direction. The four components carrying no edge state their anchors instead of a composed one, and each is defensibly outside every use-case path. M8's asymmetry between the two hops is stated at P6 and is the finding this phase most needed, because it is the one property no anomaly row records.

#### Design Model

**Major — `Design Model#F2`, criterion `trace-gap`.** Four trace edges this model's own Traceability table declares are still marked `SUSPECT` at the phase close: `CLS-020 → UC-007` and `CLS-020 → UC-010` against the System Analyst, `CLS-001 → TBL-001` and `CLS-007 → TBL-002` against the Designer. I queried the graph and all four return the marking. The artifact does not conceal this — it states it twice and correctly explains that neither the Database Designer nor the lens may clear an edge it does not own.

That is why this is a Major and not a Critical: nothing is at issue in the content, and the act is available. The Design Model already states the evidence for each edge, so the clearance needs no re-reading of the code — `CLS-001` is four properties in four columns of `Todos`, `CLS-007` adds no member while `AspNetUsers` stores the fifteen it inherits, and `CLS-012` names `typeof(TodoItem)` on the `/todos` group so both operations carry `CLS-020`'s filter. The consequence of leaving it is concrete: `G7` reads "Open — the phase's live criterion" in the plan, `R033` is carried at 4 × 4 = 16 in the High band, and a suspect left open at phase close is a Major against the artifact that holds it. Both owners — the Designer and the System Analyst — hold a stage in this iteration, so the phase can close on this act alone.

Everything else in the model is anchored to file and lines: 42 classes, 8 tables, the keys, the referential actions, the enforced-rule surface that separates what the schema binds from the five rules that rest on a handler, and a relationship inventory that states each association's kind and multiplicity. Its persistent-data sections are the most rigorously anchored content in the set.

#### Deployment Model

Approved from this lens. The §5.2 trigger genuinely holds and the artifact is the reason it does: a browser process, three .NET processes, two short-lived children and one container on one machine, with a proxy hop between two of them and an `appsettings` pair per serving project. Its Environment Mapping matches the code on the point that matters most and that four other artifacts got wrong in Excavation and have since corrected: the budget in force is 50 / 50 / queue 50, not the code's 100 series. It also states the three ungated surfaces — the logging stage, the root redirect and the OpenAPI document — correctly, which is what made `Supplementary Specification#F4` visible.

#### Risk List

Approved from this lens. Thirty-four risks; every one of the 29 anomalies is carried as a risk, and every probability and impact reproduces from the one published mapping. No risk in the Significant or High band is accepted on the Project Manager's authority: the four accepts at exposure 12 each quote the stakeholder's own answer, and `R033` at exposure 16 takes the avoid strategy, which is this role's authority at any band. `R030`, `R031` and `R032` have been restated to record a retirement that landed without claiming the exposure is removed, which is the distinction the register's own rule requires.

`R033` and `R034` are the phase's own exposures and each is correctly framed: `R033` is the exposure the graph establishes and `R034` is the one reading coverage hands forward incomplete, both with an owner, an action and a contingency.

#### Iteration Plan

Approved from this lens. Eight GHR criteria, each decided on the artifact it cites. The plan is candid about the two that are not met and does not certify either on an owner's behalf: `G7` is recorded "Open — the phase's live criterion", and `G2` records gate H5 as not put with no answer assumed. That is correct — a plan that recorded `G7` as Standing would be the defect this project has now recorded against itself twice, a criterion certified on evidence that does not state it.

Every work item belongs to a stage the process runs in Consolidation, and none schedules implementation, build, test-design or configuration-management work. The two currencies are kept apart and no per-iteration velocity or projected date is quoted. The state cells are re-derived from their artifacts in the turn the plan is written, which is the rule the previous phase's five findings of one class taught.

#### Iteration Assessment, Review Record, Change Request

`[OMITTED: Iteration Assessment — the Project Manager authors it after this review; at review time it cannot describe the iteration being reviewed, and its absence is not a defect]`

`Iteration Assessment` and `Change Request` are not judged by this lens this milestone: the first is written on the verdict and the second is not opened in the sprint zero, where no Change Control Manager works. Neither absence is a finding.

### Management Reviewer lens
<!-- review: Consolidation I1 -->

<!-- review: Consolidation I1 -->

**Stakeholder sanction: REFUSED** — gate H5 put 2026-11-23.
**Stakeholder acceptance:** "Nothing in the recovered set is wrong: the 11 use cases, the 4 exclusions, the 22 components and the eight tables stand as I confirmed them. I do not accept a handoff with Majors open: clear the six in this phase and put the gate again. One fact for the coverage count: the 45 Bootstrap files under Todo.Web/Client/wwwroot/bootstrap/ are a third-party distribution, not my system — count coverage over the delivery's own files. Nothing else to add."

Six Major defects and three Minor stand at this put, spread over four artifacts. No Critical.

```plantuml
@startuml
title DEFECT-GHR-02 Findings by severity and artifact at the GHR gate, this lens and the set it read
skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam wrapWidth 235
hide circle
hide empty members

package "Major - 6, the artifact is reworked before any role consumes it again" {
  class "Iteration Plan\nF11  exit-criterion-unmet\nG4 carries no threshold, reads Standing at 60.4 per cent" as M1 <<Major>>
  class "Iteration Plan\nF12  consumed-defect\nG3 names one of the set's two contradictions" as M2 <<Major>>
  class "Iteration Plan\nF13  exit-criterion-unmet\nG6 reads R033 'Avoid' as a performed action" as M3 <<Major>>
  class "Design Model\nF2  trace-gap\nfour edges return SUSPECT at the close" as M4 <<Major>>
  class "Supplementary Specification\nF4  consumed-defect\nOpenAPI document stated Development-only" as M5 <<Major>>
  class "System Inventory\nF4  exit-criterion-unmet\nratio over a denominator that mixes in the bundle" as M6 <<Major>>
}

package "Minor - 3, fixed by the owner's next turn, holding no milestone" {
  class "Risk List\nF4  contained-defect\nR033 scored 4 while its sign fired on all four" as m1 <<Minor>>
  class "Vision\nF2  contained-defect\nthe OpenAPI sentence repeated" as m2 <<Minor>>
  class "Software Architecture Document\nF2  contained-defect\none setting against the Deployment Model's two" as m3 <<Minor>>
}

package "Critical - 0" {
  class "none\nno undeclared scope, no contradiction in what\nthe stakeholder declared, no risk only they may accept" as C <<none>>
}

package "This lens closed at this milestone - 1" {
  class "Iteration Plan\nF10  contained-defect\nthe cells recording H4 unput no longer exist" as X <<Resolved>>
}

M1 --> C
M2 --> C
M3 --> C
M4 --> C
M5 --> C
M6 --> C

note bottom of M1
  Three of the six sit in one artifact and in one place: the criteria
  table the GHR verdict is read on. That is not three unrelated slips,
  it is one pass that certified criteria on the strategy they name
  rather than on the act the strategy requires.
end note
note bottom of M6
  The reading is sound and every unopened file carries its reason.
  The stakeholder ruled the denominator on 2026-11-23: count the
  delivery's own files, not the vendored distribution.
end note

@enduml
```

#### Iteration Plan

**Major — `Iteration Plan#F11`, criterion `exit-criterion-unmet`.** `G4` is certified "Standing" on a coverage figure that fails the bar this milestone is reviewed against, and the criterion's own text states no bar to fail. Its test asks only that "every file is either opened or named with the reason it was not, and the headline figure reproduces from the per-area table"; its evidence cites "84 opened and 55 unread of 139". 84 of 139 is 60.4%, below the 80% a Consolidation coverage count is required to reach. The ratio that does meet the bar — 84 of the 94 files of the delivery's own tree, 89.4%, over the 45 vendored Bootstrap files excluded as one third-party distribution — appears in neither artifact. A criterion with no threshold in its text and a failing ratio in its evidence reads Standing, so the phase's coverage obligation is discharged by wording rather than by evidence. The stakeholder settled the denominator in the same answer that refused the sanction: count the delivery's own files.

**Major — `Iteration Plan#F12`, criterion `consumed-defect`.** `G3` — no recovered element is reopened or contradicted — names one cause where the set carries two, and the next iteration's corrective list is derived from this table. Its evidence cell reads "R033's four suspect edges are the one way this criterion could fail". The recovered set also contradicts itself on a code fact: the Supplementary Specification's S8 lists the OpenAPI document among the Development-only surfaces and S18 concludes that a non-Development run "exposes no readiness probe and no diagnostic surface at all", while the Software Architecture Document's M12 and the Deployment Model's Environment Mapping each state the document is mapped outside the Development block, as the code does at `Todo.Api/Program.cs:58`. A further iteration planned from this cell would clear the four trace edges, run G3 again, and fail it on a contradiction the cell never named.

**Major — `Iteration Plan#F13`, criterion `exit-criterion-unmet`.** `G6` is certified Standing by treating `R033`'s strategy label as a performed action while the register records the action unperformed and the warning sign firing. The cell closes "R033 sits at exposure 16 and avoids, which is this role's authority at any band." The Risk List records the same risk "Avoid — not performed; firing", with its warning sign reading "firing now, on all four", and its opening rule states that a risk whose action has not been performed is not retired: avoidance is a claim of retirement, not a status note. A High-band exposure at 4 × 4 = 16 therefore sits live at the gate with neither a performed avoidance nor a grant, cited as evidence that the criterion holds. Recording a strategy in place of the act that performs it is the class `R031` and `Iteration Plan#F7` cost this project three iterations to learn.

The remaining five criteria hold on their artifacts: `G1` on the six artifacts' presence at this phase with `UC-001` to `UC-011`, `COMP-001` to `COMP-022` and `TBL-001` to `TBL-008`; `G5` on `R034`'s recorded version difference; `G8` on a ten-role profile in which every item belongs to a stage Consolidation runs; `G7` correctly recorded open rather than certified on the owners' behalf; and `G2` correctly recorded as the gate alone, which I then put and which was refused. Every work item belongs to a stage the process runs in this phase, the two currencies are kept apart, no per-iteration velocity and no projected date is quoted, and the plan carries no declared work to cut.

#### Design Model

**Major — `Design Model#F2`, criterion `trace-gap`.** Four trace edges this model's own Traceability table declares still return marked `SUSPECT` against the registered graph at the phase close: `CLS-001 → TBL-001` and `CLS-007 → TBL-002` marked for the Designer, `CLS-020 → UC-007` and `CLS-020 → UC-010` marked for the System Analyst. I queried all four at source rather than reading the artifact's statement of them, and all four carry the marking.

This is a Major and not a Critical because nothing in the content is at issue and the act is available: the Design Model already states the evidence for each edge, so the clearance needs no re-reading of the code. Both owners — the Designer and the System Analyst — hold a stage in this phase and neither act has been performed. The Iteration Plan's own `G7` reads "Open — the phase's live criterion" on exactly these four edges, and `R033` is carried at exposure 16 as a firing risk, so the plan and the model agree about the state and neither discharges it. A suspect edge left open at the phase close is a Major against the artifact that carries it; it is recorded here and it holds the milestone.

#### Supplementary Specification

**Major — `Supplementary Specification#F4`, criterion `consumed-defect`.** S8 states the OpenAPI document exists in Development only, and S18 concludes that a non-Development run "exposes no readiness probe and no diagnostic surface at all". Both are wrong against `Todo.Api/Program.cs`: `MapOpenApi()` is called at line 58, outside the `if (app.Environment.IsDevelopment())` block at 49-56, so the document is served in every environment and is the one diagnostic surface an operating instance does publish.

This is a consumed defect and not a stale note. The Software Architecture Document's group-answer table names this artifact as the owner of the correction — "the specification's S8 and S18 state the document among the Development-only surfaces; the code maps it unconditionally and the code is recorded" — while that document's own mechanism M12 and the Deployment Model's Environment Mapping state the opposite gating correctly. The set the milestone certifies therefore carries two answers to one question, and the requirements artifact carries the wrong one. The Deployment Manager and the Technical Writer read this artifact to write a runbook and a release note, and both would document a diagnostic surface as absent that is in fact present.

Everything else in this artifact holds, and three parts of it are the strongest content in the set: both rate-limit budgets stated under `AN-024` in M3, P1 and R8 rather than one figure; R4 stating the BFF's two outbound hops apart under `AN-023`; and the twelve behaviours the recovered use cases must not overstate, which are the constraint the Use-Case Model's flows actually obey.

#### System Inventory

**Major — `System Inventory#F4`, criterion `exit-criterion-unmet`.** The coverage this phase exists to count is 84 of 139 files — 60.4% — with a second figure of 67 of 139 anchored, 48.2%. Neither reaches the 80% bar, and the Iteration Plan certifies `G4` Standing on exactly that figure. The reading behind the count is sound and candid: every unopened file is named, 45 of the 55 are one vendored Bootstrap 5 distribution the contribution contract forbids editing, and six more carry no perimeter fact. The defect is the denominator, and the stakeholder has now ruled it: the 45 Bootstrap files are a third-party distribution, not the system, and coverage is to be counted over the delivery's own files.

The ratio over the 94 files that are the delivery's own tree — 84 opened, 89.4%; 67 anchored, 71.3% — appears nowhere in either artifact. The counting itself is correct: its Files column sums to 139 and its Read column to 84, so no count and no per-area row needs to change. Only the figure the milestone reads needs the denominator the stakeholder gave it.

Traceability checked against the registered graph and clean: the twenty-two `EP` rows and the forty `AN` `DependsOn` edges agree with the tree, and `AN-021` names `EP-004`, `EP-005` and `EP-007` as diagram, table and graph all carry them.

#### Risk List

**Minor — `Risk List#F4`, criterion `contained-defect`.** `R033`'s probability contradicts the evidence its own row states. The score reads 4 — "High, 51% to 70%" — while the strategy cell reads "Avoid — not performed; firing", the warning sign reads "firing now, on all four", and the description reads "Scored 4 × 4 because the sign has already fired". An event the register states has already occurred on all four of its instances cannot be scored as a 51 to 70% likelihood. The band does not move — 5 × 4 = 20 is still High — so no grant requirement and no milestone state turns on it; the defect is that the register's published rule, that the same word gives the same number in every row, is applied to the inventory's anomalies and not to its own firing exposure. `R031` carries the same shape, its contingency recorded as taken and performed while the probability stays at 3.

The register otherwise holds and its discipline is the set's strongest governance artifact. Thirty-four risks; all 29 anomalies carried, each with a `Refines` edge the graph confirms; every probability and impact reproducing from the one published mapping; four accepts at exposure 12 each quoting the stakeholder's own answer; no risk above Moderate accepted on the Project Manager's authority. `R030` records a retirement that landed without claiming the exposure is removed, and `R034` records an action performed without claiming the incompatibility corrected — both the distinction this register's own rule requires and the distinction that makes it usable at a gate.

#### Vision

**Minor — `Vision#F2`, criterion `contained-defect`.** A Constraints row repeats the OpenAPI gating that `Supplementary Specification#F4` records as wrong. Contained: the Vision is not the artifact the correction is owed to, it carries the same sentence in a supporting role, and no role builds a decision on it. The same correction settles it.

#### Software Architecture Document

**Minor — `SAD#F2`, criterion `contained-defect`.** The Deployment View closes "One setting separates Development from any other environment: the request budget", while the Deployment Model opens its Environment Mapping conclusion "Two settings separate the environments, not one". Both artifacts have the facts right and their facts agree; only the count is stated twice with two answers, using the same word for different things without saying so. Contained: the SAD is the architecture record and the Deployment Model is the artifact the fired trigger commissions for this question, and no role builds a decision on which count is right.

The rest of the architecture holds on the anchors. Twenty-two components with every use case's path crossing named components; its Traceability table reports the `Realizes` edges read back from the graph and cross-checked from either direction; the components carrying no edge state their anchors instead of a composed one. M8's asymmetry between the BFF's two outbound hops is the finding this phase most needed, because it is the one property no anomaly row records.

#### Development Case

**Approved.** `Development Case#F4` is closed and verified: ACT-DC-01 names Project Management in every phase partition it draws, at the intensity the canonical matrix gives it, so the diagram and the intensity table agree. The baseline is not redefined: two roles inactive, each carrying the trigger that justifies it; no CORE artifact omitted or reassigned; no artifact outside the CORE + OPTIONAL universe named; the use-case enumeration rules stated as the baseline states them. The six optional verdicts were re-evaluated this iteration against the recovered set, and the one FIRED trigger holds on this project's real facts — four processes, a browser bundle, a separate REST service, SQLite, a YARP proxy hop, and a settings pair per serving project. The five NOT FIRED verdicts each name the condition that does not hold, and each holds up.

#### Use-Case Model

**Approved.** Eleven use cases over 22 entry points, each anchored to the entry point whose code performs it; `EP-020`, `EP-021`, `EP-022` and the `admin` branch are exclusions with a stated reason, three of them the stakeholder's own rulings. No cross-cutting mechanism is modelled as a use case. The five use cases with two routes in are one use case each with two scenarios, not one per actor. The Traceability table's eleven rows match the registered graph, every `EP-NNN → UC-NNN` edge carried unmarked. The two entry-point lists are reconciled with the rule stated: the Survey's Source column names the entry point whose code performs the use case, the actor-goal matrix names the entry point the actor acts through — the screen is `EP-003`, the operation it becomes is `EP-012`. The statement of the session surface's instability beside `UC-001` to `UC-004` is the one place in the set where a recovered behavior is qualified by its own code's history.

#### Deployment Model

**Approved.** The §5.2 trigger genuinely holds and this artifact is why it was upheld: a browser process, three .NET processes, two short-lived children and one container on one machine, a proxy hop between two of them, and an `appsettings` pair per serving project. Its Environment Mapping matches the code on the point that four other artifacts got wrong in Excavation and have since corrected — the budget in force is 50/50/queue 50, not the code's 100 series — and it states the three ungated surfaces correctly, which is what made `Supplementary Specification#F4` visible to this review.

#### Iteration Assessment, Change Request

`[OMITTED: Iteration Assessment — the Project Manager authors it after this review; at review time it cannot describe the iteration being reviewed, and its absence is not a defect and not a gate condition]`

`[OMITTED: Change Request — not opened in the sprint zero, where no Change Control Manager works; the stakeholder's orders reach their owners through the Work Order]`

### Review Coordinator lens
<!-- review: Consolidation I1 -->

<!-- review: Consolidation I1 -->

**The line every number below is copied from**, written from `read_artifact_findings` across all twelve artifacts in this milestone's turn and never from a lens's narrative:

`[FINDINGS] read=12, unread=none, open Critical=0, open Major=6 [System Inventory#F4, Supplementary Specification#F4, Design Model#F2, Iteration Plan#F11, Iteration Plan#F12, Iteration Plan#F13], open Minor=3 [Risk List#F4, Vision#F2, Software Architecture Document#F2]`

Fifty-one finding entries stand against the twelve artifacts read. Forty-two carry a resolution object and were closed by the lens that recorded them. Nine are open: none Critical, six Major, three Minor.

```plantuml
@startuml
title LED-GHR-01 Consolidated finding ledger at the GHR milestone - 51 entries over 12 artifacts, 42 closed, 9 open
skinparam shadowing false
skinparam wrapWidth 235
hide circle
hide empty members

package "Major - 6, the artifact is reworked before any role consumes it again" {
  class "Design Model\nF2 trace-gap\nDesigner 2 edges, System Analyst 2 edges" as M1 <<Major>>
  class "Supplementary Specification\nF4 consumed-defect\nSystem Analyst" as M2 <<Major>>
  class "System Inventory\nF4 exit-criterion-unmet\nSoftware Archaeologist" as M3 <<Major>>
  class "Iteration Plan\nF11 exit-criterion-unmet\nProject Manager" as M4 <<Major>>
  class "Iteration Plan\nF12 consumed-defect\nProject Manager" as M5 <<Major>>
  class "Iteration Plan\nF13 exit-criterion-unmet\nProject Manager" as M6 <<Major>>
}

package "Minor - 3, fixed in the owner's next turn, holding no milestone" {
  class "Risk List\nF4 contained-defect\nProject Manager" as m1 <<Minor>>
  class "Vision\nF2 contained-defect\nSystem Analyst" as m2 <<Minor>>
  class "Software Architecture Document\nF2 contained-defect\nSoftware Architect" as m3 <<Minor>>
}

package "Critical - 0" {
  class "none\nno undeclared scope, no contradiction in what\nthe stakeholder declared, no risk only they may accept" as C <<none>>
}

M4 ..> M3 : G4 cites the coverage figure
M5 ..> M2 : G3 names one of two causes
M6 ..> M1 : G6 reads the four edges
m1 ..> M1 : one exposure, three artifacts
m2 ..> M2 : the same sentence, supporting role
M1 --> C
M2 --> C
M3 --> C

note bottom of M1
  Four edges, two owners, one act each, and the evidence
  already stated in the model. No reading of the code is owed.
end note
note bottom of M3
  Every count is right; the denominator is not the stakeholder's
  ruling. 84 of the 94 files of the delivery's own tree is 89.4
  per cent and appears in no artifact.
end note
@enduml
```

#### Open findings — nine entries, each with owner, severity and the corrective action

| Artifact | Key | Lens | Criterion | Severity | Owner | What closes it |
|---|---|---|---|---|---|---|
| Design Model | F2 | Reviewer | `trace-gap` | Major | Designer (2 edges), System Analyst (2 edges) | Clear `CLS-001 → TBL-001`, `CLS-007 → TBL-002`, `CLS-020 → UC-007`, `CLS-020 → UC-010` at the end the graph marks; then restate the Traceability section's two closing paragraphs at the state the graph holds. The evidence for all four is already in the model |
| Supplementary Specification | F4 | Reviewer | `consumed-defect` | Major | System Analyst | Correct S8 and S18 to the gating the code has: the reference UI and both health endpoints are Development-only, the OpenAPI document is mapped unconditionally, the HTTP logging stage runs in every environment. Cite `Todo.Api/Program.cs:44,49-58` and cross-reference SAD M12 and the Deployment Model's Environment Mapping |
| System Inventory | F4 | Reviewer | `exit-criterion-unmet` | Major | Software Archaeologist | State the coverage over the 94 files of the delivery's own tree — 84 opened (89.4%), 67 anchored (71.3%) — with the 45 vendored Bootstrap files named as one excluded third-party distribution. Change no count and no per-area row |
| Iteration Plan | F11 | Management Reviewer | `exit-criterion-unmet` | Major | Project Manager | Write the threshold into `G4`'s text and state both ratios in its evidence cell: 84 of 139 raw, 84 of 94 (89.4%) over the tree the reading is about |
| Iteration Plan | F12 | Management Reviewer | `consumed-defect` | Major | Project Manager | Name the second cause in `G3`'s evidence cell — the Supplementary Specification's S8/S18 against the code, SAD M12 and the Deployment Model — and list both corrections in the next iteration's work items |
| Iteration Plan | F13 | Management Reviewer | `exit-criterion-unmet` | Major | Project Manager | Restate `G6`'s evidence cell to carry `R033` at the state the register records — avoidance unperformed, warning sign firing, four edges marked — and decide the criterion on that state, not on the strategy label |
| Risk List | F4 | Management Reviewer | `contained-defect` | Minor | Project Manager | Restate `R033`'s probability at 5 on the basis its own evidence states, carrying exposure 20; apply the same test to `R031` |
| Vision | F2 | Reviewer | `contained-defect` | Minor | System Analyst | Correct the Constraints row: the OpenAPI document is served in every environment; the reference UI and both health endpoints are Development-only. Cite `Todo.Api/Program.cs:44,49-58,62` |
| Software Architecture Document | F2 | Reviewer | `contained-defect` | Minor | Software Architect | Say *configuration binding* where the Deployment View means one binding, so the count cannot be read against the Deployment Model's two environment differences |

#### Closed this milestone — forty-two entries, verified at the source

| Artifact | Entries closed | What they were, and what verified the closure |
|---|---|---|
| Development Case | F1, F2, F3 (technical); F1, F2 (management); F4 (technical) | Six entries. The unsourced enterprise version policy is gone; the duplicated role-delta list and CLS-DC-01 diagram are deleted; Document Control is brought forward; the contributor set names all six lenses with the matching CLS-DC-01 edges; ACT-DC-01 names Project Management in every phase partition at the canonical matrix's intensity. Verified in the artifact against the canonical matrix |
| System Inventory | F1, F2, F3 (technical) | The `AN-021` row carries all three entry points; the coverage headline reproduces from the per-area table; Document Control names the iteration its content belongs to |
| Risk List | F1 (technical), F1 (management), F2, F3 (technical), F2, F3 (management) | Six entries. The scores reproduce from one published mapping; `R004` and `R011` sit at 12 with the stakeholder's grant; `R024` no longer misattributes a state to the Design Model; `R030` records a retirement that landed without claiming the exposure removed; `R032` records avoidance performed on all six citing artifacts |
| Iteration Plan | F1, F2, F3, F4 (technical); F1 to F10 (management) | Fourteen entries. The twelve entry-point-bearing anomalies are named; the critical chain puts the gate ahead of the verdict it feeds; the State column states each row's actual outcome; the AR criteria cells are restated at the state their artifacts hold; A12 records the third and fourth puts as given; the Closes column holds finding keys only |
| Vision | F1 (technical), F1 (management) | Two entries. The Features diagram draws the platform mechanisms as components, not use-case ellipses, so the Vision's count agrees with the Use-Case Model's eleven |
| Use-Case Model | F1, F2, F3, F4 (technical), F1 (management) | Five entries. The `EP-003` screen edges and the five `COMP-014` edges are confirmed in the graph; the rule separating the actor-goal matrix from the Survey's Source column is stated; R6 states both budgets under `AN-024` |
| Supplementary Specification | F1, F2, F3 (technical) | The four rate-limit places state both values under `AN-024`; R4 states the two outbound hops apart under `AN-023`; Document Control names the iteration under review |
| Software Architecture Document | F1 (technical) | `SP1` and M3 state both budgets under `AN-024`, and the bounded-load quality row carries the bound in force |
| Deployment Model | F1 (technical) | The Environment Mapping preamble limits itself to what is true and the Rate limiting row reads 50/50/50 for Development against the code defaults elsewhere |
| Design Model | F1 (technical) | The PD-D3 note cites `AN-025` for the unconverted owner key; `AN-005` is cited only for `EnsureCreated` |
| Iteration Assessment | — | No finding recorded against it |
| Review Record | — | No finding recorded against it |

#### Cross-lens reconciliation — where the two executed lenses spoke on one subject

| Subject | The two lenses | Resolution recorded here |
|---|---|---|
| Design Model's four suspect edges | Technical lens records `Design Model#F2`; the management lens's `Iteration Plan#F13` rests on the same four edges via `G6` | **Two defects, not a duplicate.** `#F2` is the artifact defect; `#F13` is the plan's criterion defect — it decides a criterion on a strategy label. One owner pass at the Design Model does not close `#F13`: `G6` must still be restated on the state the register records |
| The OpenAPI gating | Technical lens records `Supplementary Specification#F4` (Major) and `Vision#F2` (Minor); the management lens records `Iteration Plan#F12` naming the same contradiction as `G3`'s unnamed second cause | **One root cause, three entries, deliberately kept apart.** The Major is the requirements artifact; the Minor is the same sentence in a supporting artifact; `#F12` is the plan's evidence cell listing one cause where the set carries two. Closing only the Major leaves the next iteration's corrective list one correction short |
| The coverage ratio | Technical lens records `System Inventory#F4`; the management lens records `Iteration Plan#F11` | **Two entries, one dependency.** `#F4` restates the denominator; `#F11` writes the threshold into `G4` and cites the ratio `#F4` produces. `#F11` cannot be closed before `#F4` |
| `Risk List#F4` | Only the management lens records it | **No conflict.** The technical lens does not dispute `R033`'s exposure or its strategy; the disagreement is that the probability does not reproduce from the row's own evidence |
| `Development Case#F4` | Technical lens records it at Excavation iteration 4; management lens had recorded the same class earlier under its own keys | **One defect, one key, closed at this milestone.** The Process Engineer's Consolidation turn corrected ACT-DC-01; both lenses' approval rests on that reading |
| Severity bands | The two lenses agree on every shared subject | **No disputed band.** No finding needed reclassification at this consolidation, and none was reclassified |

#### Review effectiveness at this milestone

| Indicator | Value | Reading |
|---|---|---|
| Review coverage | 12 of 12 planned artifacts read and formally reviewed — 100% | Full. No artifact of this phase entered the milestone unread |
| Defect density by artifact type | Requirements artifacts (Vision, Use-Case Model, Supplementary Specification): 12 entries over three artifacts. Analysis & Design artifacts (SAD, Deployment Model, Design Model): 5 entries over three. Project Management artifacts (Iteration Plan, Risk List): 24 entries over two. Discovery (System Inventory): 4 entries. Environment (Development Case): 6 entries | Concentration is in the planning artifacts, not the recovered content. The recovered set absorbed 5 entries across the three design artifacts; the two Project Management artifacts absorbed 24. That is the phase's principal process finding: the plan and the register, not the model of the system, are what failed this milestone |
| Defect removal efficiency (review vs test) | **Not measurable at this milestone.** No test artifact exists in the sprint zero; the Test discipline's first executable statement is Elaboration's | Recorded as unmeasured, not as zero. No figure is invented for it |
| Rework effort | **Not measurable in this milestone's units.** The open entries are corrections to documents; the process measures tokens and elapsed time per phase, and no per-finding spend is recorded | What is measured is the phase's spend, in the Iteration Plan's two currencies. No hour figure is derived from it |
| Findings overdue at the close | 0 of 9. Every open entry was recorded in this milestone's own turn and is scheduled in Consolidation iteration 2 | No review debt carried out of the milestone unattended, which is the condition the stakeholder set at the SBC close |

No trend is reported against a prior milestone. Every finding in this ledger was recorded in this Consolidation iteration's review; there is no earlier Consolidation review to compare against, and a trend drawn against Excavation's entries would compare a different artifact set.

## Resolutions and Actions
### Reviewer lens
<!-- review: Consolidation I1 -->

#### Closed this milestone by this lens

| Finding | Criterion | What closed it | Verified at |
|---|---|---|---|
| `Development Case#F4` | `contained-defect` | ACT-DC-01 now names Project Management in all seven phase partitions, at the canonical intensity for each phase; the diagram and the intensity table agree | Development Case — Disciplines and Intensity, ACT-DC-01 |

#### Open, and what closes each

| Finding | Criterion | Severity | What closes it | Owner | Where the work belongs |
|---|---|---|---|---|---|
| `Design Model#F2` | `trace-gap` | Major | Clear `CLS-020 → UC-007`, `CLS-020 → UC-010` (System Analyst) and `CLS-001 → TBL-001`, `CLS-007 → TBL-002` (Designer), each stating the reading that keeps it; then restate the Traceability section's closing paragraphs at the state the graph holds | System Analyst, Designer | Analysis & Design — both hold a stage in this phase. Closes `R033` and G7 |
| `Supplementary Specification#F4` | `consumed-defect` | Major | Correct S8 and S18 against `Todo.Api/Program.cs:44,49-58`: the reference UI and both health endpoints are Development-only, the OpenAPI document is mapped unconditionally, the logging stage runs in every environment | System Analyst | Requirements — this phase's stage. Unblocks the Deployment Manager and the Technical Writer |
| `System Inventory#F4` | `exit-criterion-unmet` | Major | State the ratio over the 94 files that are the delivery's own tree (84 opened, 89.4%) beside the 139-file count, and have `G4` cite the ratio that meets the bar with its denominator named | Software Archaeologist, then Project Manager for G4 | Discovery — this phase's stage |
| `Vision#F2` | `contained-defect` | Minor | Correct the Constraints row: the OpenAPI document is served in every environment | System Analyst | Requirements — after the Majors |
| `SAD#F2` | `contained-defect` | Minor | Restate "one setting" as one configuration binding, with the Development-only surfaces named beside it as the Deployment Model counts them | Software Architect | Analysis & Design — after the Majors |

#### What the two Majors have in common, and why it matters for the next iteration

`Supplementary Specification#F4` and `SAD#F2` are the same class of defect this project has now recorded seven times across three phases: one fact, stated twice, in two artifacts, with two answers. The rule that closes the class is already written in the Development Case's "Process rule this phase adds" — a document that reports another artifact's state re-derives it from that artifact in the same turn the artifact changes. It has held for the Iteration Plan this iteration and the plan's cells are clean; it has not yet been applied to the four artifacts that describe the environment, which is where both of these findings sit.

`System Inventory#F4` is a different class, and it is the one this milestone should not lose: the reading is thorough (every unopened file named, every reason given, the arithmetic reproducing) and the number it publishes understates what it did, because the denominator counts a vendored bootstrap bundle as though it were the delivery. The correction is one sentence. What would be wrong is to read the 60.4% as a thin reading and order more of the tree opened — nothing is hidden, and the 45 unopened Bootstrap files carry no behaviour of the system.

#### Actions the next iteration carries

| # | Action | Owner | Closes |
|---|---|---|---|
| 1 | Clear the four suspect edges at their own ends | System Analyst (2), Designer (2) | `Design Model#F2`, `R033`, G7 |
| 2 | Correct S8 and S18 to the code's actual gating | System Analyst | `Supplementary Specification#F4` |
| 3 | State the coverage ratio over the delivery's own tree, and have G4 cite it | Software Archaeologist, Project Manager | `System Inventory#F4`, G4 |
| 4 | Correct the Vision's Constraints row | System Analyst | `Vision#F2` |
| 5 | Restate the SAD's "one setting" sentence | Software Architect | `SAD#F2` |
| 6 | Re-read all four environment-describing artifacts against `Todo.Api/Program.cs` in one pass once actions 2, 4 and 5 land, so the class closes rather than the instance | System Analyst, Software Architect | closes the class, not a finding |

No action above schedules work a later phase performs. Actions 1 to 5 sit in stages this phase runs; action 6 is a reading, not new content.

### Management Reviewer lens
<!-- review: Consolidation I1 -->

<!-- review: Consolidation I1 -->

Findings my lens closed at this milestone: one. All six Major defects and three Minor stand open and are the further iteration's work.

| Artifact | Key | Criterion | Owner | The corrective action |
|---|---|---|---|---|
| Iteration Plan | F11 | `exit-criterion-unmet` | Project Manager | Write the threshold into G4 — every file either opened or named with its reason, and coverage of the delivery's own tree at 80% or more — and state both ratios in the evidence cell: 84 of 139 raw, and 84 of 94 (89.4%) over the tree the reading is about, naming the 45 vendored Bootstrap files as the one excluded third-party distribution. The stakeholder ruled that denominator on 2026-11-23 |
| Iteration Plan | F12 | `consumed-defect` | Project Manager | Name the second cause in G3's evidence cell — the Supplementary Specification's S8 and S18 against `Todo.Api/Program.cs:58` and against the SAD's M12 and the Deployment Model's Environment Mapping — and list both corrections in the further iteration's work items, not the four trace edges alone |
| Iteration Plan | F13 | `exit-criterion-unmet` | Project Manager | Restate G6's evidence cell to carry R033 at the state the register records — exposure in the High band, avoidance unperformed, warning sign firing, all four edges marked — and decide the criterion on that state rather than on the strategy label |
| Design Model | F2 | `trace-gap` | Designer (2 edges), System Analyst (2 edges) | Each owner reads its own end and clears the edge stating why it still holds, or retires and re-registers it with the link type its evidence supports: `CLS-001 → TBL-001` and `CLS-007 → TBL-002` for the Designer; `CLS-020 → UC-007` and `CLS-020 → UC-010` for the System Analyst. The evidence is already written in the model, so no re-reading of the code is needed |
| Supplementary Specification | F4 | `consumed-defect` | System Analyst | Correct S8 and S18 against the code: `MapOpenApi()` is mapped at `Todo.Api/Program.cs:58`, outside the `if (app.IsDevelopment())` block at 49-56, so the OpenAPI document is served in every environment and is a diagnostic surface an operating instance does publish. Bring S18's conclusion with it |
| System Inventory | F4 | `exit-criterion-unmet` | Software Archaeologist | State the two ratios the tree actually has and settle which one coverage is counted on. Keep 139 files / 84 opened / 55 unopened as the raw count and add the ratio over the 94 files that are the delivery's own tree — 84 opened, 89.4%, 67 anchored — with the 45 vendored Bootstrap files named as one third-party distribution the stakeholder does not call their system. Change no count and no per-area row: the arithmetic reproduces |
| Risk List | F4 | `contained-defect` | Project Manager | Restate R033's probability at 5 with a one-line basis naming what the evidence states, or state why an exposure whose warning sign has already fired is scored in the 51 to 70% band. Apply the same test to R031 |
| Vision | F2 | `contained-defect` | System Analyst | Settle the OpenAPI gating with `Supplementary Specification#F4`; one correction closes both |
| Software Architecture Document | F2 | `contained-defect` | Software Architect | State which count "one setting" and "two settings" each refer to, or adopt the Deployment Model's count and say so — the facts already agree and only the word differs |

```plantuml
@startuml
title The further Consolidation iteration - nine corrective acts, each with the role the process schedules here
skinparam shadowing false
skinparam wrapWidth 250

|Project Manager|
start
:Iteration Plan#F11 - G4's threshold written into the criterion,
both coverage ratios in the evidence cell;
:Iteration Plan#F12 - G3's evidence names both contradictions,
the further iteration's items carry both corrections;
:Iteration Plan#F13 - G6 decided on R033's recorded state,
not on the strategy label;
:Risk List#F4 - R033's probability against the evidence it states,
R031 tested the same way;
:plan the further iteration from this record, and re-put gate H5;

|System Analyst|
:Supplementary Specification#F4 - S8 and S18 corrected against
Todo.Api/Program.cs:58, outside the Development block at 49-56;
:Vision#F2 - the same gating settled in one pass;
:CLS-020 to UC-007 and CLS-020 to UC-010 cleared with the reading stated;

|Designer|
:CLS-001 to TBL-001 and CLS-007 to TBL-002 cleared
with the reading the model already holds;

|Software Architect|
:Software Architecture Document#F2 - the count reconciled
with the Deployment Model's;

|Software Archaeologist|
:System Inventory#F4 - the own-tree ratio stated beside the raw count,
the 45 Bootstrap files named as the excluded distribution;

|Management Reviewer|
:the GHR lens re-run on records that agree with the set;
:gate H5 put again;
stop
@enduml
```

**Why this is one iteration's work and not more.** Every one of the nine acts belongs to a role the process schedules in Consolidation — Environment, Requirements, Analysis & Design, Discovery and Project Management all run here, and the three lenses of the milestone review follow them. None requires a decision from the stakeholder: the one decision that was theirs, the coverage denominator, they gave in the answer that refused the sanction. None requires re-reading the code: the four trace edges carry their evidence in the model, the OpenAPI fact is anchored at a line number, and the coverage arithmetic reproduces from the table. No recovered content is touched, which is why the stakeholder's confirmation of the eleven use cases, four exclusions, twenty-two components and eight tables is unaffected by any act on this list.

**The one closure this lens recorded.** `Iteration Plan#F10` — three cells recording gate H4's fourth put as unanswered — is closed and verified: the plan now carries GHR's criteria in place of the AR criteria, and the fourth put is recorded as passed in the milestone sequence. The one gate the plan records as unput is H5, a different gate, which genuinely had not been put at the time and has now been put and refused.

**Two Minors the technical lens and I recorded that no criterion turns on.** `Risk List#F4` and `Software Architecture Document#F2` are inside their artifacts; the further iteration lists them with the Majors because their owners are working those artifacts anyway, not because they hold anything.

### Review Coordinator lens
<!-- review: Consolidation I1 -->

<!-- review: Consolidation I1 -->

**Stakeholder finding (2026-11-23, on the iteration-2 pass):** "Nothing to add. The order stands: coverage and the OpenAPI gating first, the plan's cells last. No priority among the six — clear all six in this iteration." The priority order below is confirmed as written and no ranking within the six is applied: all six Major findings are cleared in Consolidation iteration 2, none deferred to a later pass or to Inception.

Nine corrective actions and no escalations. Every open entry has an owner who holds a stage in Consolidation iteration 2, so none is escalated to the Project Manager for a deadline miss — no deadline has yet passed — and none is escalated to the stakeholder, because none is Critical.

#### Priority order — the order the next iteration works in

| Priority | Finding | Severity | Why it ranks here |
|---|---|---|---|
| 1 | `System Inventory#F4` | Major | The stakeholder ruled the denominator on 2026-11-23. Restating the ratio over the 94 files of the delivery's own tree is a figure, not a re-reading: the counts are right and no per-area row changes. `Iteration Plan#F11` cannot be written before it |
| 2 | `Supplementary Specification#F4` | Major | A consumed defect the Deployment Manager and the Technical Writer read to write a runbook and a release note. It also settles `Vision#F2` and supplies one of the two causes `Iteration Plan#F12` must name |
| 3 | `Design Model#F2` | Major | Four edges, two owners, the evidence already stated in the model. It closes `R033` — the phase's live High-band exposure at 4 × 4 = 16 — and it is the state `Iteration Plan#F13` must be decided on |
| 4 | `Iteration Plan#F11`, `#F12`, `#F13` | Major | Three defects in one place: the criteria table the GHR verdict is read on. All three depend on priorities 1 to 3 being settled at their artifacts; restating the cells before the artifacts hold the facts would repeat the defect |
| 5 | `Risk List#F4` | Minor | `R033`'s probability contradicts the evidence its own row states. The band does not move (20 is still High), so no grant requirement and no milestone state turns on it |
| 6 | `Vision#F2` | Minor | The same OpenAPI sentence at a supporting artifact, settled by the same correction as priority 2 |
| 7 | `Software Architecture Document#F2` | Minor | One word used for two things. Contained: both artifacts' facts are right and agree |

The order above sequences the work; it does not rank it. All six Major findings are cleared in this phase's next iteration, and the three Minor findings with them.

**Escalations: none.** No finding in this ledger is Critical, no deadline has passed, and no role has failed to provide an artifact on time. The gate H5 refusal is not an escalation of this role — it is the stakeholder's own decision, recorded as given.

```plantuml
@startuml
title ACT-GHR-02 Correction order for Consolidation iteration 2 - three artifacts land first, the plan restates after them
skinparam shadowing false
skinparam wrapWidth 250

|Software Archaeologist|
start
:1  System Inventory#F4
state the coverage over the 94 files of the
delivery's own tree - 84 opened, 89.4 per cent,
67 anchored, 71.3 per cent;
:name the 45 vendored Bootstrap files as one
third-party distribution excluded by the
stakeholder's ruling of 2026-11-23;
:change no count and no per-area row;

|System Analyst|
:2  Supplementary Specification#F4
correct S8 and S18 to the gating the code has -
the OpenAPI document is mapped unconditionally;
:then Vision#F2
the same sentence at its own artifact;

|Designer and System Analyst|
:3  Design Model#F2
clear CLS-001 to TBL-001 and CLS-007 to TBL-002,
CLS-020 to UC-007 and CLS-020 to UC-010
each at the end the graph marks;

|Project Manager|
:4  Risk List#F4
restate R033's probability at 5 on the basis its
own evidence states, carry exposure 20;
:5  Iteration Plan#F11, F12, F13
write G4's threshold and cite step 1's ratios,
name both causes in G3, decide G6 on step 3's state;
:6  Software Architecture Document#F2
one word for two things - configuration binding
against environment difference;
:Steps 1 to 3 are independent and run in either order.
Steps 4 to 6 wait on them: a plan cell citing a ratio,
a cause or an edge cannot be restated before the
artifact holds it;
:All six Major findings clear in this iteration
none is deferred to a later pass or to Inception;

|Reviewer|
:7  technical lens re-run over the corrected set;

|Management Reviewer|
:8  management lens re-run;
:9  gate H5 put a second time;

|Stakeholder|
:10  sanction decision read from the finding data;

|Review Coordinator|
:11  GHR verdict on the second put;
stop
@enduml
```

#### Finding lifecycle — where each entry stands at this close

```plantuml
@startuml
title MET-GHR-01 Finding lifecycle at the GHR milestone - 51 entries, where each stands
skinparam shadowing false
skinparam wrapWidth 235

state "Recorded by a lens\n51 entries this milestone" as R
state "Assigned\nowner and severity on the entry\n51" as A
state "In progress\nthe owner holds a stage in Consolidation\n51" as P
state "Resolved\nowner performed the correction\n42" as RV
state "Verified\nlens checked it at the artifact\n42" as VF
state "Closed\nresolution object on the entry\n42" as C
state "Open at the close\nholds the milestone if Major\n9" as O

R --> A
A --> P
P --> RV
RV --> VF
VF --> C
P --> O : corrective act not performed
O --> P : Consolidation iteration 2

note right of C
  Closed by lens - technical 25, management 17.
  One management entry, Development Case#F2, was
  recorded at Excavation under the stakeholder's
  order and closed at this milestone.
end note
note right of O
  Open by lens - technical 5, management 4.
  Severity - 6 Major, 3 Minor, 0 Critical.
  All nine owners hold a stage in Consolidation
  iteration 2, which the process schedules.
end note
@enduml
```

#### Review calendar — the milestone's cadence and the second put

The GHR review is scheduled against the iteration boundary, not a calendar date: it opens when the iteration's artifacts are in target state and the plan's `G1` to `G8` are written, and it closes when the verdict is recorded. Because the stakeholder refused the sanction on 2026-11-23, the same review is re-scheduled for the close of Consolidation iteration 2 — the iteration this verdict records as required. No later milestone review (LCO, LCA, IOC, PR) is moved by this: each remains anchored to its own phase exit.

```plantuml
@startuml
title CAL-GHR-01 Consolidation review calendar - review events at the iteration boundary
skinparam shadowing false
skinparam wrapWidth 300

|Review Coordinator|
start
:Calendar the GHR review for the end of
Consolidation iteration 1, aligned to the
Iteration Plan's GHR criteria G1 to G8;

|Reviewer|
:GHR technical lens executes
12 artifacts read
30 entries recorded, 25 closed, 5 open;

|Business Reviewer|
:INACTIVE - did not evaluate this review
Business Modeling inactive per the Development Case
nothing in the verdict rests on this lens;

|Management Reviewer|
:GHR management lens executes
12 artifacts read
21 entries recorded, 17 closed, 4 open;
:Put gate H5;

|Stakeholder|
:Gate H5 answered 2026-11-23
sanction REFUSED - six Majors cleared in this phase
coverage counted over the delivery's own files;
:Order confirmed for the iteration-2 pass
all six cleared in this iteration, no ranking among them;

|Review Coordinator|
:Consolidate the two executed lenses
51 entries - 42 closed, 9 open
0 Critical, 6 Major, 3 Minor;
:Verdict - phase scope incomplete
Consolidation iteration 2 carries the nine open entries;
:Calendar the second GHR put
for the close of Consolidation iteration 2;

|Correction owners|
:Iteration 2 - the nine open entries corrected
at their artifacts by their owners;

note right
  Two of the six Majors depend on a third:
  Iteration Plan#F11 cites the ratio
  System Inventory#F4 restates,
  Iteration Plan#F12 names the cause
  Supplementary Specification#F4 corrects.
end note

|Reviewer|
:Lens re-run on the corrected set;

|Management Reviewer|
:Management lens re-run;
:Gate H5 put a second time;

|Stakeholder|
:Sanction decision on the recorded finding data;

stop
@enduml
```

## Disposition
### Reviewer lens
<!-- review: Consolidation I1 -->

**Disposition: Approved with Changes.**

Nine of the twelve artifacts are approved from this lens with nothing recorded against them. Three are not, and the three are reworked before any role consumes them again:

- `Design Model#F2` — four suspect edges open at the phase close, which is the one GHR exit criterion the phase has not moved (`G7`, `R033`)
- `Supplementary Specification#F4` — the OpenAPI document's gating stated backwards in the artifact the Deployment Manager and the Technical Writer will read
- `System Inventory#F4` — the coverage ratio published against a denominator that hides the reading's actual reach, on the criterion `G4` certifies

**No Critical finding is recorded, and none needs the stakeholder to unblock it.** Every defect above is a correction its owner can make inside this phase with the evidence already in hand; none needs a decision on scope, on a contradiction in what was declared, or on a risk only the stakeholder may accept. This lens therefore sends nothing to gate H5 and escalates nothing.

**What this lens does not decide.** Whether the milestone closes is the Review Coordinator's verdict, read on all three lenses and on gate H5's answer. This lens records the technical position only: the set is substantially complete and anchored, its recovered content is confirmed and no finding reopens it, and five corrections stand between it and a clean technical certification.

**On the two that hold the milestone.** `Design Model#F2` and `System Inventory#F4` each fail a criterion the milestone is read on, and each closes on one act in a stage this phase runs. Nothing about either requires another iteration: the owners hold their stages this iteration, the evidence is in the artifacts, and the corrections add no content and reopen no recovered element. If an iteration is opened, it is opened for them, not for the set.

**On the recovered content.** Nothing in this review touches it. The eleven use cases, the four stated exclusions, the twenty-two components and the eight tables stand as the stakeholder confirmed them at gate H4, and this lens found nothing wrong with any of them. `R033` is a bookkeeping defect in the graph, not a defect in what the graph describes — which is why the correction is a clearance and not a re-reading.

**The one thing worth carrying past this milestone.** The class of defect this project keeps paying for is one fact stated twice in two artifacts with two answers. It cost four Majors at the AR milestone and two more here. The rule that closes it is written in the Development Case; it needs applying to the four artifacts that describe the environment, in one pass, in the same turn the fact changes. That is action 6 of this lens's list, and it is the only action that prevents a finding rather than closing one.

### Management Reviewer lens
<!-- review: Consolidation I1 -->

<!-- review: Consolidation I1 -->

**Verdict: No-Go.** The Greenfield Handoff Ready milestone is not achieved at this put. One Major at a lifecycle milestone is a stop signal; six is a phase that has not finished. The burden of proof rests on the project team and it has not been discharged.

**Gate H5 — put 2026-11-23, refused.** The question carried the defect list and the coverage figure inside it, and nothing pre-filled. The stakeholder's answer is the record of the gate, and their second answer is the order the further iteration works to.

```plantuml
@startuml
title GHR milestone disposition - what holds the gate, and what the further iteration clears
skinparam shadowing false
skinparam wrapWidth 250

start
:Consolidation iteration 1 closes;
:eight GHR criteria read, each on the artifact it cites;
note right
  G1, G5, G8 met on the evidence.
  G4 and G6 not met as the plan states them.
  G3 and G7 fail outright. G2 put and refused.
end note

:six Major and three Minor stand across four artifacts;
if (any Critical open?) then (yes)
  :escalate to the stakeholder;
  stop
else (no)
  :no defect needs a decision only the stakeholder can take;
endif

:verdict - No-Go at this put;
note right
  A missed criterion at a lifecycle milestone is a stop
  signal, not a negotiating point. There is no partial GHR.
end note

:gate H5 put with the defect list inside the question;
if (stakeholder sanctions the advance?) then (Yes)
  #lightgreen:the Majors carry into Inception as its first work;
  stop
else (No)
  #pink:a further Consolidation iteration is planned from this record;
  :nine corrective acts, each with the role this phase schedules;
  :the recovered set is confirmed and nothing in it changes;
  :gate H5 re-put on records that agree with the set;
  stop
endif
@enduml
```

**Project health at this gate.** Four dimensions, each rated on evidence and none on the project's own word.

```plantuml
@startuml
title Project health at the GHR gate - four dimensions, each rated on the evidence this review read
skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam wrapWidth 240
hide circle
hide empty members

class "SCOPE  -  Green" as SC {
  11 use cases, 22 entry points, 4 stated exclusions
  22 components, 8 tables, 42 classes
  every element anchored to file and lines
  no declared scope exists to measure against
  no recovered element reopened
}
class "SCHEDULE  -  Attention" as SD {
  sprint zero at iteration 1 of Consolidation
  against Survey 2 and Excavation 4
  six Majors open at this put, no Critical
  every corrective act sits with a role this phase schedules
}
class "COST  -  Not measurable" as CO {
  Survey 2 it: 8,995,433 tokens, 29 min agent, 5 min queue
  Excavation 3 it: 14,424,767 tokens, 28 min, 7 min
  Excavation 4 it: 9,735,197 tokens, 26 min, 10 min
  Consolidation: in flight, no figure until it closes
  no token budget declared, so no variance exists
}
class "QUALITY  -  Attention" as QU {
  0 Critical open
  6 Major open across 4 artifacts
  3 Minor open, none holding the milestone
  every Major a correction its owner can make in phase
}

SC --> QU : content sound, record not
SD --> QU : no slippage in the recovered set
note bottom of CO
  Two clocks, never added. No per-iteration velocity and no
  projected date is derived from these figures.
end note
note bottom of QU
  The one dimension that is not green: six Major defects stand
  and a milestone is not sanctioned over a Major.
end note

@enduml
```

**Risk retirement is real and not uniform, and the difference is the finding.**

```plantuml
@startuml
title Risk retirement across the sprint zero - what moved, what did not, and the one exposure now firing
skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam wrapWidth 245
hide circle
hide empty members

package "Retired - the action performed, verified at the artifact" {
  class "R031  a criterion's owner not scheduled\nmaterialized twice; contingency taken; Environment\nran as the phase's first discipline" as R31 <<closed>>
  class "R032  one fact transcribed inconsistently\navoidance performed on all six citing artifacts,\nR6 named, both budgets under AN-024" as R32 <<closed>>
  class "R030  the session surface never settles\nstatement landed beside UC-001 to UC-004;\nthe exposure stays live, AN-012 stands" as R30 <<landed>>
  class "R034  the snapshot names another product version\naction performed: recorded where the next role reads it;\nthe incompatibility itself is not corrected" as R34 <<landed>>
}

package "Live and accepted on the stakeholder's grant - unchanged this phase" {
  class "R004  4 x 3 = 12  admin branch never granted" as R4 <<granted>>
  class "R011  4 x 3 = 12  token minted from internals" as R11 <<granted>>
  class "R012  4 x 3 = 12  BFF and client untested" as R12 <<granted>>
  class "R016  4 x 3 = 12  no document of the system" as R16 <<granted>>
}

package "Live, avoidance owed by this phase's owners" {
  class "R001 R002 R003 R005 R007 R009 R010 R018\nR020 R021 R023 R024 R026 R028 R029\nall avoid; no action due in Consolidation" as RB <<carried>>
  class "R033  4 x 4 = 16  HIGH, firing\nfour edges still marked SUSPECT at the gate\nneither owner has performed the clearance" as R33 <<firing>>
}

R30 --> R33 : same failure shape, different subject
R31 --> R33 : a criterion certified on an act not performed
R33 --> RB : the one High-band exposure at the gate
note bottom of R33
  The trend is the finding: the register retired three exposures and
  added one that is firing. A top-band risk whose sign fires at the
  milestone the set is certified on is not a static register entry.
end note
note bottom of R34
  Recording an exposure is not retiring it. The action named is
  "write it where the next role reads it", and that landed.
end note

@enduml
```

Three exposures retired with their actions observed in the artifacts that carry them, two more with their retirement landed and their exposure correctly stated as live, and one that is firing at the gate: `R033`, a High-band risk whose avoidance both owners still owe. A register that carried the same top risk unchanged across two milestones would be evidence that risk retirement is not occurring; this one did move, and the exposure it added this phase is the one that has not been discharged. That is not a static register — it is a register that tells the truth about where the phase failed.

**What the stakeholder decided.** Two things, and neither is widened here. They refused the sanction: the six Majors are cleared in this phase and the gate is put again. And they ruled the coverage denominator: the 45 Bootstrap files under `Todo.Web/Client/wwwroot/bootstrap/` are a third-party distribution and not their system, so coverage is counted over the delivery's own files. They confirmed the recovered set unchanged — the eleven use cases, the four exclusions, the twenty-two components and the eight tables stand as they confirmed them at gate H4 — so no act on the corrective list touches recovered content.

**What the further iteration must reach before the gate is re-put.** The six Majors closed and verified at their artifacts, and the three Minors corrected with them where the same owner is working the same artifact. `G4` stated with its threshold and with the denominator the stakeholder gave it; `G3` naming both contradictions in the set; `G6` decided on `R033`'s recorded state; all four trace edges cleared by the roles the graph marks; the Supplementary Specification's S8 and S18 corrected against `Todo.Api/Program.cs:58`; the System Inventory's own-tree ratio stated beside its raw count. When those hold, the criteria can be read again on records that agree with the set they report, and gate H5 can be put a second time.

**No milestone, iteration or phase is recorded as completed by this review.** The Review Coordinator reads this verdict and the finding ledger; the milestone's disposition is theirs to record.

### Review Coordinator lens
<!-- review: Consolidation I1 -->

<!-- review: Consolidation I1 -->

**Verdict: the phase scope is incomplete. The GHR milestone is NOT sanctioned, and Consolidation iteration 2 is required.**

The verdict is read from the finding data, not from judgment. Every condition it rests on is a count or a recorded answer:

| Condition the verdict reads | State |
|---|---|
| Artifacts read | 12 of 12, `unread=none` |
| Open Critical | 0 |
| Open Major | **6** — `Design Model#F2`, `Supplementary Specification#F4`, `System Inventory#F4`, `Iteration Plan#F11`, `Iteration Plan#F12`, `Iteration Plan#F13` |
| Open Minor | 3 — `Risk List#F4`, `Vision#F2`, `Software Architecture Document#F2` |
| Stakeholder sanction | **REFUSED** — gate H5 put and answered 2026-11-23 |
| The recovered set confirmed | Yes, and unchanged since gate H4's fourth put |
| The set complete | Yes — 11 use cases, 4 stated exclusions, 22 components, 8 tables |
| Stakeholder direction for the iteration-2 pass | Received 2026-11-23 — the order confirmed, no ranking among the six, all six cleared in this iteration |

`[STATE_BLOCKED: S2_CALENDAR -> milestone_verdict/VERDICT_DONE]` Reason: six unresolved Major findings and a refused stakeholder sanction. The guard into `VERDICT_DONE` requires open Major = 0 and a `Stakeholder sanction: GRANTED` line; neither holds.

```plantuml
@startuml
title DIS-GHR-01 The GHR verdict and the conditions it was read on
skinparam shadowing false
skinparam wrapWidth 245
hide circle
hide empty members

package "Conditions met" {
  class "12 artifacts read\nunread = none" as X1 <<met>>
  class "open Critical = 0" as X2 <<met>>
  class "set complete and anchored\n11 UC, 4 exclusions, 22 COMP, 8 TBL" as X3 <<met>>
  class "recovered set confirmed at gate H4\nunchanged since" as X4 <<met>>
}

package "Conditions not met - the verdict" {
  class "open Major = 6" as N1 <<not met>>
  class "Stakeholder sanction\nREFUSED 2026-11-23" as N2 <<not met>>
}

package "Verdict" {
  class "GHR milestone NOT sanctioned\nrequiresIteration = TRUE\nConsolidation iteration 2" as V <<verdict>>
}

X1 --> V
X2 --> V
X3 --> V
X4 --> V
N1 --> V : holds the milestone
N2 --> V : a refusal admits no\nConditional Go

note bottom of N1
  Six Major over four artifacts. All six are corrections
  their owners can make inside this phase; none needs a
  decision only the stakeholder can take, which is why
  there is no Critical in the set. The stakeholder's
  direction of 2026-11-23 is to clear all six here.
end note
note bottom of V
  The phase is not closed and no later phase opens.
  Inception is not entered on a refused gate.
end note
@enduml
```

**Why this is not a Critical escalation and not a Conditional Go.** No finding in the ledger meets the Critical bar: nothing here is a decision on scope, a contradiction in what the stakeholder declared, or a risk only the stakeholder may accept. All six Major findings are corrections their owners perform with the evidence already in the artifacts. And a refused sanction admits no Conditional Go — the stakeholder's own decision on 2026-11-23 was to clear the six in this phase and put the gate again, so the process does not reinterpret the refusal as a conditional grant.

**What the next iteration carries.** Nine open entries, in the order recorded above, all by owners the process schedules in Consolidation iteration 2: the Software Archaeologist, the System Analyst, the Designer, the Project Manager, the Software Architect. The recovered content is not at issue in any of the six Majors, so no recovered element is reopened, no count changes, and no per-area row of the System Inventory moves.

**The stakeholder's ruling of 2026-11-23, applied.** The 45 Bootstrap files under `Todo.Web/Client/wwwroot/bootstrap/` are a third-party distribution and not part of the system; coverage is counted over the delivery's own files. That ruling is the substance of `System Inventory#F4` and the threshold `Iteration Plan#F11` must carry. The stakeholder also recorded that nothing in the recovered set is wrong — the 11 use cases, the 4 exclusions, the 22 components and the eight tables stand as confirmed at gate H4.

**Stakeholder input for the iteration-2 pass, 2026-11-23, verbatim:** "Nothing to add. The order stands: coverage and the OpenAPI gating first, the plan's cells last. No priority among the six — clear all six in this iteration."

**Recorded as given — the stakeholder's answer at gate H5, verbatim:** "Nothing in the recovered set is wrong: the 11 use cases, the 4 exclusions, the 22 components and the eight tables stand as I confirmed them. I do not accept a handoff with Majors open: clear the six in this phase and put the gate again. One fact for the coverage count: the 45 Bootstrap files under Todo.Web/Client/wwwroot/bootstrap/ are a third-party distribution, not my system — count coverage over the delivery's own files. Nothing else to add."

**The Iteration Assessment is not judged here.** `[OMITTED: Iteration Assessment — the Project Manager authors it on this verdict; at review time it cannot describe the iteration being reviewed, and its absence is not a defect and not a gate condition]`

**The Change Request ledger does not exist here.** `[OMITTED: Change Request — not opened in the sprint zero, where no Change Control Manager works; the stakeholder's orders reach their owners through the Work Order and through this Review Record]`
