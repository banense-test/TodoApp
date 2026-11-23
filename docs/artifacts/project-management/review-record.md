## Document Control
### Reviewer lens
<!-- review: Survey I1 -->

- Phase: Survey
- Status: Technical lens complete for the SBC milestone review. Seven findings recorded: 0 Critical, 4 Major, 3 Minor, 0 Info. Disposition — Approved with Changes.
- Milestone Target: end-of-Survey (SBC) — not yet achieved; the four Major findings require rework before any role consumes these artifacts.
- Iteration: 1, Cycle 1
- Owner: Reviewer

### Management Reviewer lens
<!-- review: Survey I1 -->

<!-- review: Survey I1 -->

- Phase: Survey
- Status: Management lens complete for the SBC milestone review. Three findings recorded by this lens: 0 Critical, 2 Major, 1 Minor. Disposition — No-Go. Stakeholder sanction REFUSED on 2026-11-23.
- Milestone Target: end-of-Survey (SBC) — not achieved; the sanction was withheld and six Major findings stand across the four artifacts under review.
- Iteration: 1, Cycle 1
- Owner: Management Reviewer

## Review Scope and Criteria
### Reviewer lens
<!-- review: Survey I1 -->

**Review type.** Milestone review, technical lens, at the SBC (end-of-Survey) review point. The question applied is exit criteria: whether the four artifacts collectively satisfy the conditions for transition into Excavation — not whether the iteration's objectives were completed.

**Artifacts under review.** Development Case (Process Engineer), System Inventory (Software Archaeologist), Risk List (Project Manager), Iteration Plan (Project Manager). All four are the artifacts the SBC inventory carries; the Review Record is this lens's own output.

**Checklist applied.** Per artifact type: Environment tailoring → DC Baseline Conformance and Optional Trigger Justification against the IARI baseline held in this prompt. Recovery → EVIDENCE, the Survey lens: every fact about an existing system must rest on the file it cites, so the anchors were opened rather than trusted. Project Management → the IARI risk scale, the two-currency rule, and the phase's exit criteria.

**Method.** All 41 registered trace edges were read. The perimeter and anomaly anchors were opened in the repository: `Todo.Api/Program.cs`, `Todo.Api/Todos/TodoApi.cs`, `Todo.Api/Todos/Todo.cs`, `Todo.Api/Users/UsersApi.cs`, `Todo.Api/Authorization/CurrentUser.cs`, `Todo.Api/Extensions/RateLimitExtensions.cs`, `Todo.Api/TodoDbContext.cs`, `Todo.Web/Server/AuthApi.cs`, `Todo.Web/Server/AuthClient.cs`, `Todo.Web/Server/Program.cs`, `Todo.Web/Server/TodoApi.cs`, `Todo.Web/Server/Authentication/AuthenticationExtensions.cs`, `Todo.Web/Server/appsettings.json`, `Todo.Web/Server/Todo.Web.Server.csproj`, `Todo.Web/Client/TodoList.razor`, `Todo.Web/Client/TodoClient.cs`, `Todo.Web/Client/TodoApp.razor`, `Todo.Web/Client/Components/LogInForm.razor`, `Todo.Web/Server/App.razor`, `Todo.Web/Shared/SharedClass.cs`, `Todo.Api.Tests/TodoApplication.cs`, `Todo.Api.Tests/TokenService.cs`, `Todo.Api.Tests/Todo.Api.Tests.csproj`, `TodoApp.AppHost/Extensions.cs`, `.devcontainer/devcontainer.json`, `Directory.Build.props`, `global.json`, `README.md`, `Requests/todo.http`, `docs/CONTRIBUTING.md`, `.iari/README.md`.

**Anchor verdict.** Every load-bearing anchor states what the artifacts claim it states, including the claims that carry the most risk: the admin branch at `TodoApi.cs:33,59,69` with nothing granting the role, `AuthApi.cs:55-62` taking the provider name straight from the route, `AuthApi.cs:64-97` redirecting to `/` on every path, `UsersApi.cs:16`'s own service-to-service auth TODO, the two `/todos` policies in `Program.cs` versus `UsersApi.cs:10-20`, `TodoList.razor:24-27`'s unbound checkbox, and `.devcontainer/devcontainer.json`'s SDK 8.0 image against `net10.0` — the target in `Directory.Build.props` being `net9.0` and the pin `9.0.100`. No finding is raised against the reading's accuracy. Every finding below sits in a count, an edge, a score or an unsourced assertion.

**SCM evidence.** No open pull requests exist, so nothing is disposed in this review. The repository carries no IARI pipeline file on `main`: the build environment is the Integrator's Inception work item and no branch or build of this process exists yet. No red build and no open pull request is therefore a finding, and no phase-discipline defect is available to detect.

```plantuml
@startuml
title Compliance matrix — the four SBC artifacts against the Reviewer checklist

skinparam classAttributeIconSize 0
skinparam shadowing false
hide empty members

package "Development Case — tailoring" {
  class "Development Case" as DC {
    dc-baseline / roster 24 work, 2 declared inactive : Pass
    dc-baseline / 16 CORE produced, none omitted : Pass
    dc-baseline / ownership unchanged : Pass
    dc-baseline / nothing outside CORE and OPTIONAL : Pass
    optional-trigger / Deployment Model fired, condition holds : Pass
    optional-trigger / 5 not fired, each condition checked : Pass
    consumed-defect / every governing statement sourced : FAIL
    contained-defect / one fact stated once : FAIL
    Document Control current : Pass
    UML present and valid : Pass
  }
}

package "System Inventory — recovery" {
  class "System Inventory" as SI {
    every perimeter component anchored : Pass
    every external system anchored : Pass
    every entry point has kind, initiator, anchor : Pass
    size and file counts anchored : Pass
    every unread area declared with its reason : Pass
    coverage arithmetic equals the per-area table : FAIL
    anomalies anchored and carried as risks : Pass
    anomaly edges equal the trace tree : FAIL
    documentation checked claim by claim : Pass
    trace table complete for EP and AN : Pass
    UML present and valid : Pass
  }
}

package "Risk List — scoring" {
  class "Risk List" as RL {
    the IARI scale, none of its own : Pass
    magnitude is the band of P x I, never chosen : Pass
    all 21 anomalies carried : Pass
    scores agree with the inventory likelihood and impact : FAIL
    Significant accepts granted by the stakeholder : Pass
    each risk has strategy, owner, action, contingency : Pass
    no human-team unit anywhere : Pass
    trace table complete for R001 to R022 : Pass
    UML present and valid : Pass
  }
}

package "Iteration Plan — sequencing" {
  class "Iteration Plan" as IP {
    each objective has a satisfied-when and an owner : Pass
    no calendar date projected : Pass
    milestone sequence matches the inherited process : Pass
    every risk lands on a milestone : Pass
    work items are stages the process runs in Survey : Pass
    roles working match the Development Case : Pass
    anomaly handoff agrees with the System Inventory : FAIL
    gate position agrees with the recorded answer : FAIL
    exit criteria stated and evidenced : Pass
    UML present and valid : Pass
  }
}

DC --> SI : consumed by Excavation
SI --> RL : anomalies scored
RL --> IP : risks sequence the plan
IP --> DC : roles and gates
@enduml
```

## Findings
### Reviewer lens
<!-- review: Survey I1 -->

```plantuml
@startuml
title Defect distribution — Reviewer lens findings by severity and artifact, SBC review

skinparam shadowing false
skinparam classAttributeIconSize 0
hide empty members

class "Development Case" as DC {
  Critical : 0
  Major : 1
  Minor : 1
}
note right of DC
  Major - consumed-defect
  an enterprise version policy asserted
  that no file records
  Minor - contained-defect
  one diagram and one delta list twice
end note

class "System Inventory" as SI {
  Critical : 0
  Major : 1
  Minor : 1
}
note right of SI
  Major - trace-gap
  AN-021 row holds two edges,
  the artifact and the tree hold three
  Minor - contained-defect
  coverage headline unreproducible
end note

class "Risk List" as RL {
  Critical : 0
  Major : 1
  Minor : 0
}
note right of RL
  Major - consumed-defect
  13 of 21 scores contradict the
  inventory, two below the grant band
end note

class "Iteration Plan" as IP {
  Critical : 0
  Major : 1
  Minor : 1
}
note right of IP
  Major - consumed-defect
  twelve anomalies claimed, seven named
  Minor - contained-defect
  the gate drawn after the verdict it feeds
end note

class "Total for this lens" as TOT {
  Critical : 0
  Major : 4
  Minor : 3
  Info : 0
  Findings : 7
}

DC ..> TOT
SI ..> TOT
RL ..> TOT
IP ..> TOT
@enduml
```

#### Development Case

Two findings. The tailoring verdicts themselves hold: two disciplines inactive each with its own recorded condition (`business-process-led = false`, `real-time-system = false`), 24 roles working, no CORE artifact omitted or reassigned, nothing listed outside the CORE + OPTIONAL universe, and the one fired OPTIONAL — Deployment Model — justified by a genuinely distributed four-process topology with a YARP proxy hop and per-process configuration pairs. The five NOT FIRED verdicts were each checked against its §5.2 condition and each holds: eight entity types is below the Data Model threshold, the architecture already runs so no mechanism needs empirical validation, no regulator or contract consumes test reporting, no UX decision waits on the stakeholder, and the vocabulary is plain English.

- **Development Case#F1 — Major, `consumed-defect`.** The "Tool and configuration references" section asserts that an enterprise version policy "is recorded with the process and is anchored by the Software Architect in the Software Architecture Document" and that "it governs over the registry's latest for every package the delivery adds". `docs/CONTRIBUTING.md` records central pinning in `Directory.Packages.props` and the nuget.org-only source rule; neither states a rule preferring a pinned version over a registry's latest, and no file in the tree records such a policy. The Software Architect is directed in Excavation to anchor a document that does not exist. **Remediation:** name the file that records the policy, or replace the sentence with what is true — version selection follows central pinning, nuget.org being the only configured source.

- **Development Case#F2 — Minor, `contained-defect`.** The role deltas are stated twice inside "Roles and Ownership" and the CLS-DC-01 role-artifact diagram is embedded twice, verbatim. **Remediation:** keep one statement of the deltas and one CLS-DC-01 diagram; delete the duplicate.

#### System Inventory

Two findings. The recovery itself is the strongest artifact of the four: 22 entry points each with kind, initiator and file anchor; 19 perimeter components and 9 external systems each anchored; every anomaly row carrying evidence with line numbers; and a Coverage section that declares its unread remainder and why rather than leaving it implicit. The two stakeholder decisions of 2026-11-23 are carried consistently into the Perimeter prose, the Perimeter diagram notes and the affected entry-point rows — the external-provider path as a recovered use case marked unreachable, the admin branch as an exceptional entity. No `[DERIVED]` or `[SCOPE_QUESTION]` marker survives an answered question.

- **System Inventory#F1 — Major, `trace-gap`.** The Traceability row for AN-021 reads `DependsOn EP-004, EP-005`. The artifact's own Anomalies diagram carries `A21 --> E4`, `A21 --> E5` and `A21 --> E7`, and the registered trace tree carries the same three edges. The row registers two of the three the artifact and the tree hold. **Remediation:** add EP-007 to the AN-021 row.

- **System Inventory#F2 — Minor, `contained-defect`.** Coverage states "77 were opened" of 129, while the per-area Read column sums to 76 (23+7+8+0+14+1+6+2+1+7+1+2+1+1+1+1), and the docs row records `3 | 1` beside a note saying all three were opened. The Iteration Plan cites the derived figure — "52 files unread of 129" — as criterion C6's evidence. **Remediation:** recompute the headline from the per-area table, decide explicitly whether the two artifact files under `docs/` count as read, and make the column and the headline agree.

#### Risk List

One finding. The register's structure is sound: the IARI scale is reproduced from the baseline and no scale of its own is defined, magnitude is derived as the band of exposure rather than chosen, all 21 anomalies are carried with an explicit note explaining the 22nd risk's separate origin, every row names a strategy, an owner, an action, a contingency and a warning sign, and the two Significant accepts carry the stakeholder's grant in their own words. No person-week, person-month or story-point unit appears anywhere.

- **Risk List#F1 — Major, `consumed-defect`.** Thirteen of the twenty-one rows score a risk differently from the likelihood and impact the System Inventory states for the same anomaly, and the same inventory word scores differently in different rows: "likely / moderate" gives 4×3 for AN-001 but 4×2 for AN-003 and AN-011; "likely / low" gives 4×1 for AN-006 and AN-008 but 2×2 or 4×2 for AN-013, AN-014, AN-015, AN-017 and AN-019; "possible / high" becomes 2×3 for AN-002. The consequence is not cosmetic. AN-004's "likely / moderate" would place R004 at exposure 12 — the Significant band whose acceptance is the stakeholder's to grant — where it is recorded 2×2 and accepted by the Project Manager; the same applies to R011. The magnitudes then sequence the Iteration Plan's milestones and underlie the same grant band the stakeholder's R012 and R016 accepts came from. **Remediation:** score each risk once from the IARI scale and reconcile it against the inventory's column, or delete the inventory's likelihood and impact as a scoring claim and state that the score is the Project Manager's own reading of the cited evidence. Where a reconciled score lands in the Significant or High band, put that acceptance to the stakeholder in this iteration — R004 and R011 are the candidates.

#### Iteration Plan

Two findings. The plan is otherwise conformant to the process it must instantiate: the milestone sequence runs Survey → Excavation → Consolidation → Inception → Elaboration → Construction → Transition, every discipline intensity quoted matches the canonical matrix, the roles recorded as working in this iteration are exactly those the Survey row of the inherited process names plus its three reviewing roles, every work item is a stage that process actually runs in Survey, no calendar date is projected from an estimate, and the two currencies are kept apart with the human gate bounded as R022 rather than estimated.

- **Iteration Plan#F1 — Major, `consumed-defect`.** "Use Cases and Scenarios Addressed" states that "the 12 anomalies that sit on an entry point" are handed to Excavation and then names seven: AN-001, AN-002, AN-004, AN-018, AN-019, AN-020, AN-021. AN-008, AN-009, AN-010, AN-015 and AN-017 are dropped, and they are the ones constraining the reference-UI, Identity, key-ring and app-host reading — priorities 6 and 8 of the order Excavation reads in. Excavation is told a count and handed a list that does not match it. **Remediation:** name all twelve, or drop the enumeration and point at the System Inventory's Anomalies table as Excavation's constraint list.

- **Iteration Plan#F2 — Minor, `contained-defect`.** The critical-chain activity diagram places Gate H1 after the Review Coordinator's verdict, while the coarse roadmap, exit criteria C2/C5/C8 and the H1 row all record the gate answered on 2026-11-23 ahead of the review. **Remediation:** move Gate H1 ahead of the Reviewer in the diagram.

```plantuml
@startuml
title Where each open Major lands — the artifact that carries it and the role that inherits it

skinparam shadowing false
skinparam componentStyle rectangle
left to right direction

package "Carries the defect" {
  component "Development Case" as DC
  component "System Inventory" as SI
  component "Risk List" as RL
  component "Iteration Plan" as IP
}

package "Open Major" {
  component "Development Case#F1\nan enterprise version policy\nno file records" as DC1
  component "System Inventory#F1\nAN-021 row short of\nthe tree by one edge" as SI1
  component "Risk List#F1\n13 scores contradict\nthe inventory's own words" as RL1
  component "Iteration Plan#F1\ntwelve anomalies claimed,\nseven named" as IP1
}

package "Inherits it, and when" {
  component "Software Architect\nExcavation — anchors a policy\nthat exists nowhere" as ARC
  component "System Analyst\nExcavation — reads the anomaly\ntable as its constraint list" as SYA
  component "Project Manager\nthis iteration — a grant band\nbelow the stakeholder's reach" as PM
  component "System Analyst\nExcavation — five constraints\nnot handed over" as SYA2
}

DC --> DC1
SI --> SI1
RL --> RL1
IP --> IP1
DC1 --> ARC
SI1 --> SYA
RL1 --> PM
IP1 --> SYA2
@enduml
```

## Resolutions and Actions
### Reviewer lens
<!-- review: Survey I1 -->

**Prior findings of this lens.** None. This is iteration 1 of Survey and no finding of the Reviewer lens existed on any of the four artifacts before this review, so nothing is resolved, deferred or rejected in this pass.

**Actions ordered by this review.** Each is the remediation of a finding above, and each is closed by the same lens that raised it in the next pass.

| Action | Artifact | Owner | Finding |
|---|---|---|---|
| Name the file recording the version policy, or replace the claim with central pinning and nuget.org-only | Development Case | Process Engineer | Development Case#F1 |
| Delete the duplicated role-delta list and the duplicated CLS-DC-01 diagram | Development Case | Process Engineer | Development Case#F2 |
| Add EP-007 to the AN-021 Traceability row | System Inventory | Software Archaeologist | System Inventory#F1 |
| Recompute Coverage from the per-area table; settle whether the `docs/` rows count as read | System Inventory | Software Archaeologist | System Inventory#F2 |
| Reconcile every probability and impact against the inventory, or state the score is the Project Manager's own reading; put any Significant or High acceptance to the stakeholder | Risk List | Project Manager | Risk List#F1 |
| Name all twelve entry-point-bearing anomalies, or point at the Anomalies table | Iteration Plan | Project Manager | Iteration Plan#F1 |
| Move Gate H1 ahead of the Reviewer in the critical-chain diagram | Iteration Plan | Project Manager | Iteration Plan#F2 |

**Not a finding.** The absence of a Test Plan, a Data Model and a Glossary is the Development Case's own NOT FIRED verdict on each, checked and found to hold — not a gap in the delivery. The absence of an Iteration Assessment is correct at this point: the Project Manager authors it after this review, and its absence is never a gate condition.

## Disposition
### Reviewer lens
<!-- review: Survey I1 -->

**Approved with Changes.**

No Critical finding was raised: nothing in these four artifacts needs a decision only the stakeholder can take, and the two decisions this iteration did need — the priority order, and the R012 and R016 acceptances — were already answered on 2026-11-23. The three Minor findings are recorded for their owners' next turn and do not hold the milestone.

The four Major findings do. Each is content another role builds on: the Software Architect is directed to a policy no file records, the System Analyst is handed a constraint list five short of the count stated beside it, and the magnitudes sequence the milestones on scores that cannot be reproduced from their stated inputs. The SBC milestone is therefore not sanctioned by this lens until those four are reworked and this review re-runs against them. Excavation reads the recovered perimeter, not these corrected assertions, so it may proceed in parallel only on the reading itself.
