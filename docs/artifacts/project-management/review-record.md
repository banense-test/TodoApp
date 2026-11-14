## Document Control
### Reviewer lens
<!-- review: Survey I3 -->

Phase: Survey
Status: Draft — technical lens of the SBC review, re-held at iteration 3. Two prior findings of this lens closed Resolved; 4 new findings (0 Critical, 2 Major, 2 Minor) on 2 artifacts.
Milestone Target: End-of-Survey (SBC) — not yet achieved; the sanction is the stakeholder's and this lens does not hold it

### Management Reviewer lens
<!-- review: Survey I3 -->

<!-- review: Survey I3 -->

Phase: Survey
Status: Draft — management lens of the SBC review, re-held at Survey iteration 3. Five findings of this lens closed Resolved against the corrected text and its anchors; 1 new finding (0 Critical, 0 Major, 1 Minor) on the Iteration Plan. Every artifact of the sprint zero is approved.
Milestone Target: End-of-Survey (SBC) — sanctioned by the stakeholder on 2026-11-14; the four Major corrections that sanction required are landed and verified this iteration.

### Review Coordinator lens
<!-- review: Survey I2 -->

<!-- review: Survey I2 -->

Phase: Survey
Status: Draft — coordination lens of the SBC review re-held at Survey iteration 2. Lens participation: Technical EXECUTED, Management EXECUTED, Business INACTIVE. 18 prior lens records closed; 7 records open — 0 Critical, 4 Major, 3 Minor.
Milestone Target: End-of-Survey (SBC) — perimeter confirmed and stakeholder sanction GRANTED on 2026-11-14; the milestone decision below records the phase under iteration until the four Majors are landed and re-verified

## Review Scope and Criteria
### Reviewer lens
<!-- review: Survey I3 -->

Phase: Survey, iteration 3. The third hold of the end-of-Survey (SBC) milestone review, technical lens. Four artifacts in scope, all read in full this iteration.

| Artifact | Owner | Discipline | State reviewed |
|---|---|---|---|
| Development Case | Process Engineer | Environment | Revised — Guidelines and Procedures gained a Version policy and a Measurement policy subsection |
| System Inventory | Software Archaeologist | Discovery | Revised — the Provenance row now names the four files Coverage names |
| Risk List | Project Manager | Project Management | Revised — R002 and R011 bounded to the RUP phases, R023's citation repaired, Document Control bounded |
| Iteration Plan | Project Manager | Project Management | Revised — criterion 1 restored, G2 deleted, the retirement map rebuilt, the accounting restated |

The Iteration Assessment is read and is not a gate input, and its absence or lag is no defect: the Project Manager writes it against this verdict.

#### Review point and lens

The review point is the **Lifecycle Milestone** (SBC), so the question is **exit criteria**. Two jobs, in this order. First, reconcile the two findings this lens carried in — re-tested against the corrected text and the file each correction cites, never against a claim that a correction was made. Second, review the corrected set afresh: three artifacts were rewritten substantially this iteration, and a correction can introduce a defect. That second job is where both Majors come from.

#### Criteria applied

| Criterion | Source | Applied to |
|---|---|---|
| Anchor verification — every corrected fact checked against the file or section it cites | Survey depth rule | All four |
| DC baseline conformance — no roster, ownership, CORE or optional-universe redefinition | IARI baseline | Development Case |
| Optional trigger justification — every FIRED verdict audited against its own §5.2 condition | IARI §5.2 | Development Case |
| Every cited document, section or file resolves to what it is cited for | Baseline conformance | Development Case, Risk List |
| Coverage consistency — nothing declared read and unread, and the counts agree with the enumeration | SBC criterion 3 | System Inventory |
| Band arithmetic — every magnitude the band of its own exposure | Risk magnitude table | Risk List |
| Acceptance authority — no High or Significant risk accepted by someone without the authority | Risk magnitude table | Risk List |
| Strategy executability — every disposal names work that remains to be done | SBC criterion 4 | Risk List |
| Exit-criteria integrity — every criterion gates the milestone it names, and claims nothing it does not have | SBC criterion 6 | Iteration Plan |
| Risk-retirement completeness — all 26 accounted for once, at the milestone that actually retires each | SBC criterion 6 | Iteration Plan |
| Role accounting — every role at work in the iteration is on its profile, and no stood-down role is | Development Case tailoring | Iteration Plan |
| Measurement discipline — no invented size, budget, forecast or date | IARI DC §8.1 | Iteration Plan |
| Scope adherence — no marker retired except by the stakeholder's answer | Scope Guard | All four |

#### Anchor verification this iteration

The two closures rest on opening what the corrections cite, not on reading the corrections.

| Anchor | Claim under test | Result |
|---|---|---|
| System Inventory, Provenance vs Coverage | The Provenance row agrees with the section it summarises | **Confirmed.** Four files named, no fifth; 53 + 4 = 57 agrees with Document Control, the "Files opened: 57" statement and the enumeration |
| Development Case, Guidelines and Procedures | R023's repair cites the pins, and the Version policy the iteration-2 finding said was absent | **Confirmed, and the section now exists.** It states the pins are the policy and that raising one is a Change Request owned by the Software Architect |
| `Todo.Web/Server/Todo.Web.Server.csproj` (sha d31a15d, 1115 bytes) | R023's repair names the file the change touches | **Not confirmed.** `<RazorLangVersion>8.0</RazorLangVersion>` is in that file's `PropertyGroup`; the file carries seven `PackageReference` entries and no Razor package. Recorded as Risk List F4 |
| System Inventory, Coverage vs Risk List R005 | R005's premise and its `avoid` strategy describe work still to be done | **Not confirmed.** Coverage enumerates `HttpAuthenticationStateProvider.cs` among the 57 opened and closes "No file in that group blocks a use case now". Recorded as Risk List F3 |

Two of four confirmed and two not, on six facts cross-checked. The two failures are the review's findings.

#### Scope marker audit

| Marker or decision | Where | Verdict |
|---|---|---|
| The `admin` branch — unreachable, role provisioning out of scope | System Inventory, Decisions; Risk List R007 | Held. Quoted verbatim in both |
| External login — configured-at-runtime, no use case this cycle | System Inventory, Decisions; Risk List R008 | Held, with the stakeholder's own condition ("revisit if credentials are supplied") |
| BFF trust boundary — known limitation of the single-host baseline | System Inventory, Decisions; Risk List R012 | Held, carried as an accepted risk |
| The system is never run in any phase | Nowhere — superseded | **Correctly retired, and by the right authority.** Coverage, the Risk List and the Iteration Plan all narrow it to Survey, Excavation and Consolidation, on the stakeholder's answer of 2026-11-14. No artifact states the project-wide version any longer |
| The perimeter confirmed at this milestone, no second confirmation | System Inventory, Perimeter; Iteration Plan, Evaluation Criteria | Held. G2 is deleted from roadmap, gantt and gate list; four gates remain |
| No `[DERIVED]` marker anywhere | All four | Correct — nothing here derives from a declared `FR-NNN`; the sprint zero recovers from code |

No marker was retired by a CCB decision, an approval or the passage of an iteration. The one that disappeared was retired by the stakeholder's own later answer, which is the only authority that could retire it. No `undeclared-scope` finding is recorded.

#### SBC exit criteria — this lens's verdict

```plantuml
@startsalt
title SBC exit criteria, Survey iteration 3 — the technical lens verdict on each criterion as it now stands
{
{S
<b>Criterion (Iteration Plan, Evaluation Criteria)</b> | <b>Verdict</b> | <b>Basis</b>
1 The perimeter is confirmed by the stakeholder | <color:green>MET</color> | Process wording restored; evidenced by the confirmation of 2026-11-14 over seven projects, the entry-point surface, the stores and the external systems; no later gate re-obtains it
2 The reading priorities are ordered | <color:green>MET</color> | Eight areas, each naming what the next reading settles
3 The unread areas are declared rather than omitted | <color:green>MET</color> | 57 files opened and enumerated; Provenance now agrees; the two read-only claims declared for the sprint zero
4 Every anomaly is a classified risk whose strategy can execute | <color:orange>FAIL F3</color> | 26 risks, all bands correct — but R005's avoid names work already performed, so its strategy cannot execute and its evidence already exists
5 The process is tailored and the tailoring is auditable | <color:green>MET</color> | Five tool rows resolve; every optional verdict checked against its condition; two new subsections audited
6 The plan instantiates the process and schedules no work the phase does not run | <color:orange>FAIL F3</color> | Criterion 1 and the gates are right, and every owner is on its milestone — but the retirement map books R005 at AR for work Survey 2 performed
--
Technical lens disposition | <color:orange>APPROVED WITH CHANGES</color> | 0 Critical, 2 Major, 2 Minor
}
}
@endsalt
```

Criteria 1, 2, 3 and 5 are met on this lens's evidence and none of the four Majors touches them. Criterion 4 fails on one row of 26 and criterion 6 on one row of the retirement map — the same row. No other criterion is affected.

### Management Reviewer lens
<!-- review: Survey I3 -->

#### Review point and scope

The end-of-Survey Lifecycle Milestone Review (**SBC**), re-held at Survey iteration 3 — the same milestone, the same four artifacts, re-tested against the text as corrected by the stakeholder's corrective order. The question at this review point is **exit criteria**, not feasibility and not completeness of intent.

| Artifact | Owner | Revised this iteration | State reviewed |
|---|---|---|---|
| Development Case | Process Engineer | No | Read in full — the Version policy and Measurement policy subsections added at Survey 2, and the sprint-zero read-only property in Disciplines and Intensity |
| System Inventory | Software Archaeologist | Yes — the Coverage closing statement narrowed to the sprint zero | Coverage and Provenance read against the corrected text and the enumeration |
| Risk List | Project Manager | Yes — R002 and R011 bounded, the Classification premise and Document Control rewritten | Read in full |
| Iteration Plan | Project Manager | Yes — criterion 1 restored, G2 deleted, the retirement map rebuilt, the LCO row corrected | Read in full |

The Iteration Assessment is read and is not a gate input: the Project Manager writes it against the verdict of the lens sequence that ends with this lens, so it cannot yet describe the iteration being reviewed. Its state is not a finding and not a gate condition.

#### Criteria applied

| Checklist item | What it tests |
|---|---|
| Every exit criterion evidenced as worded | The criterion states the process's condition and the evidence supports it |
| Size and count facts match the anchor | A perimeter fact the stakeholder confirmed is accurate |
| No acceptance without the authority to grant it | No Significant or High band risk rests on a grant nobody gave |
| The acceptance recorded is the acceptance given | The register's grant is neither narrower nor wider than the stakeholder's answer |
| No acceptance stated over more of the lifecycle than was decided | A sprint-zero acceptance is not recorded as running to the project's end |
| Every risk strategy can execute | No disposal rests on an activity the project does not perform |
| Every risk accounted for exactly once, at the milestone that retires it | The plan's accounting describes what the milestones do |
| Every role the plan assigns work to is at work in that milestone | No iteration carries risks with no accountable owner |
| No role at work the tailoring stood down | No gate staffs a stood-down lens |
| Every gate the plan books is a gate the stakeholder will attend | The plan asks for no decision that has been refused |
| Every cited reference resolves | The process authority and the register are auditable |
| No invented size, token budget, forecast or calendar date | The plan measures only what this project can measure |
| Both clocks reported apart and never added | Agent time and human queue time are never summed |
| Marker retired only by the stakeholder's own answer | No inference is promoted to declared scope |
| State column reports the gate as it now stands | A status column does not overstate or understate an open defect |

#### Anchor verification this iteration

Each closure rests on opening the corrected text and, where the finding concerned a fact outside the artifact, the anchor that carries it — never on a claim that a correction was made.

| Anchor | Claim under test | Result |
|---|---|---|
| System Inventory, Coverage closing statement | The no-observation constraint is bounded to the sprint zero and leaves a later build-and-test run as a settlement path | **Confirmed.** "No process is run in Survey, Excavation or Consolidation … carried as accepted risk until the RUP phases start, when the pipeline builds the solution and runs its test suites; the first such run is what settles each." "For the life of this project", "in any phase" and the prohibition on later milestones are gone, and the Runtime behaviour row carries the same horizon |
| Risk List, R002 and R011 | Both acceptances are bounded to the start of the RUP phases and neither band changed | **Confirmed.** R002 reads "accept until the RUP phases start — stakeholder grant, 2026-11-14" at 5×2=10; R011 reads "accept until the RUP phases start" at 2×4=8; Document Control states no acceptance runs to the end of the project |
| Risk List, Band and Strategy distribution | The register's own tallies agree with its rows | **Confirmed.** 2 High / 8 Significant / 12 Moderate / 3 Minor / 1 Low closes at 26; 18 avoided and 8 accepted names every row once |
| Iteration Plan, Evaluation Criteria row 1 | Criterion 1 carries the process wording and the confirmation of 2026-11-14 as its evidence | **Confirmed.** "The perimeter of the existing system is confirmed by the stakeholder … confirmed by the stakeholder at the SBC gate of 2026-11-14 … Evidenced — the confirmation has been given" |
| Iteration Plan, gantt markers, roadmap and Resources gate list | G2 exists nowhere and no reference dangles | **Confirmed.** Four gold markers, G1, G3, G4 and G5; Resources books four gates; no roadmap row names G2 |
| Iteration Plan, retirement property and the accounting table | Observation is a retirement path from Inception on, and all 26 risks are accounted for once | **Confirmed.** "No retirement in the sprint zero runs the system, and observation returns as a path from Inception on", the Tester named as producer and the Test Manager as recorder; 15 + 2 + 1 + 8 = 26 |
| Iteration Plan, LCO row | R006 and R025 are no longer credited to LCO | **Confirmed.** The LCO row's risk column reads "—" and the Survey 2 row carries R006, R025 and R026 |
| Iteration Plan, Evaluation Criteria row 3 and the fine plan's Minors row | The Provenance Minor is reported as outstanding | **Not confirmed.** It closed Resolved this iteration and the row is correct. Recorded as Iteration Plan F10 |

Seven of eight confirmed, on thirteen facts cross-checked. The one failure is this lens's finding.

#### Scope marker audit

| Marker or decision | Where | Verdict |
|---|---|---|
| The `admin` branch — unreachable, role provisioning out of scope | System Inventory, Decisions; Risk List R007 | Held. The stakeholder's words are quoted verbatim in both |
| External login — configured-at-runtime, no use case this cycle | System Inventory, Decisions; Risk List R008 | Held, with the stakeholder's own condition ("revisit if credentials are supplied") |
| BFF trust boundary — known limitation of the single-host baseline | System Inventory, Decisions; Risk List R012 | Held, carried as an accepted risk |
| The system is never run in any phase | Nowhere — superseded everywhere it stood | **Correctly retired, and by the right authority.** The System Inventory, the Risk List, the Iteration Plan and the Development Case all narrow it to Survey, Excavation and Consolidation on the stakeholder's answer of 2026-11-14. No artifact states the project-wide version |
| The perimeter confirmed at this milestone, no second confirmation | System Inventory, Perimeter; Iteration Plan, Evaluation Criteria | Held. G2 is gone from the gantt, the roadmap and the gate list; four gates remain, and an element Excavation finds outside the perimeter goes back then |
| No `[DERIVED]` marker anywhere | All four | Correct — nothing here derives from a declared `FR-NNN`; the sprint zero recovers from code |

No marker was retired by a CCB decision, a lens's approval or the passage of an iteration. The one that disappeared was retired by the stakeholder's own later answer, which is the only authority that could retire it. No `undeclared-scope` finding is recorded.

### Review Coordinator lens
<!-- review: Survey I2 -->

<!-- review: Survey I2 -->

#### Review event

End-of-Survey Lifecycle Milestone Review (**SBC**), re-held at Survey iteration 2 — the same milestone, the same four artifacts, re-tested against the corrected text after the sanction was withheld on 2026-11-14. A correction under a withheld sanction is not a new review type.

| Field | Value |
|---|---|
| Review type | Lifecycle Milestone Review (SBC) — re-held |
| Triggering condition | "Close-Out Phase" — the corrective iteration's artifacts complete and the phase gate reached again |
| Artifacts in scope | Development Case, System Inventory, Risk List, Iteration Plan |
| Artifacts read for the verdict | 6 of 6 — the four in scope, plus Review Record and Iteration Assessment; unread = none |
| Review point | Lifecycle Milestone — the question is **exit criteria**, not feasibility and not completeness of intent |
| Entry criteria | Met. All four artifacts existed in target state before the lenses ran; the 18 prior lens records were open at entry and were the iteration's work order |
| Exit criteria | **Not met.** 4 Major records open across three artifacts |

The Iteration Assessment is read and is not a gate input: the Project Manager writes it against the verdict of the lens sequence that ends with this lens, so at this point in the sequence it cannot yet describe the iteration being reviewed. Its state is not a finding.

#### Lens participation

| Lens | Executed | Findings yielded this review | Disposition |
|---|---|---|---|
| Technical / Reviewer | Yes | 2 records — 0 Critical, 0 Major, 2 Minor | Approved |
| Business / BusinessReviewer | **INACTIVE — did not evaluate this review** | None | Not applicable |
| Management / ManagementReviewer | Yes | 5 records — 0 Critical, 4 Major, 1 Minor | Conditional Go — sanction recorded as GRANTED |

The Business lens is inactive by tailoring, not by omission: the Development Case records `business-process-led = false` and stands the Business Reviewer down for the whole project, stating that the gate loses one lens while Reviewer and Management Reviewer remain. No record is attributed to it and the milestone decision below rests on the two lenses that executed.

#### Review calendar — this milestone and the events it opens

```plantuml
@startuml
title Review calendar — the SBC re-hold at Survey iteration 2, and the review events it opens
skinparam shadowing false

|#LightBlue|Survey 1 — SBC|
start
:G1 stakeholder gate — three scope facts put and answered;
:Lifecycle Milestone Review SBC — Reviewer, Management Reviewer, Review Coordinator;
note right
  Business lens INACTIVE — business-process-led = false,
  stood down for the whole project
end note
:Sanction asked — REFUSED, 2026-11-14;
:Corrective Survey iteration 2;

|#LightBlue|Survey 2 — SBC re-held|
:Lifecycle Milestone Review SBC — the same three lenses, the same four artifacts, re-tested against the corrected text;
:Stakeholder gate — perimeter confirmed at this milestone, sanction GRANTED, 2026-11-14;
:Review Coordinator verdict — four Majors owed as rework inside the artifacts;
:Corrective Survey iteration 3 — the four Majors landed and re-verified;

|#LightBlue|Excavation 1 — AR|
:Iteration Plan Review — the AR plan;
:Lifecycle Milestone Review AR — Reviewer, Management Reviewer, Review Coordinator;
:No stakeholder gate — the perimeter was confirmed at SBC;
note right
  A part of the system Excavation finds outside
  the perimeter goes back to the stakeholder then.
  There is no standing second-confirmation gate.
end note

|#LightBlue|Consolidation 1 — GHR|
:Lifecycle Milestone Review GHR — the three lenses;
:No stakeholder gate;

|#PaleGreen|Inception 1 to Transition 1|
:Iteration Plan Review before every iteration;
:PRA Review during execution;
:Iteration Evaluation Criteria Review, then Iteration Acceptance Review, at iteration close;
:Lifecycle Milestone Review at LCO, LCA, IOC and PR;
:G3 at LCO — the stakeholder accepts the life-cycle objectives;
:G4 at LCA — the stakeholder accepts the architecture baseline;
:G5 at PR — the customer takes ownership of the product;
stop
@enduml
```

The calendar carries one structural change the stakeholder ordered at this gate: the second perimeter confirmation at Consolidation 1's start does not exist. The perimeter is confirmed at SBC. From Excavation on, the only route back to the stakeholder on perimeter scope is an element Excavation finds outside it.

#### Effectiveness metrics — this review, against the first

```plantuml
@startmindmap
skinparam shadowing false
title SBC review effectiveness — the second review event, measured against the first
* SBC review · Survey iteration 2
** Coverage
*** Planned artifacts: 4
*** Reviewed: 4
*** Coverage: 100 %
** Prior records closed this review
*** Closed Resolved: 18 of 18
*** Carried open: 0
** New records this review: 7
*** Critical: 0
*** Major: 4
*** Minor: 3
** New-defect density by artifact
*** Iteration Plan: 3
*** System Inventory: 2
*** Risk List: 2
*** Development Case: 0
** Lens yield
*** Technical lens: 2 new records, both Minor
*** Management lens: 5 new records, 4 Major 1 Minor
*** Business lens: INACTIVE, no evaluation
** Anchor verification
*** Anchors re-opened: 3
*** Confirmed: 2
*** Not found: 1
** Two-point comparison with Survey 1
*** Iteration 1: 15 defects, 10 Major
*** Iteration 2: 7 defects, 4 Major
*** Reading: the four Majors arrived with the stakeholder's two corrections, after the corrections were written
** Not measurable at this review
*** Rework effort: the phase has not closed
*** Removal efficiency: no test phase has executed
@endmindmap
```

| Metric | Survey 1 | Survey 2 | Interpretation |
|---|---|---|---|
| Review coverage | 4 of 4 — 100 % | 4 of 4 — 100 % | No artifact escaped review in either event |
| Prior records closed | none — the first event | **18 of 18** | The corrective iteration's work order was met in full. No record was carried open into this review, which is why every record open now is new |
| Defects raised | 15 — 10 Major, 5 Minor | 7 — 4 Major, 3 Minor | Defect yield halved, and the Major band fell by six |
| Defect density — Iteration Plan | 7 | 3 | Still the densest artifact. It carries cross-artifact obligations — role profiles against the tailoring, risk owners against the register, gates against exit conditions — so it is where a contradiction between two correct documents surfaces |
| Defect density — System Inventory | 3 | 2 | The perimeter's content is not in dispute; both records are about statements that reach beyond it |
| Defect density — Risk List | 3 | 2 | Band arithmetic stable across both events; both records are about durations and citations, not scores |
| Defect density — Development Case | 2 | **0** | The artifact that carried the most cross-role misdirection now carries none |
| Anchor verification yield | 17 opened, 1 wrong — 6 % | 3 opened, 1 unresolved — 33 % | A higher rate on a much smaller sample: this iteration's three anchors were chosen because a correction was claimed against them, and the one that failed is the review's substantive discovery |
| Rework effort | Not measurable | **Not measurable** | The phase has not closed, so no rework has been performed that this record could measure. Estimate NONE — not zero, and not a figure |
| Defect removal efficiency | Not measurable | **Not measurable** | No test phase has executed. Review is still the only detection activity in the project, so there is no ratio to compute |
| Lens yield | Reviewer 7, Management 11 | Reviewer 2, Management 5 | The Management lens found every Major in both events. Two lenses remain the reason: the Reviewer alone would have approved this artifact set at 0 Major |

The trend these two points support, stated no more strongly than the evidence carries: **the corrective iteration worked, and it did not produce an artifact set fit to consume.** Every defect it was given was corrected and verified — 18 closures on 18 records — and the defect count fell by more than half. But four Majors are open, and all four arrived **after** those corrections were written, from two decisions the stakeholder took with the sanction: a constraint narrowed and a gate withdrawn. That is a stakeholder answering precisely, not a corrective iteration failing.

Two things these numbers cannot say. Rework effort and defect removal efficiency are unmeasurable until the phase closes and a test phase executes, and no figure is projected to fill them. And a two-point comparison is a comparison, not a trend line: no third event exists.

## Findings
### Reviewer lens
<!-- review: Survey I3 -->

#### Development Case

Environment discipline, Survey. Verdict: **Approved** — no open finding from this lens, and none carried in.

| Checklist item | Verdict |
|---|---|
| Baseline conformance: roster, CORE set, ownership unchanged | Pass |
| Every FIRED optional trigger holds its own §5.2 condition | Pass — Deployment Model alone, on the four-process topology read from `TodoApp.sln` and the YARP forwarder |
| Every NOT FIRED verdict still holds | Pass — Data Model on eight tables of which six are framework-generated, Proof-of-Concept deferred to Elaboration on its own terms, Test Plan on no audit obligation, UI Prototype on a delivered UI, Glossary on common words fixed by the schema |
| Every cited tool reference resolves in the tree | Pass — five rows, each a path |
| No constraint stated over more of the lifecycle than was decided | Pass |

This artifact changed this iteration: Guidelines and Procedures gained a **Version policy** subsection and a **Measurement policy** subsection. Both are audited here.

The Version policy states that the delivered pins are the policy — `net9.0` and `LangVersion preview` in `Directory.Build.props`, the 30 central pins in `Directory.Packages.props` — and that raising a framework, language or package version is a baseline change owned by the Software Architect and entering as a Change Request. It is consistent with the register, and it repairs the defect this lens recorded in iteration 2: R023 no longer cites a policy the Development Case does not contain, because the policy now exists. One clause of it under-reaches and is recorded against the Risk List as F4 rather than here: it names only `Directory.Packages.props` and `Directory.Build.props`, while R023's property lives in `Todo.Web/Server/Todo.Web.Server.csproj`.

The Measurement policy states the three quantities the baseline measures and, for each, the decision it enables and who reads it, then binds three rules: the two clocks are never added, no figure is quoted as a velocity, no budget is assumed. It invents no figure and names no authority to narrow scope to meet one. It is a policy about measurement, not a measurement.

#### System Inventory

Discovery discipline, Survey — the perimeter record the stakeholder confirmed at the SBC gate of 2026-11-14. Verdict: **Approved** — no open finding from this lens.

| Checklist item | Verdict |
|---|---|
| Every perimeter element carries an anchor that says what is claimed | Pass — not re-opened; 20 anchors verified across the two prior iterations and no correction disturbed one |
| Size and count facts match the file | Pass — 30 pins in all three places, 6 + 19 + 5 |
| Coverage declares its gaps rather than omits them | Pass — F3 of iteration 2 closed |
| The Provenance row agrees with the section it summarises | **Pass** — was F3, closed this iteration |
| No constraint stated over more of the lifecycle than was decided | Pass — the closing statement now reads "No process is run in Survey, Excavation or Consolidation … carried as accepted risk until the RUP phases start, when the pipeline builds the solution and runs its test suites; the first such run is what settles each" |
| Runtime behaviour claimed nowhere | Pass — Coverage states no process was run, and the two claims stay marked read-not-observed |

F3 is verified against the text, not against a claim of correction. Provenance now reads "57 files opened — the 53 of the first pass plus the four `Coverage` names as added in the second reading", names `ValidationFilter.cs`, `HttpAuthenticationStateProvider.cs`, `TodoApp.razor` and `LogInForm.razor`, and no longer names `RateLimitExtensions.cs`. 53 + 4 = 57 agrees with the Document Control tally, the "Files opened: 57" statement and the path-by-path enumeration.

The narrowing the Management lens required is also in place, and it is stated twice — in Coverage and in Perimeter completeness and its limits — with the same horizon. The declarations the stakeholder endorsed stand unchanged. This artifact carries no open record from this lens.

#### Risk List

Project Management discipline, Survey. Verdict: **Changes owed** — one Major, one Minor.

| Checklist item | Verdict |
|---|---|
| Every anomaly of the System Inventory is carried as a scored risk | Pass — 26 rows; 22 anomaly rows plus the absence finding set, the declared coverage limits, and R026 |
| Every magnitude is the band of its own exposure | Pass — all 26 recomputed against the exposure grid and the band distribution; 2 High / 8 Significant / 12 Moderate / 3 Minor / 1 Low closes at 26 and agrees with the register row for row |
| Every risk's strategy can actually execute | **Fail — F3** |
| No High or Significant risk rests on an acceptance nobody granted | Pass — both High-band risks `avoid`; R002 alone accepted in the Significant band, on the stakeholder's words |
| Every acceptance bounded to its horizon | **Pass** — was the Management lens's F3; R002 and R011 read "accept until the RUP phases start", the Mitigation section opens "Every acceptance in this register is bounded by the same horizon", and Document Control states it |
| The recorded acceptance is the acceptance given | Pass |
| Traceability table present, one row per declared `RNNN`, recovered elements with empty `Traces From` | Pass — 26 rows, correct form |
| The only non-agent delay is bounded here, as the plan claims | Pass — R026, 3×4=12, `avoid` on its own bound |

##### F3 — Major — R005 is scored on a condition the perimeter record says was already eliminated

R005 reads "Six files are declared unread, and one — `HttpAuthenticationStateProvider.cs` — blocks the login and logout scenarios", and its mitigation is "The System Analyst opens `HttpAuthenticationStateProvider.cs` before recovering the login and logout scenarios".

Coverage enumerates that file among the 57 opened. It records it as one of the four opened in the previous iteration — "the authentication-state bridge flagged as the one file blocking a use case" — and closes "No file in that group blocks a use case now." Provenance already carries the fact the row was opened for: "The Blazor authentication state is `HttpContext.User` or an empty identity; the provider holds no token and no provider state (369 bytes)."

Two things follow. The strategy `avoid` is attached to work already performed, so it does not name an artifact a role will write — it names one a role has written. And "six files are declared unread" no longer describes Coverage's declaration set, which is two Razor imports plus `Server/App.razor`, `OpenApiOptionsExtensions.cs`, six migration files, three manifests, five launch and appsettings files, the assets, two fixture files and the four project-management records.

This is a Major because two artifacts consume the row: the Iteration Plan books R005's retirement at AR and names it in the System Analyst's Excavation risk column. It is the only Significant-band risk in the register whose evidence the perimeter record says already exists.

Recommendation: restate R005 as the anomaly at the first reading with its resolution — declared unread at Survey 1, opened at Survey 2, its content recorded in Provenance, retired at Survey 2 — SBC. Drop or restate the "six files" clause to Coverage's current set. Keep the band, the owner and the exposure: the risk was real and was retired by an artifact the process ran, so no re-scoring is owed. While restating the Risk Register's opening sentence, make the composition exact: R025 enters from a review finding, not from an anomaly of the Inventory.

##### F4 — Minor — R023's restated mitigation routes the change to the wrong file

R023 now reads "Framework and Razor language version stay as delivered. Raising either changes the pins in `Directory.Packages.props`, which the Software Architect owns, and enters as a Change Request."

Its own anchor is `Todo.Web/Server/Todo.Web.Server.csproj`, and that is where the property sits: the file declares `<RazorLangVersion>8.0</RazorLangVersion>` in its `PropertyGroup` and carries seven `PackageReference` items, none of them a Razor package. Raising the Razor language version edits that project file, not the central pin file.

The iteration-2 defect is genuinely closed — the row no longer cites a Development Case section that does not exist, and the Development Case now has the section. What remains is the same misdirection in a new place: the register names a file the change does not touch.

Recommendation: read "Raising it sets `<RazorLangVersion>` in `Todo.Web/Server/Todo.Web.Server.csproj`, owned by the Software Architect, and enters as a Change Request." The Development Case's Version policy sentence should gain "or the project file that declares the property", so the policy covers this case and the register can cite it.

#### Iteration Plan

Project Management discipline, Survey. Verdict: **Changes owed** — one Major, one Minor.

| Checklist item | Verdict |
|---|---|
| Exit criterion 1 carries the process wording and is evidenced | **Pass** — was the Management lens's F8; criterion 1 reads "The perimeter of the existing system is confirmed by the stakeholder", evidenced by the confirmation of 2026-11-14 over the seven projects, the entry-point surface, the stores and the external systems |
| No gate the plan books has been deleted | **Pass** — G2 is gone from the coarse roadmap, the gantt markers and the Resources gate list; four gates remain, G1, G3, G4, G5, with no dangling identifier |
| No constraint stated over more of the lifecycle than was decided | **Pass** — was the Management lens's F9; the retirement property reads "No retirement in the sprint zero runs the system, and observation returns as a path from Inception on", and the Tester and Test Manager are named as the evidence's producer and recorder |
| A retirement path that exists is used, not foreclosed | **Pass** — R011 and the observable statements of R002 are placed at LCA on the first build-and-test run, each with its producer named |
| Every risk accounted for exactly once, at the milestone that retires it | **Fail — F3** |
| Every role a milestone assigns work to is at work in that milestone | Pass — every one of the 26 risk owners appears on the profile of the milestone whose row retires the risk |
| Roles at work reported as they were | **Fail — F4** |
| No role at work that the tailoring stood down | Pass — Business Process Analyst, Business Reviewer and Capsule Designer sit on no gate and execute no stage |
| No invented size, budget, forecast or date | Pass — no work item sized, every bar declared "the renderer's unit step", no start date, no budget proposed |
| Both clocks reported apart and never added | Pass |
| Milestone order matches the phase sequence | Pass |

##### F3 — Major — the retirement map books R005 at AR by re-opening a file already opened

Three places carry it. The retirement diagram reads "AR — Excavation 1: Reading completed — R005, opening `HttpAuthenticationStateProvider.cs` first". The disposal table lists R005 among the 15 "retired by a milestone artifact". The Excavation 1 role profile names R005 in the System Analyst's risk column.

The System Inventory's Coverage enumerates the file among the 57 opened and states no file in that group blocks a use case now, and Provenance records what it was opened for. The evidence R005's retirement rests on exists and was produced at Survey 2.

So the plan schedules reading work already performed, reports a met retirement as pending, and counts R005 in the wrong group of the accounting it publishes as 15 + 2 + 1 + 8 = 26. The arithmetic still closes at 26 and no risk is lost or double-counted — what is wrong is which milestone the plan says retires R005.

This is a Major because the risk-retirement map is the instrument by which the plan claims its risks retired, and the plan currently sends a Significant-band risk's retirement to a milestone that has nothing left to do for it. It propagates into the Excavation 1 profile, which will brief the System Analyst to open a file it will find already read.

Recommendation: move R005 into the "Retired at Survey 2 — SBC" group and restate the accounting as 14 + 3 + 1 + 8 = 26. Drop R005's step from the AR row of the diagram and from the Excavation 1 risk-owner column, leaving R017 as the System Analyst's AR owner. Restate the Risk List's R005 row in the same turn so register and plan state one retirement.

##### F4 — Minor — Resources states no role but two was at work, and a third was

Resources states: "No other role is at work: every open defect of this gate sits in an artifact the Software Archaeologist or the Project Manager holds, and the three lenses review. The Development Case carries no open record from either lens, so the Process Engineer executes no stage here."

The Development Case was revised this iteration. Its Guidelines and Procedures now carries a **Version policy** subsection and a **Measurement policy** subsection — both of which the Management Reviewer's iteration-2 review recorded as absent, in terms: "No section states a version policy." The correction is real and it is the one R023's citation needed.

The statement that R006 and R025 were retired at Survey 2 is correct. The conclusion drawn from it is not: the Process Engineer executed a stage here. The fine plan lists eight work items and none of them is the Development Case revision, so this iteration contains a ninth piece of work with no work item, no owner on the profile and no attribution.

A Minor because it stays inside the plan's own reporting: the work was done, is correct, and changes no roadmap row, no gate and no criterion. It is the same class of defect the iteration-2 review recorded as F7 — a misattributed correction.

Recommendation: add the Development Case revision as a work item — Process Engineer, Development Case — Guidelines and Procedures, the Version policy and Measurement policy subsections added — and name the Process Engineer on this iteration's role profile; or state in Resources that the Process Engineer revised the Development Case at Survey 3 and for what purpose. "No new artifact is produced" stays true; "no other role is at work" does not.

#### Pull requests

`scm_list_pull_requests` over all states returns none. Survey produces no source code, so an empty pull-request set is the correct shape for this milestone rather than a gap. Nothing awaits approval, nothing needs changes requested, and nothing needs deferring out of phase.

### Management Reviewer lens
<!-- review: Survey I3 -->

#### Development Case

Environment discipline, Survey. Verdict: **Approved** — no open finding from this lens, and none carried in.

| Checklist item | Verdict |
|---|---|
| Tailoring is a delta over the IARI baseline — no roster, CORE, ownership or optional-universe redefinition | Pass |
| Every FIRED optional trigger holds its own §5.2 condition | Pass — Deployment Model alone, on the genuine four-process topology read from `TodoApp.sln` and the YARP forwarder |
| Every NOT FIRED verdict holds against its condition | Pass — Data Model on the tables the snapshot declares, Proof-of-Concept deferred to Elaboration on its own terms, Test Plan on no audit obligation, UI Prototype on a delivered UI |
| Every cited tool reference resolves in the tree | Pass — five rows, each a path |
| Discipline intensities match the canonical matrix, no self-granted deviation | Pass — Discovery Critical in Survey, Environment High, business-process-led and real-time-system false |
| No stood-down role at work the tailoring removes | Pass — Business Process Analyst and Business Reviewer stood down, Capsule Designer for `real-time-system = false` |
| No constraint stated over more of the lifecycle than was decided | Pass |

This artifact is the one that carried the most cross-role misdirection at the first hold of this milestone, and it now carries no open record from any lens. The sprint-zero read-only property in Disciplines and Intensity is the narrowing this lens required elsewhere, stated at its source: "In Survey, Excavation and Consolidation no process is run … From Inception on the pipeline runs the solution", with the explicit close "The sprint-zero read-only property is not carried past Consolidation, and no artifact of this tailoring states it over the RUP phases." A role reading its process authority now finds the correct horizon there rather than in a register or a plan. **Criterion 5: Pass.**

One consequence for a later role, recorded as an observation and not a finding: with no written coding standard in the repository, the Code Reviewer's checklist is `Directory.Build.props`'s compiler-enforced conventions, the central pins and the Software Architecture Document's mechanisms. The Development Case states exactly that, so the Code Reviewer is not left improvising.

#### System Inventory

Discovery discipline, Survey — the perimeter record the stakeholder confirmed at the SBC gate of 2026-11-14. Verdict: **Approved** — no open finding from this lens, and the one carried in is closed.

| Checklist item | Verdict |
|---|---|
| Every perimeter element carries an anchor that says what is claimed | Pass — not re-opened here; twenty anchors verified across the prior iterations and no correction disturbed one |
| Size and count facts match the file | Pass — the pin tally is 30 in all three places it is stated, 6 + 19 + 5 |
| Coverage declares its gaps rather than omits them | Pass |
| No constraint stated over more of the lifecycle than was decided | **Pass** — was F3, closed this iteration |
| Runtime behaviour claimed nowhere, and the two read-only claims still marked as such | Pass — the declarations stand and the settlement path is now the first build-and-test run |

F3 is verified against the text, not against a claim of correction. Coverage now closes: "No process is run in Survey, Excavation or Consolidation … Within the sprint zero, therefore, neither statement is settled by observation, and both stay declared as read but not observed. They are carried as accepted risk until the RUP phases start, when the pipeline builds the solution and runs its test suites; the first such run is what settles each." All three overreaching phrases are absent, the Runtime behaviour row of the unread table carries the same horizon, and the closing clause states what the declarations are — "the honest record of what this reading could and could not establish, and no reading alone promotes either to fact."

The Provenance row reads "57 files opened — the 53 of the first pass plus the four `Coverage` names as added in the second reading", and 53 + 4 = 57 agrees with the Document Control tally, the "Files opened: 57" statement and the path-by-path enumeration.

#### Risk List

Project Management discipline, Survey. Verdict: **Approved** — no open finding from this lens, and the one carried in is closed.

| Checklist item | Verdict |
|---|---|
| Every anomaly of the System Inventory is carried as a scored risk | Pass — 26 rows |
| Every magnitude is the band of its own exposure | Pass — 2 High / 8 Significant / 12 Moderate / 3 Minor / 1 Low closes at 26 and agrees with the register row for row |
| No High or Significant risk rests on an acceptance nobody granted | Pass — both High-band risks `avoid`; R002 alone accepted in the Significant band, on the stakeholder's own words |
| The acceptance recorded is the acceptance given | Pass |
| No acceptance stated over more of the lifecycle than was decided | **Pass** — was F3, closed this iteration |
| Every risk's strategy can execute | Pass — from Inception on a build or test result is a retirement path the plan uses, and within the sprint zero every `avoid` names an artifact a role writes |
| The only non-agent delay in the project is bounded here, as the plan claims | Pass — R026, 3×4=12, `avoid` on its own bound |
| Traceability table present, one row per declared `RNNN` | Pass — 26 rows, recovered elements with empty `Traces From`, which is the right form |

F3 is verified against the rows and against the register's own tallies. R002 now reads "none is run in Survey, Excavation or Consolidation … From Inception on the pipeline builds the solution and runs its test suites, and a result it produces settles the statements it covers", with strategy "accept until the RUP phases start — stakeholder grant, 2026-11-14", band 5×2=10 unchanged. R011 drops "which this project does not do" for "not settled by reading within the sprint zero" and adds "A test that exercises the limiter settles it from Inception on", strategy "accept until the RUP phases start", band 2×4=8 unchanged. Document Control states the bound: "No acceptance here runs to the end of the project." Risk Mitigation and Contingency opens "Every acceptance in this register is bounded by the same horizon", and Risk Classification narrows the observation claim to "unavailable as a retirement path **within the sprint zero**".

Both High-band risks remain `avoid` and retired by artifacts the process already runs — R001 by the Test Case at LCA, R009 by the Use-Case Model at GHR. Of the eight Significant risks, seven are `avoid`; R002 alone is accepted and its grant is the stakeholder's. R026 bounds the project's only non-agent delay at 14 days of queue time, estimate none, and the Iteration Plan cites it by identifier, so plan and register state the same control.

#### Iteration Plan

Project Management discipline, Survey. Verdict: **Approved with changes** — one Minor.

| Checklist item | Verdict |
|---|---|
| Every exit criterion evidenced as worded | Pass — criterion 1 carries the process wording and the confirmation given at SBC |
| Every gate booked is a gate the stakeholder will attend | Pass — four gates, G1, G3, G4, G5, and no dangling identifier |
| No constraint stated over more of the lifecycle than was decided | Pass |
| A retirement path that exists is used, not foreclosed | Pass — R011 and the observable statements of R002 are placed at LCA on the first build-and-test run, with the Tester named as producer and the Test Manager as recorder |
| Every risk accounted for exactly once, at the milestone that retires it | Pass — 15 + 2 + 1 + 8 = 26, and the LCO row now carries no retired risk |
| Every role a milestone assigns work to is at work in that milestone | Pass — every one of the 26 risk owners appears on the profile of the milestone whose row retires the risk |
| No role at work that the tailoring stood down | Pass |
| No invented size, budget, forecast or date | Pass — no work item sized, every bar declared the renderer's unit step, no start date, no budget proposed |
| Both clocks reported apart and never added | Pass |
| Milestone order matches the phase sequence | Pass |
| State column reports the gate as it now stands | **Fail — F10** |

Four findings of this lens are closed this iteration and one Minor is new.

##### F10 — Minor — the exit-criteria table reports a defect that has closed

Criterion 3's state column reads "Evidenced — the declaration holds; the Provenance row is its owner's Minor", and the fine plan carries the work item "Restate the Provenance row to the four files Coverage names … Owner's next turn". That Provenance Minor is the technical lens's System Inventory#F3, and it was closed Resolved this iteration: the row names exactly the four files Coverage names and 53 + 4 = 57 agrees with the tally and the enumeration.

The plan therefore tells a reader of the SBC exit-criteria table that a declaration is under an open record when the record has closed and the row is correct. It is the mirror image of the defect this lens recorded as F6 at the first hold — a status column that misreports where the gate stands — in the opposite direction: F6 understated an open defect, F10 overstates a closed one.

A Minor because it stays inside the artifact's own reporting. Criterion 3's evidence and verdict are unaffected, the declaration the criterion turns on holds either way, and no roadmap row, gate or criterion follows from it. It does not hold the milestone, and its owner fixes it in the next turn after any Critical and Major across the project — of which there are none.

Recommendation: restate criterion 3's state to "Evidenced — the declaration holds; the Provenance row now agrees with the enumeration the Coverage section publishes", and drop the "Restate the Provenance row" row from the fine plan's work items. The work is performed and verified, not owed. No other row of the Evaluation Criteria table changes.

#### Pull requests

`scm_list_pull_requests` over all states returns none. Survey produces no source code, so an empty pull-request set is the correct shape for this milestone rather than a gap. Nothing awaits approval, nothing needs changes requested, and nothing needs deferring out of phase.

### Review Coordinator lens
<!-- review: Survey I2 -->

<!-- review: Survey I2 -->

#### Consolidated finding ledger

Coordinated from `read_artifact_findings` over all six artifacts. **Seven lens records are open — not one carries a resolution object.** Eighteen are closed, each by the lens that emitted it. A Review Record sentence saying a defect was fixed is not a resolution; the ledger object is, and every one of the 18 closures carries one with its verification evidence.

```plantuml
@startuml
title Consolidated finding ledger — 7 open lens records across 3 artifacts, after 18 closures
skinparam shadowing false
skinparam classAttributeIconSize 0

package "System Inventory — 2 open" #LightYellow {
  class "SI-A  Minor (Reviewer F3)\nProvenance counts 58 into a 57-file total" as SIA
  class "SI-B  Major (Management F3)\nCoverage states the no-observation\nconstraint over the whole lifecycle" as SIB
}

package "Risk List — 2 open" #LightYellow {
  class "RL-A  Minor (Reviewer F2)\nR023 cites a version policy the\nDevelopment Case does not contain" as RLA
  class "RL-B  Major (Management F3)\na bounded acceptance is recorded\nas one that runs to the project's end" as RLB
}

package "Iteration Plan — 3 open" #LightYellow {
  class "IP-A  Major (Management F8)\ncriterion 1 defers to a G2 gate\nthe stakeholder has deleted" as IPA
  class "IP-B  Major (Management F9)\nthe plan forecloses a retirement\npath that exists from Inception on" as IPB
  class "IP-C  Minor (Management F7)\nLCO is credited with two retirements\nthis milestone performed" as IPC
}

package "Closed this review — 18 records" #PaleGreen {
  class "Development Case\n2 closed" as DCC
  class "System Inventory\n3 closed" as SIC
  class "Risk List\n3 closed" as RLC
  class "Iteration Plan\n10 closed" as IPC2
}

note right of SIB
  SI-B, RL-B and IP-B are one premise
  with two consequences: the stakeholder
  narrowed the no-run constraint to the
  sprint zero and three artifacts state it
  project-wide.
end note
note right of SIA
  Finding keys collide across lenses:
  System Inventory#F3 is SI-A from the
  Reviewer and SI-B from the Management
  Reviewer. Every action names the lens.
end note
note bottom of IPA
  IP-A and RL-B both arrive from the same
  stakeholder answer, and neither is a
  question they have left open.
end note
@enduml
```

| Defect | Artifact | Severity | Lens record | Owner | Holds the milestone |
|---|---|---|---|---|---|
| SI-B — Coverage states the no-observation constraint over the whole lifecycle, and forbids later milestones from retiring the two claims | System Inventory | Major | Management F3 | Software Archaeologist | Yes |
| RL-B — R002 and R011 record a sprint-zero acceptance as open-ended to the end of the project | Risk List | Major | Management F3 | Project Manager | Yes |
| IP-A — exit criterion 1 defers the perimeter's confirmation to a gate the stakeholder has deleted | Iteration Plan | Major | Management F8 | Project Manager | Yes |
| IP-B — the plan states no retirement anywhere in the project runs the system, foreclosing a path that exists from Inception on | Iteration Plan | Major | Management F9 | Project Manager | Yes |
| SI-A — the Provenance row counts 58 into a 57-file total | System Inventory | Minor | Reviewer F3 | Software Archaeologist | No |
| RL-A — R023's mitigation and contingency cite a version policy the Development Case has no section for | Risk List | Minor | Reviewer F2 | Project Manager | No |
| IP-C — the retirement map credits LCO with two retirements this milestone performed | Iteration Plan | Minor | Management F7 | Project Manager | No |

#### Conflicts between lenses, and how I resolved them

| Conflict | Resolution |
|---|---|
| **Whole-artifact disposition.** Technical lens: all four artifacts Approved, 2 Minor. Management lens: Iteration Plan Rejected, System Inventory and Risk List Approved with changes, 4 Major. | The Management lens governs the gate. Both lenses reviewed the same corrected text; the difference is that the Management lens tested whether each artifact's statements reach beyond the stakeholder's decision, and the Reviewer's checklist did not carry that item. The Reviewer's findings stand and are not disturbed — every corrected fact was re-verified against its anchor, and that verification is the reason no content defect is open. |
| **System Inventory — one artifact, two verdicts.** Approved with changes for a Minor (Reviewer), Approved with changes for a Major (Management). | Not a conflict of evidence but of reach. The Reviewer audited the declaration of what was read and found it sound; the Management lens audited what the same section says about the future and found it over-stated. Both hold; the Major governs consumption. |
| **Risk List — the same shape.** The Reviewer's band arithmetic is pass across all 26 rows; the Management lens passes the arithmetic and fails the duration of an acceptance. | Complementary. The scores and bands are sound and no finding contests one. What fails is the period an acceptance is recorded as running for. No re-scoring is ordered by either lens. |
| **Iteration Plan — the sharpest split.** Reviewer: Approved, no Major, and it explicitly verified that criterion 1 no longer claims an unevidenced confirmation. Management: Rejected on two Majors, one of which is that criterion 1 now *under*-states a confirmation actually obtained. | Both readings are correct about different moments. The Reviewer closed the iteration-1 defect correctly: the criterion no longer claims what SBC did not obtain. The stakeholder then confirmed the perimeter at this gate, so the corrected text now under-states a met condition and books a deleted gate. That is a new defect created by a later decision, not a failed correction — which is why the iteration-1 record stays closed and F8 is a new record. |
| **Root cause.** Management identifies three Majors as one premise; the Reviewer records two Minors as independent. | Both accounts are true of their own set. Consolidated: the four Majors are **one premise with two consequences** (SI-B → RL-B, IP-B) plus **one independent governance defect** (IP-A). The three Minors are independent. The grouping determines the corrective order: correcting the premise last means correcting RL-B and IP-B twice. |

#### Where the lenses agreed, recorded as agreed

- **The perimeter's content is sound and is not in dispute.** The stakeholder confirmed it at this gate. Twenty anchors were opened across the two iterations; the one fact that failed was corrected and re-counted. No record contests a perimeter element.
- **Risk magnitudes are coherent.** All 26 were recomputed in iteration 1 and no lens misbanded one in either event. Both High-band risks are `avoid`; the single Significant-band acceptance is the stakeholder's own and its band is unchanged.
- **The Development Case now carries no open record from either lens.** It is the only artifact in scope with a clean sheet, and it is the artifact that carried the most cross-role misdirection in iteration 1.
- **No Critical record exists, and none is owed.** Stated with its basis under Disposition.

#### What I record as not a defect

- **The Iteration Assessment's content.** Both lenses reached this independently: the Project Manager writes it against this verdict, so it cannot describe the iteration it is the verdict for. Its current content assesses iteration 1 against the refused sanction, which is what it can describe.
- **Risk scores.** Six scores would move under a different Project Manager. Both lenses declined to contest them and the plan states that disagreement with a score does not fail the milestone. A scoring judgement is not converted into a finding here.
- **The two Minors of the Technical lens.** Recorded, owned, and not milestone-holding. Neither leaves its artifact: no role builds on the wrong arithmetic and no exit criterion turns on R023's citation.
- **The empty trace graph.** Survey declares no element family of the trace chain — the System Inventory and the four process artifacts cite declared ids where they use them and register none of their own. A blank graph at SBC is the correct shape, not a `trace-gap`. The Risk List's empty `Traces From` rows are the right form for recovered elements.

I did not re-adjudicate any lens record. Where a record quotes its evidence, the evidence is in the record.

## Resolutions and Actions
### Reviewer lens
<!-- review: Survey I3 -->

#### Closure ledger — the two findings this lens carried in

Each was re-tested against the corrected text **and** against the file or section the correction cites, then closed by the tool call that materializes the state change. Both calls were applied before this entry was written.

```plantuml
@startuml
title Closure reconciliation — the 2 findings of this lens carried into Survey iteration 3
skinparam shadowing false

state "Open at the start of the iteration" as OPEN
state "Resolved — correction verified against the artifact and its anchor" as RES

state OPEN {
  state "System Inventory F3  Minor\nProvenance counted 58 into a 57-file total" as A1
  state "Risk List F2  Minor\nR023 cited a version policy the\nDevelopment Case had no section for" as A2
}

[*] --> OPEN
A1 --> RES : Provenance now names the four files\nCoverage names — 53 + 4 = 57
A2 --> RES : R023 names the pins and the owner;\nthe Development Case now has a Version policy
RES --> [*]

note bottom of RES
  A resolution is the tool call, not a sentence.
  Both were applied before this entry was written.
  R023's replacement text is under a NEW Minor (RL F4):
  it names Directory.Packages.props, while the
  property lives in Todo.Web.Server.csproj.
end note
@enduml
```

| Finding | Severity | Correction found in the artifact | Closed |
|---|---|---|---|
| System Inventory F3 — Provenance counted 58 into a 57-file total | Minor | The row reads "the 53 of the first pass plus the four `Coverage` names as added in the second reading", names `ValidationFilter.cs`, `HttpAuthenticationStateProvider.cs`, `TodoApp.razor` and `LogInForm.razor`, and no longer names `RateLimitExtensions.cs` | Resolved |
| Risk List F2 — R023 cited a version policy the Development Case had no section for | Minor | R023 now reads "Raising either changes the pins in `Directory.Packages.props`, which the Software Architect owns, and enters as a Change Request", and the Development Case's Guidelines and Procedures gained a Version policy subsection stating the same rule | Resolved |

Neither closure rests on a claim of correction. The Provenance row was counted against Coverage's enumeration, and R023's citation was read against the Development Case section the Process Engineer added.

The second closure is recorded with its residue: the replacement text names a file the change does not touch, and that is a new defect with its own key (Risk List F4), not a reopening. The finding asked that the citation resolve; it now resolves. Whether it resolves to the right file is a separate test that the replacement fails.

#### Open findings and their actions

| Finding | Artifact | Severity | Owner | Holds the milestone | Action |
|---|---|---|---|---|---|
| Risk List F3 — R005 is scored `avoid` on a condition Coverage records as already eliminated, and its "six files are declared unread" no longer matches Coverage's set | Risk List | Major | Project Manager | Yes | Restate R005 as the anomaly at the first reading with its resolution at Survey 2 — SBC; correct the unread count; keep band, owner and exposure; make the Register's composition sentence exact about R025 |
| Iteration Plan F3 — the retirement map, the disposal table and the Excavation 1 profile book R005's retirement at AR by re-opening a file opened at Survey 2 | Iteration Plan | Major | Project Manager | Yes | Move R005 to "Retired at Survey 2 — SBC" and restate the accounting as 14 + 3 + 1 + 8 = 26; drop it from the AR diagram step and the Excavation 1 risk column |
| Risk List F4 — R023's mitigation routes the change to `Directory.Packages.props`, while `<RazorLangVersion>` lives in `Todo.Web/Server/Todo.Web.Server.csproj` | Risk List | Minor | Project Manager | No | Name the property and the project file that holds it; add "or the project file that declares the property" to the Development Case's Version policy so the register can cite it |
| Iteration Plan F4 — Resources states no role but the Software Archaeologist and the Project Manager was at work, while the Process Engineer revised the Development Case this iteration | Iteration Plan | Minor | Project Manager | No | Add the Development Case revision as a work item and name the Process Engineer on this iteration's profile, or state in Resources that the revision happened and why |

Risk List F3 and Iteration Plan F3 are one defect in two artifacts: the register holds the stale premise and the plan builds the retirement on it. They are repaired in one turn, and the register's row is the one that must be corrected first — the plan's disposal table derives from it.

The two Minors are independent and each stays inside its own artifact. Risk List F4 crosses into the Development Case only to the extent of one clause in a sentence that already exists; the Process Engineer is named as the role to add it, and the Project Manager may name the file and the owner without it.

#### What this lens deliberately did not raise

Recorded so each omission is a decision rather than an oversight.

- **The perimeter's content.** Twenty anchors have been opened across the three iterations and every one says what the artifact claims. The stakeholder confirmed the perimeter at this milestone. No record of any lens contests an element of it, and re-verifying it would spend the gate's budget restating what is established.
- **Risk scores.** No lens has misbanded a risk in three events. R005's exposure is real and was retired by an artifact the process ran; the defect is where the artifact records the retirement, not the number. Re-scoring would misprice a risk whose control worked.
- **The Development Case's new subsections.** Audited, not contested. The Version policy under-reaches by one clause, recorded against the Risk List as F4 rather than as a Development Case finding, because the artifact that misdirects the reader is the register.
- **The empty pull-request set.** Survey produces no source code, so an empty set is the correct shape for this milestone.
- **The empty trace graph.** Survey declares no element family of the trace chain. A blank graph at SBC is the right shape, not a `trace-gap`.
- **The Iteration Assessment.** The Project Manager writes it against this verdict. Its absence or lag is no defect and no gate condition.

### Management Reviewer lens
<!-- review: Survey I3 -->

#### Closure ledger — the five findings this lens carried into Survey iteration 3

Each was re-tested against the corrected text **and**, where the finding concerned a fact outside the artifact, against the anchor that carries it. The `resolve_artifact_finding` call materializes the state change; all five were applied before this entry was written.

```plantuml
@startuml
title Closure ledger — the five findings this lens carried into Survey iteration 3, and what verified each
skinparam shadowing false
skinparam classAttributeIconSize 0

package "Open at the start of the iteration — 4 Major, 1 Minor" #LightYellow {
  class "System Inventory F3  Major\nCoverage stated the no-observation\nconstraint over the whole lifecycle\nand forbade later milestones from\nretiring the two claims" as A
  class "Risk List F3  Major\nR002 and R011 recorded a bounded\nacceptance as open-ended to the\nend of the project" as B
  class "Iteration Plan F8  Major\ncriterion 1 deferred to a G2 gate\nthe stakeholder had deleted" as C
  class "Iteration Plan F9  Major\nthe plan foreclosed a retirement\npath that exists from Inception on" as D
  class "Iteration Plan F7  Minor\nLCO credited with two retirements\nSBC performed" as E
}

package "Closed Resolved this iteration — verified against the corrected text" #PaleGreen {
  class "Coverage narrowed\nNo process runs in Survey, Excavation\nor Consolidation; the first build-and-test\nrun from Inception on settles each" as A2
  class "Both rows accepted until the\nRUP phases start\nDocument Control states no acceptance\nruns to the end of the project" as B2
  class "Criterion 1 carries the\nprocess wording\nG2 gone from gantt, roadmap and gate\nlist; four gates remain" as C2
  class "Property scoped to the\nsprint zero\nR011 and half of R002 placed at LCA\nwith the Tester named as producer" as D2
  class "R006 and R025 moved to\nthe Survey 2 row\naccounting 15 + 2 + 1 + 8 = 26" as E2
}

A --> A2 : re-read in Coverage
B --> B2 : re-read in the register
C --> C2 : re-read in Evaluation Criteria
D --> D2 : re-read in the roadmap
E --> E2 : re-read in the accounting table

note right of A2
  A resolution is the tool call, not a sentence.
  All five were applied before any section of
  this block was written.
end note
note bottom of E2
  The corrections are genuinely repaired. What
  this lens finds new is not a failed correction:
  F10 is a state column in the plan that still
  reports the Provenance Minor as outstanding,
  while that Minor closed Resolved this iteration.
end note
@enduml
```

| Finding | Severity | Correction found in the artifact | Closed |
|---|---|---|---|
| System Inventory F3 — Coverage stated the no-observation constraint over the whole lifecycle and forbade later milestones from retiring the two claims | Major | Coverage now reads "No process is run in Survey, Excavation or Consolidation … carried as accepted risk until the RUP phases start, when the pipeline builds the solution and runs its test suites; the first such run is what settles each"; all three overreaching phrases gone; the declarations stand unchanged | Resolved |
| Risk List F3 — R002 and R011 recorded a bounded acceptance as open-ended to the end of the project | Major | Both rows read "accept until the RUP phases start"; R002's 5×2=10 and R011's 2×4=8 unchanged; Document Control, Risk Classification and Risk Mitigation and Contingency all state the horizon | Resolved |
| Iteration Plan F8 — criterion 1 deferred the perimeter's confirmation to a gate the stakeholder had deleted | Major | Criterion 1 carries the process wording, evidenced by the confirmation of 2026-11-14; G2 is absent from the gantt, the roadmap and the gate list, which books four gates | Resolved |
| Iteration Plan F9 — the plan foreclosed a retirement path that exists from Inception on | Major | The property is scoped to the sprint zero, observation returns from Inception on, and a section places R011 and the observable statements of R002 at LCA with the Tester as producer | Resolved |
| Iteration Plan F7 — the retirement map credited LCO with two retirements this milestone performed | Minor | The LCO row's risk column reads "—"; R006 and R025 sit on the Survey 2 row; the accounting reads 15 + 2 + 1 + 8 = 26 | Resolved |

No closure rests on a claim of correction. Each rests on the sentence now in the artifact and, for the two that turn on a fact, on the register's own tallies and the plan's own gate list.

#### The stakeholder's corrective order, and how it was followed

The order set at this gate was: the System Inventory sentence first, then the Risk List and Iteration Plan statements that quote it, then the deleted gate, then the three Minors in each owner's next turn. The artifacts show that sequence held — the premise is narrowed identically in all four artifacts, and no artifact now states the project-wide version.

Two Minors of the three the stakeholder named are closed: the Iteration Plan's F7 above, and the Risk List's citation, closed by the technical lens under its own key. The third — the System Inventory's Provenance arithmetic — was closed by the technical lens this iteration. All three are therefore resolved; the only new record is F10, which reports one of them as still outstanding.

#### Action owed at the owner's next turn

| Action | Artifact | Owner | Closes |
|---|---|---|---|
| Restate criterion 3's state to record that the Provenance row now agrees with the enumeration, and drop the "Restate the Provenance row" row from the fine plan's work items | Iteration Plan | Project Manager | F10 |

F10 does not hold the milestone. It is a Minor: the state column changes no evidence, no gate and no criterion, and the declaration criterion 3 turns on holds either way. The artifact is approved; its owner corrects the column in the next turn.

#### Action owed at the owner's next turn — carried from the technical lens

Four records from the technical lens are open on two artifacts the Project Manager owns. They are not my lens's to close, and I record them here only so the owner sees one list:

| Record | Artifact | Severity | Holds the milestone |
|---|---|---|---|
| Risk List F3 — R005 is scored `avoid` on a condition Coverage records as already eliminated | Risk List | Major | Yes |
| Iteration Plan F3 — the retirement map books R005's retirement at AR by re-opening a file opened at Survey 2 | Iteration Plan | Major | Yes |
| Risk List F4 — R023's mitigation routes the change to a directory-pin file while the property lives in the project file | Risk List | Minor | No |
| Iteration Plan F4 — Resources states no role but two was at work, while the Development Case was revised this iteration | Iteration Plan | Minor | No |

The two Majors are one defect in two artifacts: the register holds a stale premise and the plan builds the retirement on it. My lens did not find them — the technical lens did, by checking R005's premise against the Coverage enumeration — and I do not re-adjudicate them. What I record is their consequence for the milestone, in Disposition below.

#### No Critical, and why

A Critical is a defect only the stakeholder can unblock: a scope decision, a contradiction in what they declared, or a risk only they may accept. Nothing at this gate qualifies.

All three scope questions put at Survey 1 were answered on 2026-11-14 and each answer was re-tested against the code it disposes of; all three hold and none is reopened. The two corrections the stakeholder added to their sanction are fully absorbed: the perimeter is confirmed at SBC with no second gate anywhere in the plan, and the no-observation constraint is narrowed to the sprint zero in all four artifacts that stated it. A decision already taken and correctly recorded everywhere it bears is not an open question, and escalating it again would ask the stakeholder to answer what they have decided twice.

#### No Major from this lens, and why

A Major means another role builds on wrong content or a milestone exit criterion fails. Neither holds for this lens's checklist.

- Every correction this lens ordered was checked against the anchor that carries it, and each resolves. No role is pointed at content that does not exist.
- Five of the six SBC exit criteria are evidenced as worded on this lens's evidence, and the sixth is evidenced on the artifacts' own text.
- Every acceptance is bounded, R002's Significant-band grant is the stakeholder's own and its band is unchanged, and no acceptance outlives its horizon.
- Every risk strategy can execute: within the sprint zero each `avoid` names an artifact a role writes, and from Inception on a build or test result is a path the plan uses rather than forecloses.
- All 26 risks are accounted for once, and the owner of every one is at work in the milestone whose row retires it.
- Four gates are booked, each is a decision the stakeholder will give, and none staffs a stood-down lens.

### Review Coordinator lens
<!-- review: Survey I2 -->

<!-- review: Survey I2 -->

#### Closure ledger — the 18 records this iteration resolved

Each was closed by the lens that emitted it, after that lens re-tested the correction against the artifact and, where the record concerned a file outside it, against the anchor. The tool call materializes the closure; this table records what it rests on.

```plantuml
@startuml
title Finding lifecycle across the SBC re-hold — from record to verified closure
skinparam shadowing false

[*] --> Open : record_artifact_finding by the originating lens
Open --> Assigned : owner and severity named at review close
Assigned --> InProgress : owner reworks the artifact
InProgress --> Resolved : the correction lands and the owning lens calls resolve_artifact_finding
Resolved --> Reopened : corrective action inadequate — re-recorded under its key, occurrence + 1
Reopened --> InProgress
Resolved --> Closed
Open --> Escalated : deadline missed
Assigned --> Escalated : deadline missed
Escalated --> Assigned : prioritised by the Project Manager, or by the stakeholder where the grant is theirs
Closed --> [*]

note right of Resolved
  Only the lens that emitted a record may close it.
  A Review Record sentence saying "Resolved"
  is not a resolution — the ledger object is.
end note
note bottom of Open
  A finding key is scoped per artifact AND per lens:
  System Inventory#F3 names two different defects —
  a Reviewer Minor and a Management Major.
  Every action names the defect and its lens.
end note
@enduml
```

| Lens | Artifact | Records closed | Verified against |
|---|---|---|---|
| Technical | Development Case | 2 — F1 Major, F2 Minor | Tool references: five rows, each an existing path, no written standard claimed; ownership redrawn with component and artifact elements |
| Technical | System Inventory | 2 — F1 Major, F2 Minor | `Directory.Packages.props` re-counted: 6 + 19 + 5 = 30; the stale `(unread)` qualifier is gone |
| Technical | Risk List | 1 — F1 Minor | R018's mitigation separates establishing the values from recording them |
| Technical | Iteration Plan | 2 — F1 Major, F2 Minor | Criterion 1 restated; all 26 risks accounted for, R023 named |
| Management | Development Case | 1 — F1 Major | Same five-row verification; SBC criterion 5's auditable-tailoring question answered |
| Management | System Inventory | 2 — F1 Major, F2 Major | Pin tally re-counted from the file; the settlement sentence replaced |
| Management | Risk List | 2 — F1 Major, F2 Major | R026 present at 3×4=12 and cited by the plan by identifier; R002 and R011 restated `accept` with the grant quoted |
| Management | Iteration Plan | 5 — F1 Major, F2–F5 Major, F6 Minor | No stood-down role on a gate; Excavation profile staffed; five gates booked; retirement map rebuilt; per-criterion state |
| **Total** |  | **18 — 13 Major, 5 Minor** |  |

Two closures deserve the note on why they stand although the surrounding content is now under a new Major, because a reader will otherwise read them as withdrawn. **System Inventory F2 (Management)** asked that an impossible settlement path be replaced by the stakeholder's decision; it was, and that is what the record required. **Iteration Plan F1 (both lenses)** asked that a criterion stop claiming an unevidenced confirmation; it no longer claims one. That the replacement content then over-reached the sprint zero (SI-B, IP-B) and that the criterion now under-states a confirmation actually obtained (IP-A) are new defects with their own recommendations. Reopening the closed records would obscure which correction failed; a closure answers the defect its record names.

#### Action owed at each owner's next turn

None of the four Majors asks the stakeholder a question. Each narrows content back to a decision they have already taken, twice.

| Defect | Artifact | Owner | Action | Position |
|---|---|---|---|---|
| SI-B | System Inventory | Software Archaeologist | Restate the Coverage closing statement to the scope given: no process is run in Survey, Excavation or Consolidation, so within the sprint zero neither read-only claim is settled by observation; both stay declared as read but not observed and are carried as accepted risk until the RUP phases start. Remove "for the life of this project", "in any phase" and the "no milestone may count them as retired" sentence, and leave open that a later phase recording a build-and-test result settles them. The declarations themselves stand unchanged | 1 |
| RL-B | Risk List | Project Manager | Restate R002 and R011 as accepted until the RUP phases start, when the pipeline builds the solution and runs its tests; correct R002's "no later reading can settle it" and R011's "which this project does not do" to the sprint-zero scope; keep both acceptances and both bands; state in Document Control that the acceptance is bounded to the sprint zero | 2 |
| IP-B | Iteration Plan | Project Manager | Scope "no retirement runs the system" to the sprint zero; state that from Inception on the CI pipeline builds the solution and runs its test suites so a later phase may retire a risk by a build or test result, and name who produces that evidence; then re-examine the retirement map for what a build and test run can settle and place each at the milestone whose execution produces it | 2 |
| IP-A | Iteration Plan | Project Manager | Restore criterion 1 to the process wording — the perimeter confirmed by the stakeholder — evidenced by the confirmation given at SBC on 2026-11-14 over the seven projects, the entry-point surface, the stores and the external systems. Delete G2 from the coarse roadmap, the gantt markers and the Resources gate list, leaving G1, G3, G4 and G5 and no dangling identifier. Replace "Where the perimeter is confirmed" with what happened, and do not restate the deferral's rationale as a live reason | 3 |
| IP-C | Iteration Plan | Project Manager | Move R006 and R025 from the LCO row to a line for Survey 2 — SBC, and restate the accounting so it reads fifteen retired by a later milestone artifact, two at SBC, one by its own bound and eight carried on acceptance — twenty-six | Minor — owner's next turn |
| SI-A | System Inventory | Software Archaeologist | Restate the Provenance row to the four files the Coverage sentence names, dropping `RateLimitExtensions.cs` so the row and the 57-file tally agree | Minor — owner's next turn |
| RL-A | Risk List | Project Manager | Cite what exists — raising either version changes the pins in `Directory.Packages.props`, owned by the Software Architect, and enters as a Change Request — instead of a Development Case section that does not exist | Minor — owner's next turn |

#### Corrective order — the sequence is the plan

```plantuml
@startuml
title Corrective sequence for the four Majors — the order that stops one overstatement propagating twice
skinparam shadowing false

|#Pink|Premise|
start
:System Inventory F3 — narrow the Coverage closing statement to Survey, Excavation and Consolidation;
note right
  Fixing this last means fixing Risk List F3
  and Iteration Plan F9 twice: both quote the sentence.
end note

|#Orange|Acceptance duration|
:Risk List F3 — restate R002 and R011 as accepted until the RUP phases start;
:Bound the acceptance in Document Control to the sprint zero;

|#LightBlue|Plan — gates and retirement path|
:Iteration Plan F8 — restore criterion 1 to the process wording, delete G2 from roadmap, gantt and gate list;
:Iteration Plan F9 — scope no-run to the sprint zero, state that the pipeline builds and tests from Inception on, re-examine the retirement map for what a build and test run can settle;

|#PaleGreen|Minors — owner's next turn|
:System Inventory F3 Minor — Provenance counts 58 into a 57-file total;
:Risk List F2 Minor — R023 cites a version provision the Development Case does not contain;
:Iteration Plan F7 Minor — R006 and R025 are retired at SBC, not at LCO;
stop
@enduml
```

**SI-B first, then RL-B and IP-B, then IP-A.** They are not four independent defects: one sentence in the perimeter record states a sprint-zero constraint over the whole lifecycle, and the register and the plan both quote it. Correcting them in the other order writes the same narrowing three times into three artifacts that then disagree about the same two risks — the failure mode the previous milestone's corrective order existed to prevent.

**The three Minors are owed at their owners' next turn.** Each stays inside its own artifact, and each is a single row.

#### What is deliberately not an action

- **A new stakeholder question at this gate.** All four Majors are corrections to what the artifacts say about decisions already given. Putting any of them back to the stakeholder would ask them to answer what they have answered twice, which is the defect IP-A names.
- **A Change Request.** None of the seven open records needs one. Each is a correction inside an artifact its owner already holds — no scope change, no baseline change, nothing for the CCB.
- **Re-scoring any risk.** No lens contests a magnitude in either event, and the plan states that disagreement with a score does not fail the milestone.
- **A schedule change beyond the iteration count.** Corrective iteration 3 is the plan's own lever for a milestone whose exit criteria do not pass. Declared scope is not narrowed, no role is added in parallel, and no criterion is re-interpreted to fit what was produced.

#### Stakeholder finding — the corrective order, set by the stakeholder

Put to the stakeholder this milestone with the four Majors named and their owners' actions recorded above. Their answer:

> "Close the System Inventory sentence first, then the Risk List and Iteration Plan statements that quote it, then the deleted gate; the three Minors in each owner's next turn."

This sets the sequence and adds no defect, no condition and no new action. Read against the ledger it orders the four Majors as SI-B; then RL-B and IP-B; then IP-A; and it leaves the three Minors to their owners' next turn. The stakeholder named no part of the existing system missing from the perimeter and corrected none of the actions above; no record is added or removed on account of this answer. The position column above carries this order.

## Disposition
### Reviewer lens
<!-- review: Survey I3 -->

```plantuml
@startsalt
title SBC, Survey iteration 3 — compliance matrix: checklist item x verdict, per artifact
{
{S
<b>Checklist item</b> | <b>DC</b> | <b>SI</b> | <b>RL</b> | <b>IP</b>
Baseline conformance, no redefinition | <color:green>PASS</color> | - | - | <color:green>PASS</color>
Every optional trigger holds its own condition | <color:green>PASS</color> | - | - | -
Every cited reference resolves to a file or a section | <color:green>PASS</color> | - | <color:orange>FAIL F4</color> | -
Every perimeter fact rests on its anchor | - | <color:green>PASS</color> | - | -
Size and count facts match the file | - | <color:green>PASS</color> | - | -
Coverage declares its gaps consistently | - | <color:green>PASS</color> | - | -
No constraint stated over more of the lifecycle than was decided | - | <color:green>PASS</color> | <color:green>PASS</color> | <color:green>PASS</color>
Every magnitude is the band of its own exposure | - | - | <color:green>PASS</color> | -
Every risk strategy can execute | - | - | <color:orange>FAIL F3</color> | -
Every risk accounted for exactly once, at the milestone that retires it | - | - | - | <color:orange>FAIL F3</color>
Every exit criterion evidenced as worded | - | - | - | <color:green>PASS</color>
No acceptance without the authority to grant, none open-ended | - | - | <color:green>PASS</color> | <color:green>PASS</color>
No role at work the tailoring stood down | <color:green>PASS</color> | - | - | <color:green>PASS</color>
Roles at work reported as they were | - | - | - | <color:orange>FAIL F4</color>
No invented size, budget, forecast or date | - | - | - | <color:green>PASS</color>
Marker retired only by the stakeholder | <color:green>PASS</color> | <color:green>PASS</color> | <color:green>PASS</color> | <color:green>PASS</color>
--
Lens verdict | APPROVED | APPROVED | CHANGES OWED | CHANGES OWED
}
}
@endsalt
```

```plantuml
@startuml
title Defect distribution, SBC Survey iteration 3 — 2 Major and 2 Minor across 2 artifacts
skinparam shadowing false
skinparam classAttributeIconSize 0

package "Risk List" #LightYellow {
  class "F3  Major\nconsumed-defect\nR005 scored on a condition\nCoverage says is already eliminated" as RL3
  class "F4  Minor\ncontained-defect\nR023 routes the change to\nDirectory.Packages.props; the\nproperty lives in Todo.Web.Server.csproj" as RL4
}

package "Iteration Plan" #LightYellow {
  class "F3  Major\nconsumed-defect\nR005 booked as retired at AR by\nre-opening a file opened at Survey 2" as IP3
  class "F4  Minor\ncontained-defect\nResources states no role but two was\nat work; the Process Engineer revised\nthe Development Case this iteration" as IP4
}

package "Clean this iteration — no open finding from this lens" #PaleGreen {
  class "Development Case\nVersion policy and Measurement policy\nsubsections audited; five tool rows resolve" as DC
  class "System Inventory\nF3 Minor closed: Provenance now names\nthe four files Coverage names" as SI
}

note right of RL3
  RL3 and IP3 are one defect in two
  artifacts: the register holds the
  stale premise and the plan builds
  the retirement on it.
end note
note bottom of DC
  Both prior Minors of this lens are
  closed Resolved this iteration —
  System Inventory#F3 and Risk List#F2.
end note
@enduml
```

#### Technical lens disposition

**Approved with changes.** 0 Critical, 2 Major, 2 Minor. Two of the four artifacts carry no open record from this lens. The milestone itself is the Review Coordinator's to rule on: this lens reports its verdict on the artifacts, it does not sanction the phase.

```plantuml
@startuml
title SBC Survey iteration 3 — technical lens disposition across the four artifacts
skinparam shadowing false
skinparam classAttributeIconSize 0

package "Approved — no open finding from this lens" #PaleGreen {
  class "Development Case\nEnvironment\n5 FIRED / NOT FIRED verdicts audited\n2 new subsections audited" as DC
  class "System Inventory\nDiscovery\nF3 Minor closed Resolved\nprovenance arithmetic verified" as SI
}

package "Changes owed — 2 Major, 2 Minor, 0 Critical" #LightYellow {
  class "Risk List" as RL {
    F3 Major — R005 stale premise
    F4 Minor — R023 names the wrong file
  }
  class "Iteration Plan" as IP {
    F3 Major — R005 retired at the wrong milestone
    F4 Minor — Process Engineer absent from the profile
  }
}

package "Recorded, not a defect" #LightBlue {
  class "Pull requests: none\nSurvey produces no source code" as PR
  class "Trace graph: empty\nno element family declared at SBC" as TR
  class "Iteration Assessment\nwritten against this verdict" as IA
}

DC -[hidden]-> SI
RL -[hidden]-> IP
SI -[hidden]-> PR
IP -[hidden]-> TR

note right of RL
  The two Majors are one defect in two artifacts:
  the register holds the premise and the plan
  builds the retirement on it.
  No Critical exists — both are corrections inside
  an artifact its own owner holds, and neither asks
  the stakeholder a question.
end note
note bottom of DC
  Two artifacts of this phase now carry no open
  record from this lens.
end note
@enduml
```

#### The seven findings of the previous gate, as this lens now finds them

Five are closed on evidence and two on this iteration's corrections. Each closure rests on reading the corrected text, not on a claim of correction.

| Prior finding | Lens | Status this iteration |
|---|---|---|
| Coverage stated the no-observation constraint over the whole lifecycle | Management, System Inventory | Corrected. Coverage and Perimeter completeness both read "No process is run in Survey, Excavation or Consolidation … carried as accepted risk until the RUP phases start; the first such run is what settles each" |
| R002 and R011 recorded a bounded acceptance as open-ended | Management, Risk List | Corrected. Both rows read "accept until the RUP phases start", the section opens with the horizon, and Document Control states it |
| The plan foreclosed a retirement path that exists from Inception on | Management, Iteration Plan | Corrected. The property is scoped to the sprint zero, and R011 and the observable statements of R002 are placed at LCA with the Tester named as producer |
| Criterion 1 deferred to a deleted gate | Management, Iteration Plan | Corrected. Criterion 1 carries the process wording, evidenced by the confirmation given at SBC; G2 is gone from roadmap, gantt and gate list, leaving four gates |
| The retirement map credited LCO with two retirements SBC performed | Management, Iteration Plan | Corrected. The disposal table now reads "Retired at Survey 2 — SBC … R006, R025" |
| Provenance counted 58 into a 57-file total | Technical, System Inventory | Closed Resolved this iteration |
| R023 cited a version policy the Development Case lacks | Technical, Risk List | Closed Resolved this iteration; its replacement text is under the new Minor RL F4 |

The four Majors are genuinely repaired. What this lens finds new is not a failure of those corrections: it is a defect none of them touched, in a risk row no prior finding named.

#### Why the two Majors are Major and not Critical

A Critical is a question only the stakeholder can answer. Neither Major is one.

R005's row and the plan's retirement of it are both wrong about a fact the artifacts already establish between themselves: Coverage says the file was opened and states no file in that group blocks a use case. The correction is a restatement inside two artifacts their owner holds. There is no scope decision, no contradiction in what the stakeholder declared, and no risk for them to accept. Putting it to them would ask a question the perimeter record already answers.

Both hold the milestone on one ground each: the Risk List's strategy for a Significant-band risk does not name work that remains to be done, and the plan's retirement map names the wrong milestone for that same risk.

#### Why the two Minors do not hold the milestone

Each stays inside its own artifact. RL F4 misdirects a reader of an accepted Moderate risk's mitigation to a file the change does not touch — no exit criterion turns on it, and R023's contingency, a Change Request, is the same either way. IP F4 misreports which roles worked this iteration — the work was done and is correct, and no roadmap row, gate or criterion depends on the reporting.

They are recorded and owned, owed at their owner's next turn, after the two Majors.

#### What this lens confirms and does not disturb

- **The perimeter is confirmed and is not in dispute.** The stakeholder confirmed it at this gate over the seven projects, the entry-point surface, the stores and the external systems. Twenty anchors were opened across the three iterations and the one fact that failed was corrected and re-counted. No record of this lens contests an element.
- **The tailoring is auditable.** Every cited reference resolves, every optional verdict is checked against its own §5.2 condition, and the two subsections added this iteration are policy rather than measurement.
- **No acceptance outlives its grant.** R002 is the only Significant-band acceptance and its words are the stakeholder's; every acceptance states a horizon and none runs to the end of the project.
- **No work item assumes a run of the system inside the sprint zero, and observation returns as a path from Inception on**, with its producer and recorder named.
- **No invented figure anywhere.** No work item is sized, no bar is a duration, no start date is given, no token budget is proposed.
