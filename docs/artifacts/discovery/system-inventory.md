## Document Control

Phase: Survey
Status: Draft — first reading of the delivered system
Milestone Target: End-of-Survey (SBC) — not yet achieved

## Perimeter

The delivered system is the public sample `davidfowl/TodoApp` (MIT) at commit `307a1ead` of 2026-02-12, copied wholesale into this repository. It is a multi-process .NET 9 solution: a Blazor WebAssembly client served by a Blazor server host acting as a backend-for-frontend, a minimal-API backend, an Aspire orchestrator, a shared service-defaults library, and an integration-test project.

```plantuml
@startuml
title Perimeter of the existing TodoApp system — components, stores and external systems
skinparam componentStyle rectangle
skinparam shadowing false

actor "Person using the task list" as USER

package "TodoApp solution — 7 projects (Source: TodoApp.sln)" {
  component "Todo.Web.Client\nBlazor WASM\nRazor components" as WASM
  component "Todo.Web.Shared\nSharedClass only" as SHARED
  component "Todo.Web.Server\nBFF · cookie auth · YARP forwarder" as BFF
  component "Todo.Api\nASP.NET Core minimal API" as API
  component "TodoApp.ServiceDefaults\nhealth checks · OpenTelemetry · service discovery" as SD
  component "TodoApp.AppHost\nAspire orchestrator · EF migration step" as APPHOST
  component "Todo.Api.Tests\nxunit · MVC.Testing · InMemory EF" as TESTS
}

node "Browser" as BROWSER
database "SQLite file\n.db/Todos.db — 8 tables" as DB
component "sqliteweb\n<<docker container tomdesinto/sqliteweb>>" as SQLWEB
cloud "External identity providers\nGitHub · Google · Microsoft · Auth0 OIDC" as EXT
cloud "OTLP endpoint\n(only if OTEL_EXPORTER_OTLP_ENDPOINT is set)" as OTLP
cloud "NuGet feed\napi.nuget.org · packageSourceMapping '*'" as NUGET

USER --> BROWSER
BROWSER --> WASM : runs (assets served by BFF)
BROWSER --> BFF : HTTPS · auth cookie
BFF --> API : YARP forwarder\nhttp://todoapi · Bearer access token
BFF --> EXT : OIDC / OAuth challenge\n/auth/login/{provider}
API --> DB : EF Core Sqlite\nconnection string "Todos"
SQLWEB --> DB : browse\n(run mode only)
APPHOST ..> API : launches · "dotnet ef database update"
APPHOST ..> BFF : launches
APPHOST ..> SQLWEB : launches
API ..> SD : AddServiceDefaults()
BFF ..> SD : AddServiceDefaults()
TESTS ..> API : WebApplicationFactory\nin-process · EF InMemory
API ..> OTLP : logs · metrics · spans
BFF ..> OTLP : logs · metrics · spans
NUGET ..> API : restore (Directory.Packages.props)
NUGET ..> BFF : restore
WASM --> SHARED
BFF --> SHARED

note right of API
  Endpoint groups (Source: Todo.Api/Program.cs):
  MapTodos() -> /todos
  MapUsers() -> /users (MapIdentityApi + /token/{provider})
  /openapi, /scalar/v1 (dev only), /, /health, /alive
end note
note right of BFF
  Endpoint groups (Source: Todo.Web/Server/Program.cs):
  MapAuth() -> /auth/*
  MapTodos() -> /todos/{*path} forwarded
end note
@enduml
```

| Component | What it is | Boundary the code shows |
|---|---|---|
| `Todo.Api` | ASP.NET Core minimal API; owns the data and all business rules | The only writer of the SQLite file. Authenticates with the Identity bearer scheme. `Source: Todo.Api/Program.cs`, `Todo.Api/Todos/TodoApi.cs`, `Todo.Api/Users/UsersApi.cs` |
| `Todo.Web.Server` | BFF; owns the browser session (cookie) and forwards `/todos` to the API | Holds the access token inside the auth cookie and re-issues it as a Bearer header. `Source: Todo.Web/Server/TodoApi.cs` |
| `Todo.Web.Client` | Blazor WebAssembly assembly running in the browser | Talks only through relative URLs (`todos`, `auth/login`, …), so it reaches the BFF and never the API directly. `Source: Todo.Web/Client/TodoClient.cs` |
| `Todo.Web.Shared` | Project reference shared by Client and Server | Holds one empty class. `Source: Todo.Web/Shared/SharedClass.cs` (unread — declared from the tree) |
| `TodoApp.ServiceDefaults` | Cross-cutting library: OpenTelemetry, health checks, service discovery, resilience | Referenced by both runnable hosts, not by the client. `Source: TodoApp.ServiceDefaults/Extensions.cs` |
| `TodoApp.AppHost` | Aspire orchestration; also runs the EF migration before the API starts | Launches API and BFF, optionally `sqliteweb`; creates `.db/` and runs `dotnet ef database update` when the directory is absent. `Source: TodoApp.AppHost/Program.cs`, `TodoApp.AppHost/Extensions.cs` |
| `Todo.Api.Tests` | xunit integration suite | Drives `Todo.Api` in-process with a real SQLite in-memory connection. `Source: Todo.Api.Tests/TodoApplication.cs`, `Todo.Api.Tests/TodoApiTests.cs`, `Todo.Api.Tests/UserApiTests.cs` |

External systems and stores, each with the anchor that proves the dependency:

| External element | Direction | Anchor |
|---|---|---|
| External identity providers — GitHub, Google, Microsoft, Auth0 | BFF → provider (OAuth2 / OIDC) | `Todo.Web/Server/Authentication/AuthenticationExtensions.cs` registers the four schemes by name, each only when its `Authentication:Schemes:<name>` section exists |
| SQLite database file `.db/Todos.db` | API → file | `Todo.Api/Program.cs` connection string `"Todos"` with fallback `Data Source=.db/Todos.db` |
| `tomdesinto/sqliteweb` container | AppHost → container, container → database file | `TodoApp.AppHost/Program.cs` |
| OTLP endpoint | API and BFF → collector | `TodoApp.ServiceDefaults/Extensions.cs` exports only when `OTEL_EXPORTER_OTLP_ENDPOINT` is non-empty |
| `api.nuget.org` | build → feed | `nuget.config` clears inherited sources and maps `*` to nuget.org |

The entry-point surface, recorded because every recovered use case must point back to it:

```plantuml
@startuml
title Entry-point surface — the traces the use cases will be recovered from
skinparam componentStyle rectangle
skinparam shadowing false

actor "Visitor" as VIS
actor "Signed-in user" as USR
actor "Administrator\n(role claim only)" as ADM

package "Todo.Web.Server — BFF (Source: Todo.Web/Server/AuthApi.cs, TodoApi.cs)" {
  component "POST /auth/register" as BREG
  component "POST /auth/login" as BLOGIN
  component "POST /auth/logout" as BLOGOUT
  component "GET /auth/login/{provider}\nchallenge" as BEXT
  component "GET /auth/signin/{provider}\ncallback" as BSIGN
  component "/todos/{*path}\nYARP forward + Bearer transform" as BFWD
}

package "Todo.Api (Source: Todo.Api/Todos/TodoApi.cs, Users/UsersApi.cs)" {
  component "GET /todos\nown todos only" as TGET
  component "GET /todos/{id}\nowner or admin" as TGET1
  component "POST /todos\ntitle + owner from claim" as TPOST
  component "PUT /todos/{id}\nowner or admin · title + IsComplete" as TPUT
  component "DELETE /todos/{id}\nowner or admin" as TDEL
  component "POST /users/register · /users/login · /users/refresh\n+ MapIdentityApi group" as UIDN
  component "POST /users/token/{provider}\nexternal login, protected provider key" as UEXT
}

package "Todo.Web.Client (Source: Todo.Web/Client/TodoClient.cs, Components/TodoList.razor)" {
  component "Todo list screen\nadd · list · delete" as UI1
  component "Log-in screen" as UI2
}

VIS --> BREG
VIS --> BLOGIN
VIS --> BEXT
USR --> BLOGOUT
USR --> UI1
UI1 --> BFWD
UI2 --> BREG
UI2 --> BLOGIN
BREG --> UIDN
BLOGIN --> UIDN
BEXT --> BSIGN
BSIGN --> UEXT
BFWD --> TGET
BFWD --> TDEL
ADM -.-> TGET1
ADM -.-> TPUT
ADM -.-> TDEL
TGET --> TGET1

note right of UI1
  No completion toggle in the UI even though
  PUT /todos/{id} sets IsComplete
  (TodoList.razor renders an unbound checkbox)
end note
note bottom of BFWD
  Every /todos request carries the access token
  stored in the auth cookie (TokenNames.AccessToken)
end note
note bottom of UIDN
  /users group carries no group-level authorization;
  MapIdentityApi supplies its own endpoint set
end note
@enduml
```

Scheduled jobs, batch processes and reports: none. `Source: TodoApp/` tree — no hosted service, no timer, no job configuration.

## Technology and Size

| Concern | Value | Anchor |
|---|---|---|
| Framework | `net9.0`, `Nullable enable`, `ImplicitUsings enable`, `LangVersion preview` | `Directory.Build.props` |
| SDK | `9.0.100`, `rollForward: latestFeature`, `allowPrerelease: true` | `global.json` |
| Package management | Central (`ManagePackageVersionsCentrally`), 28 pins | `Directory.Packages.props` |
| Persistence | EF Core 9.0.8 + `Microsoft.EntityFrameworkCore.Sqlite` 9.0.8 | `Directory.Packages.props`, `Todo.Api/Todo.Api.csproj` |
| Identity | `Microsoft.AspNetCore.Identity.EntityFrameworkCore` 9.0.8, `AddIdentityCore<TodoUser>()` + `AddEntityFrameworkStores` + `AddApiEndpoints` | `Todo.Api/Program.cs` |
| Authentication | Bearer token scheme in the API; cookie scheme in the BFF; four external OAuth/OIDC schemes | `Todo.Api/Program.cs`, `Todo.Web/Server/Authentication/AuthenticationExtensions.cs` |
| Proxying | `Yarp.ReverseProxy` 2.3.0 with `MapForwarder` and a request transform | `Todo.Web/Server/TodoApi.cs` |
| Service discovery | `Microsoft.Extensions.ServiceDiscovery` 9.5.0 + `.Yarp` 9.5.0; the BFF resolves the base address `http://todoapi` | `Todo.Web/Server/Program.cs` |
| Observability | OpenTelemetry 1.12.0 (AspNetCore, Http, Runtime) + HttpLogging | `TodoApp.ServiceDefaults/Extensions.cs`, `Todo.Api/Program.cs` |
| API documentation surface | `Microsoft.AspNetCore.OpenApi` + `Scalar.AspNetCore` 2.6.8, mapped in Development only | `Todo.Api/Program.cs` |
| Validation | `MiniValidation` 0.9.2 via `WithParameterValidation` | `Todo.Api/Todos/TodoApi.cs` |
| Tests | xunit 2.9.3, `Microsoft.AspNetCore.Mvc.Testing` 9.0.8, `coverlet.collector` 6.0.4, `EntityFrameworkCore.InMemory` 9.0.8 | `Todo.Api.Tests/Todo.Api.Tests.csproj` |
| Build/CI | GitHub Actions: restore, build Release, test Release on push and pull request | `.github/workflows/ci.yaml` |

Size, by project and by what the tree shows:

| Project | Composition | Weight |
|---|---|---|
| `Todo.Api` | `Program.cs`, `TodoDbContext.cs`, `Todos/` (2), `Users/` (2), `Authorization/` (3), `Extensions/` (2), `Filters/` (1), `Migrations/` (7), 2 `appsettings`, `launchSettings.json` | The heaviest hand-written area; the only area carrying migrations |
| `Todo.Web.Server` | `Program.cs`, `AuthApi.cs`, `AuthClient.cs`, `TodoApi.cs`, `Authentication/` (5), `App.razor`, `_Imports.razor`, 2 `appsettings`, `launchSettings.json` | Second heaviest; concentrates the authentication logic |
| `Todo.Web.Client` | `Program.cs`, `TodoApp.razor`, `TodoClient.cs`, `_Imports.razor`, `Components/` (2 razor), `wwwroot/` (45 vendored Bootstrap files, `css/app.css`, `bg.png`, `favicon.ico`) | Small hand-written surface behind a large vendored asset tree |
| `Todo.Api.Tests` | 6 C# files including the fixture, token helper and two test classes | ~16 KB of test source |
| `TodoApp.AppHost` | `Program.cs`, `Extensions.cs`, 2 `appsettings`, `launchSettings.json` | ~2.4 KB of orchestration |
| `TodoApp.ServiceDefaults` | `Extensions.cs` | ~4.5 KB |
| `Todo.Web.Shared` | `SharedClass.cs` | Placeholder only |

The client's `wwwroot/bootstrap` accounts for 45 of the tree's 163 entries; it is third-party CSS/JS, not project code.

## Persistent Data

No SQL scripts, stored procedures or triggers exist. `Source: .iari/README.md` ("Database scripts. No SQL files, stored procedures or triggers. The schema exists only as code, in the migrations of the API project") — confirmed against the tree, which holds no `.sql` file.

The schema is defined by `TodoDbContext` and materialised by three EF Core migrations plus a model snapshot.

| Table | Purpose | Anchor |
|---|---|---|
| `Todos` | `Id` INTEGER identity key, `Title` TEXT required, `IsComplete` INTEGER (bool), `OwnerId` TEXT required; index on `OwnerId`; cascade delete from the owner | `Todo.Api/Migrations/TodoDbContextModelSnapshot.cs` |
| `AspNetUsers` | `TodoUser : IdentityUser` with no added properties; unique `NormalizedUserName`, index `EmailIndex` | same |
| `AspNetRoles`, `AspNetRoleClaims`, `AspNetUserClaims`, `AspNetUserLogins`, `AspNetUserRoles`, `AspNetUserTokens` | ASP.NET Core Identity's framework tables, cascade-deleted from user/role | same |

| Migration | Anchor |
|---|---|
| `20221123071234_Initial` | `Todo.Api/Migrations/20221123071234_Initial.cs` |
| `20221123165051_RemoveIsAdmin` | `Todo.Api/Migrations/20221123165051_RemoveIsAdmin.cs` |
| `20230714032431_ForeignKeyChange` | `Todo.Api/Migrations/20230714032431_ForeignKeyChange.cs` |

The relationship is configured in code, not only generated: `Todo` → `TodoUser` by `OwnerId`, principal key `Id`, `.WithMany()`. `Source: Todo.Api/TodoDbContext.cs`.

Data lifecycle: the database file is created and migrated **only** by the AppHost in run mode, and only when the `.db` directory does not yet exist (`if (!Directory.Exists(dbDirectory))` then `AddEfMigration`). `Source: TodoApp.AppHost/Extensions.cs`, `TodoApp.AppHost/Program.cs`. There is no migration runner inside `Todo.Api` itself, so running the API standalone leaves it pointing at a database file that nothing creates.

The snapshot declares `ProductVersion` `8.0.0` while the package pins are 9.0.8 — see Anomalies.

## Documentation

### What the owner declared, against what the tree holds

`Source: .iari/README.md` is the only file the delivery places in `.iari/`. It makes four statements; three hold against the tree, one no longer does.

| Declaration | Verdict against the tree |
|---|---|
| "Database scripts. No SQL files, stored procedures or triggers." | Holds — no `.sql` anywhere; schema lives in `Todo.Api/Migrations` |
| "Documents. No requirements, design or architecture documents, and no manuals." | [OBSOLETE] in part — true of the delivered snapshot, but the tree now also carries `docs/artifacts/environment/development-case.md`, added by this sprint zero |
| "A running installation. … no production data and no users." | Holds — no deployment descriptor, no seed data, no connection string to a live store |
| "Its authors. … cannot be asked." | Holds — nothing in the tree names them beyond the MIT copyright line in `LICENSE` |

The single sentence "The only document is the `README.md` at the root of the repository" has to be read with the two commits that created `docs/`: the folder did not come from the upstream sample.

### The document inventory

```plantuml
@startuml
title Documentation the delivery carries, what it covers, and where no document exists
skinparam componentStyle rectangle
skinparam shadowing false

package "Documents present" {
  component "README.md\n4509 bytes · prose only" as README
  component "Requests/todo.http\n793 bytes · 5 requests" as HTTPFILE
  component ".iari/README.md\n777 bytes · delivery statement" as IARI
  component "LICENSE\nMIT, (c) 2022 David Fowler" as LIC
  component "docs/artifacts/environment/\ndevelopment-case.md\n16418 bytes · process" as DC
  component "Configuration as documentation\nDirectory.Build.props · Directory.Packages.props\nglobal.json · nuget.config · ci.yaml · appsettings\naspire/settings.json · devcontainer" as CFG
  component "Code comments and TODO markers\n(only inline record of known gaps)" as COMMENTS
}

package "System areas" {
  component "Api/Todos — CRUD over /todos" as A1
  component "Api/Users — Identity + token" as A2
  component "Server/Auth — BFF login dance" as A3
  component "Client — Blazor task list UI" as A4
  component "Persistence — 8 tables, 3 migrations" as A5
  component "Composition — AppHost, ServiceDefaults" as A6
  component "Tests — integration suite" as A7
}

README --> A1 : setup, /users/register and /users/login walkthrough
README --> A4 : lists the two apps, one screenshot
README --> A6 : "run TodoApp.AppHost", Aspire prerequisites
README --> A2 : bearer token response shape
README --> A3 : external providers setup, secrets, Auth0 schema
HTTPFILE --> A1 : POST, GET all, DELETE — no PUT, no GET by id
CFG --> A5 : connection string default, migration command
CFG --> A1 : rate limit and logging settings only
COMMENTS --> A3 : "TODO: Support remote logout", "TODO: Handle the failure somehow"
COMMENTS --> A2 : "TODO: Add service to service auth between the BFF and this API"
DC --> A7 : names the test conventions
IARI --> A5 : no SQL scripts — schema is code

README ..> A3 : no document of the /auth/* contracts
README ..> A7 : no document of what the suite covers
COMMENTS ..> A4 : completion toggle exists in API, absent in UI, unremarked

note bottom of DC
  Authored in this sprint zero (Process Engineer,
  commits 2026-11-14). It is process documentation,
  not documentation of the delivered system.
end note
note bottom of COMMENTS
  CONTRIBUTING.md is cited as the coding standard by
  the Development Case but is absent from the tree.
end note
@enduml
```

| Document | Kind | Weight | What it actually covers | Anchor |
|---|---|---|---|---|
| `README.md` | prose, no structure beyond headings | 4509 bytes, 0 diagram, 0 table | The two applications, a feature list, prerequisites (.NET 9, Aspire CLI), how to run via `TodoApp.AppHost`, standalone API usage, external-provider and Auth0 configuration schemas, OpenTelemetry mention | `README.md` |
| `Requests/todo.http` | executable request file (REST Client / VS Code) | 793 bytes, 5 requests | `POST /users/register`, `POST /users/login`, `POST /todos`, `GET /todos`, `DELETE /todos/{id}` | `Requests/todo.http` |
| `.iari/README.md` | delivery statement | 777 bytes | What is and is not in the delivery | `.iari/README.md` |
| `LICENSE` | licence text | MIT, `(c) 2022 David Fowler` | Legal terms only | `LICENSE` |
| `docs/artifacts/environment/development-case.md` | process tailoring | 16418 bytes | The sprint-zero process: classification, disciplines, artifact catalogue, optional triggers, roles | committed 2026-11-14 (`37986fb`, `520a590`, `a1e2d77`, `6f554f8`, `e0bc4e6`) |

Configuration read as documentation — the only authoritative statement of several behaviours:

| Behaviour documented only here | File |
|---|---|
| Target framework, nullable, implicit usings, `LangVersion preview` | `Directory.Build.props` |
| 28 package pins, including the only record that YARP 2.3.0 and Scalar 2.6.8 are intended | `Directory.Packages.props` |
| SDK band and prerelease policy | `global.json` |
| Package-source lockdown (`<clear />` + `*` → nuget.org) | `nuget.config` |
| CI gate: restore → build Release → test Release, on push and pull request | `.github/workflows/ci.yaml` |
| Default log levels; YARP warnings suppressed | `Todo.Api/appsettings.json`, `Todo.Web/Server/appsettings.json` |
| AppHost path for the Aspire tooling | `.aspire/settings.json` |
| Developer environment: SDK 8.0 image, forwarded ports 5000/5001, auto-install of `dotnet-ef` | `.devcontainer/devcontainer.json`, `.devcontainer/init.sh` |
| Recommended editor extensions (C#, REST Client) | `.vscode/extensions.json` |

### Documentation carried only in code comments

These comments are the sole record of intent or of a known gap, and each is an anchor for a later reading:

| Statement | Anchor |
|---|---|
| "TODO: Add service to service auth between the BFF and this API" | `Todo.Api/Users/UsersApi.cs` |
| "TODO: Support remote logout" | `Todo.Web/Server/AuthApi.cs` |
| "TODO: Handle the failure somehow" (external login failure path) | `Todo.Web/Server/AuthApi.cs` |
| "TODO: We should have the user pick a user name to complete the external login dance" | `Todo.Web/Server/AuthApi.cs` |
| "This is a hack from hell to avoid having to know if this is running server or client side" | `Todo.Web/Client/TodoClient.cs` |
| "TODO: Support passing a connection string" (migration step) | `TodoApp.AppHost/Extensions.cs` |
| "TODO: Follow up on the new errors" — two field-level assertions commented out | `Todo.Api.Tests/UserApiTests.cs` |
| "Adding health checks endpoints to applications in non-development environments has security implications" | `TodoApp.ServiceDefaults/Extensions.cs` |

### What has no document at all

| Undocumented | What the reader must do instead |
|---|---|
| The `/auth/*` contract of the BFF (register, login, logout, the two-step external challenge/callback) | Read `Todo.Web/Server/AuthApi.cs`; the `README.md` describes only the API's `/users` endpoints |
| The YARP forwarding rule and the cookie→Bearer token translation | Read `Todo.Web/Server/TodoApi.cs` |
| The complete `/todos` contract — `GET /todos/{id}` and `PUT /todos/{id}` appear in neither the README nor `todo.http` | Read `Todo.Api/Todos/TodoApi.cs` |
| The authorization rules (owner-only reads, owner-or-admin writes) and the fact that reads use `FindAsync` before the ownership check | Read `Todo.Api/Todos/TodoApi.cs`; `Todo.Api.Tests/TodoApiTests.cs` covers the behaviour |
| The rate-limit policy and its configuration keys | Read `Todo.Api/Extensions/RateLimitExtensions.cs` (unread) and `Todo.Api/Program.cs` |
| Which endpoints the test suite covers | Read `Todo.Api.Tests/TodoApiTests.cs`, `Todo.Api.Tests/UserApiTests.cs` |
| The database lifecycle — that only the AppHost creates and migrates `.db/Todos.db` | Read `TodoApp.AppHost/Extensions.cs` |
| The API's OpenAPI surface | No committed OpenAPI file; it is generated at runtime and exposed at `/openapi` with `/scalar/v1` in Development |
| Any ADR, architecture note, glossary, deployment instruction beyond `README.md` | Nothing exists — `.iari/README.md` declares this and the tree confirms it |

### Documentation the delivery cites but does not contain

`docs/artifacts/environment/development-case.md` lists `CONTRIBUTING.md` as "Coding standard and review conventions" with the Software Architect and Code Reviewer as owners. **`CONTRIBUTING.md` does not exist in the tree** — a direct read fails with "was not found". The Development Case's other tool references (`ci.yaml`, `Directory.Packages.props`, `global.json`, `Directory.Build.props`, `Todo.Api.Tests`, `README.md`) all resolve.

Recorded as an absence, not filled in: no coding standard exists beyond what `Directory.Build.props` enforces (nullable, implicit usings, preview language version) and what the code demonstrates.

## History

Commit history read from the SCM. The whole-repository listing covers the 50 most recent commits, 2023-07-14 to 2026-11-14, and reports that older history exists. Per-area listings follow.

| Area | Commits listed | Period | What the commits show |
|---|---|---|---|
| Whole repository | 50 | 2023-07-14 → 2026-11-14 (older history exists) | Two clusters of change: July 2023 (Blazor SSR adoption, `31b28b3`, `5e9c05b`, `182c354`, `7c18bec`) and November 2024 (the largest rework: `6b9f07e` "Aspirfy!", `3530e8a` ".NET 9", `1449c43` "Use new open api and scalar", `bbd680d` "Move files around", `3308193` "TodoApi -> TodoApp"). After 2024-11-27 only three substantive commits remain: `beb0011` (2025-01-11), `1d4e043` (2025-01-11, "Remove tasks and launch.json"), `a6dea68` (2025-08-07, "Update everything! (#105)"), `d772504` and `a6ff858` (2025-09-28), and `307a1ea` (2026-02-12, "Upgrade Aspire SDK to 13.1.1") — which is the commit the delivery was taken at |
| `README.md` | 20 | 2022-12-02 → 2025-09-28 | Steady low-churn documentation: rewritten at each platform move (`2e54de3` .NET 8, `6b9f07e` Aspirify!, `3308193` rename) and polished twice since (`d772504`, `a6ff858`). No README commit after 2025-09-28, so the README post-dates nothing the delivery contains |
| `Requests/` | 5 | 2022-11-12 → 2024-03-26 | Last touched by `abd9421` "Fix up docs and http file for net8 identity framework (#92)"; not touched by the .NET 9 work of November 2024 |
| `Todo.Api/Migrations` | 1 | 2024-11-23 only | The single listed commit is a path move (`bbd680d` "Move files around"), not a schema change. The migration set itself is old: `Initial` and `RemoveIsAdmin` (both 2022-11-23), `ForeignKeyChange` (2023-07-14) |
| `.devcontainer` | 6 | 2022-11-13 → 2023-12-15 | Last touched by `2e54de3` ".NET 8 RTM Update" (2023-12-15) — before the .NET 9 upgrade of 2024-11-15 (`3530e8a`). No later commit, which is consistent with the image still pinning SDK 8.0 |

Instability, read from these commits only:

- **The authentication and BFF surface is the most volatile area.** Between 2024-11-23 and 2024-11-27 five commits target it (`fb0032e`, `2d0d82d`, `228dc29`, `fdc49bb`, `69127f1`, `a519c10` — the last being "Protect the user id to make sure only the BFF can call the external auth API (#100)"). That is more churn in five days than any other area shows in a year, and the newest of those commits changes a trust boundary.
- **The persistence schema is consolidating.** Three migrations, all created in 2022–2023, none since; `RemoveIsAdmin` shows functionality deliberately taken out of the schema.
- **The dev environment is stale relative to the code.** Its last commit precedes the framework upgrade.
- **The sprint-zero commits of 2026-11-14** (five for the Development Case, one for the repository `README.md`, `ccf6401`) are process commits and carry no change to the delivered system.

## Anomalies

Each is stated with its evidence, a probability that it bites, and the impact if it does. The Project Manager assigns the `RNNN` identifiers when curating the Risk List.

| Anomaly | Evidence | Probability | Impact |
|---|---|---|---|
| `CONTRIBUTING.md` is cited as the coding standard but does not exist | `docs/artifacts/environment/development-case.md` names it under Tool references; a read of `CONTRIBUTING.md` returns "was not found"; the tree has no such entry | Certain — already true | Medium: the Software Architect and Code Reviewer are assigned an artifact that is not there; coding conventions must be read off the code or re-authored |
| The dev container cannot build the solution | `.devcontainer/devcontainer.json` pins `mcr.microsoft.com/dotnet/sdk:8.0`; `global.json` requires `9.0.100` with `rollForward: latestFeature`. Roll-forward does not bridge a major version | High | Medium for anyone using the container; the CI path (`actions/setup-dotnet@v3`) is unaffected because it resolves the SDK from `global.json` |
| The README's completion-toggle feature is unreachable from the UI | `PUT /todos/{id}` writes `IsComplete` (`Todo.Api/Todos/TodoApi.cs`); `Todo.Web/Client/Components/TodoList.razor` renders `<input type="checkbox" />` with no `@bind` and no handler, and `TodoClient` exposes no update call | Certain | Medium: a delivered capability has no user-facing entry point, so a use case recovered from the API would have no screen trace |
| The `admin` role is not obtainable at runtime | `CurrentUser.IsAdmin` reads `Principal.IsInRole("admin")` (`Todo.Api/Authorization/CurrentUser.cs`); `Todo.Api/Program.cs` calls `AddIdentityCore<TodoUser>()` with no role store and no role seeding; the only producer of an `admin` role claim in the tree is `Todo.Api.Tests/TokenService.cs`, a test fixture | High | Medium: the owner-or-admin branches in `GET/PUT/DELETE /todos/{id}` are exercised only by tests; whether an administrator exists in the product is undetermined by the code |
| The test suite asserts less than it appears to | `Todo.Api.Tests/UserApiTests.cs` comments out its field-level assertions under "TODO: Follow up on the new errors", leaving status-code-only checks; no test covers `PUT`'s `id != todo.Id` branch or the rate limiter | High | Medium: the CI gate is green but weaker than a reader would assume |
| The EF model snapshot is from the 8.0 era while the package pins are 9.0.8 | `Todo.Api/Migrations/TodoDbContextModelSnapshot.cs` declares `ProductVersion` `8.0.0`; `Directory.Packages.props` pins EF Core 9.0.8; no migration commit after 2024-11-23 | Medium | Low to Medium: the next `dotnet ef migrations add` may produce a snapshot diff unrelated to the intended change |
| Server-side prerendering returns an empty list with a success status | `Todo.Web/Client/TodoClient.cs`: when `client.BaseAddress is null` it `return (HttpStatusCode.OK, new())`, with the comment "This is a hack from hell" | Certain | Low: a first paint shows an empty task list rather than an error or a spinner |
| The Development Case's role/artifact ownership diagram is drawn as a class diagram | `docs/artifacts/environment/development-case.md` uses `class` elements and `-->` arrows to express ownership | Certain | Low: cosmetic in a process document; recorded because downstream roles read that artifact |
| `docs/` is not declared in `.iari/README.md` even though it exists | `.iari/README.md` says the only document is the root `README.md`; the tree holds `docs/artifacts/environment/development-case.md`, created 2026-11-14 | Certain | Low: the delivery statement now under-describes the tree it sits in |
| `README.md` links a badge to a differently-named repository | The badge URL is `github.com/davidfowl/TodoApi/actions/...` while the project was renamed to `TodoApp` in `3308193` | Certain | Low: external link only |
| `Todo.Web.Shared` is an empty project carried by two references | Tree holds only `SharedClass.cs` and the `.csproj`; both `Todo.Web.Server` and (per the solution) the client reference it | Certain | Low: dead weight in the build graph |

Absences recorded as findings rather than filled in: no architecture description, no ADR, no deployment instruction, no data dictionary, no API contract document, no operational runbook, no user guide, and no author to ask (`Source: .iari/README.md`).

## Priorities

Ordered by where the code concentrates and by what the Development Case and the delivery statement make load-bearing. Each entry states why it is where it is; this order drives the Excavation reading.

| Order | Area | Why it is here |
|---|---|---|
| 1 | `Todo.Api/Todos` — the `/todos` surface | The only area that carries the system's actual domain (`Todo`, `IsComplete`, `OwnerId`), the only area with behavioural tests, and the surface the declared product purpose rests on. Five endpoints, two authorization rules, three distinct failure modes |
| 2 | Authentication and identity — `Todo.Api/Users`, `Todo.Api/Authorization`, `Todo.Web/Server/Auth*`, `Server/Authentication` | The most complex and most volatile area: 5 commits in 5 days of November 2024, the newest of which changes a trust boundary (`a519c10`). It carries two schemes, four external providers, a data-protection key shared between processes, and four TODO markers naming known gaps. Nothing readable is safe to assume here |
| 3 | Persistence — `Todo.Api/TodoDbContext`, `Todo.Api/Migrations` | The schema is the system's ground truth and exists nowhere else. The snapshot/product-version drift and the AppHost-only migration path both have consequences for any later change |
| 4 | Composition and deployment — `TodoApp.AppHost`, `TodoApp.ServiceDefaults` | The Development Case fired the Deployment Model on this topology. The AppHost also owns the database lifecycle, which the API does not |
| 5 | `Todo.Web.Client` | Small, but it holds the only user-facing UI and a documented defect (the prerender hack) and the missing completion toggle. Read after the API, because the client's contract is the BFF's |
| 6 | `Todo.Api.Tests` | The evidence for rules 1 and 2, but weaker than it looks — the assertions disabled in `UserApiTests.cs` are why this ranks below the code they test |
| 7 | `Todo.Web.Shared`, `wwwroot/bootstrap`, tooling configs | Placeholder, vendored, and already read at the level they need |

Deliberately not read first: the vendored Bootstrap tree, `Properties/launchSettings.json` files, and the Razor `_Imports`/`App` plumbing — they carry no perimeter facts.

## Coverage

The tree reports 163 entries. Of these, 45 are vendored Bootstrap CSS/JS files under `Todo.Web/Client/wwwroot/bootstrap` and are excluded from the reading by kind.

**Files opened: 42.** Enumerated, so the next iteration does not re-read them:

`.iari/README.md`, `README.md`, `LICENSE`, `Requests/todo.http`, `Directory.Build.props`, `Directory.Packages.props`, `global.json`, `nuget.config`, `TodoApp.sln`, `.github/workflows/ci.yaml`, `.devcontainer/devcontainer.json`, `.devcontainer/init.sh`, `.aspire/settings.json`, `.vscode/extensions.json`, `docs/artifacts/environment/development-case.md`, `Todo.Api/Program.cs`, `Todo.Api/TodoDbContext.cs`, `Todo.Api/Todo.Api.csproj`, `Todo.Api/appsettings.json`, `Todo.Api/Todos/Todo.cs`, `Todo.Api/Todos/TodoApi.cs`, `Todo.Api/Users/TodoUser.cs`, `Todo.Api/Users/UsersApi.cs`, `Todo.Api/Authorization/CurrentUser.cs`, `Todo.Api/Migrations/TodoDbContextModelSnapshot.cs`, `Todo.Api.Tests/Todo.Api.Tests.csproj`, `Todo.Api.Tests/TodoApplication.cs`, `Todo.Api.Tests/TokenService.cs`, `Todo.Api.Tests/TodoApiTests.cs`, `Todo.Api.Tests/UserApiTests.cs`, `Todo.Web/Server/Program.cs`, `Todo.Web/Server/TodoApi.cs`, `Todo.Web/Server/AuthApi.cs`, `Todo.Web/Server/Todo.Web.Server.csproj`, `Todo.Web/Server/appsettings.json`, `Todo.Web/Server/Authentication/AuthenticationExtensions.cs`, `Todo.Web/Server/Authentication/ExternalProviders.cs`, `Todo.Web/Client/TodoClient.cs`, `Todo.Web/Client/Components/TodoList.razor`, `TodoApp.AppHost/Program.cs`, `TodoApp.AppHost/Extensions.cs`, `TodoApp.ServiceDefaults/Extensions.cs`.

**Files confirmed absent: 1** — `CONTRIBUTING.md`, cited by the Development Case.

**Areas left unread, declared rather than omitted:**

| Unread | Why it can wait |
|---|---|
| `Todo.Web/Client/Program.cs`, `TodoApp.razor`, `_Imports.razor`, `Components/LogInForm.razor` | Client registration and markup; the log-in form's contract is inferable from `TodoClient` and must be confirmed in Excavation |
| `Todo.Web/Server/AuthClient.cs`, `Authentication/AuthClient` path, `AuthenticationSchemes.cs`, `HttpAuthenticationStateProvider.cs`, `TokenNames.cs` | The BFF→API auth mechanics; needed before any use-case recovery of the login flow, not before the perimeter |
| `Todo.Api/Authorization/CheckCurrentUserAuthHandler.cs`, `CurrentUserExtensions.cs` | The handler that makes `RequireCurrentUser()` bite; confirms the admin anomaly and is first in the next reading |
| `Todo.Api/Extensions/OpenApiOptionsExtensions.cs`, `RateLimitExtensions.cs`, `Filters/ValidationFilter.cs` | Mechanism details behind `/openapi` and the rate limiter; the limiter's policy values are unknown |
| `Todo.Api/Migrations/2022*.cs`, `2023*.cs` (3 migration files, 6 with designers) | The schema is read from the snapshot; the per-migration diffs matter only when reconstructing schema history |
| `Todo.Web/Shared/SharedClass.cs`, `Todo.Web.Client/Todo.Web.Client.csproj`, `Todo.Web.Shared.csproj`, `TodoApp.AppHost.csproj`, `TodoApp.ServiceDefaults.csproj` | Placeholder and manifests restating pins already read centrally |
| All `appsettings.Development.json`, all `Properties/launchSettings.json` | Local-only overrides and ports; no perimeter fact |
| `Todo.Api/appsettings.json` was read; `Todo.Web/Server/appsettings.Development.json` was not | Development-only keys, including any external-provider configuration, are unknown |
| `.gitignore`, `bg.png`, `favicon.ico`, `css/app.css`, all Bootstrap files | Assets and ignore rules; no perimeter fact |
| `Todo.Api.Tests/DbContextExtensions.cs`, `GlobalUsings.cs` | Fixture plumbing already inferable from `TodoApplication.cs` |
| Whole-repository commits older than 2023-07-14 | Older history exists; the schema-era commits of 2022 are the candidates for the next history reading |

What this coverage does **not** claim: the `/auth/*` behaviour is described from the endpoints and the provider registration, not from the state machine that drives the external login; the rate-limit policy values are not read; and no file outside the 42 opened has been looked at, so a fact about an unread file would be an assumption.

## Provenance

| Fact | Anchor |
|---|---|
| The delivery is the MIT sample `davidfowl/TodoApp` at `307a1ead`, 2026-02-12, with no authors reachable | `.iari/README.md` |
| `.iari/` holds only `README.md` at delivery | `.iari/README.md`; tree listing |
| No SQL scripts, stored procedures or triggers | `.iari/README.md`; tree listing |
| Seven projects and their names | `TodoApp.sln` |
| `net9.0`, `Nullable enable`, `ImplicitUsings enable`, `LangVersion preview` | `Directory.Build.props` |
| SDK `9.0.100`, `rollForward: latestFeature`, `allowPrerelease: true` | `global.json` |
| 28 package pins; EF Core, Identity, YARP, Scalar, OpenTelemetry, xunit versions | `Directory.Packages.props` |
| Package source locked to nuget.org | `nuget.config` |
| CI runs restore, Release build and Release test on push and pull request | `.github/workflows/ci.yaml` |
| API composition: service defaults, data protection discriminator `TodoApp`, bearer auth, `AddIdentityCore<TodoUser>`, SQLite, current-user service, OpenAPI, rate limiting, HTTP logging, Scalar in Development | `Todo.Api/Program.cs` |
| `/todos` group requires the current user, a per-user rate limit, and parameter validation | `Todo.Api/Todos/TodoApi.cs` |
| Five `/todos` operations and their owner/admin rules | `Todo.Api/Todos/TodoApi.cs` |
| `GET /todos/{id}` reads via `FindAsync` before the ownership check | `Todo.Api/Todos/TodoApi.cs` |
| `/users` group maps `MapIdentityApi<TodoUser>` plus `POST /users/token/{provider}` | `Todo.Api/Users/UsersApi.cs` |
| External user ids are data-protected before transport | `Todo.Api/Users/UsersApi.cs`; `Todo.Web/Server/AuthApi.cs` |
| `CurrentUser.IsAdmin` reads the `admin` role claim | `Todo.Api/Authorization/CurrentUser.cs` |
| `Todo` shape and the `TodoItem` DTO that hides `OwnerId` | `Todo.Api/Todos/Todo.cs` |
| `TodoUser` adds no properties to `IdentityUser` | `Todo.Api/Users/TodoUser.cs` |
| Eight tables and their columns, keys and indexes | `Todo.Api/Migrations/TodoDbContextModelSnapshot.cs` |
| Snapshot `ProductVersion` is `8.0.0` | `Todo.Api/Migrations/TodoDbContextModelSnapshot.cs` |
| Relationship `Todo.OwnerId` → `TodoUser.Id`, `.WithMany()` | `Todo.Api/TodoDbContext.cs` |
| Three migrations, their names and dates | `Todo.Api/Migrations/` file names |
| Connection string `"Todos"`, fallback `Data Source=.db/Todos.db` | `Todo.Api/Program.cs` |
| The database is created and migrated only by the AppHost, only when `.db` is absent | `TodoApp.AppHost/Extensions.cs`; `TodoApp.AppHost/Program.cs` |
| `sqliteweb` container mounting the database directory | `TodoApp.AppHost/Program.cs` |
| BFF composition: cookie auth, data protection discriminator, `TodoClient`, Razor components with WASM render mode, YARP forwarder with service discovery, `AuthClient` base address `http://todoapi` | `Todo.Web/Server/Program.cs` |
| BFF forwards `/todos/{*path}` and rewrites the cookie token into a Bearer header | `Todo.Web/Server/TodoApi.cs` |
| BFF auth endpoints: register, login, logout, `login/{provider}`, `signin/{provider}` | `Todo.Web/Server/AuthApi.cs` |
| Four external providers, each gated on its configuration section | `Todo.Web/Server/Authentication/AuthenticationExtensions.cs` |
| All non-cookie schemes are treated as social providers for the UI | `Todo.Web/Server/Authentication/ExternalProviders.cs` |
| Client call surface: add, delete, list, login, register, logout | `Todo.Web/Client/TodoClient.cs` |
| Prerender returns `(OK, empty)` when `BaseAddress` is null — "hack from hell" | `Todo.Web/Client/TodoClient.cs` |
| Task-list UI renders an unbound checkbox; no completion toggle | `Todo.Web/Client/Components/TodoList.razor` |
| OpenTelemetry, health checks, service discovery and resilience defaults | `TodoApp.ServiceDefaults/Extensions.cs` |
| OTLP export only when `OTEL_EXPORTER_OTLP_ENDPOINT` is set | `TodoApp.ServiceDefaults/Extensions.cs` |
| Health endpoints mapped in Development only | `TodoApp.ServiceDefaults/Extensions.cs` |
| Test host uses a real SQLite in-memory connection, relaxed Identity password rules, ephemeral data protection | `Todo.Api.Tests/TodoApplication.cs` |
| The `admin` role claim is added only by the test token helper | `Todo.Api.Tests/TokenService.cs` |
| Nine `[Fact]` tests over `/todos`, including owner isolation and admin override | `Todo.Api.Tests/TodoApiTests.cs` |
| Seven `[Fact]` tests over `/users`; field-level assertions commented out under a TODO | `Todo.Api.Tests/UserApiTests.cs` |
| README contents: feature list, prerequisites .NET 9 + Aspire CLI, run via AppHost, standalone API walkthrough, external provider and Auth0 configuration, OpenTelemetry | `README.md` |
| `README.md` is 4509 bytes, `Requests/todo.http` 793 bytes, `.iari/README.md` 777 bytes, `development-case.md` 16418 bytes | SCM file metadata for each path |
| `Requests/todo.http` carries five requests and no `PUT` or `GET /todos/{id}` | `Requests/todo.http` |
| Badge URL names `TodoApi` while the project is `TodoApp` | `README.md`; commit `3308193` |
| `.devcontainer` pins SDK 8.0 and forwards ports 5000/5001 | `.devcontainer/devcontainer.json` |
| `dotnet-ef` installed globally by the dev container setup | `.devcontainer/init.sh` |
| AppHost path recorded for Aspire tooling | `.aspire/settings.json` |
| Editor extension recommendations | `.vscode/extensions.json` |
| MIT licence, copyright 2022 David Fowler | `LICENSE` |
| `CONTRIBUTING.md` is cited by the Development Case | `docs/artifacts/environment/development-case.md`, Tool references |
| `CONTRIBUTING.md` does not exist | read attempt returned "was not found"; tree listing |
| Development Case classification (`business-process-led = false`, `real-time-system = false`), inactive Business Modeling, fired Deployment Model, stood-down roles | `docs/artifacts/environment/development-case.md` |
| Commit history of the whole repository, 50 commits, 2023-07-14 → 2026-11-14, older history exists | `scm_list_commits` over the repository, 2025-11-14 run |
| Two change clusters (July 2023, November 2024) and the post-November-2024 commits | same listing: `31b28b3`, `5e9c05b`, `182c354`, `7c18bec`, `6b9f07e`, `3530e8a`, `1449c43`, `bbd680d`, `3308193`, `beb0011`, `1d4e043`, `a6dea68`, `d772504`, `a6ff858`, `307a1ea` |
| Five authentication-surface commits between 2024-11-23 and 2024-11-27 | `fb0032e`, `2d0d82d`, `228dc29`, `fdc49bb`, `69127f1`, `a519c10` |
| `README.md` history: 20 commits, 2022-12-02 → 2025-09-28 | `scm_list_commits` over `README.md` |
| `Requests/` history: 5 commits, 2022-11-12 → 2024-03-26 | `scm_list_commits` over `Requests` |
| `Todo.Api/Migrations` history: 1 commit, 2024-11-23, a path move | `scm_list_commits` over `Todo.Api/Migrations` |
| `.devcontainer` history: 6 commits, 2022-11-13 → 2023-12-15, last `2e54de3` | `scm_list_commits` over `.devcontainer` |
| `docs/` created by the sprint-zero commits of 2026-11-14 | whole-repository listing: `ccf6401`, `37986fb`, `520a590`, `a1e2d77`, `6f554f8`, `e0bc4e6` |
| 163 tree entries, 45 of them vendored Bootstrap files | `scm_get_repo_tree` |
| 42 files opened in this reading | the enumeration in Coverage |
| No scheduled job, batch process or report exists | `TodoApp/` tree; no hosted service or job configuration in any read manifest |
| Priorities order and Coverage declarations | This reading — no external anchor; they are the Software Archaeologist's judgement over the evidence above |
