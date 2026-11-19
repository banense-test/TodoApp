- Phase: Excavation
- Status: Draft — Domain Model and Design Packages recovered; Use-Case Realizations, Interface Contracts and Persistent Data Classes not yet recovered
- Milestone Target: end of Excavation (AR) — not yet achieved

## Design Overview
This document records the design the delivered code already holds. Nothing here is designed by this project: every class, member, visibility modifier and relationship is read out of the file named beside it, and no member is named that the code does not declare. Where the code is silent — a concurrency token, a lifecycle state an operation would need but no operation exists to reach — the silence is recorded as such, not filled.

The model is produced in stages. This iteration recovers the **domain model** and the **design packages**; the use-case realizations, the interface contracts and the persistent-data classes follow in later stages of this phase, and each section below states its own status.

| Section | What its diagram fixes | Status this iteration |
|---|---|---|
| Domain Model | The classes the code declares as business objects, their members, and the one relationship that holds between them | Recovered |
| Design Packages and Classes | The same classes grouped by the component that declares them, with every operation the code implements | Recovered |
| Use-Case Realizations | Which objects collaborate, in what order, for each of the eight recovered use cases | Not yet recovered |
| Interface Contracts | Pre/postconditions on every operation a component boundary crosses | Not yet recovered |
| Persistent Data Classes | Column, key, index and cascade detail of the eight tables | Owned by the Database Designer |
| Boundary Classes and Navigation Map | The Razor components as boundary classes | Owned by the User Interface Designer |
| Capsules, Protocols and Signals | — | `[OMITTED: Capsules, Protocols and Signals — Development Case DC-D3: real-time-system = false, so no capsule, protocol or signal work runs in any phase]` |

**What is recovered and what is not.** Fifteen classes carry the product's own business objects and its declared wire shapes: one entity the project authored (`Todo`), the Identity-derived user, and six DTO declarations that exist twice over — once in each host. Eight further classes carry the code that reads and writes those objects. Each is anchored where it is described; a class with no member the code declares is shown with none.

