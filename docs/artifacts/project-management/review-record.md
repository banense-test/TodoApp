## Document Control
### Reviewer lens
<!-- review: Excavation I2 -->

<!-- review: Excavation I2 -->

- Phase: Excavation
- Status: Technical lens complete for the AR (end-of-Excavation) milestone review, iteration 2. Nine findings of this lens closed on verified evidence; three open — 0 Critical, 2 Major, 1 Minor. Disposition — Approved with Changes; the two Majors hold the milestone until their artifact is reworked.
- Milestone Target: end-of-Excavation (AR) — not achieved. Two Majors are open on the Use-Case Model, and a suspect trace remains registered at the phase close.
- Iteration: 2, Cycle 1
- Owner: Reviewer

### Management Reviewer lens
<!-- review: Excavation I2 -->

- Phase: Excavation
- Status: Draft — produced for the end-of-Excavation (AR) milestone review, iteration 2, cycle 1
- Milestone Target: end-of-Excavation (AR) — not yet achieved
- Iteration: 2, Cycle 1
- Review point: Lifecycle Milestone Review (AR re-take), exit-criteria lens
- Verdict this lens issues: No-Go

### Review Coordinator lens
<!-- review: Excavation I1 -->

<!-- review: Excavation I1 -->

- Phase: Excavation
- Status: Iteration 1 consolidated; the AR milestone verdict is recorded in Disposition
- Milestone Target: end-of-Excavation (AR) — not sanctioned on this iteration's evidence
- Iteration: 1, Cycle 1
- Owner: Review Coordinator

## Review Scope and Criteria
### Reviewer lens
<!-- review: Excavation I2 -->

<!-- review: Excavation I2 -->

#### Review scope — Excavation iteration 2, technical lens

The ten artifacts the AR review left findings against, plus the two this lens read for exit-criteria evidence. Each was re-read at the section its finding named, and each corrected fact was checked at its source code rather than taken from the finding's remedy.

| Artifact | Reviewed for | Iteration-2 outcome |
|---|---|---|
| Development Case | Document Control currency; tailoring against the IARI baseline; optional triggers | 1 Minor open |
| System Inventory | Coverage arithmetic; anomalies anchored; entry points accounted for | Clean |
| Risk List | Score reproducibility; retirement claims; the grant band | Clean — F2 closed |
| Iteration Plan | Exit-criteria evidence; risk sequencing | Clean |
| Vision | Use-case count; mechanism shapes | Clean — F1 closed |
| Use-Case Model | The recovered set; trace rows against the graph; the two entry-point readings | 2 Major open |
| Supplementary Specification | The recovered figures under AN-024 and AN-023 | Clean — F1, F2 closed |
| Software Architecture Document | The recovered figures; component trace rows | Clean — F1 closed |
| Deployment Model | Environment mapping against the files it maps | Clean — F1 closed |
| Design Model | Anomaly citations; the persistent store | Clean — F1 closed |

#### Criteria applied

This milestone's question is EXIT CRITERIA, not feasibility or completion. Eight items were tested; each is a test with a pass or fail answer, not an opinion.

| # | Criterion | What passes |
|---|---|---|
| C1 | Recovered, not declared | No element claims scope the delivery does not hold; a recovered element cites the file it was read from |
| C2 | Anchored | Every recovered element rests on the file and lines it names |
| C3 | No cross-cutting mechanism as a use case | Authentication, sync, logging, audit, health and migration are mechanisms, not actor goals |
| C4 | One goal, one use case | A multi-actor process is one use case with scenarios; not one per actor |
| C5 | Trace rows carried | Every row a trace-chain artifact declares is carried by the registered graph |
| C6 | No suspect trace open at the phase close | No edge named in a declared row carries a SUSPECT marking |
| C7 | Document Control current | Phase, Status, Milestone Target and Iteration name the phase and iteration whose review the artifact is under |
| C8 | Diagram-dominant | Formal UML carries the content; prose supplements what a diagram cannot express |

#### Evidence verified at source this iteration

The four Majors the AR review raised were all about one class of defect — a recovered fact transcribed inconsistently into the artifacts citing it. Closing them on the artifact's own text alone would have repeated the mistake that created them, so each corrected fact was opened at the code it cites.

| Fact | Artifact statements checked | Code opened | Result |
|---|---|---|---|
| Development halves the request budget | Supplementary Specification M3, S2, P1, R8, F10; SAD SP1, M3, Process View P4, Quality; Deployment Model Environment Mapping and its Rate limiting row | `Todo.Api/appsettings.Development.json` — `RateLimiting` `TokenLimit` 50, `TokensPerPeriod` 50, `QueueLimit` 50; `RateLimitExtensions.cs` — the code defaults 100, 100, queue 100 bound from a `RateLimiting` section | Reproduces. All three artifacts now state both values under AN-024 |
| Two BFF hops, unequal resilience | Supplementary Specification R4 | `TodoApp.ServiceDefaults/Extensions.cs:32-42` — `ConfigureHttpClientDefaults` with `AddStandardResilienceHandler()`; `Todo.Web/Server/TodoApi.cs` — `MapForwarder("{*path}", "http://todoapi", new ForwarderRequestConfig(), …)` with no handler | Reproduces. R4 states the two hops apart under AN-023 |
| Coverage arithmetic | System Inventory Coverage — 139 files, 84 read, 55 unread | Per-area Files column sums to 139, Read to 84, unread cells to 55; every unread category is named | Reproduces |
| The three EP-003 trace edges | Use-Case Model Traceability rows for UC-006, UC-007, UC-008 | Trace graph, EP-003 downstream | All three now report OK; the SUSPECT marking is gone |

#### SCM and build evidence

The repository reports no pull requests in any state and no IARI pipeline file, so there is no code review or CI result to weigh at this gate. That is correct for the phase rather than a defect: Excavation produces no production code, and the tree's own code is unchanged since `307a1ea` of 2026-02-12. This lens's disposition therefore rests on artifact evidence alone, and the absence of SCM evidence is stated here rather than silently omitted.

### Management Reviewer lens
<!-- review: Excavation I1 -->

Entry criteria were checked before the review: all twelve Excavation artifacts exist and are readable, the Software Architecture Document — the artifact this lens cannot proceed without — is present, and the Iteration Plan carries the AR exit criteria the milestone is judged on. No review was taken against a placeholder.

**Review point and lens.** This is the Lifecycle Milestone Review at the Architecture Recovered gate. The question is neither feasibility (Project Approval, Planning) nor completion (Iteration Acceptance): it is whether the artifacts collectively satisfy the conditions for the phase transition. The criteria are the Project Manager's A1 to A13, and each is re-decided here against the artifact it names, not against the criterion's own state cell.

**Artifacts read in full, not sampled:** Vision, Use-Case Model, Supplementary Specification, Software Architecture Document, Deployment Model, Design Model, System Inventory, Risk List, Iteration Plan, Development Case, and the findings ledger of every artifact under review. The Iteration Assessment is absent and its absence is not a finding: the Project Manager authors it after this review, so it cannot yet describe the iteration being judged.

#### The criteria, re-decided

| # | Criterion | State after this lens | What the state rests on |
|---|---|---|---|
| A1 | Operations recovered as use cases | Met | 11 use cases, each with its `EP-NNN`; the four exclusions stated and ruled by the stakeholder on 2026-11-23. Use-Case Model#F1 carries the closure of three suspect screen edges |
| A2 | Priorities 1 to 5 reached, remainder named for Consolidation | **Not met as written** | Iteration Plan#F4: the `EP-020`/`EP-021`/`EP-022`/admin rows are permanent exclusions, not work deferred to Consolidation, and priorities 6 to 8 are named nowhere |
| A3 | Architecture recovered and checked against the use cases | **Contested, not certifiable** | 22 components with `Realizes` rows for eleven use cases, and SEQ-1 to SEQ-3 walk three of them. But Software Architecture Document#F1 (Major) leaves SP1 and M3 stating a value the code contradicts |
| A4 | Data recovered with anchors | Met | Design Model PD-D1 to PD-D5: eight tables, keys, indexes, referential actions, enforced and unenforced rules, each anchored to the migrations and the snapshot |
| A5 | Deployment modelled | **Contested, not certifiable** | The fired OPTIONAL exists and states nodes, stores and the shared key ring. But Deployment Model#F1 (Major) states the one setting that differs between environments backwards |
| A6 | Coverage measured and remainder declared | Met | System Inventory Coverage: 84 opened, 55 unread of 139; the per-area Read column sums to 84 and the Files column to 139, and all 55 unread are named by category |
| A7 | Every anomaly carried as a scored risk | Met | 29 `Refines` edges from `AN-NNN`; `R022` and `R031` state their separate origins; every anomaly-derived row reproduces from the one published word-to-score mapping |
| A8 | No grant-band accept without the stakeholder | Met | Four accepts at 4 × 3 = 12, each holding the stakeholder's verbatim answer of 2026-11-23; the sixteen other Significant-band risks avoid, which the Project Manager may do at any band |
| A9 | Every risk actionable | Met | 31 rows carrying strategy, action, owner, contingency and warning sign |
| A10 | The recovery states what the code does | **Not met as written** | Iteration Plan#F3: certified on the System Inventory identifying a contradiction while three artifacts still state the contradicted value as fact |
| A11 | The four SBC Minors closed | **Not met — three of four** | `Iteration Plan#F2`, `Iteration Plan#F3` and `System Inventory#F3` are corrected in their artifacts and verified closed. `Development Case#F2` stands: "Roles and Ownership" still reads "Reviewer, CodeReviewer, plus the Configuration Manager's baseline record", and CLS-DC-01 draws no edge into the Review Record from the Management Reviewer, the Business Reviewer or the Review Coordinator. Carried as `R031` |
| A12 | The recovered set confirmed by the stakeholder | **Not met — refused** | Asked at this review, the stakeholder answered "No" and ordered that all major findings be corrected |
| A13 | The plan names no work the process does not run | Met | Items 1 to 12 and 14 are Excavation stages or the stakeholder's own order; the Process Engineer's single item is recorded as that order and not as a discipline stage |

**The one criterion this lens adds.** A milestone gate is also the place a Conditional verdict from a prior gate is verified as resolved. The SBC re-take issued Go with one open Minor — `Development Case#F2` — and the stakeholder ordered it closed in this phase. It is not closed, and it is the only reason a criterion the phase's own plan counts cannot be certified. That is not a surprise the review should absorb silently; it is the exposure `R031` predicted, and it has materialized.

#### Risk retirement, as the review reads it

A review that only counts open findings misses the question the register exists to answer: are the high-magnitude exposures moving? At this gate, five of the twenty Significant-band risks were due to be retired in this iteration by an action an Excavation role performs.

| Risk | Exposure | Action due in this iteration | What the artifacts show |
|---|---|---|---|
| R002 | 4 × 3 = 12 | Software Architect records that the BFF-to-API hop carries no service authentication | Performed — ADR-003 and the Process View record it, anchored to the code's own `TODO` |
| R009 | 3 × 3 = 9 | Software Architect records the limiter's coverage and the partition-key gap | Performed — M3 and ADR-007 state `/todos` only, and why the policy cannot move as written |
| R019, R020, R021 | 4 × 2 = 8; 4 × 3 = 12; 4 × 3 = 12 | System Analyst records the challenge's unchecked scheme, the callback's single exit, and the one 401 | Performed — UC-003 A1 and A2, and UC-001 A1 / UC-002 A1, each anchored |
| R023 | 4 × 3 = 12 | System Analyst records that lockout is checked at sign-in alone | Performed — UC-002 step 5 and the shared gate diagram |
| R024 | 3 × 3 = 9 | (Software Architect) record that the two hops differ | Performed in SAD P6, but Supplementary Specification#F2 shows the artifact that carries the false half is still uncorrected |
| **R030** | **4 × 3 = 12** | **System Analyst records the session surface's instability beside those flows** | **Not performed — and the register records the risk as avoided.** Risk List Management Reviewer#F2 |

Ten of the twenty Significant-band risks are retired on evidence in an artifact. R030 is the one recorded as retired by an action that is not in any artifact, and it is the largest band present. Its own warning sign — "a design cites the session surface as settled" — is precisely what Consolidation will do with a Use-Case Model that presents UC-001 to UC-004 without that caveat.

#### What this review does not claim

The Development Case's optional-trigger table is audited rather than accepted. Deployment Model FIRED on a genuinely distributed topology: a browser-hosted WebAssembly client, a server host, a separate API process, a SQLite store and a reverse-proxy hop, with per-project settings pairs. That condition holds. The five NOT FIRED verdicts each hold against the project's real facts: eight persisted entity types sit below the >10 Data Model threshold, no untried mechanism needs empirical validation, the UI is recovered rather than designed, and no regulator or contract consumes test reporting. No trigger is over-fired and none is unjustified.

### Review Coordinator lens
<!-- review: Excavation I1 -->

<!-- review: Excavation I1 -->

**Lens participation at this milestone — authoritative, not inferred from the artifact.** Excavation's milestone review runs Reviewer, Management Reviewer, Review Coordinator. The Business Reviewer's first stage is LCO, so at AR it is not a scheduled participant.

| Lens | Participation | What it evaluated | Bearing on the verdict |
|---|---|---|---|
| Reviewer (technical) | EXECUTED | Ten findings over nine artifacts — 6 Major, 4 Minor — each against an anchor in the code | Counted in full |
| Management Reviewer | EXECUTED | The thirteen AR criteria, the grant band, and the two Majors of its own; 2 Major and 4 Minor recorded | Counted in full |
| Business Reviewer | **INACTIVE — did not evaluate this review** | Nothing | No verdict is attributed to it, and none is inferred from its absence |
| Review Coordinator | Consolidating this milestone | The consolidated ledger, the cross-lens reconciliation, the verdict | Records the verdict in Disposition |

**Review events of this milestone, each triggered by a workflow activity.** The calendar is the sprint zero's full sequence; the two Excavation events are this milestone's.

```plantuml
@startuml
title Review calendar - every review event of the sprint zero, each triggered by a workflow activity, none on a calendar date

skinparam shadowing false
skinparam wrapWidth 240

|Review events|
start
:Project Approval Review and Project Planning Review
held inside the SBC milestone, never as separate events;
:Iteration Plan Review - Survey iteration 1;
:Iteration Evaluation Criteria Review - Survey iteration 1;
:Milestone Review SBC iteration 1 - No-Go
5 Major open, the stakeholder refused the perimeter;
:Iteration Plan Review - Survey iteration 2;
:Iteration Evaluation Criteria Review - Survey iteration 2;
:Milestone Review SBC iteration 2 - Go
0 Major, 1 Minor, the perimeter sanctioned;

|Excavation iteration 1|
:Iteration Plan Review - A1 to A13 read on the plan;
:Iteration Evaluation Criteria Review - technical lens
10 findings, 6 Major and 4 Minor, over 9 artifacts;
:Milestone Review AR - management lens
6 findings read at this gate, 2 Major and 4 Minor;
note right
  Business Reviewer INACTIVE - did not evaluate
  this review. Excavation runs Reviewer,
  Management Reviewer, Review Coordinator.
end note

|The gate and the verdict|
:Gate H4 put to the stakeholder
the 11 use cases, 22 components, 8 tables, 4 exclusions;
:Gate H4 answered No
order given - correct all major findings;
:AR verdict on the consolidated ledger
16 open - 0 Critical, 8 Major, 8 Minor;
:milestone NOT sanctioned
requiresIteration true;
stop

@enduml
```

**Entry and exit criteria actually enforced at this milestone.**

| Event | Entry criterion | Exit criterion | Held |
|---|---|---|---|
| Iteration Plan Review | The plan carries this iteration's work items with owners and its exit criteria read on the artifact each cites | Every criterion decided on its own artifact's evidence | Yes — the plan was re-read and the two Minors it carried closed; the Management Reviewer then found A10 certified on an adjacent artifact |
| Iteration Evaluation Criteria Review | The recovered artifacts are in their target state and the anchors exist to be checked | Every criterion decided on evidence the cited section carries | Yes — the technical lens read the code behind each Major |
| Milestone Review AR | Both executed lenses have returned and the stakeholder's gate answer is on the record | 0 Critical, 0 Major open; the stakeholder's sanction GRANTED | **No** — 8 Major open and the sanction REFUSED |

**The review process for a finding at this milestone** — the state each of the 16 open findings is in, and who owns the act that closes it.

```plantuml
@startuml
title Finding lifecycle at this milestone - the 16 open findings, their states, and the act that closes each

skinparam shadowing false
skinparam wrapWidth 240

[*] --> Open : a lens records it via record_artifact_finding
Open --> Assigned : owner named in the lens Remediation
Assigned --> InProgress : owner reworks the artifact
InProgress --> Resolved : the corrective action is in the artifact
Resolved --> Verified : the SAME lens re-reads the section
Verified --> Closed : resolve_artifact_finding accepted
Resolved --> Open : the lens finds the defect still stands

state "Escalated" as ESC
Open --> ESC : deadline missed by more than 1 business day
Assigned --> ESC : no owner action, or no stage in the phase
ESC --> Assigned : Project Manager re-assigns, or the phase plans a slot

state "Carried into Excavation iteration 2" as CARRY
Open --> CARRY : Major - reworked before any role consumes it
Assigned --> CARRY : Minor - owner's next turn, after the Majors

note right of CARRY
  All 16. Eight Major hold the milestone; eight Minor
  are ordered corrected by the stakeholder on 2026-11-23.
end note
note bottom of ESC
  Development Case F2 is already here - its owner, the
  Process Engineer, has no stage in Excavation, which is
  what R031 predicts and materializes.
end note

@enduml
```

A finding closes only when the lens that recorded it re-reads the corrected section and calls `resolve_artifact_finding`. A correction an owner states in prose does not close it; a coordinator's consolidation does not close it.

## Findings
### Reviewer lens
<!-- review: Excavation I2 -->

<!-- review: Excavation I2 -->

#### Compliance matrix

Each artifact against the eight items of this milestone's checklist. An item is marked Pass only where the artifact carries the evidence itself; N/A marks an item the artifact's shape does not engage.

```plantuml
@startuml
title Compliance: the recovered set against the Excavation checklist - 10 artifacts, 8 checklist items

skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam wrapWidth 210
hide circle
hide empty members

package "Checklist items tested" {
  class "C1 Recovered, not declared\nno undeclared-scope element" as C1 <<check>>
  class "C2 Every element anchored\nto the file it was read from" as C2 <<check>>
  class "C3 No cross-cutting mechanism\ncarried as a use case" as C3 <<check>>
  class "C4 One goal, one use case\nnot one per actor" as C4 <<check>>
  class "C5 Declared trace rows\ncarried by the trace tree" as C5 <<check>>
  class "C6 No suspect trace open\nat the phase close" as C6 <<check>>
  class "C7 Document Control on\nthis phase and iteration" as C7 <<check>>
  class "C8 Diagram-dominant\nformal UML content" as C8 <<check>>
}

package "Artifacts reviewed" {
  class "Development Case\nF3 open" as A_DC <<minor>>
  class "System Inventory\nclean" as A_SI <<pass>>
  class "Risk List\nclean" as A_RL <<pass>>
  class "Iteration Plan\nclean" as A_IP <<pass>>
  class "Vision\nclean" as A_VIS <<pass>>
  class "Use-Case Model\nF3, F4 open" as A_UCM <<major>>
  class "Supplementary Specification\nclean" as A_SS <<pass>>
  class "Software Architecture Document\nclean" as A_SAD <<pass>>
  class "Deployment Model\nclean" as A_DM <<pass>>
  class "Design Model\nclean" as A_DES <<pass>>
}

C1 --> A_UCM : partial
C1 --> A_VIS : pass
C2 --> A_SI : pass
C2 --> A_SAD : pass
C3 --> A_UCM : pass
C3 --> A_VIS : pass
C4 --> A_UCM : pass
C5 --> A_UCM : pass
C5 --> A_DES : pass
C5 --> A_SAD : pass
C6 --> A_UCM : FAIL
C7 --> A_DC : FAIL
C8 --> A_SI : pass
C8 --> A_SAD : pass
C8 --> A_DES : pass

note right of A_UCM
  C6 fails: five COMP-014 edges are
  marked SUSPECT and no closure is
  recorded. C1 partial: the rules
  diagram states one request budget
  where the recovered fact is two.
end note
note bottom of A_DC
  C7 fails on the four Document Control
  fields, carried from iteration 1 under F3.
  The tailoring content itself is current.
end note

@enduml
```

| Artifact | C1 | C2 | C3 | C4 | C5 | C6 | C7 | C8 |
|---|---|---|---|---|---|---|---|---|
| Development Case | N/A | Pass | Pass | N/A | N/A | N/A | **Fail** | Pass |
| System Inventory | Pass | Pass | Pass | N/A | N/A | Pass | Pass | Pass |
| Risk List | Pass | Pass | N/A | N/A | Pass | Pass | Pass | Pass |
| Iteration Plan | N/A | Pass | N/A | N/A | N/A | N/A | Pass | Pass |
| Vision | Pass | Pass | Pass | Pass | N/A | N/A | Pass | Pass |
| Use-Case Model | **Partial** | Pass | Pass | Pass | Pass | **Fail** | Pass | Pass |
| Supplementary Specification | Pass | Pass | Pass | Pass | N/A | N/A | Pass | Pass |
| Software Architecture Document | Pass | Pass | N/A | Pass | Pass | Pass | Pass | Pass |
| Deployment Model | Pass | Pass | N/A | N/A | N/A | N/A | Pass | Pass |
| Design Model | Pass | Pass | N/A | N/A | Pass | Pass | Pass | Pass |

#### Defect distribution

```plantuml
@startuml
title Defect distribution: findings open at the AR review, by severity and artifact

skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam wrapWidth 220
hide circle
hide empty members

package "Critical - 0" {
  class "none\nno stakeholder decision\nis outstanding" as NOCRIT <<none>>
}

package "Major - 2" {
  class "Use-Case Model#F3\ntrace-gap\nfive COMP-014 edges SUSPECT" as M1 <<major>>
  class "Use-Case Model#F4\nconsumed-defect\none budget stated where two are in force" as M2 <<major>>
}

package "Minor - 1" {
  class "Development Case#F3\ncontained-defect\nDocument Control a phase behind" as M3 <<minor>>
}

package "Closed this iteration - 9" {
  class "Vision#F1\nuse-case-shape" as C1 <<closed>>
  class "Use-Case Model#F1\ntrace-gap" as C2 <<closed>>
  class "Use-Case Model#F2\ncontained-defect" as C3 <<closed>>
  class "Supplementary Specification#F1\nconsumed-defect" as C4 <<closed>>
  class "Supplementary Specification#F2\nconsumed-defect" as C5 <<closed>>
  class "Software Architecture Document#F1\nconsumed-defect" as C6 <<closed>>
  class "Deployment Model#F1\nconsumed-defect" as C7 <<closed>>
  class "Design Model#F1\ncontained-defect" as C8 <<closed>>
  class "Risk List#F2\ncontained-defect" as C9 <<closed>>
}

M1 --> C2 : the same class of defect\nrecurring on another edge
M2 --> C4 : the same fact, in the one\nartifact the AR Majors missed

note bottom of M1
  Both open Majors are the two failure modes the
  nine closures removed, found elsewhere in the set:
  a recovered fact transcribed inconsistently, and
  a trace edge never confirmed. Neither is new work.
end note
note bottom of C9
  Eight of the nine were the AR review's own ledger.
  The ninth, Vision#F1, was the use-case-shape defect
  the same review recorded.
end note

@enduml
```

#### Use-Case Model — the two open Majors

##### Use-Case Model#F3 — five COMP-014 edges are suspect at the phase close (Major, trace-gap)

The registered graph marks `COMP-014 → UC-006`, `UC-007`, `UC-008`, `UC-009` and `UC-010` each «SUSPECT → System Analyst». The System Analyst is the role named, and the Use-Case Model is that role's artifact. The edges are substantively right: `Todo.Api/Todos/TodoApi.cs:19-20` applies `RequirePerUserRateLimit()` to the whole `/todos` group, and the artifact's own shared gate diagram already states the step — "The per-user token bucket applies to the whole group". What is missing is the confirmation that clears the marking, and a phase that closes with it open certifies a Use-Case View whose widest mechanism is unconfirmed for every task use case.

**Remediation.** Re-register the five edges as confirmed, having checked each against the artifact and the code. If the marking was raised because a throttling mechanism is not the operation itself, record that reading beside the gate diagram's step — the bucket gates the operation, it does not perform it — as was done for the EP-003 screen edges. The Use-Case Survey's "Why a screen entry point and the forwarded operation are both named" is the pattern to follow.

##### Use-Case Model#F4 — the rules diagram states one request budget where two are in force (Major, consumed-defect)

The rules diagram's R6 reads "The per-user token bucket, /todos only: 100 tokens, 100 per 10 s, queue 100, 429" and cites no anomaly. `Todo.Api/appsettings.Development.json` binds all three to 50 and both launch profiles select Development, so 50 is the budget in force wherever this delivery runs (AN-024). The same artifact states it correctly in the gate diagram note a few sections later, so the model now carries two answers to one question. The four rules diagrams are what a Designer or a Test Designer reads to know what the flows enforce.

**Remediation.** State the two values in force in R6 — the code defaults 100 / 100 per 10 s / queue 100 from `RateLimitExtensions.cs`, and the Development override 50 / 50 / 50 from `appsettings.Development.json` which is what the delivery enforces — and add the AN-024 citation the other rules carry. Where the diagram needs one number, give 50 as the value in force.

#### Closed this iteration

Nine findings of this lens were closed on evidence, each verified at the section named and, for the four Majors about recovered facts, at the code itself.

| Finding | Criterion | What closed it |
|---|---|---|
| Vision#F1 | use-case-shape | U12 and U13 are gone; the two mechanisms are `component` shapes under "Platform mechanisms - no actor goal, not use cases", cross-referenced to M8 and M9. The Vision states eleven use cases, as the Use-Case Model does |
| Use-Case Model#F1 | trace-gap | The three EP-003 edges report OK in the graph, and the artifact states the screen-entry reading beside the rows |
| Use-Case Model#F2 | contained-defect | The Actors section states the rule separating the two entry-point lists, and the matrix edges are labelled with what the actor acts on |
| Supplementary Specification#F1 | consumed-defect | M3, S2, P1, R8 and F10 state both budgets under AN-024 and cite `appsettings.Development.json:8-12` |
| Supplementary Specification#F2 | consumed-defect | R4 states the two hops apart under AN-023, with the three anchors the finding asked for |
| Software Architecture Document#F1 | consumed-defect | SP1, M3, Process View P4 and the Quality row state 50 as the bound in force under AN-024; the code default is named as the value no profile selects |
| Deployment Model#F1 | consumed-defect | The preamble is narrowed to what the files hold, and the Rate limiting row reads 50 / 50 / 50 for Development against the code defaults elsewhere |
| Design Model#F1 | contained-defect | PD-D3 cites AN-025 for the unconverted owner key; AN-005 is cited only for `EnsureCreated`. A paragraph at the head of the classes section states the two subjects apart |
| Risk List#F2 | contained-defect | R024 no longer attributes to the Design Model a state it does not hold; the mitigation now aims at the Supplementary Specification's R4, which was the artifact carrying the error |

#### Development Case — the Minor that persists

##### Development Case#F3 — Document Control is a phase behind (Minor, contained-defect)

Document Control still reads "Phase: Survey", "Status: Draft — produced for the end-of-Survey (SBC) milestone review", "Milestone Target: end-of-Survey (SBC) — not yet achieved", "Iteration: 2, Cycle 1". Every other artifact under this review reads Phase: Excavation, Iteration 2. The Development Case is the CORE artifact this milestone's tailoring depends on. It is contained: the tailoring content is current — both classification verdicts and all six optional triggers were re-evaluated against the recovery, and the Deployment Model's fired trigger still holds — and no criterion depends on the metadata. It is carried in second place behind the two Majors, as an un-ordered Minor.

**Remediation.** Bring the four Document Control fields forward to Excavation, iteration 2, status Draft for the AR review. No other content changes.

#### Artifacts with no finding

System Inventory, Risk List, Iteration Plan, Supplementary Specification, Software Architecture Document, Deployment Model and Design Model carry no open finding from this lens. Each was re-read at the sections this lens previously found defective and each now holds. Silence from this lens is the approval.

The System Inventory's coverage arithmetic was recomputed rather than accepted: the per-area Files column sums to 139, the Read column to 84, the unread cells to 55, and the headline figure reproduces. Every unread area is named with the reason it was not read and none carries a perimeter fact. The Risk List's 32 rows each name a strategy, an owner, an action, a contingency and a warning sign, and its own R030 states "not yet retired" rather than claiming an avoidance that has not happened — which is the honest form the register lacked in iteration 1.

### Management Reviewer lens
<!-- review: Excavation I1 -->

Four findings are this lens's own at this gate, and each is recorded through `record_artifact_finding` before this report was written. The Majors of other lenses are cited here because the milestone verdict reads them; they are not re-recorded as duplicates.

#### The criteria as this lens certifies them

```plantuml
@startuml
title AR-C1 Exit-criteria compliance - the thirteen AR criteria of Excavation iteration 1, the state each is certified in, and what the state rests on

skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam wrapWidth 250
hide empty members
hide circle

package "Met on the artifact that owns the evidence - 7" {
  class "A1 Operations recovered as use cases\n11 UCs, each with its EP-NNN, 4 exclusions stated" as A1 <<met>>
  class "A4 Data recovered with anchors\n8 tables, keys, rules, PD-D1 to PD-D5" as A4 <<met>>
  class "A6 Coverage measured and reproducible\n84 opened, 55 unread of 139, per-area sums" as A6 <<met>>
  class "A7 Every anomaly carried as a risk\n29 Refines edges, R022 and R031 origins stated" as A7 <<met>>
  class "A8 No grant-band accept without the stakeholder\n4 grants at exposure 12, 16 avoid" as A8 <<met>>
  class "A9 Every risk actionable\n31 rows: strategy, action, owner, contingency, sign" as A9 <<met>>
  class "A13 No work the process does not run\nitems 1 to 12 and 14 are Excavation stages" as A13 <<met>>
}

package "Recorded Met, not establishable as written - 2" {
  class "A2 remainder named for Consolidation\nthe named rows are permanent exclusions" as A2 <<notmet>>
  class "A10 recovery states what the code does\n3 artifacts still state the contradicted value" as A10 <<notmet>>
}

package "Not met - 2" {
  class "A11 The four SBC Minors closed\n3 of 4: Development Case#F2 stands" as A11 <<notmet>>
  class "A12 The recovered set confirmed\nGate H4 answered No" as A12 <<refused>>
}

package "Exists but not certifiable while its Major stands - 2" {
  class "A3 Architecture recovered and checked\n22 components, Use-Case View, SEQ-1 to 3" as A3 <<contested>>
  class "A5 Deployment modelled\nfired OPTIONAL, nodes, stores, key ring" as A5 <<contested>>
}

class "Software Architecture Document#F1\nSP1 and M3 state the budget as 100\nwhere Development overrides it to 50" as D3 <<open major>>
class "Deployment Model#F1\nthe one setting that differs between\nenvironments is stated backwards" as D5 <<open major>>

A3 ..> D3 : the artifact exists, but its own\nMajor holds the certification
A5 ..> D5 : the artifact exists, but its own\nMajor holds the certification

note bottom of A11
  Its owner, the Process Engineer, has no stage in
  Excavation: Environment runs at no intensity here.
  R031 carries the exposure; the criterion is not
  waived and no row of the plan is marked complete on it.
end note

note bottom of A12
  Certified by the stakeholder's answer alone. No artifact
  can hold it and no evidence cell can cite it, which is
  why the verdict reads the answer.
end note

note bottom of A2
  Contained: the recoverable operations all sit in
  priorities 1 to 5 and areas 6 to 8 are infrastructure
  that will never carry a use case. A criterion may still
  not be certified on a clause its evidence does not carry.
end note

@enduml
```

#### Risk List

`Risk List Management Reviewer#F2` — **Major**, criterion `exit-criterion-unmet`. **R030 is the one Significant-band risk whose retirement action was due in this iteration, and the action was not performed — while the register records the risk as avoided, which asserts that it was.** The Use-Case Model carries no statement of the session surface's instability beside UC-001 to UC-004; the Iteration Plan's own risk-sequencing diagram assigns `R030` to the Use-Case Model stretch, so the plan and the artifact disagree about whether the work landed. Avoidance is a claim of retirement, not a status note. Recommended: the System Analyst writes the statement beside those flows citing `AN-029`, or the register restates `R030` as not yet retired.

#### Iteration Plan

`Iteration Plan Management Reviewer#F3` — **Major**, criterion `exit-criterion-unmet`. **A10 is certified Met on the System Inventory identifying a contradiction, while three artifacts the criterion governs state the contradicted value as fact.** A10's own test is about the recovered set, not about the inventory's anomalies table: the Supplementary Specification, the Software Architecture Document and the Deployment Model each state that no `RateLimiting` section exists and that 100/100/100 are the effective values, against `appsettings.Development.json:8-12`. Recommended: hold A10 open until those three are corrected, or split the criterion so the gate can see the difference.

`Iteration Plan Management Reviewer#F4` — **Minor**, criterion `contained-defect`. A2's evidence cell certifies a clause the artifact it cites does not carry: "Not recovered, and why" names permanent exclusions, not work deferred to Consolidation, and priorities 6 to 8 carry no statement. Contained — no role builds on the missing sentence and areas 6 to 8 will never carry a use case.

`Iteration Plan Management Reviewer#F5` — **Minor**, criterion `contained-defect`. A12 still reads "Not yet asked — the gate follows this review", a state the stakeholder's answer has superseded. Contained — the true state is in this record's Disposition, and nothing another role builds turns on the plan's cell.

#### Vision

`Vision Management Reviewer#F1` — **Minor from this lens**, criterion `contained-defect`. The "Features" diagram draws two shapes as `usecase` ellipses that the Use-Case Model rules out of the use-case set: `U12` "Start the system and create its schema (`EP-022`)" and `U13` "Observe readiness and liveness (`EP-020`, `EP-021`)", under a heading that calls the diagram the goals of the one human actor.

This lens classifies it Minor because the Use-Case Model is authoritative for the set, states each exclusion with its reason, and A1 is satisfied on that artifact alone — no exit criterion depends on the Vision's count. **The technical lens records the same defect as `Vision#F1` Major**, on the ground that three artifacts will state the count and one states thirteen. The two classifications differ on consequence, not on fact, and the gate reads the higher of the two: the Vision's use-case count is a Major exposure at this milestone and is counted as one below.

#### Development Case

`Development Case Management Reviewer#F2` — **Minor**, recorded at the SBC re-take and still open, criterion `contained-defect`. The contributor set stated for the Review Record omits the Management Reviewer, the Business Reviewer and the Review Coordinator, and CLS-DC-01 draws no edge from them into it, although all three write their own block. Verified again at this gate. **This is the finding that holds A11 and therefore the phase.** The stakeholder ordered on 2026-11-23 that Minors be addressed in the next phase rather than left unattended; the order has not been executed because Environment runs at no intensity in Excavation and its owner has no scheduled slot. `R031` predicted exactly this and has materialized.

`Development Case Reviewer#F3` — **Minor**, also open: Document Control still records "Phase: Survey … Iteration: 2, Cycle 1" while the document governs an Excavation phase. Contained, and corrected by the same owner in the same turn as `#F2`.

#### The Majors of other lenses, which this verdict reads

```plantuml
@startuml
title AR-C2 Findings ledger at the AR gate - the eight open Majors, and the one anomaly three of them share

skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam wrapWidth 245
hide empty members
hide circle

package "The AN-024 cluster - one anomaly, three artifacts, three Majors" {
  class "Supplementary Specification#F1  Major\nM3, S2, P1, S4 state 100/100/100\nand 'no RateLimiting section exists'" as SS1 <<major>>
  class "Software Architecture Document#F1  Major\nSP1 and M3 state the same, and\ncite no AN-024 anywhere" as SAD1 <<major>>
  class "Deployment Model#F1  Major\n'No environment file carries a rate-limit\nvalue' - the one setting that differs" as DPM1 <<major>>
}

package "Independent Majors - 5" {
  class "Supplementary Specification#F2  Major\nR4: 'no retry ... on either hop'\nthe token hop inherits the handler" as SS2 <<major>>
  class "Use-Case Model#F1  Major\n3 suspect edges open at the phase close\nEP-003 to UC-006, UC-007, UC-008" as UCM1 <<major>>
  class "Vision#F1  Major (technical lens)\n13 use-case ellipses where the model\nrecovers 11, the extra two being exclusions" as VIS1 <<major>>
  class "Risk List Management#F2  Major\nR030 avoided, action in no artifact" as RL1 <<major>>
  class "Iteration Plan Management#F3  Major\nA10 met on the inventory's word,\nnot on the recovered set" as IP1 <<major>>
}

package "Minor - recorded, does not hold the milestone" {
  class "Use-Case Model#F2\nmatrix and survey name different entry points" as M1 <<minor>>
  class "Risk List#F2\nR024's premise names the wrong artifact" as M2 <<minor>>
  class "Iteration Plan Management#F4, #F5\nA2's unsupported clause; A12 superseded" as M3 <<minor>>
  class "Vision Management#F1\nthe same two ellipses, contained reading" as M5 <<minor>>
  class "Development Case#F2 and Reviewer#F3\ncontributor set; Survey-era Document Control" as M4 <<minor>>
}

class "AN-024\nThe Development configuration halves\nthe request budget: 50 against 100" as AN <<anomaly>>

AN --> SS1 : contradicted
AN --> SAD1 : contradicted
AN --> DPM1 : contradicted

note bottom of AN
  The System Inventory records the fact and R025 carries
  it. Three artifacts state the opposite as the system's
  behaviour, which is why one correction closes three
  Majors and why A10 cannot be certified over them.
end note

note bottom of RL1
  Its warning sign has already come true: a recovered
  model presents the session flows without the caveat
  the risk exists to attach to them.
end note

note bottom of UCM1
  The edges are substantively right; what is open is the
  confirmation that clears the suspect marking before the
  eleven-use-case count goes to the stakeholder.
end note

note bottom of VIS1
  Counted at the higher of two lenses' classifications.
  The Use-Case Model governs the set; the Vision must not
  state a different number beside it.
end note

@enduml
```

**Eight Majors, no Critical** — six from the technical lens and two from this one. None of the eight needs a stakeholder decision: each is a correction its owner can make inside this iteration, and none is a disagreement about what the system does. The facts are recovered and anchored everywhere; three artifacts simply still assert the value the reading contradicts, and one still counts a set differently from the artifact that owns it. No Critical finding exists because no ambiguity and no contradiction in what the stakeholder declared remains open.

### Review Coordinator lens
<!-- review: Excavation I1 -->

<!-- review: Excavation I1 -->

**Consolidated finding ledger.** Twenty-nine findings were recorded against ten artifacts by the two executed lenses at this milestone. Thirteen carry a resolution object and were closed by their recording lens; sixteen are open — none Critical, eight Major, eight Minor. Every count below is copied from `read_artifact_findings` on the artifact named, never from a reviewer's narrative.

The ledger line this section rests on, verbatim:

`[FINDINGS] read=12, unread=none, open Critical=0, open Major=8, open Minor=8`

**Open — the eight Majors. Each holds the milestone; none needs a stakeholder decision.**

| Artifact | Key | Lens | Severity | Criterion | Owner | The corrective action | Holds |
|---|---|---|---|---|---|---|---|
| Supplementary Specification | F1 | Reviewer | Major | `consumed-defect` | System Analyst | State both rate-limit values with sources in M3, S2, P1 and R8 — code defaults 100/100/queue 100 (`RateLimitExtensions.cs:14-31`), Development override 50/50/50 (`appsettings.Development.json:8-12`); cite AN-024 | Yes |
| Supplementary Specification | F2 | Reviewer | Major | `consumed-defect` | System Analyst | Rewrite R4 as the two hops stated apart: the token hop inherits `AddStandardResilienceHandler` (`TodoApp.ServiceDefaults/Extensions.cs:32-42`, `Todo.Web/Server/Program.cs:23-26`), the forwarder hop inherits nothing; cite AN-023 / R024 | Yes |
| Software Architecture Document | F1 | Reviewer | Major | `consumed-defect` | Software Architect | Correct SP1, M3 and the Quality view's "bounded load" row; cite AN-024 | Yes |
| Deployment Model | F1 | Reviewer | Major | `consumed-defect` | Software Architect | Narrow the environment preamble to what is true; rewrite the Rate limiting row — Development 50/50/50, any other environment the code defaults | Yes |
| Use-Case Model | F1 | Reviewer | Major | `trace-gap` | System Analyst | Re-register the three EP-003 edges as confirmed and record in the Use-Case Survey why a screen entry point and the forwarded operation are both named | Yes |
| Vision | F1 | Reviewer | Major | `use-case-shape` | System Analyst | Remove U12 and U13 from the Features diagram; keep the two rows as platform mechanisms cross-referenced to Supplementary Specification M8 and M9 | Yes |
| Risk List | F2 | Management Reviewer | Major | `exit-criterion-unmet` | System Analyst, then Project Manager | Write R030's statement beside UC-001 to UC-004 citing AN-029, or restate R030 as not yet retired rather than avoided | Yes |
| Iteration Plan | F3 | Management Reviewer | Major | `exit-criterion-unmet` | Project Manager | Hold A10 open naming the three artifacts that state AN-024's contradicted value, or split the criterion; do not certify it on the inventory's word | Yes |

**Open — the eight Minors. Recorded, assigned, and not holding the milestone.** The stakeholder ordered on 2026-11-23 that no Minor be left unattended; all eight are owned and none is recorded as closed or deferred.

| Artifact | Key | Lens | Criterion | Owner | The corrective action |
|---|---|---|---|---|---|
| Use-Case Model | F2 | Reviewer | `contained-defect` | System Analyst | State the matrix-versus-Survey distinction once and relabel the matrix's edges |
| Vision | F1 | Management Reviewer | `contained-defect` | System Analyst | The same two ellipses, read as contained because the Use-Case Model governs the set |
| Risk List | F2 | Reviewer | `contained-defect` | Project Manager | Restate R024 without the misattribution; point its mitigation at the Supplementary Specification's R4, which still carries the error |
| Design Model | F1 | Reviewer | `contained-defect` | Designer | Change PD-D3's citation from AN-005 to AN-025 |
| Development Case | F2 | Management Reviewer | `contained-defect` | Process Engineer | Name every lens in the Review Record's contributor set and draw the edges in CLS-DC-01. **This is the finding that holds A11** |
| Development Case | F3 | Reviewer | `contained-defect` | Process Engineer | Bring the four Document Control fields to Excavation iteration 1 |
| Iteration Plan | F4 | Management Reviewer | `contained-defect` | Project Manager | Narrow A2 to what its evidence carries, or add the deferred-set sentence to the Use-Case Model's "Not recovered, and why" |
| Iteration Plan | F5 | Management Reviewer | `contained-defect` | Project Manager | Set A12 to "Not met — refused" with the answer as given |

```plantuml
@startuml
title Open findings at the AR gate - 16 open over 10 artifacts, 0 Critical, 8 Major, 8 Minor

skinparam shadowing false
skinparam classAttributeIconSize 0
hide empty members
hide circle
skinparam wrapWidth 250

package "Artifacts carrying an open Major - 7" {
  class "Supplementary Specification" as SS {
    Major F1 : rate limit 100 where Development reads 50
    Major F2 : R4 denies the resilience handler
  }
  class "Software Architecture Document" as SAD {
    Major F1 : the same figure, AN-024 uncited
  }
  class "Deployment Model" as DEP {
    Major F1 : the one setting that differs, backwards
  }
  class "Use-Case Model" as UCM {
    Major F1 : three EP-003 edges suspect
    Minor F2 : matrix against Survey column
  }
  class "Vision" as VIS {
    Major F1 : thirteen ellipses against eleven
    Minor F1 : the same two, contained reading
  }
  class "Risk List" as RL {
    Major F2 : R030 avoided, action unperformed
    Minor F2 : R024 premise misattributed
  }
  class "Iteration Plan" as IP {
    Major F3 : A10 met on an adjacent artifact
    Minor F4 : A2 clause unsupported
    Minor F5 : A12 superseded by the answer
  }
}

package "Artifacts carrying a Minor only - 3" {
  class "Design Model" as DM {
    Minor F1 : PD-D3 cites AN-005 for AN-025
  }
  class "Development Case" as DC {
    Minor F2 : contributor set - holds A11
    Minor F3 : Survey-era Document Control
  }
  class "System Inventory" as SI {
    none : F1 to F3 closed
  }
}

class "AN-024" as AN {
  the Development override
  halves the request budget
}
AN --> SS : contradicted
AN --> SAD : contradicted
AN --> DEP : contradicted

note bottom of AN
  One anomaly, three Majors. Correcting it in three
  artifacts closes three of the eight and moves A10.
end note
note bottom of DC
  F2 is the only finding that holds an exit criterion.
  A11 counts it and its owner has no stage in Excavation.
end note
note bottom of SI
  Zero open findings. Coverage, the anomaly count
  and Document Control all reproduce.
end note

@enduml
```

**Closed this milestone — thirteen, each by the lens that recorded it.**

| Artifact | Key | Lens | Severity | Closed against |
|---|---|---|---|---|
| Development Case | F1 | Reviewer | Major | "Tool and configuration references" — no version policy asserted |
| Development Case | F2 | Reviewer | Minor | "Roles and Ownership" — one CLS-DC-01 diagram, one role-deltas block |
| Development Case | F1 | Management Reviewer | Minor | The same section, under the stakeholder's order of 2026-11-23 |
| System Inventory | F1 | Reviewer | Major | "Traceability" — the AN-021 row reads all three entry points |
| System Inventory | F2 | Reviewer | Minor | "Coverage" — the headline recomputes from the per-area table |
| System Inventory | F3 | Reviewer | Minor | "Document Control" — Excavation iteration 1 |
| Risk List | F1 | Reviewer | Major | "Risk Classification" — one published word-to-score mapping; every row reproduces |
| Risk List | F1 | Management Reviewer | Major | The grant band re-derived; four grants at exposure 12 |
| Iteration Plan | F1 | Reviewer | Major | "Use Cases and Scenarios Addressed" — twelve anomalies, 21 edges |
| Iteration Plan | F2 | Reviewer | Minor | The coarse roadmap and the critical chain — the gate precedes the verdict |
| Iteration Plan | F1 | Management Reviewer | Major | "Evaluation Criteria" — C2a/C2b, C6, C7a/C7b |
| Iteration Plan | F3 | Reviewer | Minor | The fine plan's State column, each row against its artifact |
| Iteration Plan | F2 | Management Reviewer | Minor | The superseded C2b row no longer exists; A1 to A13 replace it |

**Cross-lens reconciliation — no contradiction, one severity disagreement, one duplicate subject.**

| Subject | The two lenses | Resolution this verdict records |
|---|---|---|
| The rate limiter (AN-024) | All three artifacts named by the Reviewer; the Management Reviewer reaches the same conclusion through A10 | Not a conflict — the Management Reviewer classified it at the criterion, not at the artifact. One fact, three corrections, both lenses agreed on the defect |
| The Vision's two ellipses (`U12`, `U13`) | Reviewer: **Major** (`Vision#F1`, `use-case-shape`) — thirteen use cases where the recovery holds eleven. Management Reviewer: **Minor** (`Vision#F1`, `contained-defect`) — the Use-Case Model governs the set, no criterion depends on the Vision's count | **The two lenses disagree on consequence, not on fact.** Counted at the **Major** band for the gate: gate H4 puts a use-case count to the stakeholder, and a supporting artifact stating a different count beside it is a defect in the material the sanction rests on. The Minor is recorded and does not double the work — one correction closes both |
| `Risk List#F2` | Two findings share the key under different lenses and different subjects: the Reviewer's Minor on R024's premise, the Management Reviewer's Major on R030's unperformed retirement | Two distinct findings, not a duplicate. The R024 Minor's remedy is partly satisfied by the R030 Major's — both point the mitigation at an artifact that still carries the error — but each lens closes only its own key |
| `Development Case#F2` | Recorded by both lenses at SBC, closed by the Reviewer's key, still open under the Management Reviewer's | No duplicate recorded at this gate: the technical lens named it and did not re-record it. Only the Management Reviewer may close it, and only that key holds A11 |

**Priority of what remains — the order the second iteration takes them.** Majors before Minors, and within each band, the finding that unblocks another first.

| Priority | Finding | Why it ranks here |
|---|---|---|
| 1 | Supplementary Specification#F1 | The root of three Majors; correcting M3, S2, P1 and R8 lets the Software Architect and the Deployment Model copy one settled figure |
| 2 | Software Architecture Document#F1 | Reads the same fact from the Supplementary Specification; the Deployment Model's environment table inherits this copy |
| 3 | Deployment Model#F1 | The only statement in the delivery of what differs between environments; Consolidation would copy it unchanged |
| 4 | Supplementary Specification#F2 | Independent of the rate limiter, and the SAD's P6 already holds the correct reading, so the correction is a transcription |
| 5 | Use-Case Model#F1 | The eleven-use-case count gate H4 puts rests on the three edges; confirming them also clears the material the Vision's count is checked against |
| 6 | Vision#F1 | Cheapest of the eight — delete two ellipses — and it must follow priority 5 so the count matches |
| 7 | Risk List#F2 (Management Reviewer) | A Significant exposure read as retired; its warning sign has already come true |
| 8 | Iteration Plan#F3 (Management Reviewer) | The plan's own certification; re-taken after priorities 1 to 4 land, so A10 can be certified on the recovered set |
| 9–16 | The eight Minors | In the order of Resolutions and Actions; `Development Case#F2` first among them because A11 counts it |

**One fact, three Majors, one correction.** The three rate-limit Majors are one wrong sentence in three artifacts. The recovery already holds the right answer in the same phase — the System Inventory records it as AN-024 and the Risk List carries it as R025, both anchored. The defect is not a failure of reading; it is three documents asserting the value their own reading contradicts.

## Resolutions and Actions
### Reviewer lens
<!-- review: Excavation I2 -->

<!-- review: Excavation I2 -->

#### Closures materialized this iteration

Each row is a `resolve_artifact_finding` call that transitioned the ledger, not a narrative claim. The evidence column names where the corrected content was read.

| Finding | Criterion | Resolution | Evidence read |
|---|---|---|---|
| Vision#F1 | use-case-shape | Resolved | Features diagram: `component … PM1` / `PM2` under "Platform mechanisms - no actor goal, not use cases"; eleven `usecase` shapes only |
| Use-Case Model#F1 | trace-gap | Resolved | Trace graph, EP-003 downstream: three `Refines` edges, all OK |
| Use-Case Model#F2 | contained-defect | Resolved | Actors: "Two entry points, two different questions"; matrix edges read `acts on EP-003` / `calls EP-013` |
| Supplementary Specification#F1 | consumed-defect | Resolved | R8, P1, S2 all state 50 / 50 / 50 under AN-024; `appsettings.Development.json` opened and confirmed |
| Supplementary Specification#F2 | consumed-defect | Resolved | R4 states the token hop and the forwarder hop apart under AN-023; `ServiceDefaults/Extensions.cs:32-42` and `Todo.Web/Server/TodoApi.cs` opened and confirmed |
| Software Architecture Document#F1 | consumed-defect | Resolved | SP1: "50 tokens, 50 per 10 s and a queue of 50 is the budget in force wherever this delivery runs … The fact is AN-024" |
| Deployment Model#F1 | consumed-defect | Resolved | Environment Mapping preamble narrowed; Rate limiting row reads 50 / 50 / 50 for Development |
| Design Model#F1 | contained-defect | Resolved | PD-D3 note cites AN-025; AN-005 confined to the `EnsureCreated` statement |
| Risk List#F2 | contained-defect | Resolved | R024: "The Design Model already states the difference correctly at PKG-D3, and the Supplementary Specification's R4 states the opposite - which is the artifact the mitigation is aimed at" |

#### Actions this iteration opens

Each is an owner's corrective action, stated so it can be performed without a follow-up question. The first two hold the milestone; the third does not.

| Finding | Owner | Action | Holds the milestone |
|---|---|---|---|
| Use-Case Model#F3 | System Analyst | Confirm the five `COMP-014 → UC-006` to `UC-010` edges in the registered graph, each checked against `Todo.Api/Todos/TodoApi.cs:19-20`, and record in the shared gate diagram that the bucket gates each operation rather than performing it. Re-query the graph and report no SUSPECT marking on any edge the Use-Case Model declares | Yes — a suspect trace open at phase close fails criterion C6 |
| Use-Case Model#F4 | System Analyst | Correct R6 in the rules diagram to state the code defaults 100 / 100 per 10 s / queue 100 and the Development override 50 / 50 / 50 as the value in force, citing AN-024 and `appsettings.Development.json:8-12`, so the artifact holds one answer to the question its gate diagram already answers correctly | Yes — the four Majors of the AR review were this same class of defect |
| Development Case#F3 | Process Engineer | Bring the four Document Control fields to Excavation, iteration 2, status Draft for the AR review. No other content changes | No — a Minor does not hold the milestone |

#### Carried state read for this disposition

| Item | State read |
|---|---|
| Gate H4 (the stakeholder's confirmation of the recovered set) | The AR review records it answered No, with the order "We must correct all major findings." That order is what this iteration performed. It is not this lens's to re-put |
| The AR review's own ledger of eight Majors | Of those within this lens, four Majors (Supplementary Specification#F1, #F2; Software Architecture Document#F1; Deployment Model#F1) and one Minor (Design Model#F1) were this lens's. All five are closed on verified evidence. The two remaining Majors of this lens (#F3, #F4) are new defects found in this iteration's re-read, not survivors of the old ledger |
| Exit criterion A10 (the recovery states what the code does) | Certifiable on the recovered set as this lens reads it, on condition that Use-Case Model#F4 is corrected: as the artifact stands, one of its own diagrams contradicts the fact the criterion turns on |
| Suspect traces | Five remain registered against COMP-014 at the phase close. Criterion C6 is not satisfied |
| Open pull requests | None in any state |
| Build status | No IARI pipeline file exists; nothing to report for `main`. Excavation produces no production code, so this is correct for the phase, not a gap |

### Management Reviewer lens
<!-- review: Excavation I1 -->

#### Findings this lens closed at this gate

Four findings of this lens were reconciled before any new defect was recorded, each verified against the artifact it names through the lens's own `resolve_artifact_finding` call. Closure is the tool call; what follows is the rationale.

| Finding | What it claimed | Why it is closed |
|---|---|---|
| `Development Case#F1` | The duplication the stakeholder ordered deleted on 2026-11-23 — the role-delta list and the CLS-DC-01 diagram, each stated twice | Verified at "Roles and Ownership": one CLS-DC-01 diagram, one "### Role deltas" block with two bullets. The correction is in the artifact, not merely promised |
| `Iteration Plan#F1` | C2b recorded "Not met" after the stakeholder had granted gate H2 — a cell stating a state the answer superseded | The row no longer exists. The plan's Evaluation Criteria now carries A1 to A13, and the Survey milestone is stated once in the coarse roadmap as "SBC — passed … Met at the re-take on 2026-11-23" |
| `Risk List#F1` | SBC criterion C8 could not be established: `R004` and `R011` sat at Minor and Moderate and were accepted on the Project Manager's authority while the inventory's words scored them 12 | The scores are reconciled against one published word-to-score mapping; both rows read 4 × 3 = 12 and carry the stakeholder's verbatim grant of 2026-11-23. Recomputed row by row, all 29 anomaly-derived rows reproduce |
| `Iteration Plan#F2` | The fine plan's State column stated outcomes its artifacts did not carry | Row 9 now states the Document Control correction that is verifiably in the System Inventory, row 10 records `Development Case#F2` as "Not started" and names the exact sentence that still omits three lenses, and rows 11 to 14 state the review's own position. No row claims a correction its artifact does not carry |

#### Actions this lens's findings require, in the order the phase can hold them

| Order | Owner | Action | Criterion it moves |
|---|---|---|---|
| 1 | System Analyst | Correct the Supplementary Specification: M3, S2, P1 and R8 state the code's 100/100/100 **and** the Development override to 50 with its anchor; rewrite R4 as two hops, the token hop inheriting the standard resilience handler and the forwarder hop inheriting nothing | A10, A3 |
| 2 | Software Architect | Correct SP1, M3 and the Quality view's "bounded load" row the same way, citing `AN-024` | A10, A3 |
| 3 | Software Architect | Correct the Deployment Model's preamble and Rate limiting row: the Development value is 50 and any other environment 100, and this is one of the settings that differ | A10, A5 |
| 4 | System Analyst | Write R030's statement beside the recovered session flows, citing `AN-029`; confirm the three `EP-003` edges so the eleven-use-case count is not resting on a suspect marking; and bring the Vision's Features diagram to eleven use cases, matching the Use-Case Model | A1, risk retirement, the count gate H4 puts |
| 5 | Project Manager | Re-state A2 and A10 against what their evidence establishes, and set A12 to the answer as given | The plan's own certification |
| 6 | Process Engineer | `Development Case#F2`: name every lens in the Review Record's contributor set and draw the three missing edges in CLS-DC-01; bring Document Control forward to Excavation | **A11 — the criterion that holds the phase** |

Actions 1 to 5 are work an Excavation role performs in the phase as the process runs it. Action 6 is not: Environment has no intensity in Excavation, so its owner has no scheduled stage. That asymmetry — not the size of any defect — is what makes Excavation iteration 1 unable to close on its own evidence, and it is the materialization of `R031`.

#### The two outcomes this gate permits, and what each costs

```plantuml
@startuml
title AR-S1 The state the Architecture Recovered milestone is in at this review, and what moves it forward

skinparam shadowing false
skinparam wrapWidth 250

[*] --> UnderReview : iteration 1 artifacts written
UnderReview --> CriteriaAssessed : management lens reads A1 to A13
CriteriaAssessed --> SanctionSought : 8 Major open, A11 not met

state "Sanction sought at gate H4" as SanctionSought {
  SanctionSought : the recovered set put to the stakeholder
  SanctionSought : 11 use cases, 22 components, 8 tables
  SanctionSought : 4 stated exclusions
}

SanctionSought --> Refused : stakeholder answers No
SanctionSought --> Sanctioned : stakeholder answers Yes

state "Milestone NOT sanctioned" as Refused {
  Refused : verdict No-Go at this review
  Refused : A11 not met - 3 of 4 Minors closed
  Refused : A12 not met - sanction refused
  Refused : order given - correct all major findings
}

state "Rework inside Excavation iteration 2" as Rework {
  Rework : 8 Major closed by their owners
  Rework : A11 owned by a role the phase does not schedule
  Rework : R030 retirement performed or the risk restated
}

Refused --> Rework : iteration 2 planned from the Review Record
Rework --> CriteriaAssessed : criteria re-taken
Rework --> PlanA11 : if the Process Engineer still has no stage

state "A11 stands - R031 materializes" as PlanA11 {
  PlanA11 : the phase needs an iteration
  PlanA11 : it did not plan
  PlanA11 : declared work is never cut to avoid it
}

PlanA11 --> Rework : plan the extra iteration

state "Milestone sanctioned" as Sanctioned {
  Sanctioned : exit criteria met on their own evidence
  Sanctioned : Consolidation may start
}

Sanctioned --> [*]

note right of Refused
  A refusal is not a defect the team fixes: it is the
  stakeholder's to give. What it changes is the verdict,
  which may not grant a sanction they withheld.
end note

note bottom of Rework
  Nothing in the eight Majors needs a stakeholder decision.
  Each is a correction its owner can make in this iteration:
  one anomaly, AN-024, accounts for three of them.
end note

note bottom of PlanA11
  Environment runs at no intensity in Excavation, so the
  Development Case's owner has no scheduled slot here. That
  is why one Minor holds the phase, and why R031 exists.
end note

@enduml
```

**A second iteration is not a schedule failure; refusing the gate would be the failure.** Seven of the eight Majors were avoidable within this iteration had the artifacts been corrected against the anomaly their own reading had already recorded — `AN-024` was in the System Inventory and `R025` in the register, and three documents still asserted the opposite. The eighth, the Vision's use-case count, is the cheapest of all: delete two ellipses. The rework is cheap now and would not have been later: the Deployment Model's environment table is the only statement in the delivery of what differs between environments, and Consolidation would have copied it.

#### What does not move

- **No declared scope is cut.** The delivery declares none, so nothing is deferred to protect a figure.
- **No plan is re-sized.** Excavation has no measured actual — it has not closed — so no forecast is stated here and none is invented. The two currencies stay apart: agent work in tokens and elapsed time, the stakeholder's queue in days of waiting, never summed.
- **`R031` is not accepted away.** It stays an avoided Significant risk, and its contingency — a second iteration planned from this record — is what is now required.
- **The stakeholder's order is recorded as given**: "We must correct all major findings." No further condition, limit or prohibition was stated, and none is recorded.

### Review Coordinator lens
<!-- review: Excavation I1 -->

<!-- review: Excavation I1 -->

**Actions, in the order the second iteration takes them.** Each action is the remediation its recording lens wrote, with its owner and the act that closes it. No action states a calendar date: the sprint zero declares none beyond the issue date of the Work Order, and a projected date computed from an estimate would read downstream as an observation. The due point is the state of the work, not a day.

| # | Action | Artifact | Owner | Closes | Due point | Escalates if |
|---|---|---|---|---|---|---|
| 1 | State both rate-limit values with their sources in M3, S2, P1 and R8; cite AN-024 | Supplementary Specification | System Analyst | `Supplementary Specification#F1` | Before the Software Architect's next pass | The figure is still single-valued after two owner turns |
| 2 | Correct SP1, M3 and the Quality view's "bounded load" row; cite AN-024 | Software Architecture Document | Software Architect | `Software Architecture Document#F1` | After action 1, same iteration | The correction contradicts action 1's text |
| 3 | Narrow the environment preamble; rewrite the Rate limiting row — Development 50/50/50, other environments the code defaults | Deployment Model | Software Architect | `Deployment Model#F1` | With action 2, same turn | — |
| 4 | Rewrite R4 as the two hops stated apart; cite AN-023 / R024 | Supplementary Specification | System Analyst | `Supplementary Specification#F2` | With action 1, same turn | — |
| 5 | Re-register the three EP-003 edges as confirmed; record the screen-versus-operation reading in the Use-Case Survey | Use-Case Model | System Analyst | `Use-Case Model#F1` | Before gate H4 is re-put | The edges stay suspect at the next milestone |
| 6 | Remove U12 and U13 from the Features diagram; keep the two rows as mechanisms cross-referenced to M8 and M9 | Vision | System Analyst | `Vision#F1` (both lenses) | After action 5, so the count matches | The Vision states a count the Use-Case Model does not |
| 7 | Write R030's statement beside UC-001 to UC-004 citing AN-029, or restate R030 as not yet retired | Risk List, Use-Case Model | System Analyst, then Project Manager | `Risk List#F2` (Management Reviewer) | Before the register is read again as retired | The register still reads Avoid with the action unperformed |
| 8 | Hold A10 open naming the three artifacts, or split it into identification and agreement; set A12 to "Not met — refused" (`Iteration Plan#F5` alongside) | Iteration Plan | Project Manager | `Iteration Plan#F3` (Management Reviewer), `#F5` | After actions 1 to 4 land, so A10 can be re-taken on a corrected set | A10 is certified again on the inventory's word |
| 9 | Name every lens in the Review Record's contributor set and draw the three edges in CLS-DC-01 | Development Case | Process Engineer | `Development Case#F2` (Management Reviewer) — **holds A11** | Excavation iteration 2, on the stakeholder's order | No stage in the phase — escalate; `R031` materializes |
| 10 | Bring the four Document Control fields to Excavation iteration 1 | Development Case | Process Engineer | `Development Case#F3` | With action 9, same turn | — |
| 11 | State the matrix-versus-Survey distinction and relabel the matrix's edges | Use-Case Model | System Analyst | `Use-Case Model#F2` | After action 5 | — |
| 12 | Restate R024 without the misattribution; point its mitigation at Supplementary Specification R4 | Risk List | Project Manager | `Risk List#F2` (Reviewer) | After action 4, so the mitigation has a target | — |
| 13 | Change PD-D3's citation from AN-005 to AN-025 | Design Model | Designer | `Design Model#F1` | Owner's next turn | — |
| 14 | Narrow A2 to its evidence, or add the deferred-set sentence to the Use-Case Model's "Not recovered, and why" | Iteration Plan | Project Manager | `Iteration Plan#F4` | With action 8 | — |

**Escalation protocol as applied at this milestone.** One finding is escalated and one class of exposure is escalated; nothing else is overdue.

```plantuml
@startuml
title The escalation path a finding takes when its owner cannot act, applied to Development Case F2

skinparam shadowing false
skinparam wrapWidth 240

|Recording lens|
start
:record_artifact_finding - severity, criterion, recommendation;
if (owner has a stage in this phase?) then (yes)
  :owner's next turn, after the Critical and Major findings;
  :lens re-reads the corrected section;
  if (defect gone?) then (yes)
    :resolve_artifact_finding;
    stop
  else (no)
    :stays open, re-recorded under its key;
    stop
  endif
else (no)
  :escalate - written notice to the Project Manager
  with the ledger entry as evidence;
  note right
    Development Case F2. The Process Engineer has no
    stage in Excavation: Environment runs at no
    intensity here. The finding is not waived.
  end note
endif

|Project Manager|
:The exposure is carried as a scored risk - R031;
if (can the phase plan a slot?) then (yes)
  :plan the iteration that gives the owner a stage;
else (no)
  :the criterion stays not met;
  :the milestone cannot close on this iteration's evidence;
endif

|Review Coordinator|
:record the criterion's true state in the ledger;
:neither waive nor close it;
:report the exposure to the milestone verdict;
stop

@enduml
```

**Escalated to the Project Manager, with the ledger as evidence.** `Development Case#F2` — a Minor on any reading, and the only finding at this milestone that holds an exit criterion. A11 counts four Minor closures and reads three of four. Its owner, the Process Engineer, has no stage in Excavation because Environment runs at no intensity in the phase. `R031` predicted exactly this and has materialized. The exposure is not the size of the defect — it is that a criterion depends on a role the phase does not schedule.

**No escalation to the Configuration and Change Management Board.** No systemic process failure is visible in this ledger: the same two lenses evaluated the same ten artifacts, each finding is anchored to the code or the artifact text, and the rework the Majors require is inside the artifacts their owners hold. The Change Control Manager does not work in the sprint zero, so no change request is opened for any finding; the stakeholder's order reaches its owners through this record and through their Work Order.

**Review effectiveness — this milestone's measured counts.** First review of this phase; there is no prior Excavation iteration or cycle to compare against, so these are current values only and no trend is stated.

| Indicator | Value | What it is computed from |
|---|---|---|
| Review coverage | 10 of 10 artifacts subject to review received at least one lens read | The ten artifacts of this phase with findings or an explicit "no finding" statement from both executed lenses. The Iteration Assessment and this Review Record are not review subjects at their own milestone |
| Findings recorded | 29 — 8 Major, 21 Minor | `read_artifact_findings` across the ten artifacts, both lenses |
| Findings open at the gate | 16 — 0 Critical, 8 Major, 8 Minor | The `[FINDINGS]` line; 13 closed by their recording lens |
| Defect density by artifact type | Requirements artifacts 6 (5 Major, 1 Minor over Vision, Use-Case Model, Supplementary Specification); Analysis and Design 3 (2 Major, 1 Minor over SAD, Deployment Model, Design Model); Project Management 5 (3 Major, 2 Minor over Risk List, Iteration Plan); Environment 2 (0 Major, 2 Minor); Discovery 0 | The open and closed ledger, by the artifact carrying each finding |
| Lens agreement | 0 contradictory findings; 1 severity disagreement (`Vision#F1`, Major vs Minor); 2 keys shared by two lenses on distinct subjects | The reconciliation table in Findings |
| Duplicate defects found by two lenses | 1 subject — the rate limiter, reached by both lenses through different criteria | Both lenses named it; neither recorded the other's key |
| Defect removal efficiency | Not computable at this milestone | No test execution has occurred in the sprint zero. Nothing has been found by test against which review-found defects could be compared, and no ratio is invented |
| Rework effort | Not measured | Tokens and elapsed agent time per artifact are not recorded per finding in this phase; the phase has not closed so no measured actual exists to attribute |

**What the metrics say.** The two lenses found the same defect independently and classified it the same way at the artifact level, which is the signature of a real defect and not a lens artefact. The defect density is concentrated: the three rate-limit Majors are one anomaly recorded three times, so the four artifacts of the Requirements and Analysis surface carry an apparent density four times the underlying defect count. The review process worked — every Major is anchored, every Minor is owned, and the defect that mattered had already been recorded as `AN-024` in the same phase by the same role's own reading. What it did not do is prevent three artifacts from asserting the opposite of a fact the phase already held.

**No finding recorded for three absences, and why.** The absence of a Data Model, a Glossary and a Test Plan is the Development Case's NOT FIRED verdict on each trigger, which both lenses checked against the §5.2 conditions. The absence of an Iteration Assessment describing this iteration is correct state — the Project Manager authors it after this review. The absence of any SCM condition is the sprint zero's correct state: no branch of this process exists, no pull request is open, no defect issue is filed.

## Disposition
### Reviewer lens
<!-- review: Excavation I2 -->

<!-- review: Excavation I2 -->

#### Disposition — Approved with Changes

The recovered set improved decisively this iteration and it is not yet approvable. Nine of the ten artifacts this lens previously faulted now hold, each verified at its section and — for the four Majors about recovered facts — at the code itself. Two Majors remain, both on the Use-Case Model, and both are the two failure modes the nine closures removed, found elsewhere in the same set.

```plantuml
@startuml
title Disposition: the AR technical verdict, and what stands between it and an approval

skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam wrapWidth 215
hide circle
hide empty members

package "Verdict - Approved with Changes" {
  class "Nine of the ten artifacts\nthis lens previously faulted\nnow hold on verified evidence" as V <<pass>>
  class "No Critical finding\nno stakeholder decision\nis outstanding from this lens" as VC <<pass>>
  class "Two Majors hold the milestone\nboth on one artifact\nboth owner-correctable in-phase" as VM <<major>>
}

package "What an approval requires" {
  class "Use-Case Model#F3\nfive COMP-014 edges confirmed\nno SUSPECT left at close" as R1 <<action>>
  class "Use-Case Model#F4\nR6 states both budgets\nunder AN-024" as R2 <<action>>
  class "Development Case#F3\nfour Document Control fields\nbrought forward" as R3 <<minor>>
}

package "What this lens does not decide" {
  class "Gate H4\nthe stakeholder's confirmation\nof the recovered set" as H4 <<stakeholder>>
  class "The AR milestone verdict\nconsolidated by the\nReview Coordinator" as RC <<stakeholder>>
}

V --> VM
VM --> R1 : closed by
VM --> R2 : closed by
VM --> R3 : does not hold the gate
R1 --> RC : then re-read
R2 --> RC : then re-read
R3 --> RC : in the owner's next turn
RC ..> H4 : put after the Majors land

note right of VM
  Both Majors are the two failure modes the nine
  closures removed, found elsewhere in the same set:
  one recovered fact transcribed inconsistently, and
  one trace edge never confirmed. Neither is new scope.
end note
note bottom of H4
  The AR review records the stakeholder answering No with
  the order "We must correct all major findings." That order
  is what this iteration performed; re-putting the gate is
  not this lens's to do.
end note

@enduml
```

#### Verdict on the AR exit criteria, as this lens reads them

| Criterion | This lens's reading | Basis |
|---|---|---|
| A3 Architecture recovered and checked | Met | Twenty-two components with connectors; every one of the eleven use cases has a stated component path, including the seven not diagrammed. The figure contradictions the AR review faulted are corrected and reproduce from the code |
| A4 Data recovered with its anchors | Met | Eight tables with keys, indexes, referential actions and enforced rules; AN-025 correctly cited at PD-D3 and AN-005 confined to `EnsureCreated` |
| A5 Deployment modelled | Met | The fired optional records the processes, the stores, the ports, the key ring and the two settings that separate the environments, each anchored |
| A6 Coverage measured | Met | 84 read and 55 unread of 139; the per-area columns reproduce and every unread category is named |
| A7 Anomalies carried as risks | Met | Thirty-two risks, twenty-nine on `Refines` edges from the anomalies, three with their separate origins stated |
| A9 Every risk actionable | Met | Each row names a strategy, an owner, an action, a contingency and a warning sign; R030 states "not yet retired" rather than claiming a retirement that has not happened |
| A10 The set states the code's behaviour | **Not certifiable as it stands** | Two of the facts it turns on are correct in four artifacts, and a fifth — the Use-Case Model's rules diagram — states one of them wrongly at R6. Criterion A10's test is a test about what the recovered artifacts state |
| A11 The SBC Minors closed | Not met — unchanged | Three of four. `Development Case#F2` is the Management Reviewer's lens, not this one's; this lens's own `Development Case#F3` is a different defect on the same artifact |
| A12 The recovered set confirmed | Not met — unchanged | Gate H4 answered No. Not an artifact's to hold |

A1 and A2 sit on the Use-Case Model with the two open Majors: A1 (operations recovered as use cases) holds on the Survey and the exclusion table, which neither Major touches. A2 holds on the priorities order.

#### Why this is Approved with Changes and not Rejected

A rejection would say the recovered set is not a model of the existing system. It is: the eleven use cases, the twenty-two components and the eight tables each rest on the file they cite, and this iteration verified that at source rather than accepting it from the artifacts' own text. The two open Majors are a confirmation the graph registers as missing and one diagram that states a figure its own artifact states correctly elsewhere. Neither calls the recovery into question; both are corrections their owner performs inside this phase.

#### Why it is not Approved

Approval would certify a Use-Case View with five suspect edges at the phase close and a rules diagram whose request budget contradicts the code and its own artifact. The AR review held the milestone on exactly this class of defect and the stakeholder's order was to correct all Majors. Certifying the set with two of them open would repeat the failure the last gate caught.

#### Preserved

No artifact outside the ten reviewed was re-read for a finding, and none is changed by this lens. The Review Record is this lens's only output.

### Management Reviewer lens
<!-- review: Excavation I1 -->

#### Verdict

**No-Go.** The Architecture Recovered milestone is **not sanctioned** at the end of Excavation iteration 1.

I put the milestone to the stakeholder at this review with my leaning stated — Conditional Go, seven Majors open at the time of asking, none requiring their decision — and the recovered set for confirmation. They answered:

- **Stakeholder sanction: REFUSED.** Asked whether they confirm the recovered set as the model of the existing system — the 11 use cases and the 4 stated exclusions, the 22-component architecture across four processes, and the eight-table data model — and sanction advancing past the Architecture Recovered milestone into Consolidation with the Majors cleared first, the stakeholder answered **"No"**.
- **Stakeholder acceptance, as given:** "We must correct all major findings."

That is the whole of what they stated. No condition, limit or prohibition beyond it is recorded here, and none is inferred.

**Why No-Go rather than Conditional.** A sanction is an affirmative grant; the burden of proof rests on the project team, and I may not grant what the stakeholder withheld. Two exit criteria are not met on the phase's own evidence, and both are structural rather than editorial:

- **A11 — the four SBC Minors closed — is not met, three of four.** `Development Case#F2` stands. It is contained in its own document and a lens writes its block whatever the tailoring says, but the phase's plan counts it, this lens counts it, and its owner has no scheduled stage in Excavation because Environment runs at no intensity here. `R031` was written down as this exact exposure at 3 × 4 = 12. It has materialized, and that is now a statement of fact rather than a forecast.
- **A12 — the recovered set confirmed — is refused.** The gate the phase waits on returned No.

Neither is repairable by the same set of artifacts. The first needs a role the phase does not schedule; the second needs the stakeholder asked again after the Majors are cleared. A Conditional Go would have claimed the second was obtainable by editing documents, and it is not.

#### Four-axis health

```plantuml
@startuml
title AR-H1 Four-axis health scorecard for Excavation iteration 1 - no single axis decides the gate, and two of the four are red

skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam wrapWidth 260
hide empty members
hide circle

class "Scope\nAMBER" as S <<scope>> {
  recovered : 11 use cases over 22 entry points
  recovered : 22 components, 8 tables, all anchored
  recovered : 4 exclusions stated and ruled
  gap : A2 names no work left for Consolidation
  gap : 3 screen edges suspect, unconfirmed
  gap : priorities 6 to 8 carry no statement
}

class "Schedule\nRED" as T <<schedule>> {
  planned : one iteration, AR gate at its end
  actual : gate not passed on this iteration
  cause : A11 needs a role the phase does not schedule
  cause : A12 refused at gate H4
  cost : a second iteration the phase did not plan
}

class "Cost\nAMBER" as C <<cost>> {
  declared : no token budget, so none set
  measured : Survey 29 min agent, 5 min queue
  measured : Survey 8,995,433 tokens, 10 runs
  unmeasured : Excavation, open, so no figure
  rule : no forecast invented before it closes
}

class "Quality\nRED" as Q <<quality>> {
  open : 8 Major, 0 Critical, 6 Minor
  cause : AN-024 reaches 3 artifacts as one fact
  cause : R030 avoided, action unperformed
  cause : A10 certified on the inventory's word
  closed : 4 findings of this lens since SBC
}

Q --> T : three Majors are one cause,\nso one correction moves two axes
S --> T : the unsupported clauses are\nwhat the next iteration re-does
C ..> T : the second iteration is\nunmeasured until it closes

note bottom of T
  Red is not lateness: no calendar was promised. It is
  that the phase's own exit criteria are not met on the
  evidence it produced, which is what a gate reports.
end note

note bottom of Q
  A red axis is not overruled by three green ones. Two
  red means the milestone does not close, whatever the
  other two say.
end note

note bottom of C
  The two clocks are never added: 29 min of agent time and
  5 min of stakeholder queue are reported apart, and the
  queue excludes the approval gate, which is not measured.
end note

@enduml
```

**Quality is red on eight Majors and zero Criticals**, and the distribution matters more than the count: three of the eight are one anomaly — `AN-024` — stated as fact in three documents while the System Inventory records the contradiction and `R025` carries it. Correcting those three against the anomaly their own reading already found is short work with the anchor to hand. The fourth Major is a two-hop claim collapsed into one sentence; the fifth is three trace edges whose substance is right and whose confirmation was never registered; the sixth is a use-case count stated as thirteen where the artifact that owns the set recovers eleven; the seventh is a Significant risk recorded as retired by an action that is in no artifact; the eighth is a criterion certified on a neighbouring artifact's word.

**Scope is amber, not green**, because two of the certifyable criteria were recorded Met on evidence that does not carry them. The recovered set itself is strong: eleven use cases over twenty-two entry points with every exclusion stated, twenty-two components with a `Realizes` row per use case, eight tables with keys, indexes, referential actions, and a table of the rules the schema does *not* enforce — that last being the most useful page in the phase. The amber is for the certification, not the content.

**Schedule is red.** One iteration was planned with the AR gate at its end; the gate is not passed. The cause is not that the work was large — it is that one criterion depends on a role the phase does not schedule, and one gate answer cannot be obtained until the Majors are cleared.

**Cost is amber and deliberately carries no projection.** The project declares no token budget, so no box exists to fit and no declared work was cut or deferred to meet an estimate. The one measured actual is the closed phase: 29 minutes of agent time, 5 minutes of stakeholder queue, 8,995,433 tokens across 10 runs — reported in the two currencies, apart, never summed. Excavation has not closed, so it has no measured actual and no forecast is stated for it.

#### What is sanctioned, and what is not

| Item | State |
|---|---|
| The Architecture Recovered milestone | **Not sanctioned** — No-Go |
| Advancement into Consolidation | **Not sanctioned** |
| The recovered content — 11 use cases, 22 components, 8 tables, 4 exclusions | **Exists, anchored, and not confirmed by the stakeholder** |
| Excavation phase | **Open** — a second iteration required, planned from this record |
| The stakeholder's order | **"We must correct all major findings."** |
| `R031` | **Materialized** — an avoided Significant risk whose contingency is now the required path |

#### Closing statement

The gate holds. Eight Majors and two unmet criteria are open, the stakeholder refused the sanction, and they ordered the Majors corrected. Excavation iteration 2 is planned from this record: actions 1 to 5 of "Resolutions and Actions" are their owners' work in that iteration, and action 6 — the one Minor that holds the phase — needs the Process Engineer given a work item in an Excavation iteration, because the process does not otherwise put that role in this phase. If that item lands, A11 reads four of four on re-take. If it does not, `R031` says what happens next: the phase opens the further iteration its own register already budgeted for, and nothing the phase declared is cut to avoid it.

I do not sanction a phase because the calendar says it should end. I sanction it when its exit criteria are met on the evidence each criterion cites — and at the end of Excavation iteration 1 they are not.

### Review Coordinator lens
<!-- review: Excavation I1 -->

<!-- review: Excavation I1 -->

**Verdict — the AR milestone is NOT sanctioned on Excavation iteration 1's evidence.** The decision is read from the ledger, not from judgment: the `[FINDINGS]` line reports 12 artifacts read, unread none, 0 open Critical, 8 open Major, 8 open Minor; the recovery's own statement of completeness leaves exit criterion A11 at three of four; and the stakeholder answered gate H4 **No**, with the order "We must correct all major findings." Nothing in this record advances the project past Architecture Recovered.

```plantuml
@startuml
title AR milestone verdict - the guard each path is taken on, read from the finding ledger

skinparam shadowing false
skinparam wrapWidth 240

start
:read the ledger - read_artifact_findings on every artifact;
:emit the FINDINGS line - read, unread, open Critical, open Major;
if (any unresolved Critical?) then (yes)
  :ESCALATE - each open Critical put to the stakeholder verbatim;
  :requiresIteration true;
elseif (any open Major, or an unread artifact, or no GRANTED sanction line?) then (yes)
  :STAKEHOLDER CONTRIBUTION - fold the answer in, iterate;
  :requiresIteration true;
  note right
    Taken at this gate. 8 open Major, unread none,
    and gate H4 answered No, so the sanction line
    reads REFUSED. The milestone is not sanctioned
    and the phase iterates.
  end note
else (no)
  :SCOPE COMPLETE - verify on data, then ask before advancing;
  :requiresIteration false;
endif
stop

@enduml
```

**The guard, taken on data.** Three of its four conditions are false, so the milestone does not advance and the phase iterates.

| Guard condition | Required | At this milestone | Holds |
|---|---|---|---|
| Unresolved Critical findings | 0 | 0 | Yes |
| Open Major findings | 0 | 8 | **No** |
| Artifacts unread at the gate | none | none — all 12 read | Yes |
| Stakeholder sanction line | GRANTED | **REFUSED** — gate H4 answered No on 2026-11-23 | **No** |

**The recovery's own completeness, as the two criteria read.**

| Criterion | State | Evidence |
|---|---|---|
| A11 — the Minors the SBC review left open are closed | **Not met — three of four** | `Iteration Plan#F2`, `Iteration Plan#F3` and `System Inventory#F3` are corrected in their artifacts. `Development Case#F2` stands: "Roles and Ownership" still omits the Management Reviewer, the Business Reviewer and the Review Coordinator, and CLS-DC-01 draws no edge from them into this artifact. Carried as `R031` |
| A12 — the recovered set is confirmed by the stakeholder | **Not met — refused 2026-11-23** | Gate H4 answered No. The 11 use cases, the 22-component architecture, the eight-table data model and the four stated exclusions were put and not accepted |
| A10 — the recovery states what the code does | **Not met as written** | Three artifacts state AN-024's contradicted value as fact: the Supplementary Specification, the Software Architecture Document and the Deployment Model. The criterion is certified on the inventory's identification of the contradiction, not on the recovered set |

A11 is not waived and no row of the plan is marked complete on it. A12 is the stakeholder's to give and is not this record's to supply.

**What this milestone found, in one paragraph.** The recovery itself is sound: eleven use cases each anchored to the entry point whose code performs it, four exclusions stated with their reasons and confirmed by the stakeholder's own rulings of 2026-11-23, 22 components with their connectors, eight tables with their keys and enforced rules, and 84 of 139 files opened with the remainder named. The defects are one class and they are not reading failures: a fact the phase had already recorded as `AN-024` was asserted backwards in three documents, and the phase already held the correct statement in its own inventory and register. Four of the eight Majors are that one file. The Vision's count is the cheapest of the rest. The eighth, `Iteration Plan#F3`, is a criterion certified on an adjacent artifact's answer — the shape a milestone verdict exists to catch.

**The stakeholder's contribution, collected at this milestone and recorded as given.** Gate H4 was put inside this milestone, which is where the Management Reviewer's gate sits, and answered: **No** to confirming the recovered set and sanctioning advancement into Consolidation, with the direction **"We must correct all major findings."**

- Recorded as the sanction answer and as a `Stakeholder finding` this record acts on. It is verified against the ledger rather than deferred: the eight open Majors are exactly the items it names, each carries an owner and a due point in Resolutions and Actions, and none is recorded as closed or waived.
- No new defect is minted for the order — every item it names is already in the ledger with a owner and a remedy.
- The question of what else the second pass should read was answered in the same breath: correct all major findings, no prohibition stated, no exclusion re-opened, no recovered use case named as wrong or missing. Nothing further is asked of the stakeholder here.

**What does not move.**

| Item | Standing |
|---|---|
| Declared scope | The delivery declares none, so nothing is deferred or cut to protect a figure |
| The four stated exclusions | Untouched. The stakeholder re-opened none of them: external-provider sign-in stays recovered and unreachable, the admin branch stays an exceptional entity, the health endpoints and the migration event stay outside the use-case set |
| `R031` | Stays an avoided Significant risk. Its contingency — a second iteration planned from this record — is what is now required, not what is declined |
| The recovered set | Not withdrawn. Every element remains in its artifact with its anchor; what fails is the claim that it is confirmed and complete |
| The plan | Not re-sized. Excavation has no measured actual — it has not closed — so no forecast is stated and none is invented. The two currencies stay apart: agent work in tokens and elapsed time, the stakeholder's queue in days of waiting, never summed |
| The measured actuals of the closed phase | Survey: 29 min agent time, 5 min stakeholder queue, 8,995,433 tokens, 10 agent runs, 6 artifacts. Per phase, not per iteration; no velocity is quoted from it |

**What the next iteration carries.** Excavation iteration 2, planned from this record: the fourteen actions in Resolutions and Actions, taken in the order given — the three rate-limit corrections and the resilience correction first, because one settled figure unblocks four artifacts and one criterion; then the three EP-003 edges and the Vision's count; then the two Management Reviewer Majors, the one on `R030` and the one on A10; then the eight Minors, `Development Case#F2` first among them because A11 counts it.

**A second iteration is not a schedule failure.** The rework is cheap now and would not have been later: the Deployment Model's environment table is the only statement in the delivery of what differs between environments, and Consolidation would have copied it unchanged. Seven of the eight Majors were avoidable within this iteration had each artifact been corrected against the anomaly the phase's own reading had already recorded.

**Recorded through the process's own channel.**
