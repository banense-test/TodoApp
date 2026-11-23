## Working with IARI

For how a change is requested, labelled and reviewed in this repository, this file holds over any other guide in it.

The root `README.md` documents how to build and run the system. It states no label, no branch rule and no review rule, so nothing in it is replaced by this file.

### 1. Requesting a change

Every change starts as an issue. An issue that asks for a change to the product or to the process is a change request and carries the label `change-request`.

The `Change Control Manager` is the only role that labels a change request beyond that point. The originator states the **severity**, by consequence; the `Change Control Manager` assigns the **priority**, by urgency, never from the severity. The two axes are independent labels.

The `Change Control Manager` moves the request through its states and, on approval, adds `assigned:<role-kebab>` naming the role that executes it. A `cr:approved` issue whose `assigned:` label names no role is not approved for execution, and a role does not start work on one.

| Label | Means | Raised by | Read by |
|---|---|---|---|
| `change-request` | The issue is a change request. Every change request carries it. | Change Control Manager, Tester | Capsule Designer, Database Designer, Designer, Implementer, Process Engineer, Reviewer, Test Manager, Tester, Change Control Manager, Software Architect |
| `cr:new` | State of a change request: new. | Change Control Manager | nobody |
| `cr:logged` | State of a change request: logged, waiting for triage and for the decision. | Change Control Manager, Tester | Change Control Manager |
| `cr:approved` | State of a change request: approved. The role its `assigned:` label names executes it. | Change Control Manager | Capsule Designer, Database Designer, Designer, Implementer, Process Engineer, Change Control Manager |
| `cr:assigned` | State of a change request: assigned. | Change Control Manager | nobody |
| `cr:complete` | State of a change request: complete. The correction is verified and the issue is closed. | Change Control Manager | nobody |
| `cr:rejected` | State of a change request: rejected. The issue is closed. | Change Control Manager | nobody |
| `cr:hold` | State of a change request: on hold. | Change Control Manager | nobody |
| `cr:deferred-next-iteration` | State of a change request: deferred to the next iteration. | Change Control Manager | nobody |
| `cr:deferred-next-release` | State of a change request: deferred to the next release. The issue is closed. | Change Control Manager | nobody |
| `assigned:<role-kebab>` | The role that executes an approved change request, its name in kebab-case. | Change Control Manager | Capsule Designer, Database Designer, Designer, Implementer, Process Engineer |
| `severity:blocker` | Fatal: the product, its build or its integration cannot be used. | Tester, Configuration Manager, Integrator, Change Control Manager | Configuration Manager, Integrator |
| `severity:major` | A major function is not performed. | Tester, Change Control Manager | nobody |
| `severity:minor` | The function works; a minor annoyance. | Tester, Configuration Manager, Change Control Manager | nobody |
| `severity:trivial` | Cosmetic: no function is affected. | Tester, Change Control Manager | nobody |
| `priority:critical` | Urgent (resolve immediately). Holds the release. | Change Control Manager | Change Control Manager, Reviewer, Tester |
| `priority:high` | High. Holds the release. | Change Control Manager | Change Control Manager, Reviewer, Tester |
| `priority:medium` | Normal. Does not hold the release. | Change Control Manager | Change Control Manager |
| `priority:low` | Low. Does not hold the release. | Change Control Manager | Change Control Manager |
| `nature:defect` | Nature of the change: a defect. | Tester, Configuration Manager, Integrator, Change Control Manager, IARI | Reviewer, Test Manager, Tester, Implementer |
| `nature:enhancement` | Nature of the change: an enhancement. | Integrator, Change Control Manager | nobody |
| `nature:new-feature` | Nature of the change: a new feature. | Change Control Manager | nobody |
| `nature:refactoring` | Nature of the change: a refactoring. | Change Control Manager | nobody |
| `impact:architectural` | Impact of the change: architectural. The Software Architect decides on it before it is approved. | Change Control Manager | Change Control Manager |
| `impact:local` | Impact of the change: local. | Change Control Manager | nobody |
| `impact:cross-cutting` | Impact of the change: cross-cutting. | Change Control Manager | nobody |
| `needs-architect-review` | The change request is parked until the Software Architect decides on it. | Change Control Manager | Software Architect, Change Control Manager |
| `architect:concurs` | The Software Architect concurs with the change request parked for its decision. | Software Architect | Change Control Manager |
| `architect:rejects` | The Software Architect rejects the change request parked for its decision. | Software Architect | Change Control Manager |
| `ready-for-review` | On a branch: its work is handed off for code review. | Implementer | Code Reviewer, Integrator, Reviewer |
| `handoff:release-notes` | The issue is the release summary of an iteration, handed off for the Release Notes and the release tag. | Integrator | Configuration Manager |
| `iteration-close` | The issue is the closing summary of an iteration. | Integrator | nobody |
| `missing-approval` | Gate failure: the review has not approved. | Configuration Manager | nobody |
| `ci-broken-on-main` | Gate failure: the pipeline is red on the main branch. | Configuration Manager | nobody |
| `release-blocker` | The gate failure blocks the release baseline. | Configuration Manager | nobody |
| `naming-violation` | A branch name breaks the naming convention. | Configuration Manager | nobody |
| `integration-regression` | A merge left the integration line or the main branch red. | Integrator | nobody |
| `integration-blocked` | A pull request the Integrator could not merge. | Integrator | nobody |
| `missing-dependency` | An artifact the integration depends on is missing. | Integrator | nobody |
| `production-break` | A merged hotfix broke the main branch after the merge. | Integrator | nobody |
| `self-audit` | IARI's self-audit found that a role broke a process invariant. | IARI | IARI |
| `process-defect` | A defect of the process: a role broke one of its invariants. | IARI | nobody |

A label written differently from this table reaches no role. The case and the separator are part of the label.

### 2. Branching and deployment

Branching and deployment are the `Configuration Manager`'s and the `Integrator`'s. This file states what a contributor must know and points to where the rest lives; it does not restate their rules.

| Rule | Owner | Where it lives |
|---|---|---|
| What is baselined, when a branch is cut, how a release is tagged | Configuration Manager | the Configuration Manager's baseline plan, in the Iteration Plan of the phase |
| What the pipeline runs on a push and on a pull request | Integrator | `.github/workflows/ci.yaml` |
| How a change reaches `main` — merge, review gate, build gate | Integrator | the Integrator's iteration plan, recorded in the Iteration Plan of the iteration |
| How a release is deployed and what the release baseline is | Deployment Manager | the Deployment Model and the Release Notes |

A change reaches `main` through a pull request. The `Integrator` merges it; a contributor does not push to `main` directly.

### 3. Code and test conventions

The conventions below are the ones the code in this repository follows. Each is cited to the file that states it; that file is the source, and this list is a reading of it.

**Build and language** — `Directory.Build.props`:

- `TargetFramework` is `net9.0` for every project in the solution.
- `Nullable` is `enable` — nullable reference types are on, and a new file annotates them.
- `ImplicitUsings` is `enable` — no explicit `using` for the implicit namespaces.
- `LangVersion` is `preview`.

**SDK** — `global.json`: SDK `9.0.100`, `rollForward` `latestFeature`, `allowPrerelease` `true`.

**Packages** — `Directory.Packages.props`:

- `ManagePackageVersionsCentrally` is `true`. A `<PackageReference>` names the package and carries **no** `Version` attribute; the version is in `Directory.Packages.props`.
- A new dependency is added as a `<PackageVersion>` there first, then referenced without a version.

**Package sources** — `nuget.config`: sources are cleared and only `nuget.org` is added; `packageSourceMapping` maps `*` to `nuget.org`. A package from another feed does not restore.

**Tests** — `Todo.Api.Tests/Todo.Api.Tests.csproj`, `Todo.Api.Tests/GlobalUsings.cs`, `Todo.Api.Tests/TodoApiTests.cs`:

- Framework is xunit, tests are marked `[Fact]`, and the class is `public class <Area>Tests` in namespace `TodoApi.Tests`.
- Tests are integration tests over the HTTP surface: they start the API through `new TodoApplication()` (`WebApplicationFactory`) and act through `application.CreateClient(userId)`. The API's own types are not called directly where a request can be made.
- A test seeds through `application.CreateTodoDbContext()` and `application.CreateUserAsync(userId)`, then asserts on the HTTP response (`HttpStatusCode.Created`, `HttpStatusCode.NotFound`, `HttpStatusCode.Forbidden`) and on the persisted row.
- The usings the suite relies on are declared in two places: `Todo.Api.Tests/GlobalUsings.cs` for the ASP.NET Core and EF Core types, and the `<Using>` items of `Todo.Api.Tests/Todo.Api.Tests.csproj` for `System.Net`, `System.Net.Http`, `System.Net.Http.Json` and `Xunit`. A suite-wide using goes in one of those two, never in a test file.
- `xunit.runner.visualstudio` and `coverlet.collector` carry `PrivateAssets="all"`; `xunit`, `Microsoft.NET.Test.Sdk` and `Microsoft.AspNetCore.Mvc.Testing` are referenced without it. Coverage is collected by `coverlet.collector`.
- The API exposes its internals to the test project through `InternalsVisibleTo` in `Todo.Api/Todo.Api.csproj`.

**API conventions** — `Todo.Api/Program.cs`, `Todo.Api/Filters/ValidationFilter.cs`, `Todo.Api/Todos/TodoApi.cs`, `Todo.Api/Users/UsersApi.cs`:

- Endpoints are minimal APIs grouped in one file per area, mapped under `/todos` and `/users`.
- Validation returns `400` with a `ValidationProblemDetails` body; the title is `One or more validation errors occurred.` and the `Errors` dictionary carries the field name.
- A resource the caller does not own answers `404`, not `403`. `GetTodosWithoutDbUser` is the one place the code answers `403`, for a caller with no database user at all.
- The current user is resolved in `Todo.Api/Authorization/CheckCurrentUserAuthHandler.cs` and reached through `CurrentUser`; a handler does not read the identity from the request itself.

**Persistent data** — `Todo.Api/TodoDbContext.cs`, `Todo.Api/Migrations/`:

- One `DbContext` derives from `IdentityDbContext<TodoUser>`, so the Identity tables are part of the schema.
- Model configuration is written in `OnModelCreating` with the fluent API; data annotations are not used for relationships.
- A schema change is a new EF Core migration in `Todo.Api/Migrations/`, named `<Timestamp>_<PascalCaseDescription>`; an existing migration is never edited. `dotnet-ef` is installed by `.devcontainer/init.sh`.

**UI** — `Todo.Web/Client/Components/`:

- Razor components live under `Todo.Web/Client/Components/`, one component per file, with its markup, `@inject` and `@code` in that file; a routable component adds `@page` there. Shared imports are in `Todo.Web/Client/_Imports.razor`.
- HTTP calls to the API go through `TodoClient.cs`; a component does not construct an `HttpClient` for the API itself.
- Styling is the vendored Bootstrap under `Todo.Web/Client/wwwroot/bootstrap/` plus `wwwroot/css/app.css`; the vendored copy is not edited.

**Environment** — `.devcontainer/devcontainer.json`, `.aspire/settings.json`, `.vscode/extensions.json`:

- The dev container runs `.devcontainer/init.sh` on create and forwards ports 5000 and 5001.
- The Aspire app host is `TodoApp.AppHost/TodoApp.AppHost.csproj`, declared in `.aspire/settings.json`; the application runs through it.
- Recommended editor extensions are `ms-dotnettools.csharp` and `humao.rest-client`; request samples are in `Requests/todo.http`.

**One disagreement in the sources.** `.devcontainer/devcontainer.json` names the image `mcr.microsoft.com/dotnet/sdk:8.0` while `Directory.Build.props` targets `net9.0` and `global.json` pins SDK `9.0.100`. Both files are cited above as they are written; the `Integrator` owns the build environment and settles which of the two holds.

### 4. What a review checks

The `Code Reviewer` reviews the pull request; the `Reviewer` reviews the artifact the iteration produces. A review looks for:

- **Trace** — the change cites the identifier it comes from: a `FR-`/`NFR-` for declared work, a `Source:` anchor for work recovered from the code already here. A change that cites neither is not reviewable.
- **Scope** — the change does what its change request states and adds no functional area the stakeholder did not declare. An addition the request does not carry is a recommendation, not part of the merge.
- **Conventions** — section 3 of this file holds: central package versions, nullable on, no version attribute on a `PackageReference`, a schema change as a new migration.
- **Tests** — a changed behaviour is covered by a test in `Todo.Api.Tests/` that asserts on the HTTP response, and the suite passes.
- **Labels and state** — the change request carries its `severity:`; a `cr:approved` request names its executor in `assigned:<role-kebab>`.

A pull request whose work is ready for that review carries `ready-for-review`.

### 5. Questions about the process

The `Process Engineer` owns this file and the Development Case. A question about how the process applies, a template that does not fit, or a gate whose approver is unstated goes to the `Process Engineer` and is answered inside the iteration. A blocking one is escalated to the stakeholder in the same turn it is raised, not carried to the next iteration.
