## Document Control

- Phase: Excavation
- Status: Draft — produced for the end-of-Excavation (AR) milestone review
- Milestone Target: end-of-Excavation (AR) — not yet achieved
- Iteration: 1, Cycle 1
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
actor "ACT-002 External identity provider\nGitHub, Google, Microsoft account, Auth0" as A2
actor "ACT-003 Developer using the API directly\nbearer token, reference UI" as A3

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
  ACT-002 initiates only EP-008, on the person's
  behalf. It initiates no use case of its own.
end note

@enduml
```

## Actors
| ID | Actor | Kind | Who or what it is, as established | Source |
|---|---|---|---|---|
| ACT-001 | Person with a task list | Human, primary | The only human actor the perimeter names. Anonymous until they register or sign in; owns the task rows they create. Reaches the system through the three screens of the Blazor client | System Inventory — External actors and systems; `Todo.Web/Server/App.razor:5`; `Todo.Web/Client/Components/LogInForm.razor:3-26` |
| ACT-002 | External identity provider | External system, primary of UC-003 | GitHub, Google, Microsoft account or Auth0. Authenticates the person and returns them to the callback. Initiated from the system's side and answered by the provider, which is why the perimeter names it the initiator of the callback | System Inventory — External actors and systems; System Inventory — Entry points `EP-008`; `Todo.Web/Server/Authentication/AuthenticationExtensions.cs:39-92` |
| ACT-003 | Same person, reaching the API directly | Human, the same individual as ACT-001 | The perimeter's "authenticated caller holding a bearer token". The README addresses this role by name: run `Todo.Api` standalone, obtain a token from `/users/login`, then call the endpoints with the reference UI or a client of choice | System Inventory — Entry points `EP-010`–`EP-019`; `README.md`, "Using the API standalone" |

**One human being, two actor roles.** ACT-001 and ACT-003 are the same person. ACT-003 is not a second human actor and does not contradict the perimeter, which names exactly one: it is the role in which that person reaches the API without a cookie, holding a bearer token obtained from `/users/login` and calling the endpoints directly, as the delivery's own README directs. The role exists because the two routes authenticate differently and reach different operations — `EP-009` requires a cookie and rewrites it, while `EP-010` to `EP-019` accept any bearer token.

The task use cases therefore carry **one main flow with two scenarios** — through the screens, or directly with a bearer token — and are not split per actor. UC-009 and UC-010 are reached by ACT-003 alone, because no screen and no client call reaches `EP-011` or `EP-013`. UC-005 is reached by ACT-003 alone for the same reason: the client's six calls reach no Identity endpoint beyond register and login, so `EP-015`'s recovery and management operations have no screen.

```plantuml
@startuml
title Actor-goal matrix - each actor handle against the use cases it reaches, with the entry points it uses

left to right direction
skinparam shadowing false
skinparam wrapWidth 195

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

A1 --> UC1 : EP-002, EP-004
A1 --> UC2 : EP-002, EP-005
A1 --> UC3 : EP-002
A1 --> UC4 : EP-001, EP-006
A1 --> UC6 : EP-001, EP-003, EP-009
A1 --> UC7 : EP-003, EP-009
A1 --> UC8 : EP-003, EP-009

A3 --> UC1 : EP-015
A3 --> UC2 : EP-015
A3 --> UC5 : EP-015
A3 --> UC6 : EP-010
A3 --> UC7 : EP-012
A3 --> UC8 : EP-014
A3 --> UC9 : EP-011
A3 --> UC10 : EP-013
A3 --> UC11 : EP-017, EP-018, EP-019

A2 --> UC3 : EP-008, answered on the person's behalf

note right of UC5
  ACT-003 alone: no screen and no client call
  reaches EP-015. ACT-001 carries no edge here.
end note

note bottom of UC3
  EP-007 and EP-016 complete this use case for
  ACT-001; EP-008 is answered by ACT-002.
  Unreachable in the delivered configuration.
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


## Use-Case Specifications
Every flow below is the flow the code performs, not a flow anyone intended. Each step carries the file and lines it was read from; where the code contradicts a document, the code is recorded and the contradiction is named.

### UC-001 Create an account

| Field | Content |
|---|---|
| Primary actor | ACT-001 through `EP-002`; ACT-003 through `EP-015` |
| Trigger | The person activates Create User on the login form; or a caller posts to the API's registration endpoint |
| Precondition | None. An anonymous caller reaches it |
| Postcondition | A user row exists; the browser caller holds a session cookie whose `NameIdentifier` and `Name` are the email and whose token set carries an access token |

| # | Main flow — the screen route |
|---|---|
| 1 | The person enters an email and a password on `EP-002` and activates Create User. `Todo.Web/Client/Components/LogInForm.razor:3-26` |
| 2 | The client validates the fields: both required, the email at most 256 characters, the password 6 to 32 characters containing a lower-case letter, an upper-case letter, a digit and a special character. A failure stops the flow and the form reports the field error. `Todo.Web/Client/Components/LogInForm.razor:55-68` |
| 3 | The client posts `{ email, password }` to `/auth/register` `EP-004`. `Todo.Web/Client/TodoClient.cs` (`CreateUserAsync`) |
| 4 | The BFF posts the same body to the API's `/users/register` `EP-015`. `Todo.Web/Server/AuthClient.cs` (`CreateUserAsync`) |
| 5 | Identity creates the user, or refuses it against its password and email policy. `Todo.Api/Users/UsersApi.cs:20` |
| 6 | On success the BFF posts `/users/login`, receives an access token, and signs in on the cookie scheme with the email as both `NameIdentifier` and `Name`, storing the token in the token set. `Todo.Web/Server/AuthApi.cs:14-25,99-116` |
| 7 | The shell re-renders as signed in and shows the todo list `EP-003`. `Todo.Web/Client/TodoApp.razor:3-11` |

| Alternative or exception | What the code does | Anchor |
|---|---|---|
| A1 — the API refuses the registration | The API's answer is discarded and the BFF answers `401` with no body; the form shows the fixed string "Failed to create user". The same answer covers an email already taken, a password the Identity policy refuses, and an unreachable API. No recovered flow may claim a distinguishable failure | AN-021; `Todo.Web/Server/AuthApi.cs:14-25`; `Todo.Web/Server/AuthClient.cs`; `Todo.Web/Client/Components/LogInForm.razor:73-84` |
| A2 — the registration succeeds but the follow-up login fails | The user row now exists and no cookie is written; the person sees the same "Failed to create user" and a second attempt with the same email is refused as taken | `Todo.Web/Server/AuthClient.cs` (`CreateUserAsync`, which returns the token from a second call) |
| S2 — the direct route, ACT-003 | The caller posts to `EP-015` `/users/register` and then `/users/login`, and receives an `AccessTokenResponse` with `tokenType`, `accessToken`, `expiresIn` and `refreshToken`. No cookie is involved and the client-side validation of step 2 does not apply | `README.md`, "Using the API standalone"; `Todo.Api/Users/UsersApi.cs:20` |

```plantuml
@startuml
title UC-001 Create an account and UC-002 Sign in with email and password - the flow the code performs, and the one answer it gives on failure

skinparam shadowing false
skinparam wrapWidth 225

|ACT-001 Person and client|
start
:Enters an email and a password on EP-002;
:Client validation: both required, email at most 256
characters, password 6 to 32 with a lower-case letter,
an upper-case letter, a digit and a special character;
if (client validation fails) then (yes)
  :the form reports the field error and posts nothing;
  stop
else (no)
endif
if (the person chose Create User) then (create)
  :POST /auth/register EP-004;
  |BFF|
  :POST /users/register to the API EP-015;
  |API|
  :Identity creates the user, or refuses it
  against its own password and email policy;
  |BFF|
  if (the API answered success) then (yes)
    :POST /users/login to the API EP-015;
    |API|
    :Verifies the credentials and returns an access token;
    |BFF|
  else (no)
    :401 with no body;
    |ACT-001 Person and client|
    :shows the fixed string "Failed to create user";
    note right
      The same answer covers an email already taken, a password
      the Identity policy refuses, and an unreachable API:
      the BFF discards the API's validation problem. AN-021
    end note
    stop
  endif
else (login)
  :POST /auth/login EP-005;
  |BFF|
  :POST /users/login to the API EP-015;
  |API|
  :Verifies the credentials and returns an access token;
  |BFF|
endif
if (the token is null) then (yes)
  :401 with no body;
  |ACT-001 Person and client|
  :shows the fixed string "Login failed";
  stop
else (no)
endif
|BFF|
:Signs in on the cookie scheme with NameIdentifier = the email,
Name = the email, and the access token in the token set;
|ACT-001 Person and client|
:the shell re-renders as signed in and shows EP-003;
stop
@enduml
```

### UC-002 Sign in with email and password

| Field | Content |
|---|---|
| Primary actor | ACT-001 through `EP-002`; ACT-003 through `EP-015` |
| Trigger | The person activates Login on the login form; or a caller posts to the API's login endpoint |
| Precondition | An account exists |
| Postcondition | The browser caller holds a session cookie; the direct caller holds an access token |

| # | Main flow — the screen route |
|---|---|
| 1 | The person enters an email and a password on `EP-002` and activates Login. `Todo.Web/Client/Components/LogInForm.razor:3-26` |
| 2 | The client applies the same field validation as UC-001 step 2 and stops on a failure. `Todo.Web/Client/Components/LogInForm.razor:55-68` |
| 3 | The client posts `{ email, password }` to `/auth/login` `EP-005`. `Todo.Web/Client/TodoClient.cs` (`LoginAsync`) |
| 4 | The BFF posts the same body to the API's `/users/login` `EP-015`. `Todo.Web/Server/AuthClient.cs` (`GetTokenAsync`) |
| 5 | Identity verifies the credentials and answers an access token. `Todo.Api/Users/UsersApi.cs:20` |
| 6 | The BFF signs in on the cookie scheme with the email as both `NameIdentifier` and `Name`, and stores the token in the token set. `Todo.Web/Server/AuthApi.cs:27-38,99-116` |
| 7 | The shell re-renders as signed in and shows the todo list `EP-003`. `Todo.Web/Client/TodoApp.razor:3-11` |

| Alternative or exception | What the code does | Anchor |
|---|---|---|
| A1 — the credentials are refused | `401` with no body; the form shows "Login failed". A wrong password, an unconfirmed account, a locked account and an unreachable API are one answer | AN-021; `Todo.Web/Server/AuthApi.cs:27-38`; `Todo.Web/Server/AuthClient.cs` (`GetTokenAsync`) |
| A2 — the field validation fails | Nothing is posted. The password rule is the client's own and is stricter than the server's: the client rejects a password shorter than 6 or longer than 32 characters before Identity ever sees it | `Todo.Web/Client/Components/LogInForm.razor:60-68` |
| S2 — the direct route, ACT-003 | The caller posts `{ email, password }` to `EP-015` `/users/login` and receives an `AccessTokenResponse`; it attaches `Authorization: Bearer <accessToken>` to the task operations itself | `README.md`, "Using the API standalone" |

### UC-003 Sign in with an external provider

| Field | Content |
|---|---|
| Primary actor | ACT-001, with ACT-002 authenticating the person on its behalf |
| Trigger | The person follows a provider link on `EP-002` |
| Precondition | **False in the delivered configuration.** `Todo.Web/Server/appsettings.json` carries no `Authentication:Schemes` section, so `AuthenticationExtensions.cs:57-75` registers no provider and no link is rendered. The use case is recovered and marked unreachable in the delivered configuration (stakeholder, 2026-11-23) |
| Postcondition | A user row for the provider identity exists or is reused, a login row ties the provider key to it, and the caller holds a session cookie |

| # | Main flow |
|---|---|
| 1 | The person follows one provider link rendered on `EP-002`. `Todo.Web/Client/Components/LogInForm.razor:27-34`; `Todo.Web/Server/App.razor:44-52` |
| 2 | The BFF issues a challenge with the provider name taken from the route as the scheme list and `RedirectUri` set to `/auth/signin/{provider}`, and redirects to the provider. The name is checked against no registered scheme. `Todo.Web/Server/AuthApi.cs:55-62` |
| 3 | The provider authenticates the person and redirects to `/auth/signin/{provider}` `EP-008`. |
| 4 | The BFF authenticates the external cookie and reads `NameIdentifier`, and the email falling back to the principal name. `Todo.Web/Server/AuthApi.cs:64-77` |
| 5 | The BFF protects the provider key with a data-protection protector named after the provider and posts `{ username, providerKey }` to `/users/token/{provider}` `EP-016`. `Todo.Web/Server/AuthApi.cs:82-84` |
| 6 | The API creates a protector of the same name, unprotects the key, and finds or creates the user and its login row, then signs the principal in and returns an access token. `Todo.Api/Users/UsersApi.cs:24-60` |
| 7 | The BFF writes the session cookie with `NameIdentifier`, `Name`, the access token and the provider name in the authentication properties. `Todo.Web/Server/AuthApi.cs:88-90,99-116` |
| 8 | The BFF deletes the external cookie and redirects to `/`. `Todo.Web/Server/AuthApi.cs:92-94` |

| Alternative or exception | What the code does | Anchor |
|---|---|---|
| A1 — the provider name in the route is not a registered scheme | The challenge names a scheme that does not exist and the handler raises rather than answering a redirect or a 404 | AN-019; `Todo.Web/Server/AuthApi.cs:55-62` |
| A2 — the external ticket is absent, the token exchange returns null, or the cookie sign-in does not take effect | No cookie is written; the external cookie is still deleted; the person is redirected to `/` with no message and cannot tell a rejected provider from an unreachable API. The code's own `// TODO: Handle the failure somehow` marks it | AN-020; `Todo.Web/Server/AuthApi.cs:64-97` |
| A3 — the two processes do not share a data-protection key ring | `Unprotect` in the API fails on a key protected in the BFF. Only the application discriminator is set in either process | AN-010; `Todo.Web/Server/Program.cs:13`; `Todo.Api/Program.cs:11` |
| A4 — the provider identity has no email claim | The user is created with the principal name as its user name, and that name becomes the account identity with no password | `Todo.Web/Server/AuthApi.cs:70-71` |

```plantuml
@startuml
title UC-003 Sign in with an external provider - the flow the code performs, and where the delivered configuration stops it

skinparam shadowing false
skinparam wrapWidth 215

|ACT-001 Person and client|
start
:Follows one provider link rendered on EP-002;
note right
  In the delivered configuration no provider is registered:
  Todo.Web/Server/appsettings.json carries no
  Authentication:Schemes section, so no link is rendered
  and this use case cannot be entered.
  AuthenticationExtensions.cs:57-75
end note
:GET /auth/login/{provider} EP-007;

|BFF|
:Results.Challenge with the provider name taken from the
route as the scheme list, RedirectUri /auth/signin/{provider};
note right
  The name is checked against no registered scheme, so an
  unmatched segment raises in the handler instead of
  answering a redirect or a 404. AN-019
end note
:Redirects the browser to the provider;

|ACT-002 External identity provider|
:Authenticates the person;
:Redirects to /auth/signin/{provider} EP-008;

|BFF|
:Authenticates against the external cookie scheme;
if (the external ticket) then (succeeded)
  :Reads NameIdentifier, and the email falling back
  to the principal name;
  :Creates a protector named after the provider and
  protects the provider key for transport;
  :POST /users/token/{provider} EP-016;
  |API|
  :Creates a protector of the same name and unprotects the key;
  if (a login for that provider and key exists) then (yes)
    :uses that user;
  else (no)
    :creates a user named after the email;
    :adds the login for the provider and key;
  endif
  :Signs the principal in and returns an access token;
  |BFF|
  :Signs in with a cookie carrying NameIdentifier,
  Name and the access token;
else (absent, or the exchange returned null)
  :no session cookie is written;
endif
:Deletes the external cookie;
:Redirects to /;
note right
  Every path reaches this redirect: a rejected provider,
  a null exchange and a failed cookie sign-in are
  indistinguishable and nothing is reported. AN-020
end note
stop
@enduml
```

### UC-004 Sign out

| Field | Content |
|---|---|
| Primary actor | ACT-001 |
| Trigger | The person activates Logout in the shell |
| Precondition | A session cookie exists |
| Postcondition | The session cookie is cleared; the shell renders the login form |

| # | Main flow |
|---|---|
| 1 | The person activates Logout on `EP-001`. `Todo.Web/Client/TodoApp.razor:8` |
| 2 | The client posts to `/auth/logout` `EP-006`. `Todo.Web/Client/TodoClient.cs` (`LogoutAsync`) |
| 3 | The endpoint requires authorization, so a request without a valid cookie is refused at the door. `Todo.Web/Server/AuthApi.cs:49-50` |
| 4 | The cookie is signed out. No remote sign-out is performed: the code's own `// TODO: Support remote logout` marks the gap, so a provider session opened by UC-003 stays open at the provider. `Todo.Web/Server/AuthApi.cs:40-52` |
| 5 | On success the client clears the displayed user and the shell renders the login form `EP-002`. `Todo.Web/Client/TodoApp.razor:19-21,32-38` |

| Alternative or exception | What the code does | Anchor |
|---|---|---|
| A1 — the request is refused | The client leaves the shell signed in; nothing is reported | `Todo.Web/Client/TodoApp.razor:32-38` |
| A2 — the session was opened through a provider | The local cookie is cleared and the provider's own session is untouched, so the next provider sign-in may complete without the person authenticating again | `Todo.Web/Server/AuthApi.cs:44-48` |

### UC-005 Maintain one's own account

| Field | Content |
|---|---|
| Primary actor | ACT-003. No screen and no client call reaches any of these endpoints |
| Trigger | A caller posts to one of the Identity endpoints under `/users` |
| Precondition | The operation decides its own: refresh and manage require a bearer token, the recovery endpoints do not |
| Postcondition | The operation's effect: a refreshed token, a confirmed email, a reset password, a pending two-factor change, an updated profile |

| # | Main flow of the shared shape |
|---|---|
| 1 | The caller posts to one of the endpoints the framework maps under `/users` `EP-015`: `refresh`, `confirmEmail`, `resendConfirmationEmail`, `forgotPassword`, `resetPassword`, `manage/2fa`, `manage/info`. `Todo.Api/Users/UsersApi.cs:20` |
| 2 | No rate limit applies: the token-bucket policy is required on `/todos` only. `Todo.Api/Extensions/RateLimitExtensions.cs:38-47`; `Todo.Api/Todos/TodoApi.cs:19` |
| 3 | The endpoint performs its operation against the Identity stores and answers the framework's own shape, which for a failure is a problem detail naming the cause — not the single 401 that UC-001 and UC-002 collapse to. `Todo.Api/Users/UsersApi.cs:20` |
| 4 | The effect is durable: the person's email is confirmed, their password replaced, or a new token pair issued. |

| Alternative or exception | What the code does | Anchor |
|---|---|---|
| A1 — no screen reaches any of these | The client makes six calls and none of them is an Identity endpoint beyond register and login: `AddTodoAsync`, `DeleteTodoAsync`, `GetTodosAsync`, `LoginAsync`, `CreateUserAsync` (which posts `/auth/register`) and `LogoutAsync`. Every operation here is reachable only by an API caller, so the UI cannot confirm an email, reset a password or refresh a token. ACT-001 therefore carries no edge to this use case | `Todo.Web/Client/TodoClient.cs:7-71` |
| A2 — an anonymous caller floods the recovery endpoints | No limit applies, and the policy as written could not simply be extended to them: it partitions on `NameIdentifier`, which an anonymous caller does not have | AN-009; `Todo.Api/Extensions/RateLimitExtensions.cs:38-47` |

### UC-006 See one's own tasks

| Field | Content |
|---|---|
| Primary actor | ACT-001 through the screens; ACT-003 through the API |
| Trigger | The shell renders the signed-in state; or a caller sends `GET /todos` |
| Precondition | The caller holds a valid session cookie (screens) or a bearer token (API), and a user row exists for it |
| Postcondition | The caller's own rows are read; nothing is written |

| # | Main flow — the screen route |
|---|---|
| 1 | The shell resolves the authentication state and, when a user name is present, renders the todo list `EP-003` with a spinner while the load is in flight. `Todo.Web/Server/App.razor:44-52`; `Todo.Web/Client/Components/TodoList.razor:3-8` |
| 2 | The list calls `GET todos` on initialization. `Todo.Web/Client/Components/TodoList.razor:44-55` |
| 3 | The request reaches the BFF's `/todos` group `EP-009`, which requires the cookie and rewrites the session's access token into `Authorization: Bearer`. `Todo.Web/Server/TodoApi.cs:12-25` |
| 4 | The API requires a bearer token and resolves the caller from the database by the token's `NameIdentifier`; a token for a user row that does not exist fails the requirement. `Todo.Api/Todos/TodoApi.cs:17`; `Todo.Api/Authorization/CheckCurrentUserAuthHandler.cs:31-36` |
| 5 | The per-user token bucket applies to the whole group, answering 429 when empty. `Todo.Api/Todos/TodoApi.cs:19-20`; `Todo.Api/Extensions/RateLimitExtensions.cs:38-47` |
| 6 | The query filters on `OwnerId` equal to the caller and declares no order; `OwnerId` is excluded from the returned shape. `Todo.Api/Todos/TodoApi.cs:24-27`; `Todo.Api/Todos/Todo.cs:15-21` |
| 7 | The list renders one row per task with its title and a remove control. The checkbox beside each row is bound to nothing. `Todo.Web/Client/Components/TodoList.razor:21-31` |

| Alternative or exception | What the code does | Anchor |
|---|---|---|
| A1 — the load answers 401 or 403 | The shell drops to the login form: the list raises `OnForbidden` and the shell's handler signs out | `Todo.Web/Client/Components/TodoList.razor:47-55`; `Todo.Web/Client/TodoApp.razor:3-11` |
| A2 — the caller's rows are empty | No list is rendered and no empty state is shown; the input stays available | `Todo.Web/Client/Components/TodoList.razor:21-31` |
| A3 — the bucket is empty | 429, and the client reports nothing; the spinner leaves the list empty | `Todo.Api/Extensions/RateLimitExtensions.cs:38-47` |
| S2 — the direct route, ACT-003 | The caller sends `GET /todos` with `Authorization: Bearer` itself and receives the `TodoItem` array. Steps 1 to 3 do not apply | `README.md`, "Using the API standalone"; `Todo.Api/Todos/TodoApi.cs:24-27` |
| Not modelled | The list applies no `admin` branch, while `EP-011`, `EP-013` and `EP-014` each admit one, so a caller in that role can reach a row by id that this use case cannot show. The disagreement is recorded (AN-018); the branch is not recovered as behaviour | AN-018; `Todo.Api/Todos/TodoApi.cs:24-27` vs `:29-36,52-65,67-73` |

### UC-007 Add a task

| Field | Content |
|---|---|
| Primary actor | ACT-001 through the screens; ACT-003 through the API |
| Trigger | The person submits the new-todo input; or a caller sends `POST /todos` |
| Precondition | The caller is authorized as in UC-006 |
| Postcondition | One `Todos` row exists with `OwnerId` set to the caller and `IsComplete` false |

| # | Main flow — the screen route |
|---|---|
| 1 | The person types a title in the input on `EP-003` and submits. `Todo.Web/Client/Components/TodoList.razor:12-19` |
| 2 | The client validates the title, which is required; an empty value stops the flow and the field error is shown. `Todo.Web/Client/Components/TodoList.razor:36-38,12-19` |
| 3 | The client posts `{ title }` to `todos` `EP-009`. `Todo.Web/Client/TodoClient.cs` (`AddTodoAsync`) |
| 4 | The BFF requires the cookie and rewrites the token; the API requires the token, resolves the caller, applies the rate limit and validates `Title` as required, answering 400 with a problem detail when it is missing. `Todo.Web/Server/TodoApi.cs:12-25`; `Todo.Api/Todos/TodoApi.cs:17-22`; `Todo.Api/Filters/ValidationFilter.cs:12-63` |
| 5 | A `Todo` row is inserted with `OwnerId` set to the caller and `IsComplete` left false. `Todo.Api/Todos/TodoApi.cs:38-50` |
| 6 | The API answers 201 with `Location: /todos/{id}` and the created `TodoItem`. `Todo.Api/Todos/TodoApi.cs:49` |
| 7 | The client appends the returned row to the list without reloading, clears the input and marks the form unmodified. `Todo.Web/Client/Components/TodoList.razor:57-67` |

| Alternative or exception | What the code does | Anchor |
|---|---|---|
| A1 — the title is empty | The client posts nothing and shows the field error; a caller that posts an empty title anyway receives 400 `ValidationProblemDetails` | `Todo.Web/Client/Components/TodoList.razor:36-38`; `Todo.Api/Filters/ValidationFilter.cs` |
| A2 — the API answers a failure | The client returns null, nothing is appended and nothing is reported to the person | `Todo.Web/Client/TodoClient.cs` (`AddTodoAsync`); `Todo.Web/Client/Components/TodoList.razor:57-67` |
| A3 — the body's `OwnerId` | The request shape carries no `OwnerId`, so a caller cannot create a row for someone else: the field is set from the resolved caller | `Todo.Api/Todos/Todo.cs:15-21`; `Todo.Api/Todos/TodoApi.cs:38-50` |
| S2 — the direct route, ACT-003 | The caller posts `{ title }` with its own bearer token and receives 201 with the created item | `README.md`; `Todo.Api/Todos/TodoApi.cs:38-50` |

```plantuml
@startuml
title UC-007 Add a task - the flow the code performs, across the three process boundaries it crosses

skinparam shadowing false
skinparam wrapWidth 210

|ACT-001 Person and client|
start
:The person types a title in the new-todo input
and submits the form;
:EditForm validates NewTodo, which is required;
if (the title is empty) then (yes)
  :nothing is posted;
  stop
else (no)
endif
:TodoClient.AddTodoAsync posts {title} to /todos
EP-009;

|BFF|
:A cookie session is required;
:The access token is rewritten into
Authorization: Bearer;
:Forwarded to the API;

|API|
:A bearer token is required and the user row
must exist for the caller;
:The per-user token bucket applies, 429 when empty;
:The validation filter checks Title, which is required;
if (Title is missing or empty) then (yes)
  :400 ValidationProblemDetails;
  |ACT-001 Person and client|
  :the client discards the problem and shows nothing;
  stop
else (no)
endif
|API|
:Insert Todo {Title, OwnerId = the caller,
IsComplete = false};
:201 Created with the created TodoItem;
|ACT-001 Person and client|
:appends the returned row and clears the input;
stop
@enduml
```

### UC-008 Remove a task

| Field | Content |
|---|---|
| Primary actor | ACT-001 through the screens; ACT-003 through the API |
| Trigger | The person activates the remove control on a row; or a caller sends `DELETE /todos/{id}` |
| Precondition | The caller is authorized as in UC-006 |
| Postcondition | The row is deleted, or was never the caller's |

| # | Main flow — the screen route |
|---|---|
| 1 | The person activates the remove control on a row of `EP-003`. `Todo.Web/Client/Components/TodoList.razor:28` |
| 2 | The client sends `DELETE todos/{id}` through `EP-009`. `Todo.Web/Client/TodoClient.cs` (`DeleteTodoAsync`) |
| 3 | The BFF requires the cookie and rewrites the token; the API requires the token, resolves the caller and applies the rate limit. `Todo.Web/Server/TodoApi.cs:12-25`; `Todo.Api/Todos/TodoApi.cs:17-20` |
| 4 | The delete runs against the rows where `Id` equals the route id and `OwnerId` equals the caller. `Todo.Api/Todos/TodoApi.cs:69-71` |
| 5 | One row affected answers 200 with no body; the client removes the row from the list without reloading. `Todo.Api/Todos/TodoApi.cs:73`; `Todo.Web/Client/Components/TodoList.razor:69-76` |

| Alternative or exception | What the code does | Anchor |
|---|---|---|
| A1 — no row matches | 404, whether the row does not exist or belongs to someone else: the two are never distinguished, so the operation cannot be used to probe for another person's ids through its answer alone | `Todo.Api/Todos/TodoApi.cs:73` |
| A2 — the delete fails | The row stays in the list and nothing is reported | `Todo.Web/Client/Components/TodoList.razor:69-76` |
| S2 — the direct route, ACT-003 | The caller sends `DELETE /todos/{id}` with its own bearer token | `README.md`; `Todo.Api/Todos/TodoApi.cs:67-73` |
| Not modelled | The same predicate also admits an `admin` role claim no running caller holds, so a caller with a self-minted token could delete another person's row. Not recovered as behaviour | AN-004; `Todo.Api/Todos/TodoApi.cs:69` |

### UC-009 Read one task by id

| Field | Content |
|---|---|
| Primary actor | ACT-003. No screen and no client call reaches it |
| Trigger | A caller sends `GET /todos/{id}` |
| Precondition | The caller is authorized as in UC-006 |
| Postcondition | Nothing is written |

| # | Main flow |
|---|---|
| 1 | The caller sends `GET /todos/{id}` with a bearer token `EP-011`. `Todo.Api/Todos/TodoApi.cs:29-36` |
| 2 | The API requires the token, resolves the caller and applies the rate limit. `Todo.Api/Todos/TodoApi.cs:17-20` |
| 3 | The row is looked up by primary key. The match admits the owner; the second alternative on that predicate is not reachable in the running system. `Todo.Api/Todos/TodoApi.cs:29-36` |
| 4 | A match answers 200 with the `TodoItem`, `OwnerId` excluded. `Todo.Api/Todos/Todo.cs:15-26` |
| 5 | No match answers 404 for a row that is absent and for a row belonging to someone else alike. `Todo.Api/Todos/TodoApi.cs:29-36` |

| Alternative or exception | What the code does | Anchor |
|---|---|---|
| A1 — the route id is not an integer | The route constraint does not match and the request answers 404 before the handler runs | route template `/{id}` at `Todo.Api/Todos/TodoApi.cs:29` |
| A2 — the client has no path here | The client makes six calls and none of them reads a single todo, so this operation is reachable only by an API caller | `Todo.Web/Client/TodoClient.cs:7-71` |

### UC-010 Change a task, including marking it complete

| Field | Content |
|---|---|
| Primary actor | ACT-003. **API operation only**: the client makes no update call and the list's checkbox is bound to nothing (AN-001, stakeholder decision of 2026-11-23) |
| Trigger | A caller sends `PUT /todos/{id}` |
| Precondition | The caller is authorized as in UC-006 |
| Postcondition | That row's `Title` and `IsComplete` are set to the request's values |

| # | Main flow |
|---|---|
| 1 | The caller sends `PUT /todos/{id}` with `{ id, title, isComplete }` and a bearer token `EP-013`. `Todo.Api/Todos/TodoApi.cs:52-65` |
| 2 | The API requires the token, resolves the caller, applies the rate limit, and validates `Title` as required. `Todo.Api/Todos/TodoApi.cs:17-22`; `Todo.Api/Filters/ValidationFilter.cs` |
| 3 | A body whose `id` differs from the route id answers 400 and no row is read. `Todo.Api/Todos/TodoApi.cs:54-57` |
| 4 | One statement sets `Title` and `IsComplete` on the rows where `Id` equals the route id and `OwnerId` equals the caller. `Todo.Api/Todos/TodoApi.cs:59-63` |
| 5 | Zero rows affected answers 404; otherwise 200 with no body. `Todo.Api/Todos/TodoApi.cs:65` |

| Alternative or exception | What the code does | Anchor |
|---|---|---|
| A1 — the title is empty | 400 `ValidationProblemDetails`, and no row is updated | `Todo.Api/Filters/ValidationFilter.cs`; `Todo.Api/Todos/Todo.cs:18-19` |
| A2 — the body's id and the route id disagree | 400 before any row is read | `Todo.Api/Todos/TodoApi.cs:54-57` |
| A3 — the row is absent or another person's | 404, undistinguished | `Todo.Api/Todos/TodoApi.cs:65` |
| A4 — completion | `IsComplete` is written here and nowhere else. This is the only operation that can set it, and no client call reaches it, so a task's completion state is stored on every row and can be changed by no screen | AN-001; `Todo.Web/Client/TodoClient.cs:7-71`; `Todo.Web/Client/Components/TodoList.razor:24-27` |
| Not modelled | The same predicate also admits an `admin` role claim no running caller holds | AN-004; `Todo.Api/Todos/TodoApi.cs:59` |

```plantuml
@startuml
title UC-010 Change a task - the flow the code performs, and why no screen reaches it

skinparam shadowing false
skinparam wrapWidth 220

|ACT-003 Developer using the API directly|
start
note right
  No path from EP-003 reaches this use case: the list's
  checkbox is bound to nothing and TodoClient exposes no
  update call. Reached only as an API operation. AN-001
end note
:A caller PUTs /todos/{id} with {id, title, isComplete}
EP-013;

|BFF|
:A cookie session is required;
:The access token is rewritten into the bearer header;
:Forwarded to the API;

|API|
:A bearer token is required and the user row must exist;
:The per-user token bucket applies, 429 when empty;
:The validation filter checks Title, which is required;
if (the body id differs from the route id) then (yes)
  :400, no row is read;
  stop
else (no)
endif
:Update runs against the rows where
Id equals the route id and OwnerId equals the caller;
note right
  The same predicate also admits an admin role claim.
  No running caller holds it, so the branch is an
  exceptional entity and is not part of this flow.
  AN-004, stakeholder 2026-11-23
end note
if (rows affected is zero) then (yes)
  :404 NotFound, whether the row is absent
  or belongs to someone else;
  stop
else (no)
endif
:Sets Title and IsComplete on that row;
:200 Ok with no body;
stop
@enduml
```

### UC-006, UC-008, UC-009 and UC-010 — the gate they share

The four task use cases pass the same gate, which is stated once here and referenced from each flow above.

```plantuml
@startuml
title UC-006, UC-009, UC-010 and UC-008 - the gate every task operation passes, and the one rule that decides which rows it may touch

skinparam shadowing false
skinparam wrapWidth 225

|Caller|
start
:An HTTP request to /todos or /todos/{id};
note right
  Reached two ways: through EP-009, where the BFF requires a
  cookie and rewrites it into a bearer header, or directly at
  the API with any bearer token the caller holds. AN-002
end note

|API|
if (a bearer token is present and valid) then (yes)
else (no)
  :401;
  stop
endif
:The current user is resolved from the database
by the token's NameIdentifier;
if (the row exists) then (yes)
else (no)
  :the authorization handler does not succeed, so the
  requirement fails and the request is refused;
  stop
endif
:The per-user token bucket applies to the whole /todos group;
if (the bucket is empty) then (yes)
  :429 Too Many Requests;
  stop
else (no)
endif
:Body parameters are checked against data annotations;
if (a model is invalid) then (yes)
  :400 ValidationProblemDetails;
  stop
else (no)
endif
:Query on the caller's own rows;
note right
  UC-006 filters on OwnerId equals the caller and declares no
  order. UC-009, UC-010 and UC-008 admit the same predicate plus
  an admin role claim no running caller holds, and answer 404
  when no row matches, so a row belonging to someone else is
  never distinguished from one that does not exist. AN-004, AN-018
end note
if (the operation is UC-006) then (yes)
  :200 with the caller's TodoItem list, OwnerId excluded;
  stop
else (no)
endif
if (no row is affected or found) then (yes)
  :404 NotFound;
  stop
else (no)
endif
if (the operation is UC-009) then (yes)
  :200 with the TodoItem;
else (no)
  :200 Ok with no body;
endif
stop
@enduml
```

### UC-011 Consult the API reference

| Field | Content |
|---|---|
| Primary actor | ACT-003 |
| Trigger | A caller requests the API's root, the OpenAPI document, or the reference UI |
| Precondition | For the rendered UI, the API runs in the Development environment |
| Postcondition | The caller has read the API contract; nothing is written |

| # | Main flow |
|---|---|
| 1 | The caller requests `GET /` on the API `EP-017`. `Todo.Api/Program.cs:62` |
| 2 | The API redirects to `/scalar/v1` in every environment, although the reference UI is mapped only when the environment is Development. `Todo.Api/Program.cs:49-56,62` |
| 3 | The caller reads the contract: either the rendered Scalar UI `EP-019` with the bearer scheme preselected as the preferred security scheme, or the OpenAPI document at `/openapi/v1.json` `EP-018`, which carries the bearer scheme and marks every operation that requires authorization. `Todo.Api/Program.cs:49-56`; `Todo.Api/Extensions/OpenApiOptionsExtensions.cs` |

| Alternative or exception | What the code does | Anchor |
|---|---|---|
| A1 — the API runs outside Development | The reference UI is not mapped while the root redirect still fires, so the caller is sent to an endpoint the process does not serve | AN-017; `Todo.Api/Program.cs:49-56,62` |
| A2 — the caller reads the delivery's README instead | The README directs the reader to a Swagger UI; the code mounts the Scalar reference UI and no Swagger UI exists anywhere in the tree | AN-008; `README.md`, "Using the API standalone" |
| A3 — the document's server list | The UI is configured with an empty server list, so a client generated from the document carries no base address | `Todo.Api/Program.cs:51` |

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
