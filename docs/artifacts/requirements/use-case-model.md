## Document Control
- Phase: Excavation
- Status: Draft — produced for the end-of-Excavation (AR) milestone review
- Milestone Target: end-of-Excavation (AR) — not yet achieved
- Iteration: 2, Cycle 1
- Owner: System Analyst
## Use-Case Diagram
The boundary is the one the System Inventory records: four processes, two stores, and the external systems the delivery reaches. Every use case below is anchored to the entry point whose code performs it.

```plantuml
@startuml
title Recovered system boundary - the actors the perimeter names and the use cases the existing system performs

left to right direction
skinparam shadowing false
skinparam wrapWidth 210

actor "ACT-001 Person with a task list\nthe only human actor the perimeter names" as A1
actor "ACT-002 External identity provider\nGitHub, Google, Microsoft account, Auth0\nsupporting actor of UC-003" as A2
actor "ACT-003 Same person, reaching the API directly\nbearer token, reference UI" as A3

rectangle "Todo App - the system boundary the System Inventory records" {
  package "Account" {
    usecase "UC-001 Create an account" as UC1
    usecase "UC-002 Sign in with email and password" as UC2
    usecase "UC-003 Sign in with an external provider" as UC3
    usecase "UC-004 Sign out" as UC4
    usecase "UC-005 Maintain one's own account" as UC5
  }
  package "Task list" {
    usecase "UC-006 See one's own tasks" as UC6
    usecase "UC-007 Add a task" as UC7
    usecase "UC-008 Remove a task" as UC8
    usecase "UC-009 Read one task by id" as UC9
    usecase "UC-010 Change a task,\nincluding marking it complete" as UC10
  }
  package "API reference" {
    usecase "UC-011 Consult the API reference" as UC11
  }
}

A1 --> UC1
A1 --> UC2
A1 --> UC3
A1 --> UC4
A1 --> UC6
A1 --> UC7
A1 --> UC8
A2 --> UC3 : authenticates the person\non its behalf
A3 --> UC1
A3 --> UC2
A3 --> UC5
A3 --> UC6
A3 --> UC7
A3 --> UC8
A3 --> UC9
A3 --> UC10
A3 --> UC11

note right of UC3
  Complete code, no provider registered:
  unreachable in the delivered configuration.
  Stakeholder, 2026-11-23
end note

note right of UC5
  ACT-003 alone: EP-015 is reached by no screen
  and by no client call, so ACT-001 has no edge here.
end note

note right of UC10
  The only operation that writes IsComplete,
  and no client call reaches EP-013: an API
  operation with no screen path. AN-001
end note

note bottom of UC9
  No screen and no client call reaches EP-011
  either: an API operation only.
end note

note bottom of A2
  ACT-002 answers EP-008 on the person's behalf
  and initiates no use case of its own.
end note

@enduml
```
## Actors
| ID | Actor | Kind | Who or what it is, as established | Source |
|---|---|---|---|---|
| ACT-001 | Person with a task list | Human, primary | The only human actor the perimeter names. Anonymous until they register or sign in; owns the task rows they create. Reaches the system through the three screens of the Blazor client | System Inventory — External actors and systems; `Todo.Web/Server/App.razor:5`; `Todo.Web/Client/Components/LogInForm.razor:3-26` |
| ACT-002 | External identity provider | External system, supporting actor of UC-003 | GitHub, Google, Microsoft account or Auth0. Authenticates the person and returns them to the callback. Initiated from the system's side and answered by the provider, which is why the perimeter names it the initiator of `EP-008`; the person remains the primary actor of the use case | System Inventory — External actors and systems; System Inventory — Entry points `EP-008`; `Todo.Web/Server/Authentication/AuthenticationExtensions.cs:39-92` |
| ACT-003 | Same person, reaching the API directly | Human, the same individual as ACT-001 | The perimeter's "authenticated caller holding a bearer token". The README addresses this role by name: run `Todo.Api` standalone, obtain a token from `/users/login`, then call the endpoints with the reference UI or a client of choice | System Inventory — Entry points `EP-010`–`EP-019`; `README.md`, "Using the API standalone" |

**One human being, two actor roles.** ACT-001 and ACT-003 are the same person. ACT-003 is not a second human actor and does not contradict the perimeter, which names exactly one: it is the role in which that person reaches the API without a cookie, holding a bearer token obtained from `/users/login` and calling the endpoints directly, as the delivery's own README directs. The role exists because the two routes authenticate differently and reach different operations — `EP-009` requires a cookie and rewrites it, while `EP-010` to `EP-019` accept any bearer token.

The task use cases therefore carry **one main flow with two scenarios** — through the screens, or directly with a bearer token — and are not split per actor. UC-009, UC-010 and UC-005 are reached by ACT-003 alone: no screen and no client call reaches `EP-011`, `EP-013`, or any Identity endpoint beyond register and login.

**Two entry points, two different questions.** Every use case in this model is anchored twice over, and the two lists below answer different questions, so they are not expected to agree and are not two statements of one fact:

- The **Source** column of the Survey names the entry point **whose code performs the use case**. When ACT-003 calls `POST /todos` that is `EP-012`; when ACT-001 adds a task from the list screen, the screen is `EP-003` but the request still leaves through the BFF's forwarder `EP-009` to `EP-012`.
- The **actor-goal matrix** names the entry point **the actor reaches the use case through** — the screen or the endpoint the actor itself acts on. ACT-001 acts on `EP-003`; the operation the system then performs is not named there.

A screen entry point and the forwarded operation are therefore both true of one use case, and the matrix says which one its edges name.

```plantuml
@startuml
title Actor-goal matrix - each actor handle against the use cases it reaches, naming the screen the actor acts on

left to right direction
skinparam shadowing false
skinparam wrapWidth 200

actor "ACT-001\nPerson with a task list\nthrough the three screens" as A1
actor "ACT-003\nThe same person\nthrough the API with a bearer token" as A3
actor "ACT-002\nExternal identity provider\nsupporting actor of UC-003" as A2

rectangle "Use cases of the recovered model" {
  usecase "UC-001 Create an account" as UC1
  usecase "UC-002 Sign in with email and password" as UC2
  usecase "UC-003 Sign in with an external provider" as UC3
  usecase "UC-004 Sign out" as UC4
  usecase "UC-005 Maintain one's own account" as UC5
  usecase "UC-006 See one's own tasks" as UC6
  usecase "UC-007 Add a task" as UC7
  usecase "UC-008 Remove a task" as UC8
  usecase "UC-009 Read one task by id" as UC9
  usecase "UC-010 Change a task" as UC10
  usecase "UC-011 Consult the API reference" as UC11
}

A1 --> UC1 : acts on EP-002
A1 --> UC2 : acts on EP-002
A1 --> UC3 : acts on EP-002
A1 --> UC4 : acts on EP-001
A1 --> UC6 : acts on EP-003
A1 --> UC7 : acts on EP-003
A1 --> UC8 : acts on EP-003

A3 --> UC1 : calls EP-015
A3 --> UC2 : calls EP-015
A3 --> UC5 : calls EP-015
A3 --> UC6 : calls EP-010
A3 --> UC7 : calls EP-012
A3 --> UC8 : calls EP-014
A3 --> UC9 : calls EP-011
A3 --> UC10 : calls EP-013
A3 --> UC11 : calls EP-017, EP-018, EP-019

A2 --> UC3 : answers EP-008

note right of UC5
  ACT-003 alone: no screen and no client call
  reaches EP-015. ACT-001 carries no edge here.
end note

note bottom of UC3
  The person acts on the login screen EP-002; the
  challenge leaves for EP-007 and the provider answers
  at EP-008. Unreachable in the delivered configuration.
end note

note bottom of A2
  ACT-002 answers EP-008 on the person's behalf
  and initiates no use case of its own.
end note

@enduml
```

**Actors the model does not create.** The System Inventory names "app host or operator" as the initiator of `EP-020`, `EP-021` and `EP-022`, and defines no operator: no role, no procedure and no need for one appears anywhere in the delivery. No actor is created for it, and no use case is recovered from it. `TodoApp.AppHost` is a component inside the boundary that starts the others; starting a system is not an actor goal, and no human initiates it.

**Actors the model does not create, second.** The external systems the delivery also reaches — the OTLP collector, nuget.org, the `tomdesinto/sqliteweb` image — are declared outside the boundary in the System Inventory and serve no use case. The SQLite file is a data manager inside the boundary, reached by every task operation.
## Use-Case Survey
Eleven use cases, each anchored to the entry points whose code performs it. Every one of the twenty-two entry points is either carried here or is accounted for in "Not recovered" below.

| ID | Use case | Primary actor | Source | Value the actor receives | Volatility |
|---|---|---|---|---|---|
| UC-001 | Create an account | ACT-001, ACT-003 | `EP-002`, `EP-004`, `EP-015` | An account exists and the caller is signed in, or holds a bearer token | Low |
| UC-002 | Sign in with email and password | ACT-001, ACT-003 | `EP-002`, `EP-005`, `EP-015` | A session cookie, or a bearer token, for an existing account | Low |
| UC-003 | Sign in with an external provider | ACT-001, with ACT-002 authenticating the person | `EP-007`, `EP-008`, `EP-016` | A local account tied to the provider identity, and a session cookie. **Unreachable in the delivered configuration** (stakeholder, 2026-11-23) | **High** — four providers, each configurable or absent, and the whole path is dead without one |
| UC-004 | Sign out | ACT-001 | `EP-006` | The session cookie is cleared; the screens return to the login form | Low |
| UC-005 | Maintain one's own account | ACT-003. No screen and no client call reaches any of its endpoints | `EP-015` | Token refresh, email confirmation, password reset, two-factor and profile management | Medium — the Identity endpoint set is a framework surface the delivery maps without a screen |
| UC-006 | See one's own tasks | ACT-001, ACT-003 | `EP-001`, `EP-003`, `EP-009`, `EP-010` | The caller's own task rows are read and rendered | Low |
| UC-007 | Add a task | ACT-001, ACT-003 | `EP-003`, `EP-009`, `EP-012` | A new row, owned by the caller, appended to the list without a reload | Low |
| UC-008 | Remove a task | ACT-001, ACT-003 | `EP-003`, `EP-009`, `EP-014` | The row is deleted and leaves the list | Low |
| UC-009 | Read one task by id | ACT-003 | `EP-011` | One row of the caller's is returned. API operation only: no screen and no client call reaches it | Low |
| UC-010 | Change a task, including marking it complete | ACT-003 | `EP-013` | A row's title and completion flag are set. **API operation only**: the client makes no update call and the list's checkbox is bound to nothing (AN-001) | **High** — the one operation the UI has no path to, and the one place `IsComplete` is written |
| UC-011 | Consult the API reference | ACT-003 | `EP-017`, `EP-018`, `EP-019` | The API contract is read as an OpenAPI document or in a rendered reference UI | Low |

### Not recovered, and why

| Entry point | Why it carries no use case |
|---|---|
| `EP-020` readiness, `EP-021` liveness | The perimeter names "app host or operator" as the initiator and defines no operator actor. Both are mapped in Development only, and neither delivers value to an actor the delivery names. They are a platform mechanism, stated in the Supplementary Specification — Supportability (S8) |
| `EP-022` the migration platform event | No human actor initiates it; the app host raises it before the API starts, in run mode and only when `Todo.Api/.db` does not exist. It is a component's start-up step, stated in the Supplementary Specification — Design Constraints (DC11) and as mechanism M9 |
| The `admin` role branch of `EP-011`, `EP-013`, `EP-014` | Not a use case: no actor in the running system can enter it, because nothing grants the role (AN-004). Recorded as an exceptional entity, by the stakeholder's decision of 2026-11-23, inside UC-009, UC-010 and UC-008 as a predicate the flows do not follow |
| The cross-owner read, update and delete a caller holding a self-minted `admin` token could perform | Same as above. It is the behaviour of one predicate, not an actor's goal |

### Why a screen entry point and the forwarded operation are both named

UC-006, UC-007 and UC-008 each cite `EP-003` beside their API-side entry points, and that is not a second anchor for the same fact. The three answer one question with two entry points, because on the screen route the actor's action and the operation that performs it are different entry points in different processes:

| Use case | The actor acts on | The operation performs it | What the screen contributes |
|---|---|---|---|
| UC-006 See one's own tasks | `EP-003` the todo list screen | `EP-010` `GET /todos`, reached through the forwarder `EP-009` | The list renders one row per task with its title and a remove control, and shows a spinner while the load is in flight. It renders nothing and requests nothing when the client has no base address, answering an empty list instead (`AN-026`) |
| UC-007 Add a task | `EP-003` the new-todo input | `EP-012` `POST /todos`, reached through `EP-009` | The input is the form the title is typed into and the validator that blocks an empty submit, and it is the control the created row is appended to without a reload |
| UC-008 Remove a task | `EP-003` the per-row remove control | `EP-014` `DELETE /todos/{id}`, reached through `EP-009` | The remove control is the only way a screen reaches a delete, and it is the control the deleted row is removed from |

The edge is `EP-003 → UC-NNN` because the actor's goal is entered through the screen: without `EP-003` no person reaches any of the three, and each use case's step 1 is that screen. `Todo.Web/Client/Components/TodoList.razor:3-32` carries the new-todo input and the per-row remove control, so it precedes UC-007's and UC-008's step 1, and `Todo.Web/Server/App.razor:44-52` renders it as the signed-in shell, which is the screen UC-006's step 1 names. The `EP-009` forwarder and the API operations are cited in the flows as what the screen's request becomes, not as an alternative actor route.

A reader who needs one list rather than two reads the Survey's **Source** column as the entry point whose code performs the use case; the actor-goal matrix in "Actors" names the entry point the actor acts through. Both are correct for their question, and the Survey's rows name both where both apply.

### Nothing is held back for Consolidation

All twenty-two entry points are accounted for in this model: nineteen carry a use case, and the three that do not — `EP-020`, `EP-021`, `EP-022` — are permanent exclusions reasoned in the table above, not work postponed. No operation of the delivery is recovered in a later phase. The recoverable operations all sit in the entry-point-bearing areas this reading orders first — the Todo API's task surface and its authorization, and the BFF session surface — and the areas it leaves carry no entry point at all: orchestration, build and container manifests and supporting files.

Consolidation therefore inherits no deferred use case from this model. The eleven counted above are the whole use-case set of the delivery as it stands, and the four rows under "Not recovered, and why" are exclusions that no later phase re-opens.

## Use-Case Specifications
Every flow below is the flow the code performs, not a flow anyone intended. Each step carries the file and lines it was read from, and each step is followed by the rule the code enforces at that step; where the code contradicts a document or another part of itself, the code is recorded and the contradiction is named.

The four session flows — UC-001, UC-002, UC-003 and UC-004 — sit on a surface whose failure paths were never modified and whose behaviour no test confirms. That statement is made once, with its anchors, in "The instability UC-001 to UC-004 sit on" at the end of this section; read it before those four flows.

```plantuml
@startuml
title The rules the recovered flows enforce, and the use case each one guards

skinparam shadowing false
skinparam componentStyle rectangle
skinparam wrapWidth 230
left to right direction

package "Entered by the person, in the client" {
  component "Email required, at most 256 characters; password 6 to 32\ncarrying a digit, an upper case, a lower case and a symbol" as R1
  component "No request is sent unless the email and the password\nare both non-empty" as R2
  component "A new todo requires a title" as R3
}

package "Checked at the API boundary" {
  component "Only the parameter types an endpoint registers are validated:\nTodoItem on /todos, ExternalUserInfo on /users. A violation is\n400 application/problem+json" as R4
  component "A bearer token, and a user row for its NameIdentifier.\nA deleted account's token is refused" as R5
  component "The per-user token bucket, /todos only:\n50 tokens, 50 per 10 s, queue 50, 429. AN-024" as R6
  component "The route id is an integer" as R7
}

package "Held on the row and on the write" {
  component "Title is required, on the row and on both request shapes" as R8
  component "OwnerId is required, set from the resolved caller,\nnever read from a body, never returned" as R9
  component "IsComplete is created false and every PUT replaces it" as R10
  component "PUT refuses a body id that differs from the route id" as R11
  component "Ownership: the caller's row, or an admin claim no caller holds.\nNo match answers 404, never 403" as R12
}

package "Between the BFF and the API" {
  component "The BFF requires the cookie and rewrites the token set's\naccess token into Authorization: Bearer" as R13
  component "An auth failure answers 401 with no body, whatever its cause" as R14
  component "The provider key is protected under a protector named after\nthe provider; a key from another ring raises" as R15
}

package "Use cases" {
  component "UC-001 Create an account" as U1
  component "UC-002 Sign in with a password" as U2
  component "UC-003 Sign in with a provider" as U3
  component "UC-004 Sign out" as U4
  component "UC-005 Maintain one's own account" as U5
  component "UC-006 See one's own tasks" as U6
  component "UC-007 Add a task" as U7
  component "UC-008 Remove a task" as U8
  component "UC-009 Read one task" as U9
  component "UC-010 Change a task" as U10
}

R1 --> U2 : step 2, the submit path
R1 ..> U1 : never runs on the create control
R2 --> U1 : step 4
R2 --> U2 : step 3
R3 --> U7 : step 2
R4 --> U3 : step 5
R4 --> U7 : 400 when the title is absent
R4 --> U10 : 400 when the title is absent
R5 --> U6
R5 --> U7
R5 --> U8
R5 --> U9
R5 --> U10
R6 --> U6
R6 --> U7
R6 --> U8
R6 --> U9
R6 --> U10
R7 --> U8
R7 --> U9
R7 --> U10
R8 --> U7 : step 5
R8 --> U10 : step 4
R9 --> U7 : step 5, the owner comes from the token
R10 --> U7 : created false whatever the body says
R10 --> U10 : step 4, both fields replaced
R11 --> U10 : step 3
R12 --> U8 : step 4
R12 --> U9 : steps 3 and 5
R12 --> U10 : step 4
R13 --> U6 : step 3
R13 --> U7 : step 4
R13 --> U8 : step 3
R14 --> U1 : the one refusal it can give
R14 --> U2 : the one refusal it can give
R14 --> U4 : a refused sign-out is silent
R15 --> U3 : step 6

note right of R4
  The /users group registers ExternalUserInfo alone with the
  validation filter, so a register or login body passes no
  data-annotation check at the API. UsersApi.cs:18
end note

note bottom of R6
  Two budgets, one in force. RateLimitExtensions.cs:14-31 carries
  the code defaults of 100 tokens, 100 per 10 s and a queue of 100;
  appsettings.Development.json:8-12 binds all three to 50, and both
  launch profiles of both serving processes select Development.
  The delivery configures no other environment, so 50 / 50 / 50 is
  the budget everywhere this system runs. AN-024
end note

note bottom of R12
  The list endpoint filters on OwnerId alone and declares no
  order; the item endpoints also admit the admin claim.
  The disagreement is recorded, not reconciled. AN-018
end note

@enduml
```
## Traceability

| Element | Traces From | Link Type | Traces To |
|---|---|---|---|
| UC-001 | EP-002, EP-004, EP-015 | Refines | — |
| UC-002 | EP-002, EP-005, EP-015 | Refines | — |
| UC-003 | EP-007, EP-008, EP-016 | Refines | — |
| UC-004 | EP-006 | Refines | — |
| UC-005 | EP-015 | Refines | — |
| UC-006 | EP-001, EP-003, EP-009, EP-010 | Refines | — |
| UC-007 | EP-003, EP-009, EP-012 | Refines | — |
| UC-008 | EP-003, EP-009, EP-014 | Refines | — |
| UC-009 | EP-011 | Refines | — |
| UC-010 | EP-013 | Refines | — |
| UC-011 | EP-017, EP-018, EP-019 | Refines | — |
