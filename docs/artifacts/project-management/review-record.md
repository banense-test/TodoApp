## Document Control
### Reviewer lens
<!-- review: Excavation I1 -->

<!-- review: Excavation I1 -->

- Phase: Excavation
- Status: Technical lens complete for the AR (end-of-Excavation) milestone review. Ten findings recorded this milestone: 0 Critical, 6 Major, 4 Minor, 0 Info. Two prior findings of this lens closed. Disposition — Approved with Changes, with the six Majors holding the milestone until their artifacts are reworked.
- Milestone Target: end-of-Excavation (AR) — not achieved. The six Majors are open and the recovery's own figures are contradicted by the code in three artifacts; gate H4 has not been put and is not this lens's to put.
- Iteration: 1, Cycle 1
- Owner: Reviewer

### Management Reviewer lens
<!-- review: Excavation I1 -->

- Phase: Excavation
- Status: AR (end-of-Excavation) milestone review taken at the end of Excavation iteration 1. This lens records 2 Major and 3 Minor this milestone, and carries 1 Minor from the SBC gate (`Development Case#F2`) that the phase's own criterion A11 counts. Read with the technical lens, the gate has 8 Major open and 0 Critical. Four findings of this lens closed at this gate.
- Milestone Target: end-of-Excavation (AR) — **not achieved**. Sanction refused by the stakeholder at gate H4 on 2026-11-23; the order given is "We must correct all major findings."
- Iteration: 1, Cycle 1
- Owner: Management Reviewer
- Review type: Lifecycle Milestone Review (AR) — exit-criteria lens. Nine of the thirteen AR criteria established on their own evidence; two not establishable as written; two not met.
- Verdict: **No-Go**
- Stakeholder sanction: **REFUSED**

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
<!-- review: Excavation I1 -->

<!-- review: Excavation I1 -->

**Review type.** Lifecycle milestone review, technical lens, at the AR (end-of-Excavation) review point. The question applied is exit criteria: whether the artifacts this phase produced establish that the system's operations, architecture and data have been recovered from the code — each element resting on the file it cites — and whether that recovered set may be put to the stakeholder at gate H4.

**Artifacts under review — ten, read whole.**

| Artifact | Owner | Discipline | Content read against |
|---|---|---|---|
| Vision | System Analyst | Requirements | The Use-Case Model and the System Inventory's perimeter |
| Use-Case Model | System Analyst | Requirements | The System Inventory's entry points; the registered trace graph |
| Supplementary Specification | System Analyst | Requirements | The mechanisms' anchors, opened |
| Software Architecture Document | Software Architect | Analysis & Design | The manifests, the mechanisms' anchors, the use cases |
| Deployment Model | Software Architect | Analysis & Design | The orchestration, the launch profiles, the environment files |
| Design Model | Designer, Database Designer | Analysis & Design | The migrations, the entity declarations, the anomalies |
| System Inventory | Software Archaeologist | Discovery | Its own arithmetic and its own trace rows |
| Risk List | Project Manager | Project Management | Its own scoring mapping and the artifacts it cites |
| Iteration Plan | Project Manager | Project Management | The exit criteria against the artifacts each cites |
| Development Case | Process Engineer | Environment | The IARI DC baseline in this review's own prompt |

The Iteration Assessment is not reviewed: the Project Manager authors it in the Assess touchpoint that runs after this review, so at review time it cannot describe the iteration being reviewed. Its absence is not a finding and not a gate condition.

**Checklist applied.** The EVIDENCE lens of Excavation, per artifact type: Requirements — every use case traces to the entry point whose code performs it, every entry point carried or its exclusion stated, no cross-cutting mechanism drawn as a use case, trace rows matching the graph. Analysis & Design — every component, class and mechanism resting on an anchor that says what the artifact claims, every declared technology present in a manifest, environment differences stated correctly, subsystem boundaries not named by layer. Discovery — coverage arithmetic reproducing, edge counts reproducing, Document Control naming its own iteration. Project Management — every anomaly carried, every score reproducing from one mapping, the grant band holding the stakeholder's own answers, each exit criterion certified on its own artifact's evidence. Environment — DC baseline conformance and every FIRED optional trigger holding its §5.2 condition.

**Scope of this pass — and what it is not.** This lens re-read all ten artifacts whole. It is not a re-litigation of the two SBC passes: the four Survey artifacts' iteration-2 rework is confirmed closed below and the Survey findings resolved. What is new is that Excavation produced six artifacts that did not exist at SBC, and this is the first pass over them; the two facts it found wrong cut across both the new artifacts and the ones they build on.

```plantuml
@startuml
title Compliance matrix - checklist item x artifact, this technical lens, Excavation iteration 1

skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam wrapWidth 210
hide circle
hide empty members

package "Requirements - anchor and shape" {
  class "Use-Case Model\nSystem Analyst" as UCM {
    ..
    every use case traces to its EP-NNN : PASS
    every entry point carried or exclusion stated : PASS
    no cross-cutting mechanism drawn as a use case : PASS
    one use case per goal, two scenarios not per-actor : PASS
    Traceability rows agree with the registered graph : FAIL
  }
  class "Supplementary Specification\nSystem Analyst" as SS {
    ..
    every mechanism anchored to its file : PASS
    behaviour the recovery must not overstate : PASS
    figures reproduce from the stated anchor : FAIL
    resilience stated as the code has it : FAIL
  }
  class "Vision\nSystem Analyst" as VIS {
    ..
    no scope invented for the delivery : PASS
    every feature names its EP-NNN : PASS
    cross-cutting mechanisms kept out of use-case notation : FAIL
    stakeholder rulings recorded where they bite : PASS
  }
}

package "Analysis and Design - recovered structure" {
  class "Software Architecture Document\nSoftware Architect" as SAD {
    ..
    every component carries its anchor : PASS
    components realize the recovered use cases : PASS
    every declared technology is in a manifest : PASS
    a mechanism's values reproduce from its anchor : FAIL
    upstream disagreement recorded not reconciled : PASS
  }
  class "Deployment Model\nSoftware Architect" as DEP {
    ..
    topology anchored to the orchestration : PASS
    ports stated as profiles not orchestration : PASS
    environment differences stated correctly : FAIL
    OPTIONAL trigger justified in the Development Case : PASS
  }
  class "Design Model\nDesigner, Database Designer" as DM {
    ..
    every class carries its anchor : PASS
    persistent store recovered with keys and rules : PASS
    Data Model omitted with its trigger stated : PASS
    anomaly citations point at the right anomaly : FAIL
  }
}

package "Discovery and Project Management" {
  class "System Inventory\nSoftware Archaeologist" as SI {
    ..
    every entry point and anomaly anchored : PASS
    coverage arithmetic reproduces from its table : PASS
    edge count reproduces from its own rows : PASS
    Document Control names its own iteration : PASS
  }
  class "Risk List\nProject Manager" as RL {
    ..
    every anomaly carried as one risk : PASS
    every score reproduces from one mapping : PASS
    grant band holds the stakeholder's own answer : PASS
    a risk's premise matches the artifact it cites : FAIL
  }
  class "Iteration Plan\nProject Manager" as IP {
    ..
    every work item is a stage the phase runs : PASS
    exit criteria certified on their own evidence : PASS
    State column states each row's outcome : PASS
  }
  class "Development Case\nProcess Engineer" as DC {
    ..
    no baseline redefinition : PASS
    every FIRED optional justified per its trigger : PASS
    Document Control names the current phase : FAIL
    contributor set names every lens that writes : FAIL
  }
}

@enduml
```

**Prior findings of this lens — reconciled before new defects were recorded.**

| Artifact | Finding | State this pass | What was checked |
|---|---|---|---|
| System Inventory | `System Inventory#F3` (Minor) — Document Control still read iteration 1 | Resolved | Document Control now reads "Iteration: Excavation iteration 1, cycle 1", the iteration its content belongs to |
| Iteration Plan | `Iteration Plan#F3` (Minor) — the fine plan's State column contradicted the artifacts | Resolved | The section commits to stating each row's actual outcome; row 9 cites the Document Control correction, verified in the artifact; row 10 records `Development Case#F2` as Not started rather than complete, which is the true state |

`Development Case#F2` — the contributor set omitting three lenses, ordered corrected by the stakeholder on 2026-11-23 — belongs to the **Management Reviewer's** lens, not this one, and this lens leaves it to that lens. The Iteration Plan's item 10 and its criterion A11 already record it as outstanding and carried as `R031`; the artifact still reads "Reviewer, CodeReviewer, plus the Configuration Manager's baseline record". This lens records nothing against it because it has no finding of its own on it — a second lens's key must be closed by that lens.

**Anchor verdict — the statements this phase's recovery rests on, opened rather than trusted.**

| Claim under review | Anchor opened | Verdict |
|---|---|---|
| The rate-limit values 100 / 100 / 100 are the effective ones because no `RateLimiting` section exists | `Todo.Api/appsettings.Development.json` | **Contradicted** — the file carries `"RateLimiting": { "TokenLimit": 50, "TokensPerPeriod": 50, "QueueLimit": 50 }`. Both launch profiles set `ASPNETCORE_ENVIRONMENT` to Development, so 50 is the value that applies. The System Inventory records this as AN-024 and the Risk List as R025; three of the artifacts under review state the opposite |
| No retry, circuit breaker or fallback is configured on either hop out of the BFF | `TodoApp.ServiceDefaults/Extensions.cs` | **Contradicted** — `ConfigureHttpClientDefaults(http => { http.AddStandardResilienceHandler(); ... })` applies the standard retry, circuit-breaker, timeout and rate-limiter pipeline to every container-built `HttpClient`, which reaches `AuthClient`. Only the YARP forwarder hop carries none. The SAD states this correctly at P6; the Supplementary Specification's R4 says "either hop" |
| The ownership predicate is written four times and the list applies half of it | `Todo.Api/Todos/TodoApi.cs` | **Confirmed** — `Where(todo => todo.OwnerId == owner.Id)` on the list with no admin branch; `todo.OwnerId == owner.Id \|\| owner.IsAdmin` on the read, the update and the delete. AN-018 is accurately stated in the System Inventory, the Supplementary Specification and the SAD |
| `POST /todos` copies the title alone, so a create body asking for a completed row produces `IsComplete` false | `Todo.Api/Todos/TodoApi.cs` | **Confirmed** — `new Todo { Title = newTodo.Title, OwnerId = owner.Id }`, with no assignment from `newTodo.IsComplete`. UC-007's step 5 and the Design Model's R-facts both state it correctly |
| Every entry-point-bearing anomaly edge reproduces from the System Inventory's own row | System Inventory "Traceability" and "Anomalies", both read together | **Confirmed** — 21 `DependsOn` edges across twelve anomalies, matching the Iteration Plan's twelve-row handoff table. `AN-021` carries all three of `EP-004`, `EP-005`, `EP-007`, the edge the earlier pass found missing |

Two of five anchors opened contradicted the artifacts that cite them, and each contradiction is recorded below against every artifact that carries it.

**SCM evidence.** No open pull request exists, and none should: the sprint zero writes no production code — Implementation runs from Inception — so a pull request in this phase would itself be a `scm-phase-discipline` finding. `scm_list_pull_requests(state: open)` returns none. There is no IARI pipeline on `main`, so no build status exists to be red. Nothing is disposed in this review and no code review decision is owed. This is the correct state for Excavation, not an absence to be flagged.

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
<!-- review: Excavation I1 -->

<!-- review: Excavation I1 -->

Ten findings, each naming the criterion whose test it meets. Six are Major — another role builds on the wrong content, and the recovered figures the phase would put to the stakeholder at gate H4 are wrong in three artifacts by one cause.

```plantuml
@startuml
title Defect distribution - severity x artifact, this technical lens, Excavation iteration 1

skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam wrapWidth 220
hide circle
hide empty members

class "Supplementary Specification" as SS {
  Major : 2
  Minor : 0
  Open : 2
}
class "Software Architecture Document" as SAD {
  Major : 1
  Minor : 0
  Open : 1
}
class "Deployment Model" as DEP {
  Major : 1
  Minor : 0
  Open : 1
}
class "Use-Case Model" as UCM {
  Major : 1
  Minor : 1
  Open : 2
}
class "Vision" as VIS {
  Major : 1
  Minor : 0
  Open : 1
}
class "Risk List" as RL {
  Major : 0
  Minor : 1
  Open : 1
}
class "Design Model" as DM {
  Major : 0
  Minor : 1
  Open : 1
}
class "Development Case" as DC {
  Major : 0
  Minor : 2
  Open : 2
}
class "System Inventory" as SI {
  Major : 0
  Minor : 0
  Open : 0
}
class "Iteration Plan" as IP {
  Major : 0
  Minor : 0
  Open : 0
}

note bottom of SS
  One file, one fact, three artifacts:
  appsettings.Development.json carries a
  RateLimiting section at 50/50/50, and this
  artifact, the SAD and the Deployment Model
  each state that no such section exists.
end note
note bottom of SAD
  The SAD's second defect is not this file at all:
  it is the Supplementary Specification's R4, which
  the SAD already states correctly at P6.
end note
note bottom of UCM
  The one Major is a trace-gap: three
  EP-003 edges still marked SUSPECT in the
  registered graph at phase close.
end note
note bottom of SI
  Zero findings. Coverage arithmetic, the
  21-edge anomaly count and Document Control
  all reproduce; System Inventory#F3 resolved.
end note
note bottom of IP
  Zero findings. Every exit criterion is
  certified on its own artifact's evidence
  and no row claims a correction it lacks;
  Iteration Plan#F3 resolved.
end note

SS --> SAD : same defect, two artifacts
SS --> DEP : same defect, third artifact
@enduml
```

#### Supplementary Specification

**Major** — `Supplementary Specification#F1`, criterion `consumed-defect`. The artifact states four times that no `RateLimiting` configuration section exists and that the code's defaults of 100 / 100 per 10 s / queue 100 are therefore the effective values: mechanism M3 ("no such section exists in the delivery, so these defaults are the effective values"), S2 ("a `RateLimiting` configuration section that does not exist in the delivery ... none is externally tunable as delivered"), P1 ("100 tokens per caller per 10-second period with a queue of 100") and R8. `Todo.Api/appsettings.Development.json` carries exactly such a section at `TokenLimit` 50, `TokensPerPeriod` 50 and `QueueLimit` 50, and both launch profiles set the environment to Development — so the effective budget in the only environment this delivery starts in is half the stated value. The recovery already knows this: the System Inventory records it as AN-024 and the Risk List carries it as R025. The defect reaches the Software Architect, who repeats the figure in SP1 and M3, and the Deployment Model, which copies it into its environment table; any load or throttling reading taken from this artifact is off by a factor of two. **Remediation:** state both values — the code defaults from `RateLimitExtensions.cs:14-31` and the Development override from `appsettings.Development.json:8-12` — in M3, S2, P1 and R8, and cite AN-024 so the three artifacts carry one fact under one identifier.

**Major** — `Supplementary Specification#F2`, criterion `consumed-defect`. R4 reads "No retry, circuit breaker or fallback is configured on either hop." `TodoApp.ServiceDefaults/Extensions.cs:32-42` calls `ConfigureHttpClientDefaults` with `AddStandardResilienceHandler()`, which applies the standard retry, circuit-breaker, timeout and rate-limiter pipeline to every container-built `HttpClient` — and the BFF's `AuthClient` is one, registered at `Todo.Web/Server/Program.cs:23-26`. Only the YARP forwarder carries a default `ForwarderRequestConfig` and no handler. The Software Architecture Document records exactly this at its Process View P6 and states it does not edit this artifact because the System Analyst owns it, so the correction is owed here. A role reading R4 concludes neither hop retries: wrong on the sign-in and registration path, right on the task path, and the asymmetry the architecture recovered is lost. **Remediation:** replace R4 with the two hops stated apart, citing `TodoApp.ServiceDefaults/Extensions.cs:32-42`, `Todo.Web/Server/Program.cs:23-26` and `Todo.Web/Server/TodoApi.cs:12-25`, and record it under AN-023 / R024.

#### Software Architecture Document

**Major** — `Software Architecture Document#F1`, criterion `consumed-defect`. SP1 states "No `RateLimiting` section exists, so these are the effective values and none is tunable as delivered", and mechanism M3 repeats it ("every value bindable from a `RateLimiting` section that does not exist"). The file carries one, at 50 / 50 / 50, and both launch profiles run in Development. The artifact cites its neighbouring anomalies AN-023 and AN-025 but not AN-024, which is the one that records this. This is the copy the Deployment Model's environment table inherits. **Remediation:** correct SP1 and M3 to state both values with their sources and cite AN-024; correct the Quality view's "Availability — bounded load" row so the bound in the measured environment reads 50, not 100.

#### Deployment Model

**Major** — `Deployment Model#F1`, criterion `consumed-defect`. The Environment Mapping preamble states "No environment file in the delivery carries a connection string, a provider credential, a rate-limit value or an address", and the Rate limiting row reads "Code defaults: 100 / 100 per 10 s / queue 100 | Same | No `RateLimiting` section exists anywhere, so the values are not tunable as delivered". `Todo.Api/appsettings.Development.json:8-12` carries the rate-limit values. This is the artifact where the error costs most: the section exists to state what differs between environments, it concludes that one setting separates them, and there are two — the second stated backwards. **Remediation:** narrow the preamble to what is true (no connection string, provider credential or address), and rewrite the Rate limiting row so Development reads 50 / 50 / 50 with its anchor and any other environment reads the code defaults, noting that every launch profile sets Development; cite AN-024 and R025.

#### Use-Case Model

**Major** — `Use-Case Model#F1`, criterion `trace-gap`. Three edges this artifact declares are marked SUSPECT in the registered graph and remain open at the phase close: `EP-003 → UC-006`, `EP-003 → UC-007`, `EP-003 → UC-008`, each «SUSPECT → System Analyst». The Traceability rows assert them and the Survey and every affected flow cite EP-003 — the todo list screen — as the screen an actor enters them through. The edges are substantively right; what is missing is the confirmation that clears the marking. A phase that closes with a suspect trace open leaves the screen route of three of eleven use cases unconfirmed, and the eleven-use-case count gate H4 puts to the stakeholder rests on it. **Remediation:** re-register the three edges as confirmed after checking each — `Todo.Web/Client/Components/TodoList.razor:3-32` carries the new-todo input and the per-row remove control, so it precedes UC-007's and UC-008's step 1, and it is the screen the signed-in shell renders for UC-006's step 1 (`Todo.Web/Server/App.razor:44-52`). Record in the Use-Case Survey beside the three rows why a screen entry point and the forwarded operation differ, so the graph carries the edge and the artifact explains its shape.

**Minor** — `Use-Case Model#F2`, criterion `contained-defect`. The actor-goal matrix and the Source column disagree for two use cases with nothing saying they answer different questions: the matrix draws `A1 --> UC3 : EP-002` and `A1 --> UC4 : EP-001, EP-006`, while the Use-Case Survey gives UC-003 as `EP-007, EP-008, EP-016` and UC-004 as `EP-006`, and the registered graph carries only the latter. The matrix's heading is "with the entry points it uses", which suggests the screen the actor acts on, while Source names the entry point whose code performs the operation. **Remediation:** state the distinction once in the Actors section and relabel the matrix's edges — the actor acts on EP-001 and the POST goes to EP-006 — so two lists answering different questions are visibly doing so.

#### Vision

**Major** — `Vision#F1`, criterion `use-case-shape`. The Features diagram draws two cross-cutting technical mechanisms with use-case notation: `usecase "Start the system and create its schema EP-022" as U12` and `usecase "Observe readiness and liveness EP-020, EP-021" as U13`. Schema migration and health probing are platform mechanisms with no actor goal; the Use-Case Model correctly declines to recover either, and the Supplementary Specification already homes them as M9 and M8. The effect is that the Vision states thirteen use cases in the artifact the stakeholder is asked to confirm at gate H4, while the Use-Case Model, the Iteration Plan's objective O1 and the SAD's Use-Case View all state eleven. The artifact's own note ("this Vision creates none") shows the author saw the problem and drew the shapes anyway. **Remediation:** remove U12, U13 and their package from the diagram, keep the two Features rows re-labelled as platform mechanisms cross-referenced to Supplementary Specification M8 and M9 and to the Use-Case Model's "Not recovered, and why".

#### Risk List

**Minor** — `Risk List#F2`, criterion `contained-defect`. R024's premise reads "The Design Model describes the BFF's two outbound hops as equally protected when they are not". The Design Model does the opposite: its PKG-D3 note reads "A default `ForwarderRequestConfig` and no resilience handler, so this hop neither retries nor breaks the circuit, unlike the `AuthClient` hop", and the SAD states the same at P6. The mitigation therefore names an action two artifacts have already performed, and the risk can never be observed as retired. The underlying anomaly AN-023 is real and correctly anchored; only the sentence about which artifact gets it wrong is wrong. **Remediation:** restate R024 as the risk that a later role assumes the hops are equivalent, and point the mitigation at the artifact that does still carry the open error — the Supplementary Specification's R4.

#### Design Model

**Minor** — `Design Model#F1`, criterion `contained-defect`. The migration-history diagram PD-D3 attributes the unconverted owner key to AN-005: "a row written before migration 3 keeps what it held where the constraint now expects an Id ... AN-005." AN-005's subject is that the test suite builds its schema with `EnsureCreated`; the unconverted owner key is AN-025, and the Risk List carries it correctly as R026 refining AN-025. A reader following the citation from this diagram reaches an anomaly about test coverage rather than about data conversion. **Remediation:** change the PD-D3 citation to AN-025 and keep AN-005 only where the artifact states that the test host builds its schema by `EnsureCreated`.

#### Development Case

**Minor** — `Development Case#F3`, criterion `contained-defect`. Document Control still reads "Phase: Survey", "Status: Draft — produced for the end-of-Survey (SBC) milestone review", "Milestone Target: end-of-Survey (SBC) — not yet achieved", "Iteration: 2, Cycle 1". The project is in Excavation iteration 1 and every other artifact under this review states it. **Remediation:** update the four metadata fields to Excavation iteration 1 and the AR milestone target; the tailoring content is current — both classification verdicts and all six optional triggers were re-evaluated and the Deployment Model's FIRED verdict still holds on its condition.

**Minor, recorded here and carried by another lens** — `Development Case#F2` is the Management Reviewer's finding of the Survey review, and this lens does not close or duplicate it. It stands open: "Roles and Ownership" still reads "Reviewer, CodeReviewer, plus the Configuration Manager's baseline record" and CLS-DC-01 draws no edge into the Review Record from the Management Reviewer, the Business Reviewer or the Review Coordinator. It is named here only because the Iteration Plan's criterion A11 counts it and this review read that row; the finding itself is the Management Reviewer's to reconcile.

#### System Inventory and Iteration Plan — no finding from this lens

Both artifacts were read whole and this lens records nothing against either. The System Inventory's coverage arithmetic reproduces from its own per-area table (84 read, 55 unread of 139), its anomalies carry 21 `DependsOn` edges across twelve entry-point-bearing anomalies matching the Iteration Plan's twelve-row handoff, and its Document Control now names the iteration its content belongs to. The Iteration Plan certifies every exit criterion on the artifact it cites rather than on an adjacent answer, its work items are all stages the phase runs, and its State column states each row's actual outcome. Silence from this lens is approval.

```plantuml
@startuml
title Evidence behind each Major finding - the anchor opened, and the artifact text it contradicts

skinparam shadowing false
skinparam componentStyle rectangle
skinparam wrapWidth 230
left to right direction

package "Code read by this lens" {
  component "Todo.Api/appsettings.Development.json\nRateLimiting { TokenLimit 50,\nTokensPerPeriod 50, QueueLimit 50 }" as CFG
  component "TodoApp.ServiceDefaults/Extensions.cs:32-42\nConfigureHttpClientDefaults\nAddStandardResilienceHandler()" as SD
  component "Todo.Api/Todos/TodoApi.cs:24-73\nfive operations, one ownership predicate\nwritten four times" as TODO
  component "Todo.Web/Client/Components/TodoList.razor:3-32\nnew-todo input, per-row remove control" as LIST
}

package "The artifact text that contradicts it" {
  component "Supplementary Specification\nM3, S2, P1, R8: 'no such section exists'\nfigures 100 / 100 / 100" as SS_A
  component "Supplementary Specification R4\n'no retry, circuit breaker or fallback\nis configured on either hop'" as SS_B
  component "Software Architecture Document SP1, M3\n'No RateLimiting section exists,\nso these are the effective values'" as SAD_A
  component "Deployment Model, Environment Mapping\n'No environment file ... carries a\nrate-limit value' / 'Same'" as DEP_A
  component "Use-Case Model\nTraceability UC-006, UC-007, UC-008\nrows naming EP-003" as UCM_A
  component "Vision, Features diagram\nusecase U12 'Start the system'\nusecase U13 'Observe readiness'" as VIS_A
}

package "The artifact that already holds the correct fact" {
  component "System Inventory AN-024\n'Development configuration halves\nthe request budget'" as SI_1
  component "System Inventory AN-023\n'the two hops are not equally\nprotected'" as SI_2
  component "Risk List R025, R024\ncarry both facts, correctly anchored" as RL
}

CFG --> SS_A : contradicts
CFG --> SAD_A : contradicts
CFG --> DEP_A : contradicts
SD --> SS_B : contradicts
LIST --> UCM_A : the edge is right,\nthe graph still suspects it
TODO --> VIS_A : eleven use cases, not thirteen

SI_1 --> CFG : is the correct statement of
SI_2 --> SD : is the correct statement of
RL --> SI_1 : Refines
RL --> SI_2 : Refines

note bottom of SS_B
  One code fact, three artifacts wrong, and the
  recovery already recorded it as AN-024. The
  correction is the same sentence in three places.
end note
note bottom of VIS_A
  AN-001 and the System Inventory's "Not recovered"
  table both say EP-020 to EP-022 carry no use case;
  the Vision's diagram draws them with use-case
  notation while its own note says they are not.
end note

@enduml
```

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
<!-- review: Survey I2 -->

<!-- review: Survey I2 -->

**Consolidated finding ledger.** Fourteen findings were recorded against the four artifacts by the two executed lenses across the SBC review's two iterations. Ten carry a resolution object and are closed by their recording lens; four are open, all Minor. Counts below are copied from `read_artifact_findings` on each artifact, not from any sentence in a reviewer's narrative.

| Artifact | Key | Lens | Severity | Criterion | Owner | Status | The corrective action |
|---|---|---|---|---|---|---|---|
| Development Case | F1 | Reviewer | Major | consumed-defect | Process Engineer | Resolved | The unsourced enterprise version policy is deleted; "Tool and configuration references" states only what `Directory.Packages.props`, `global.json` and `nuget.config` carry |
| Development Case | F2 | Reviewer | Minor | contained-defect | Process Engineer | Resolved | One role-deltas statement and one CLS-DC-01 diagram retained; the duplicate deleted |
| Development Case | F1 | Management Reviewer | Minor | contained-defect | Process Engineer | Resolved | The same duplication, under the stakeholder's order of 2026-11-23; verified at "Roles and Ownership" |
| Development Case | F2 | Management Reviewer | Minor | contained-defect | Process Engineer | **Open** | The co-owned-artifact sentence and CLS-DC-01 must name Management Reviewer, Business Reviewer and Review Coordinator among the lenses writing into the Review Record |
| System Inventory | F1 | Reviewer | Major | trace-gap | Software Archaeologist | Resolved | AN-021 row reads `DependsOn EP-004, EP-005, EP-007`, matching the diagram and the trace tree |
| System Inventory | F2 | Reviewer | Minor | contained-defect | Software Archaeologist | Resolved | Coverage recommends itself from its own per-area table: 133 files, 79 read, 54 unread; the `docs/` row decided explicitly |
| System Inventory | F3 | Reviewer | Minor | contained-defect | Software Archaeologist | **Open** | Set the Document Control iteration field to 2, Cycle 1 |
| Risk List | F1 | Reviewer | Major | consumed-defect | Project Manager | Resolved | One published word-to-score mapping; all 21 anomaly-derived rows reproduce from it; R004 and R011 land at 4 × 3 = 12 |
| Risk List | F1 | Management Reviewer | Major | exit-criterion-unmet | Project Manager | Resolved | The grant band re-derived from the reconciled exposures; every Significant-band acceptance holds the stakeholder's own answer |
| Iteration Plan | F1 | Reviewer | Major | consumed-defect | Project Manager | Resolved | All twelve entry-point-bearing anomalies named with their 21 edges; the nine with no entry point listed separately |
| Iteration Plan | F2 | Reviewer | Minor | contained-defect | Project Manager | Resolved | Gate H2 placed ahead of the verdict it feeds, in both the coarse roadmap and the critical chain |
| Iteration Plan | F1 | Management Reviewer | Major | exit-criterion-unmet | Project Manager | Resolved | C2 split into C2a and C2b, C6 restated on the reproducible coverage figure, C7 split into carriage and reproducibility |
| Iteration Plan | F3 | Reviewer | Minor | contained-defect | Project Manager | **Open** | Correct the fine-plan State column of rows 4, 5 and 6, or delete the column |
| Iteration Plan | F2 | Management Reviewer | Minor | contained-defect | Project Manager | **Open** | C2b restated as Met on the gate H2 answer, with that answer as its evidence |

Findings on the Iteration Assessment and on the Review Record: none recorded in either iteration.

```plantuml
@startuml
title Consolidated SBC ledger - fourteen findings over two iterations, four open Minors and nothing above them
skinparam shadowing false
skinparam classAttributeIconSize 0
hide empty members
skinparam wrapWidth 240

package "Development Case" {
  class "DC as reviewed" as DC {
    F1 Reviewer Major : resolved
    F2 Reviewer Minor : resolved
    F1 Management Minor : resolved
    F2 Management Minor : open
  }
}

package "System Inventory" {
  class "SI as reviewed" as SI {
    F1 Reviewer Major : resolved
    F2 Reviewer Minor : resolved
    F3 Reviewer Minor : open
  }
}

package "Risk List" {
  class "RL as reviewed" as RL {
    F1 Reviewer Major : resolved
    F1 Management Major : resolved
  }
}

package "Iteration Plan" {
  class "IP as reviewed" as IP {
    F1 Reviewer Major : resolved
    F2 Reviewer Minor : resolved
    F1 Management Major : resolved
    F3 Reviewer Minor : open
    F2 Management Minor : open
  }
}

class "Consolidated totals" as TOT {
  open Critical : 0
  open Major : 0
  open Minor : 4
  resolved by its recording lens : 10
  conflict between lenses : none
}

DC --> TOT
SI --> TOT
RL --> TOT
IP --> TOT
note bottom of TOT
  Open Major is zero from both executed lenses, so the
  milestone is not held by a defect. The four Minors are
  carried into Excavation on the stakeholder's order of
  2026-11-23 that none is left unattended.
end note
@enduml
```

**Cross-lens reconciliation — no conflict, four orderings.**

The two lenses raised no contradictory finding: neither found the other's defect to be absent, no owner received two incompatible instructions, and no defect was recorded twice under different criteria. Where two findings touch one subject, the order of rework was settled — and both orders have since been honoured by the owners:

| Ordering | Findings | Why that order |
|---|---|---|
| Arithmetic before the grant | Risk List#F1 (Reviewer) → Risk List#F1 (Management Reviewer) | The grant band cannot be re-derived from scores that do not reproduce. Both closed in one Project Manager pass |
| Figure before criterion | System Inventory#F2 (Reviewer) → Iteration Plan#F1 (Management Reviewer) on C6 | C6 cites a coverage figure; the figure had to be reproducible first |
| Scores before criterion | Risk List#F1 (Reviewer) → Iteration Plan#F1 (Management Reviewer) on C7 | C7 passed as a counting test while the scores it counted did not reproduce |
| Stakeholder order before the Minor queue | Development Case#F2 (Reviewer) with Development Case#F1 (Management Reviewer) | The duplication was the stakeholder's own order of 2026-11-23 and rose above the un-ordered Minors |

Two findings described one defect each under two keys — `Development Case#F2` with `Development Case#F1`, and `Risk List#F1` with `Risk List#F1 (Management Reviewer)`. One rework pass closed the subject of each pair; each lens closed only its own key, and neither lens closed the other's.

**Priority of what remains — the four open Minors, in the order Excavation should close them.**

| Priority | Finding | Why it ranks here |
|---|---|---|
| 1 | Iteration Plan#F2 (Management Reviewer) | The plan's evidence column currently reads "Not met" on a criterion the stakeholder has answered Yes; it misstates the project's standing to every reader who opens the plan |
| 2 | Iteration Plan#F3 (Reviewer) | The same artifact's State column; the Project Manager corrects both in one turn |
| 3 | Development Case#F2 (Management Reviewer) | The tailoring misdescribes who writes this Review Record — a reader of the tailoring concludes three lenses have no block in the artifact they in fact write |
| 4 | System Inventory#F3 (Reviewer) | Status metadata only; no reader is misled about content |

None of the four holds an exit criterion, blocks a downstream role, or changes the substance of the artifact it sits in. All four are the owners' corrections in Excavation's own iteration, on the stakeholder's order.

**Not findings, and recorded as such.** The absence of a Test Plan, a Data Model and a Glossary is the Development Case's own NOT FIRED verdict on each, checked against its §5.2 condition by both lenses — not a delivery gap. The absence of an Iteration Assessment describing this iteration is correct state at review time. The absence of a token budget, a velocity and a forecast is correct: the project declares no budget and no phase has closed. No SCM condition holds or clears this gate: `ci.yml` does not exist on `main`, no branch of this process exists, no pull request is open and no defect issue is filed — establishing the pipeline is the Integrator's Inception work item, not a Survey defect.

## Resolutions and Actions
### Reviewer lens
<!-- review: Excavation I1 -->

<!-- review: Excavation I1 -->

**Prior findings of this lens, closed this milestone.**

| Finding | Artifact | Resolution | What was checked in the artifact |
|---|---|---|---|
| `System Inventory#F3` | System Inventory | Resolved — the stale Survey-era iteration is gone | Document Control reads "Iteration: Excavation iteration 1, cycle 1", "Status: Draft — produced for the end-of-Excavation (AR) milestone review", "Milestone Target: end-of-Excavation (AR) — not yet achieved". The four artifacts under that Survey review no longer disagree about which iteration's state they record |
| `Iteration Plan#F3` | Iteration Plan | Resolved — the State column states each row's actual outcome against the artifact it names | The section commits to the rule ("no row reads complete whose correction is not in the artifact"); row 9 cites the Document Control correction, verified in the artifact itself; row 10 records `Development Case#F2` as **Not started**, naming the exact sentence that still omits three lenses; rows 11 to 14 read Not started / Queued, matching the review now being taken |

Both were closed by `resolve_artifact_finding` before any new defect was recorded, in the reconciliation state, not in this one. The two Survey Majors this lens recorded — `Development Case#F1` and `Iteration Plan#F1` — were already resolved at the SBC re-take and are not re-opened.

**Open findings this milestone, ordered by what the milestone does with them.**

| Finding | Criterion | Severity | Owner | Action | Holds the milestone |
|---|---|---|---|---|---|
| `Supplementary Specification#F1` | `consumed-defect` | Major | System Analyst | State both rate-limit values with their sources in M3, S2, P1 and R8; cite AN-024 | Yes — the artifact's figures are contradicted by the code |
| `Supplementary Specification#F2` | `consumed-defect` | Major | System Analyst | Replace R4 with the two hops stated apart; cite AN-023 / R024 | Yes |
| `Software Architecture Document#F1` | `consumed-defect` | Major | Software Architect | Correct SP1 and M3; cite AN-024 | Yes — the copy the Deployment Model inherits |
| `Deployment Model#F1` | `consumed-defect` | Major | Software Architect | Narrow the environment preamble; rewrite the Rate limiting row | Yes |
| `Use-Case Model#F1` | `trace-gap` | Major | System Analyst | Re-register the three EP-003 edges as confirmed and explain the screen-versus-operation shape in the Survey | Yes — a suspect trace open at phase close |
| `Vision#F1` | `use-case-shape` | Major | System Analyst | Remove U12 and U13 from the Features diagram | Yes — thirteen use cases where the recovery holds eleven |
| `Use-Case Model#F2` | `contained-defect` | Minor | System Analyst | State the matrix-versus-Survey distinction and relabel the edges | No |
| `Risk List#F2` | `contained-defect` | Minor | Project Manager | Restate R024's premise and point its mitigation at the artifact that still carries the error | No |
| `Design Model#F1` | `contained-defect` | Minor | Designer | Change the PD-D3 citation from AN-005 to AN-025 | No |
| `Development Case#F3` | `contained-defect` | Minor | Process Engineer | Bring the four Document Control fields to Excavation iteration 1 | No |

**One correction, three artifacts.** Four of the six Majors turn on a single file. `Supplementary Specification#F1`, `Software Architecture Document#F1` and `Deployment Model#F1` are the same wrong sentence in three places — the code defaults are not the effective values, because `appsettings.Development.json` overrides all three to 50 and every launch profile runs in Development. The recovery already holds the right answer: the System Inventory records it as AN-024 and the Risk List carries it as R025, in the same phase, correctly anchored. The correction is one fact, and it must land in all three artifacts before the recovered set is put to the stakeholder, because gate H4 asks them to accept figures that are currently off by a factor of two.

`Supplementary Specification#F2` is the fourth: R4 denies a resilience handler the code installs, and the Software Architecture Document already got it right at P6 and said so in the artifact rather than editing one it does not own. That is the right division of ownership; what remains is for the owner to take the correction.

**Actions, and what each requires before the milestone can close.**

1. The three rate-limit corrections and the resilience correction land in the Supplementary Specification, the Software Architecture Document and the Deployment Model, each citing AN-024 or AN-023 so one fact carries one identifier across four artifacts.
2. The three `EP-003` edges are confirmed in the graph and the Use-Case Model explains why a screen entry point and the forwarded operation are both named, so the eleven-use-case count gate H4 puts is unqualified.
3. The Vision's Features diagram carries eleven use cases, matching the Use-Case Model, the Iteration Plan's O1 and the SAD's Use-Case View.
4. The four Minors are corrected in their owners' next turn, after the Majors — `Risk List#F2` and `Design Model#F1` are one-sentence corrections, and `Development Case#F3` is four metadata fields. None holds the milestone.

**Not this lens's to close.** `Development Case#F2` — the contributor set omitting three lenses, which the stakeholder ordered corrected on 2026-11-23 — stays open in the Management Reviewer's ledger. The Iteration Plan records it as outstanding and carries it as `R031`, and criterion A11 reads three of four because of it. This lens neither resolves it nor records a duplicate: a second lens writing its own key against the same defect is what the cross-lens duplicate pattern warns against, and only the lens that emitted a finding may close it.

**Not a finding, and why.** The absence of an Iteration Assessment describing this iteration is correct state — the Project Manager authors it after this review. The absence of a Data Model is the Development Case's NOT FIRED verdict on its trigger, which this lens checked and found to hold: eight persisted entity types, below the >10 threshold, no migration in scope, and the data written inline in the Design Model. The absence of an open pull request is the sprint zero's correct state, not an omission. No finding is recorded for any of the three.

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
<!-- review: Survey I2 -->

<!-- review: Survey I2 -->

**Closed this milestone — ten findings, each by the lens that recorded it, each verified against the artifact section it names.** Closure is a lens's act: a correction stated in an owner's narrative does not close a finding; the recording lens's `resolve_artifact_finding`, called after it re-read the corrected section, does.

| Artifact | Key | Lens | Owner | Closed against |
|---|---|---|---|---|
| Development Case | F1 | Reviewer | Process Engineer | "Tool and configuration references" — no policy asserted, only the pinning files cited, checked against `global.json` and `nuget.config` |
| Development Case | F2 | Reviewer | Process Engineer | "Roles and Ownership" — one CLS-DC-01 diagram, one role-deltas block |
| Development Case | F1 | Management Reviewer | Process Engineer | The same section, verified by this lens against the stakeholder's order of 2026-11-23 |
| System Inventory | F1 | Reviewer | Software Archaeologist | "Traceability" — the AN-021 row against the Anomalies diagram and the registered edges |
| System Inventory | F2 | Reviewer | Software Archaeologist | "Coverage" — the headline recomputed from the per-area table, 79 + 54 = 133 |
| Risk List | F1 | Reviewer | Project Manager | "Risk Classification" and the register's P/I/exposure columns for all 22 rows |
| Risk List | F1 | Management Reviewer | Project Manager | The grant-band table and the four acceptance rows, each carrying the stakeholder's answer |
| Iteration Plan | F1 | Reviewer | Project Manager | "Use Cases and Scenarios Addressed" — twelve anomalies, 21 edges, against the System Inventory |
| Iteration Plan | F2 | Reviewer | Project Manager | The coarse roadmap and the fine-plan critical chain |
| Iteration Plan | F1 | Management Reviewer | Project Manager | "Evaluation Criteria" — C2a/C2b, C6, C7a/C7b |

**Actions carried into Excavation — four, one per open finding, ordered as in Findings.** Each is the remediation its recording lens wrote; none is the coordinator's own instruction of what the defect should be. No deadline column states a calendar date: the sprint zero declares no date beyond the one on this work order, and a projected date computed from an estimate would read downstream as an observation.

| # | Action | Artifact | Owner | Closes | Due |
|---|---|---|---|---|---|
| 1 | Restate C2b as Met — 2026-11-23 and replace its evidence cell with the answer as given: the stakeholder confirmed the four-process perimeter as the System Inventory records it and sanctioned advancing past SBC into Excavation | Iteration Plan | Project Manager | Iteration Plan#F2 (Management Reviewer) | Excavation iteration 1, first turn |
| 2 | Set rows 4 and 5 of the fine plan to Complete with what closed each, row 6 to In progress until the lens returns — or delete the State column and leave progress to the Iteration Assessment | Iteration Plan | Project Manager | Iteration Plan#F3 (Reviewer) | Excavation iteration 1, first turn, with action 1 |
| 3 | Name every lens that writes into the Review Record in the co-owned-artifact sentence — Reviewer, Management Reviewer, Business Reviewer, Review Coordinator, Code Reviewer, plus the Configuration Manager's baseline record — and draw the corresponding edges in CLS-DC-01 | Development Case | Process Engineer | Development Case#F2 (Management Reviewer) | Excavation iteration 1 |
| 4 | Set the Document Control iteration field to the iteration the content belongs to, matching the three other artifacts under review | System Inventory | Software Archaeologist | System Inventory#F3 (Reviewer) | Excavation iteration 1 |

```plantuml
@startuml
title Finding lifecycle - where the four open Minors stand and who closes each
skinparam shadowing false
skinparam wrapWidth 240

[*] --> Open : lens records it via record_artifact_finding
Open --> Assigned : owner named from the lens Remediation
Assigned --> InProgress : owner reworks the artifact
InProgress --> Resolved : owner states the corrective action done
Resolved --> Verified : the SAME lens re-reads the artifact
Verified --> Closed : resolve_artifact_finding accepted
Resolved --> Open : lens finds the defect still stands

state "Escalated - overdue" as Esc
Open --> Esc : deadline missed by more than 1 business day
Assigned --> Esc : no owner action by deadline
Esc --> Assigned : Project Manager assigns, or CCB opens a CR

state "Carried into Excavation" as CAR
note bottom of CAR
  Development Case#F2 (Management Reviewer)
  Iteration Plan#F2 (Management Reviewer)
  System Inventory#F3 (Reviewer)
  Iteration Plan#F3 (Reviewer)
  Each is corrected by its owner in Excavation's
  own iteration, on the stakeholder's order of
  2026-11-23 that no Minor is left unattended.
end note

Open --> CAR : Minor, ordered corrected in the next phase
note right of Open
  At this milestone: 4 open, all Minor.
  Open Critical 0, open Major 0 from both
  executed lenses.
end note
@enduml
```

**Closure procedure.** Each of the four closes only when its recording lens re-reads the corrected artifact and calls `resolve_artifact_finding` on that key. Two of the four sit on the Iteration Plan under different lenses: `Iteration Plan#F2` is the Management Reviewer's to close and `Iteration Plan#F3` the Reviewer's, and one Project Manager turn satisfies both subjects. A finding still open at the AR milestone becomes a Major finding against the artifact carrying it — criterion `contained-defect`.

**Escalation channel.** A finding past its due point by more than one business day escalates to the Project Manager in writing, with the ledger entry as evidence. A defect that reappears across artifacts as a process failure escalates to the Configuration and Change Management Board. The coordinator surfaces these; it does not correct them.

**No change request is opened for any of the four.** The Change Control Manager does not work in the sprint zero — no ledger exists and no CR is opened before Inception. The stakeholder's order reaches its owners through this record and through their Work Order, which is the route the sprint zero provides. Nothing in this iteration orders a change to declared scope.

**The stakeholder's order, recorded and acted on.** Answering gate H2 on 2026-11-23: "Yes, let's move on to the next phase. Minor findings should also be addressed during the next phase—let's not leave them unattended." It is folded in as `Stakeholder finding` — verified against the ledger rather than deferred: the four open Minors are exactly the items the order names, all four are assigned with an owner and a due point in Excavation's first iteration, and none is recorded as closed or deferred. No new defect is minted for the order, because every item it names is already in the ledger. The first half of the answer is the sanction, recorded in Disposition.

## Disposition
### Reviewer lens
<!-- review: Excavation I1 -->

<!-- review: Excavation I1 -->

**Disposition: Approved with Changes.** Six Major, four Minor. The six Majors are open and hold the AR milestone; the four Minors do not.

**What the recovered set establishes, and why it is approved rather than rejected.** The phase's real work is sound. Eleven use cases are recovered from twenty-two entry points, each citing the `EP-NNN` whose code performs it, and the entry points that carry none — `EP-020`, `EP-021`, `EP-022` and the `admin` branch — are accounted for with a reason, not dropped. Twenty-two components are recovered with their anchors, each technology declared in the artifact exists in a manifest, and the components realize the use cases whose paths they carry. The persistent store is recovered to the level of keys, indexes, referential actions and the seven rules the schema leaves to code. The System Inventory's coverage reproduces from its own table, its twenty-one anomaly edges reproduce from its own rows, and both the Risk List and the Iteration Plan certify their claims on the artifact each cites rather than on an adjacent answer. Nothing in this lens's read found a recovered element resting on an anchor that does not say what the element claims, except in the four cases recorded as Majors — and those are figures copied from one mechanism's description, not the recovery's structure.

The two contradictions are the reason this is Approved with Changes and not Approved. They are narrow and they are fully diagnosed: one code file contradicts three artifacts' statement of a value, and one service-defaults file contradicts one artifact's statement of a capability. The recovery already contains the correct answer to both, recorded as AN-024 and AN-023 in the same phase. That is why the disposition is rework rather than rejection — the artifacts do not need re-deriving, they need one fact corrected in three places and one sentence corrected in a fourth.

**What the milestone must not do while the Majors stand.** Gate H4 asks the stakeholder to accept the recovered use cases, architecture and data as the models of the existing system. They cannot be asked to accept a set whose stated request budget is double the value the system runs at, whose failure-handling claim about the task path is right and about the sign-in path wrong, whose use-case count is thirteen in one artifact and eleven in three others, and three of whose screen routes rest on trace edges the graph still marks suspect. Each of those is a question the stakeholder would be answering on wrong content.

```plantuml
@startuml
title Disposition of the ten artifacts - what this lens approves, what it holds, and why

skinparam shadowing false
skinparam componentStyle rectangle
skinparam wrapWidth 225
left to right direction

package "Approved from this lens - silence is approval" {
  component "System Inventory\nno finding\ncoverage and edge counts reproduce" as OK1
  component "Iteration Plan\nno finding\neach criterion on its own evidence" as OK2
}

package "Approved with Changes - Minors only, do not hold" {
  component "Risk List\nF2 Minor" as M1
  component "Design Model\nF1 Minor" as M2
  component "Development Case\nF3 Minor" as M3
}

package "Held - Major open, rework before H4" {
  component "Supplementary Specification\nF1 Major - rate-limit values\nF2 Major - resilience claim" as H1
  component "Software Architecture Document\nF1 Major - rate-limit values" as H2
  component "Deployment Model\nF1 Major - environment mapping" as H3
  component "Use-Case Model\nF1 Major - three suspect edges\nF2 Minor" as H4
  component "Vision\nF1 Major - thirteen use cases" as H5
}

package "Carried by another lens, not this one" {
  component "Development Case#F2\nManagement Reviewer's finding\nIteration Plan A11 reads 3 of 4" as OTHER
}

OK1 --> H1 : AN-024 is the correct\nstatement H1 contradicts
OK2 --> H5 : eleven use cases,\nas O1 states
H1 --> H2 : same fact
H1 --> H3 : same fact
H2 --> H4 : the count H4 puts to the gate

note bottom of H1
  One file, one fact, three artifacts. The
  correction is the same sentence three times,
  and the recovery already holds it as AN-024.
end note
note bottom of OTHER
  Only the lens that emitted a finding may
  resolve it. This lens records nothing
  against it and does not duplicate the key.
end note

@enduml
```

**What the milestone verdict may rely on from this lens.** Zero Critical: nothing in this review needs a decision only the stakeholder can take. The four stakeholder rulings that shaped the recovery — the provider path recovered as unreachable, the `admin` branch as an exceptional entity, the priority order standing, the perimeter confirmed — are recorded where they bite, in the System Inventory's Perimeter, the Use-Case Model's "Not recovered, and why", the Vision's Assumptions and the Risk List's grant table, each quoting the answer rather than paraphrasing a process decision. This lens found no element promoted to declared scope, no cross-cutting mechanism recovered as a use case except the two the Vision's diagram draws and `Vision#F1` records, and no recovered element with no anchor.

**The lens's own limit, stated so the coordinator can weigh it.** This review opened five anchors and two contradicted their citing artifacts. It did not open every anchor in ten artifacts — that is not possible within one pass and the Software Archaeologist's own reading is what the coverage section measures. What this lens did establish is that where the recovery and the code disagree, the disagreement is discoverable by opening the file the artifact names, and that in the two cases found the recovery's own anomaly register already knew the answer. That is the healthiest signal in this review: the reading is honest about the system even where the artifacts built on it are not yet.

**Verdict recorded.** Approved with Changes, with the six Majors holding the AR milestone. Gate H4 is not put by this lens — it follows the lenses' ruling, and the ruling is that the corrections land first.

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
