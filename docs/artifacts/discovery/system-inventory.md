## Document Control
- Phase: Survey
- Status: Draft
- Milestone Target: end of Survey (SBC) — not yet achieved

## Perimeter
The boundary is drawn by the code, not by the README. Inside it sit seven projects of `TodoApp.sln` plus the CI workflow that builds them. The browser is outside and reaches the web server only; it never calls the API directly, because the web server proxies `/todos` through YARP and re-signs each request with the stored bearer token. Two facts bound what can be read from this perimeter: nothing is deployed anywhere (`.iari/README.md`), and no external identity provider is active as delivered — `AuthenticationExtensions` registers a provider only when `Authentication:Schemes:<provider>` exists in configuration, and no shipped `appsettings.json` carries that section, so the four provider schemes in the code are reachable in principle and inert in practice.

```plantuml
@startuml
title Perimeter of the existing Todo App
skinparam componentStyle rectangle
skinparam shadowing false

actor "End user\n(browser)" as USER

package "Todo App — existing system (as delivered)" {
  component "TodoApp.AppHost\nAspire orchestration — local run" as APPHOST
  component "Todo.Web.Server\nBFF host: cookie auth, /auth, /todos forwarder" as WEBSRV
  component "Todo.Web.Client\nBlazor WebAssembly UI" as WEBUI
  component "Todo.Web.Shared\nDTO library" as SHARED
  component "Todo.Api\nMinimal-API backend" as API
  component "TodoApp.ServiceDefaults\nOpenTelemetry, health, discovery, resilience" as SVCDEF
  component "Todo.Api.Tests\nIntegration test harness (xunit)" as TESTS
}

component "SQLite Todos.db\nRelational schema" as DB
component "External identity providers\nGitHub / Google / Microsoft / Auth0" as IDP
component "OTLP collector\nAspire dashboard" as OTLP
component "sqliteweb container\ntomdesinto/sqliteweb — dev only" as SQLITEWEB

USER --> WEBSRV : HTTPS page, /auth, /todos
WEBSRV --> WEBUI : serves the WASM bundle
WEBUI --> WEBSRV : XHR /todos, /auth
WEBSRV --> API : HTTP /users (AuthClient)
WEBSRV --> API : HTTP /todos (YARP forwarder, bearer)
WEBSRV --> IDP : OAuth2 / OIDC redirect
API --> DB : EF Core
SQLITEWEB --> DB : bind mount of the .db directory
APPHOST --> API : starts, gated on the migration
APPHOST --> WEBSRV : starts, injects the API reference
APPHOST --> SQLITEWEB : starts
SVCDEF ..> API : shared host configuration
SVCDEF ..> WEBSRV : shared host configuration
API ..> OTLP : OTLP export
WEBSRV ..> OTLP : OTLP export
TESTS ..> API : in-process host, in-memory SQLite

note right of API
  Todo.Api/Program.cs:23-24 — EF Core Sqlite,
  connection "Todos" or Data Source=.db/Todos.db
  Todo.Api/Users/UsersApi.cs:12,20 — /users surface
  Todo.Api/Todos/TodoApi.cs:24-73 — /todos surface
end note

note bottom of IDP
  Registered only when Authentication:Schemes:<provider>
  exists in configuration. No such section ships in
  appsettings.json, so no provider is active as delivered.
end note

note right of DB
  Schema exists only as EF Core migrations,
  Todo.Api/Migrations/. No SQL scripts.
end note
@enduml
```

### Components

| Component | Kind | Responsibility | Implemented by |
|---|---|---|---|
| Todo.Web.Server | Subsystem | Browser-facing host (the BFF): serves the Blazor page, owns the authentication cookie, mints it against the API's bearer token, exposes `/auth`, and forwards every `/todos` request to the API with the bearer token attached. Also the only consumer of the external identity providers. | `Todo.Web/Server/Program.cs:6-58`; `Todo.Web/Server/TodoApi.cs:9-28` |
| Todo.Web.Client | Component | Blazor WebAssembly UI assembled into the browser: one page component that switches between a login form and the todo list, and an HTTP client that speaks to the web server only. | `Todo.Web/Client/TodoApp.razor:1-44`; `Todo.Web/Client/TodoClient.cs:7-71`; `Todo.Web/Client/Program.cs:5-13` |
| Todo.Web.Shared | Component | DTO library referenced by both the client and the server: `TodoItem`, `UserInfo`, `ExternalUserInfo`, `AuthToken`. | `Todo.Web/Shared/SharedClass.cs:3-37` |
| Todo.Api | Subsystem | The backend: minimal-API hosts the `/users` identity surface and the `/todos` CRUD surface, enforces bearer authentication, per-user rate limiting and parameter validation, serves the OpenAPI document and the Scalar UI. | `Todo.Api/Program.cs:5-68` |
| Todo.Api / Users | Component | ASP.NET Core Identity user store and bearer-token issue: the stock identity endpoints plus a custom `/users/token/{provider}` endpoint that creates or finds a user by external login. | `Todo.Api/Users/UsersApi.cs:10-64`; `Todo.Api/Users/TodoUser.cs:7-29` |
| Todo.Api / Todos | Component | Todo read, create, update and delete, scoped to the owning user; the `admin` role widens read, update and delete to any owner. | `Todo.Api/Todos/TodoApi.cs:8-77`; `Todo.Api/Todos/Todo.cs:1-40` |
| Todo.Api / Authorization | Component | Resolves the caller into a `CurrentUser` (claims transformation against the database) and supplies the authorization requirement that a valid token alone does not satisfy. | `Todo.Api/Authorization/CurrentUser.cs:6-15`; `Todo.Api/Authorization/CurrentUserExtensions.cs:8-35`; `Todo.Api/Authorization/CheckCurrentUserAuthHandler.cs:8-40` |
| Todo.Api / Persistence | Component | EF Core `DbContext` over ASP.NET Core Identity, the `Todo` entity with its owner foreign key, and the three migrations that define the schema. | `Todo.Api/TodoDbContext.cs:7-21`; `Todo.Api/Migrations/20221123071234_Initial.cs`; `Todo.Api/Migrations/20221123165051_RemoveIsAdmin.cs`; `Todo.Api/Migrations/20230714032431_ForeignKeyChange.cs` |
| Todo.Api / Cross-cutting | Component | Request-level mechanisms shared by the endpoints: per-user token-bucket rate limiting, parameter validation returning problem details, OpenAPI bearer-scheme metadata, HTTP logging. | `Todo.Api/Extensions/RateLimitExtensions.cs:11-71`; `Todo.Api/Filters/ValidationFilter.cs:7-58`; `Todo.Api/Extensions/OpenApiOptionsExtensions.cs:7-47` |
| TodoApp.AppHost | Subsystem | Aspire orchestration for local runs: creates the SQLite directory, runs `dotnet ef database update` before anything starts, launches the API, the web server (with the API service reference) and the sqliteweb container. | `TodoApp.AppHost/Program.cs:3-28`; `TodoApp.AppHost/Extensions.cs:3-38` |
| TodoApp.ServiceDefaults | Layer | Shared host configuration referenced by the API and the web server: OpenTelemetry traces, metrics and logs, the OTLP exporter, health checks, service discovery and the HTTP resilience handler. | `TodoApp.ServiceDefaults/Extensions.cs:16-41`; `TodoApp.ServiceDefaults/Extensions.cs:73-117` |
| Todo.Api.Tests | Component | Integration tests that boot the API in-process through `WebApplicationFactory`, replace SQLite with a shared in-memory connection, and drive the real endpoints with minted bearer tokens. | `Todo.Api.Tests/TodoApplication.cs:10-95`; `Todo.Api.Tests/TodoApiTests.cs:3-290`; `Todo.Api.Tests/UserApiTests.cs:6-170` |
| Build and verification | Component | The only executable definition of green: restore, build and test the whole solution on `ubuntu-latest` for every push and pull request. No SDK version is pinned in the workflow. | `.github/workflows/ci.yaml:1-21`; `TodoApp.sln:1-12` |

### External actors and systems

| External actor or system | Reached through | Anchor |
|---|---|---|
| End user in a browser | Remote call — HTTPS to `Todo.Web.Server` (`/`, `/auth/*`, `/todos/*`); never to the API directly | `Todo.Web/Server/App.razor:5`; `Todo.Web/Client/TodoClient.cs:8-71`; `Todo.Web/Server/Program.cs:20-37` |
| GitHub, Google, Microsoft, Auth0 — external identity providers | Remote call — OAuth2/OIDC authorization-code redirect, registered by scheme name and active only when `Authentication:Schemes:<provider>` is configured | `Todo.Web/Server/Authentication/AuthenticationExtensions.cs:40-52`; `Todo.Web/Server/AuthApi.cs:55-64` |
| OTLP collector — the Aspire dashboard locally, any endpoint named by `OTEL_EXPORTER_OTLP_ENDPOINT` | Messaging — OTLP export of logs, metrics and traces, enabled only when that setting is non-empty | `TodoApp.ServiceDefaults/Extensions.cs:73-90`; `Directory.Packages.props:37-41` |
| Container runtime (Docker/Podman) as driven by the Aspire AppHost | Service — the AppHost asks it to run the sqliteweb container | `TodoApp.AppHost/Program.cs:13-17` |
| `tomdesinto/sqliteweb` container image | File — bind mount of `Todo.Api/.db` as `/db`, opened as `Todos.db`; excluded from the published manifest | `TodoApp.AppHost/Program.cs:10-17` |
| `dotnet-ef` CLI delivered from NuGet, installed globally on the developer machine by the AppHost | Service — `dotnet tool install --global dotnet-ef`, then `dotnet ef database update --no-build` | `TodoApp.AppHost/Extensions.cs:17-33` |
| NuGet package feed (`https://api.nuget.org/v3/index.json`) | Service — restore time only; the single mapped source for all packages | `nuget.config:3-12`; `Directory.Packages.props:1-43` |

### Entry points

| ID | Entry point | Kind | Initiated by | Anchor |
|---|---|---|---|---|
| EP-001 | `POST /users/register` — create a user from email and password | Service operation | Anonymous client (API direct, or the web server's `AuthClient`) | `Todo.Api/Users/UsersApi.cs:12,20`; `Todo.Web/Server/AuthClient.cs:20-29` |
| EP-002 | `POST /users/login` — exchange credentials for a bearer token | Service operation | Anonymous client | `Todo.Api/Users/UsersApi.cs:12,20`; `Todo.Web/Server/AuthClient.cs:5-18` |
| EP-003 | `POST /users/refresh` — exchange a refresh token for a new access token | Service operation | Authenticated client | `Todo.Api/Users/UsersApi.cs:12,20` |
| EP-004 | `GET /users/confirmEmail` — confirm an email address from a code | Service operation | End user, following a link | `Todo.Api/Users/UsersApi.cs:12,20` |
| EP-005 | `POST /users/resendConfirmationEmail` — reissue the confirmation mail | Service operation | Anonymous client | `Todo.Api/Users/UsersApi.cs:12,20` |
| EP-006 | `POST /users/forgotPassword` — request a password-reset code | Service operation | Anonymous client | `Todo.Api/Users/UsersApi.cs:12,20` |
| EP-007 | `POST /users/resetPassword` — set a new password with a reset code | Service operation | Anonymous client | `Todo.Api/Users/UsersApi.cs:12,20` |
| EP-008 | `POST /users/manage/2fa` — enable or disable two-factor authentication | Service operation | Authenticated user | `Todo.Api/Users/UsersApi.cs:12,20` |
| EP-009 | `GET /users/manage/info` — read the caller's account information | Service operation | Authenticated user | `Todo.Api/Users/UsersApi.cs:12,20` |
| EP-010 | `POST /users/manage/info` — change the caller's email or password | Service operation | Authenticated user | `Todo.Api/Users/UsersApi.cs:12,20` |
| EP-011 | `POST /users/token/{provider}` — exchange an externally authenticated identity for a bearer token, creating the user on first use | Service operation | Web server BFF only (the provider key is data-protected with the provider name) | `Todo.Api/Users/UsersApi.cs:24-54`; `Todo.Web/Server/AuthClient.cs:31-42` |
| EP-012 | `GET /todos` — list the caller's todos | Service operation | Authenticated user, through the forwarder | `Todo.Api/Todos/TodoApi.cs:24-27` |
| EP-013 | `GET /todos/{id}` — read one todo; 404 unless the caller owns it or is `admin` | Service operation | Authenticated user, through the forwarder | `Todo.Api/Todos/TodoApi.cs:29-36` |
| EP-014 | `POST /todos` — create a todo owned by the caller | Service operation | Authenticated user, through the forwarder | `Todo.Api/Todos/TodoApi.cs:38-50` |
| EP-015 | `PUT /todos/{id}` — update title and completion of an owned todo | Service operation | Authenticated user, through the forwarder | `Todo.Api/Todos/TodoApi.cs:52-65` |
| EP-016 | `DELETE /todos/{id}` — delete an owned todo | Service operation | Authenticated user, through the forwarder | `Todo.Api/Todos/TodoApi.cs:67-73` |
| EP-017 | `POST /auth/register` — register through the UI and open a session | Service operation | Browser (Blazor client) | `Todo.Web/Server/AuthApi.cs:14-25`; `Todo.Web/Client/TodoClient.cs:55-63` |
| EP-018 | `POST /auth/login` — log in through the UI and open a session | Service operation | Browser (Blazor client) | `Todo.Web/Server/AuthApi.cs:27-38`; `Todo.Web/Client/TodoClient.cs:47-53` |
| EP-019 | `POST /auth/logout` — end the cookie session | Service operation | Browser (Blazor client) | `Todo.Web/Server/AuthApi.cs:40-52`; `Todo.Web/Client/TodoClient.cs:65-69` |
| EP-020 | `GET /auth/login/{provider}` — challenge the named external provider | Service operation | Browser, following the provider button rendered by the login form | `Todo.Web/Server/AuthApi.cs:55-62`; `Todo.Web/Client/Components/LogInForm.razor:34-40` |
| EP-021 | `GET /auth/signin/{provider}` — external-login callback: resolve or create the user, obtain a token, write the cookie | Service operation | External identity provider redirect | `Todo.Web/Server/AuthApi.cs:64-101` |
| EP-022 | `/todos/{*path}` — YARP forwarder for every verb, re-signed with the stored access token | Service operation | Browser (Blazor client) | `Todo.Web/Server/TodoApi.cs:14-26` |
| EP-023 | `/` — the application page: renders the login form or the todo list for the session | Screen | End user in a browser | `Todo.Web/Server/App.razor:5-25`; `Todo.Web/Client/TodoApp.razor:3-16` |
| EP-024 | `/scalar/v1`, with `/` redirecting to it — API reference and try-it-out console | Screen | Developer, development environment only | `Todo.Api/Program.cs:49-56,62`; `Todo.Api/Properties/launchSettings.json:10-24` |
| EP-025 | `/health` and `/alive` — readiness and liveness probes | Service operation | Aspire AppHost / orchestrator, development environment only | `TodoApp.ServiceDefaults/Extensions.cs:101-117`; `Todo.Api/Program.cs:60` |
| EP-026 | `dotnet ef database update` at AppHost start — creates or migrates `Todos.db` before the API serves a request | Platform event | TodoApp.AppHost, and only when `Todo.Api/.db` does not yet exist | `TodoApp.AppHost/Program.cs:3,19-25`; `TodoApp.AppHost/Extensions.cs:5-16` |

## Technology and Size
| Area | Language | Platform and frameworks, with version | Files | Anchor |
|---|---|---|---|---|
| `Todo.Api` | C# (`LangVersion preview`, nullable enabled) | ASP.NET Core minimal APIs on `net9.0`; EF Core + `Microsoft.EntityFrameworkCore.Sqlite` 9.0.8; `Microsoft.AspNetCore.Identity.EntityFrameworkCore` 9.0.8; `Microsoft.AspNetCore.OpenApi` 9.0.8 with `Microsoft.OpenApi` 1.6.22; `Scalar.AspNetCore` 2.6.8; `MiniValidation` 0.9.2; `Microsoft.AspNetCore.Authentication.BearerToken` from the shared framework. Declares container image `todo-api:latest`. | 23 (8 source, 7 migrations, 4 configuration, csproj, launch settings, `DbContext`) | `Todo.Api/Todo.Api.csproj:1-26`; `Directory.Packages.props:7-30`; `Todo.Api/Program.cs:1-68` |
| `Todo.Api.Tests` | C# | xunit 2.9.3 with `xunit.runner.visualstudio` 3.1.3; `Microsoft.NET.Test.Sdk` 17.14.1; `Microsoft.AspNetCore.Mvc.Testing` 9.0.8; `Microsoft.EntityFrameworkCore.InMemory` 9.0.8; `coverlet.collector` 6.0.4. Targets `net9.0` through `Directory.Build.props`; reaches `Todo.Api` internals via `InternalsVisibleTo`. | 7 | `Todo.Api.Tests/Todo.Api.Tests.csproj:1-24`; `Todo.Api/Todo.Api.csproj:19-21` |
| `Todo.Web/Server` | C# + Razor components | ASP.NET Core `net9.0` web host: Blazor Server hosting `AddInteractiveWebAssemblyComponents`; `Microsoft.AspNetCore.Components.WebAssembly.Server` 9.0.8; `Yarp.ReverseProxy` 2.3.0 with `Microsoft.Extensions.ServiceDiscovery.Yarp` 9.5.0; `AspNet.Security.OAuth.GitHub` 9.4.0; `Auth0.AspNetCore.Authentication` 1.5.0; `Microsoft.AspNetCore.Authentication.Google` and `.MicrosoftAccount` 9.0.8. `RazorLangVersion` pinned to 8.0. Declares container image `todo-web-server:latest`. | 15 (8 source, 5 Razor/authentication classes, 2 settings, csproj) | `Todo.Web/Server/Todo.Web.Server.csproj:1-30`; `Todo.Web/Server/Program.cs:1-58` |
| `Todo.Web/Client` | C# + Razor components, WebAssembly | `Microsoft.NET.Sdk.BlazorWebAssembly` on `net9.0`; `Microsoft.AspNetCore.Components.WebAssembly` 9.0.8; `Microsoft.Extensions.Http` 9.0.8. Carries a vendored Bootstrap 5 distribution (44 files) plus one image and two stylesheets. | 56 (8 source, 2 pages, 46 static assets) | `Todo.Web/Client/Todo.Web.Client.csproj:1-13`; `Todo.Web/Client/Program.cs:1-13`; `Todo.Web/Client/wwwroot/bootstrap/dist` |
| `Todo.Web/Shared` | C# | `Microsoft.NET.Sdk` on `net9.0`, `SupportedPlatform browser` — the DTO library both client and server compile against. No package references. | 2 | `Todo.Web/Shared/Todo.Web.Shared.csproj:1-7`; `Todo.Web/Shared/SharedClass.cs:1-37` |
| `TodoApp.AppHost` | C# | .NET Aspire AppHost, `Aspire.AppHost.Sdk/13.1.1`; output type `Exe`, `IsAspireHost`. References the API and the web server as orchestrated projects. | 6 | `TodoApp.AppHost/TodoApp.AppHost.csproj:1-3`; `TodoApp.AppHost/Program.cs:1-28` |
| `TodoApp.ServiceDefaults` | C# | `Microsoft.NET.Sdk` on `net9.0` with `FrameworkReference Microsoft.AspNetCore.App`; OpenTelemetry 1.12.0 (`Exporter.OpenTelemetryProtocol`, `Extensions.Hosting`, `Instrumentation.AspNetCore`, `Instrumentation.Http`, `Instrumentation.Runtime`); `Microsoft.Extensions.ServiceDiscovery` 9.5.0; `Microsoft.Extensions.Http.Resilience` 9.7.0. | 2 | `TodoApp.ServiceDefaults/TodoApp.ServiceDefaults.csproj:1-23`; `TodoApp.ServiceDefaults/Extensions.cs:1-118` |
| Solution root | — | `global.json` pins SDK `9.0.100`, `rollForward latestFeature`, `allowPrerelease true`; `Directory.Build.props` sets `TargetFramework net9.0`, `Nullable enable`, `ImplicitUsings enable`, `LangVersion preview`; `nuget.config` maps all packages to `nuget.org` only; `TodoApp.sln` carries 7 projects in `src`/`tests` solution folders. | 8 | `global.json:1-8`; `Directory.Build.props:1-9`; `nuget.config:1-13`; `TodoApp.sln:1-14` |
| `.github/workflows` | YAML | GitHub Actions `CI`: `actions/checkout@v3` and `actions/setup-dotnet@v3` on `ubuntu-latest`, then `dotnet restore`, `dotnet build -c Release --no-restore`, `dotnet test -c Release --no-build` over `TodoApp.sln`, on push and pull request. `setup-dotnet` is given no `dotnet-version`, so the workflow inherits whatever SDK the runner image carries. | 1 | `.github/workflows/ci.yaml:1-21` |
| `.devcontainer` | JSON + shell | Development container from `mcr.microsoft.com/dotnet/sdk:8.0` with the C# extension, a `postCreateCommand` running `init.sh`, and ports 5000/5001 forwarded. | 2 | `.devcontainer/devcontainer.json:1-12`; `.devcontainer/init.sh` |
| `Requests` | HTTP requests | The author's request file against a standalone API on `http://localhost:5000`: register, login, then bearer-authenticated create, list and delete. | 1 | `Requests/todo.http:1-37` |
| `docs/artifacts` | Markdown | Artifacts produced by this project, not by the code's authors: the System Inventory and the Development Case. | 2 | `docs/artifacts/discovery/system-inventory.md`; `docs/artifacts/environment/development-case.md` |
| `.iari` | Markdown | The handover note: provenance, and the explicit statement of what the delivery does not contain. | 1 | `.iari/README.md:1-23` |
| `.aspire`, `.vscode` | JSON | Tool configuration only: Aspire local settings; a recommended-editor extension list. | 2 | `.aspire/settings.json`; `.vscode/extensions.json` |

Total: 7 projects of `TodoApp.sln`, 128 files counted from the repository tree (165 entries including directories), of which 46 under `Todo.Web/Client/wwwroot` are a vendored Bootstrap distribution and not project code.
## Persistent Data
| Store | Kind | Data manager | Anchor |
|---|---|---|---|

## Documentation

The delivery carries no requirements, design or architecture document written by its authors: `.iari/README.md` states this and the tree agrees. What it does carry is the upstream sample's own README, a request file, a CI workflow and the MIT licence — documents of the code as it was published, not of the system as it is installed anywhere. Each was read against the code it describes.

```plantuml
@startuml
title Documents delivered with the code, and the repository facts each one is read against
hide empty members

package ".iari — the handover note" {
  class ".iari/README.md" as IARI <<Current>>
}
package "Author material — davidfowl/TodoApp @ 307a1ead (MIT)" {
  class "README.md" as RM <<Contradicted>>
  class "LICENSE" as LIC <<Current>>
  class "Requests/todo.http" as HTTP <<Current>>
  class ".github/workflows/ci.yaml" as CI <<Current>>
}
package "Produced by this project" {
  class "docs/artifacts/environment/development-case.md" as DC <<Current>>
}
package "Repository facts each document is read against" {
  class "Scalar.AspNetCore 2.6.8\nMapScalarApiReference on /scalar/v1" as SCALAR <<code>>
  class "appsettings.json — no\nAuthentication:Schemes section" as CFG <<code>>
  class "CONTRIBUTING.md\nabsent from the tree" as CONTRIB <<missing>>
}

IARI ..> HTTP : declares no documents exist
RM ..> SCALAR : calls the API explorer "Swagger UI"
RM ..> CFG : states Auth0 is "configured"
DC ..> CONTRIB : names it the home of coding, UI and test conventions

note bottom of RM
  Feature list, prerequisites and endpoint list
  hold. The API-explorer name and the "Auth0 is
  configured" statement do not: the code serves
  Scalar and configures no external scheme.
end note
@enduml
```

| Document | Useful for | How up to date | Anchor |
|---|---|---|---|
| `.iari/README.md` | The perimeter of the delivery: provenance (copy of `davidfowl/TodoApp` at commit `307a1ead` of 2026-02-12, MIT); the explicit non-existence of database scripts, requirements/design/architecture documents, manuals, a running installation, production data and reachable authors. The constraint every other row is read under. | Current | `.iari/README.md` |
| `README.md` (upstream author's) | Author's statement of the feature set and of the technical mechanisms it showcases (Blazor WebAssembly, minimal APIs, EF Core + SQLite, OpenAPI, Identity, cookie and bearer authentication, YARP forwarder, rate limiting, integration tests); prerequisites (.NET 9, Aspire CLI); how the system is started (AppHost runs web-server and API); the REST calls needed to obtain a bearer token; the configuration schema for each external identity provider and for Auth0; OpenTelemetry via the Aspire dashboard. | Contradicted by the code | `README.md`; `Todo.Api/Program.cs`; `Directory.Packages.props`; `Todo.Api/appsettings.json`; `Todo.Web/Server/appsettings.json` |
| `LICENSE` | The terms the copy is held under and its origin: MIT, "Copyright (c) 2022 David Fowler". Together with `.iari/README.md` it is the whole provenance record of the delivery. | Current | `LICENSE` |
| `Requests/todo.http` | The author's minimal happy-path request sequence against a standalone API on `http://localhost:5000`: `POST /users/register`, `POST /users/login`, then authenticated `POST /todos`, `GET /todos`, `DELETE /todos/{id}`. A cross-check on the recovered `/users` and `/todos` entry points and on the bearer scheme. | Current | `Requests/todo.http`; `Todo.Api/Users/UsersApi.cs`; `Todo.Api/Todos/TodoApi.cs` |
| `.github/workflows/ci.yaml` | The only executable statement of how the solution is verified: `dotnet restore`, `dotnet build -c Release --no-restore`, `dotnet test -c Release --no-build` on `TodoApp.sln` under `ubuntu-latest`, on push and pull request. Shows that the integration-test project is part of the build's definition of green. | Current | `.github/workflows/ci.yaml`; `TodoApp.sln` |
| `docs/artifacts/environment/development-case.md` | The tailoring governing this project: sprint zero before Inception, the recovered-element anchoring rule, the one fired OPTIONAL (Deployment Model), the inactive disciplines and the roles at work in the sprint zero. | Current | `docs/artifacts/environment/development-case.md` |

## History
| Area | Commits read and period | What was removed or reworked | Reading | Commits |
|---|---|---|---|---|

## Anomalies
| ID | Anomaly | Kind | Evidence | Likelihood | Impact |
|---|---|---|---|---|---|

## Priorities
| Order | Area | Why it comes first | Anchor |
|---|---|---|---|

## Coverage
| Area | Files | Read | Unread and why |
|---|---|---|---|

## Traceability
| Element | Traces From | Link Type | Traces To |
|---|---|---|---|
