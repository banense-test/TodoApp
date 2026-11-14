## Document Control
### Reviewer lens
<!-- review: Survey I1 -->

Phase: Survey
Status: Draft — technical lens of the SBC review recorded; 7 findings (3 Major, 4 Minor, 0 Critical) on 4 artifacts
Milestone Target: End-of-Survey (SBC) — not yet achieved

## Review Scope and Criteria


## Findings
### Reviewer lens
<!-- review: Survey I1 -->

#### Development Case

Reviewed at SBC. Environment discipline, Survey. Verdict: Approved with changes — one Major, one Minor.

| Checklist item | Verdict |
|---|---|
| Baseline conformance: roster, CORE set, ownership unchanged | Pass |
| Every FIRED optional trigger holds its own §5.2 condition | Pass |
| Every cited tool reference resolves in the tree | Fail — F1 |
| UML notation fits what it expresses | Fail — F2 |
| Classification deltas carry a basis | Pass |
| No forbidden override present | Pass |

##### All six optional verdicts audited against their conditions

Each verdict is an auditable claim, so each was checked against the project's real facts rather than accepted:

| Optional | Verdict | Audit result |
|---|---|---|
| Deployment Model | FIRED | Holds. Four processes — `Todo.Api`, `Todo.Web.Server`, `Todo.Web.Client`, `TodoApp.AppHost` — with YARP forwarding and service discovery between them. A genuine distributed topology, not a single node. |
| Data Model | NOT FIRED | Holds. `TodoDbContextModelSnapshot.cs` declares 8 tables — `Todos`, `AspNetUsers` and 6 Identity framework tables — so both the ">10 entities" and "data-centric" limbs fail; no production data and no migration in scope, so the third limb fails too. |
| Architectural Proof-of-Concept | NOT FIRED | Holds for the sprint zero. The condition requires Elaboration *and* a scored risk; the Risk List post-dates this artifact in the same iteration and Proof-of-Concept is excluded from sprint zero by the process. Correctly deferred, not dismissed. |
| User-Interface Prototype | NOT FIRED | Holds. A working Blazor UI exists in `Todo.Web` and no new UI is declared. |
| Test Plan | NOT FIRED | Holds. MIT sample code, no audit obligation, no contractual test reporting. |
| Glossary | NOT FIRED | Holds. The domain vocabulary is `Todo`, `IsComplete`, `Owner` — fixed by the recovered schema. |

##### Classification and disciplines

`business-process-led = false` is correctly derived — `Todo` carries `Title`, `IsComplete`, `OwnerId` and no policy. `real-time-system = false` follows from a request/response pipeline with no hosted service (`Todo.Api/Program.cs`, read in full: no `IHostedService`, no timer). Business Modeling declared INACTIVE on the correct trigger; Capsule Designer and Business Reviewer stood down consistently with it. All other disciplines at canonical matrix intensities, with no self-granted deviation.

##### F1 — Major — Tool references cites a file that does not exist

The row `| Coding standard and review conventions | CONTRIBUTING.md | Software Architect, with the Code Reviewer |` sends two roles to a document the repository does not contain. A read of `TodoApp/CONTRIBUTING.md` returns "was not found" and the tree carries no such entry.

The consequence is not cosmetic: this artifact is the process authority both the Software Architect and the Code Reviewer read, and it tells them their coding standard lives elsewhere. The System Inventory already records the absence and the Risk List carries it as R006 with the correction due at LCO — but the misdirection is in the artifact now, and LCO is two milestones away. Recommendation: replace the row with what actually governs — `Directory.Build.props` (nullable, implicit usings, `LangVersion preview`) and `Directory.Packages.props`, owner Software Architect — and author a written standard through a Change Request if one is wanted.

##### F2 — Minor — Ownership drawn with class elements and association arrows

`class "ProcessEngineer" as PE` … `PE --> DC : owns` models role-to-artifact ownership as an association between two classes. Ownership is not a class relationship, and the ownership table beneath the diagram states it correctly and unambiguously. Already carried as R025. The artifact is approved by default on this finding; it does not hold the milestone.

```plantuml
@startuml
title Development Case — compliance of the tailoring decisions, section by section
skinparam shadowing false
skinparam componentStyle rectangle

package "Checked and passing" {
  component "Tailoring Overview\nclassification basis stated" as P1
  component "Disciplines and Intensity\ncanonical, no self-granted delta" as P2
  component "Artifacts and Templates\nUC enumeration rule correct" as P3
  component "Optional Artifact Triggers\n6 of 6 audited against conditions" as P4
  component "Roles and Ownership\nstood-down roles consistent" as P5
  component "Version policy\nnet9.0 and SDK 9.0.100 verified" as P6
}

package "Findings" {
  component "Tool references\nCONTRIBUTING.md absent" as F1
  component "Roles and Ownership\nclass notation for ownership" as F2
}

F1 : "Major"
F2 : "Minor"

note right of P3
  The use-case enumeration rule the DC fixes
  is the baseline's and is correct: one UC per
  endpoint surface, auth/rate-limiting/logging/
  telemetry excluded as mechanisms into the
  Supplementary Specification.
end note
note right of F1
  R006 remediation brought forward from LCO.
  Two roles are currently pointed at a file
  the repository does not contain.
end note
note bottom of P6
  net9.0, 9.0.100 rollForward latestFeature and
  the EF Core 9.0.8 / YARP 2.3.0 / Scalar 2.6.8
  pins were each checked against the files the
  policy cites, and each resolves.
end note
@enduml
```

## Resolutions and Actions


## Disposition

