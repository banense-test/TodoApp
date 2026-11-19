## Document Control
- Phase: Excavation
- Status: Draft — Domain Model and Design Packages and Classes recovered; Use-Case Realizations and Interface Contracts not yet recovered
- Milestone Target: end of Excavation (AR) — not yet achieved
## Design Overview
This document records the design the delivered code already holds. Nothing here is designed by this project: every class, member, visibility modifier and relationship is read out of the file named beside it, and no member is named that the code does not declare. Where the code is silent — a concurrency token, a lifecycle state an operation would need but no operation exists to reach — the silence is recorded as such, not filled.

The model is produced in stages. This iteration recovers the **domain model** and the **design packages and classes**; the use-case realizations and the interface contracts follow in later stages of this phase, and each section below states its own status.

| Section | What its diagram fixes | Status this iteration |
|---|---|---|
| Domain Model | The classes the code declares as business objects, their members, and the one relationship that holds between them | Recovered |
| Design Packages and Classes | The same classes grouped by the component that declares them, with every operation the code implements, and the classes of the host-configuration, orchestration and verification components | Recovered |
| Use-Case Realizations | Which objects collaborate, in what order, for each of the eight recovered use cases | Not yet recovered |
| Interface Contracts | Pre/postconditions on every operation a component boundary crosses | Not yet recovered |
| Persistent Data Classes | Column, key, index and cascade detail of the eight tables | Owned by the Database Designer |
| Boundary Classes and Navigation Map | The Razor components as boundary classes | Owned by the User Interface Designer |
| Capsules, Protocols and Signals | — | `[OMITTED: Capsules, Protocols and Signals — Development Case DC-D3: real-time-system = false, so no capsule, protocol or signal work runs in any phase]` |

**What is recovered and what is not.** Thirty-four classes carry the product and its declared wire shapes. Ten are business objects: one entity the project authored (`Todo`), the Identity-derived user, six DTO declarations that exist twice over — once in each host — plus the projection helper and one token record. Seventeen carry the code that reads and writes those objects. Seven more carry the host configuration, the orchestration, the migration and the test harness — the components the architecture summarises as carrying none. Each class is anchored where it is described; a class with no member the code declares is shown with none.

**One component declares no class at all.** COMP-018 is a workflow document; `TodoApp.AppHost/Program.cs` is top-level statements. Neither is a compilation unit, so neither has a class to recover. Every other component of the architecture holds at least one.

## Domain Model
The business objects the code declares are six: one entity the product authors, the Identity-derived user, and four DTO shapes. Three of those four exist twice over, because `Todo.Api` references `TodoApp.ServiceDefaults` alone and declares its own `TodoItem`, `UserInfo` and `ExternalUserInfo` while the two web projects share a second declaration through `Todo.Web.Shared` (ADR-011, CON-A10). There is one persistent relationship in the whole model and it is the ownership edge.

```plantuml
@startuml
title Domain Model — the business objects the code declares, and the two independent declarations of every wire shape
skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam packageStyle rectangle
hide empty members
hide circle

package "Todo.Api — the API host's own declaration" {
  class "Todo\nCLS-001" as TODO <<entity>> {
    + Id : int
    + Title : string [Required]
    + IsComplete : bool
    + OwnerId : string [Required]
  }
  class "TodoUser\nCLS-002" as TODOUSER <<entity>> {
    .. no member declared ..
    (IdentityUser supplies Id, UserName, Email, PasswordHash)
  }
  class "TodoItem\nCLS-003" as APITODOITEM <<DTO>> {
    + Id : int
    + Title : string [Required]
    + IsComplete : bool
  }
  class "UserInfo\nCLS-004" as APIUSERINFO <<DTO>> {
    + Email : string [Required]
    + Password : string [Required]
  }
  class "ExternalUserInfo\nCLS-005" as APIEXTUSERINFO <<DTO>> {
    + Username : string [Required]
    + ProviderKey : string [Required]
  }
  class "TodoMappingExtensions\nCLS-010" as MAPPER <<static helper>> {
    {static} + AsTodoItem(todo : Todo) : TodoItem
  }
}

package "Todo.Web.Shared — the web projects' declaration" {
  class "TodoItem\nCLS-006" as WEBTODOITEM <<DTO>> {
    + Id : int
    + Title : string [Required]
    + IsComplete : bool
  }
  class "UserInfo\nCLS-007" as WEBUSERINFO <<DTO>> {
    + Email : string [Required]
    + Password : string [Required]
  }
  class "ExternalUserInfo\nCLS-008" as WEBEXTUSERINFO <<DTO>> {
    + Username : string [Required]
    + ProviderKey : string [Required]
  }
  class "AuthToken\nCLS-009" as AUTHTOKEN <<record>> {
    + Token : string [JsonPropertyName "accessToken"]
  }
}

TODO "0..*" --> "1" TODOUSER : OwnerId -> Id\nON DELETE CASCADE
MAPPER ..> TODO : reads
MAPPER ..> APITODOITEM : creates

apiTodoItem -[hidden]down- AUTHTOKEN
WEBTODOITEM -[hidden]down- AUTHTOKEN

note right of APITODOITEM
  ADR-011 — the wire shape is declared twice.
  TodoItem, UserInfo and ExternalUserInfo exist once per
  side and agree on member names by inspection only:
  Todo.Api/Todo.Api.csproj:24-26 references
  TodoApp.ServiceDefaults alone, never Todo.Web.Shared.
  CLS-003 Todo.Api/Todos/Todo.cs:14-19
  CLS-004 Todo.Api/Users/TodoUser.cs:12-19
  CLS-005 Todo.Api/Users/TodoUser.cs:24-29
end note

note right of TODOUSER
  AN-010 / EX-002: CurrentUser.IsAdmin reads the role claim
  "admin", but no code path grants a role and migration
  RemoveIsAdmin dropped the persisted flag. AspNetRoles and
  AspNetUserRoles exist and nothing writes them.
  CLS-002 Todo.Api/Users/TodoUser.cs:7-9
end note

note bottom of TODO
  CLS-001 Todo.Api/Todos/Todo.cs:3-12 — one entity the product
  authors; the seven Identity tables beside it are supplied by
  the framework.
  CLS-010 Todo.Api/Todos/Todo.cs:27-40
end note

note bottom of AUTHTOKEN
  CLS-006 Todo.Web/Shared/SharedClass.cs:5-11
  CLS-007 Todo.Web/Shared/SharedClass.cs:13-20
  CLS-008 Todo.Web/Shared/SharedClass.cs:22-29
  CLS-009 Todo.Web/Shared/SharedClass.cs:31
  AuthToken is web-only: AuthClient reads the API's
  AccessTokenResponse payload into this record and keeps
  one member of it. CLS-005 and CLS-008 are reached by no
  recovered use case — EP-011 is an exclusion.
end note
@enduml
```

### Domain classes, as the code declares them

| ID | Class | Stereotype | Members, as declared | Anchor |
|---|---|---|---|---|
| CLS-001 | `Todo` | `<<entity>>` | `Id : int`; `Title : string` `[Required]`; `IsComplete : bool`; `OwnerId : string` `[Required]` | `Todo.Api/Todos/Todo.cs:3-12` |
| CLS-002 | `TodoUser` | `<<entity>>` | declares no member of its own — `: IdentityUser`, which supplies `Id`, `UserName`, `NormalizedUserName`, `Email`, `PasswordHash`, `ConcurrencyStamp`, `SecurityStamp`, `LockoutEnd` and the rest of the Identity schema | `Todo.Api/Users/TodoUser.cs:7-9` |
| CLS-003 | `TodoItem` (API) | `<<DTO>>` | `Id : int`; `Title : string` `[Required]`; `IsComplete : bool` — excludes `OwnerId` by design, with the comment "we don't want that exposed to clients" | `Todo.Api/Todos/Todo.cs:14-19` |
| CLS-004 | `UserInfo` (API) | `<<DTO>>` | `Email : string` `[Required]`; `Password : string` `[Required]` | `Todo.Api/Users/TodoUser.cs:12-19` |
| CLS-005 | `ExternalUserInfo` (API) | `<<DTO>>` | `Username : string` `[Required]`; `ProviderKey : string` `[Required]` | `Todo.Api/Users/TodoUser.cs:24-29` |
| CLS-006 | `TodoItem` (web) | `<<DTO>>` | `Id : int`; `Title : string` `[Required]`; `IsComplete : bool` | `Todo.Web/Shared/SharedClass.cs:5-11` |
| CLS-007 | `UserInfo` (web) | `<<DTO>>` | `Email : string` `[Required]`; `Password : string` `[Required]` | `Todo.Web/Shared/SharedClass.cs:13-20` |
| CLS-008 | `ExternalUserInfo` (web) | `<<DTO>>` | `Username : string` `[Required]`; `ProviderKey : string` `[Required]` | `Todo.Web/Shared/SharedClass.cs:22-29` |
| CLS-009 | `AuthToken` | `<<record>>` | `Token : string` mapped to the JSON member `accessToken` by attribute | `Todo.Web/Shared/SharedClass.cs:31` |
| CLS-010 | `TodoMappingExtensions` | static extension class | `AsTodoItem(todo : Todo) : TodoItem` — projects the entity onto the DTO, dropping `OwnerId` | `Todo.Api/Todos/Todo.cs:27-40` |

### Domain relationships

| Relationship | Multiplicity the code declares | Consequence it carries | Anchor |
|---|---|---|---|
| `Todo` → `TodoUser` on `OwnerId` | many-to-one, required (`[Required]` on `OwnerId`; required by the non-nullable `string` under `Nullable enable`) | Every todo belongs to exactly one account, and no todo can exist unattached. Every read, update and delete carries the column in its predicate, so a row is never fetched by id alone and then checked — a non-owner's item answers `404`, never `403` | `Todo.Api/TodoDbContext.cs:11-15`; `Todo.Api/Todos/Todo.cs:9-11`; `Todo.Api/Todos/TodoApi.cs:33,59,69` |
| `Todo` → `TodoUser` on delete | cascade | Declared in the third migration against `AspNetUsers.Id`; the first migration had pointed the same foreign key at `AspNetUsers.UserName`. No endpoint deletes a user, so the rule exists and the operation does not | `Todo.Api/Migrations/20230714032431_ForeignKeyChange.cs:27-34` |
| `Todo` → `TodoItem` (CLS-003) | projection, not an association — computed per response | The wire shape and the stored shape are separate types, and the projection is the only place the owner is dropped. No mapping library is used | `Todo.Api/Todos/Todo.cs:27-40`; `Todo.Api/Todos/TodoApi.cs:26,35,49` |
| `TodoUser` → Identity tables | one-to-many supplied by the framework schema | Seven tables, of which `AspNetRoles` and `AspNetUserRoles` are written by nothing (AN-010, EX-003) | `Todo.Api/TodoDbContext.cs:7`; `Todo.Api/Migrations/20221123071234_Initial.cs` |

**No other association exists.** `TodoUser` exposes no collection of todos; there is no navigation property on either side, so a user's items are reachable only by a query that filters on `OwnerId`. The model is one entity and one edge, and the Identity schema the framework contributes around it.

### CLS-001 Todo — lifecycle

Three states are reachable and a fourth is declared by no operation. The diagram records which transition the delivered product cannot drive, which is the same fact AN-008 records against the update use case.

```plantuml
@startuml
title CLS-001 Todo — the lifecycle the code declares, and the transition no delivered screen can drive
skinparam shadowing false
skinparam defaultTextAlignment left

state "Incomplete" as Incomplete
Incomplete : Id : int (store-generated)
Incomplete : Title : string
Incomplete : OwnerId : string
Incomplete : IsComplete = false

state "Complete" as Complete
Complete : IsComplete = true

state "Deleted" as Deleted
Deleted : row absent; no endpoint restores it

[*] --> Incomplete : POST /todos (TodoApi.cs:38-50)\nTitle from body, OwnerId from caller,\nIsComplete left at its bool default
Incomplete --> Complete : PUT /todos/{id} (TodoApi.cs:52-65)\nIsComplete = body.IsComplete\nBR-019 — Title overwritten too
Complete --> Incomplete : PUT /todos/{id}\nIsComplete = false
Incomplete --> Deleted : DELETE /todos/{id} (TodoApi.cs:67-73)
Complete --> Deleted : DELETE /todos/{id}
Deleted --> [*]

note right of Complete
  AN-008 — the only in-product caller that could reach the
  Incomplete -> Complete transition does not exist.
  TodoList.razor:31 renders the checkbox with no @bind and no
  @onchange, and TodoClient declares no update method. The
  transition is reachable through the API only, so the state is
  writable and unreachable by any delivered actor. Exposed,
  accepted 2026-11-19, not repaired.
end note

note left of Incomplete
  BR-036 / FN-011 — no concurrency token exists on CLS-001.
  Two concurrent PUT calls both match their predicate and the
  later write wins silently; the model has no state in which a
  stale write is refused.
end note

note bottom of Deleted
  AN-010 / EX-002 — the predicate on the update and delete
  statements carries a second disjunct, owner.IsAdmin
  (TodoApi.cs:59,69). No code path grants the role, so the
  disjunct is dead: every transition above is available to the
  owner and to nobody else.
end note
@enduml
```

| State | Reachable by | Guard the code applies | Invariant |
|---|---|---|---|
| Incomplete | `POST /todos` on a new row | `Title` non-empty — CLS-016 is attached to the group and `TodoItem` is its declared type (ADR-004) | `OwnerId` is the caller's `NameIdentifier` and cannot be supplied by the body, because `TodoItem` carries no `OwnerId` member |
| Complete | `PUT /todos/{id}` with `IsComplete = true` | Route id equals body id, owner matches, single `UPDATE ... WHERE` | — |
| Deleted | `DELETE /todos/{id}` | Owner matches, single `DELETE ... WHERE` | No restore path exists |

## Design Packages and Classes
The classes group by the component that declares them, and the grouping is not the project grouping: five packages sit inside `Todo.Api`'s one project because each mechanism is a registration applied to route groups rather than a folder; the BFF package holds seven classes because they share a host and a pipeline; and the remaining four projects each contribute one package. Eleven packages across six projects. The decomposition is held by the interfaces the Software Architecture Document names (`INT-001` … `INT-012`), not by the `.csproj` files.

Every class below is read out of the file named beside it, and none is named that the code does not declare. Where the code declares a class the architecture's component summary does not mention, it is recorded here: a component is a unit of change, not a unit of source files, and the class set is what the compiler holds.

```plantuml
@startuml
title Design Packages — the eleven packages and the classes each component declares
skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam packageStyle rectangle
hide empty members
hide circle

package "Todo.Api · Todos — COMP-008" {
  class "Todo\nCLS-001" as TODO {
    + Id : int
    + Title : string
    + IsComplete : bool
    + OwnerId : string
  }
  class "TodoItem\nCLS-003" as APIDTO {
    + Id : int
    + Title : string
    + IsComplete : bool
  }
  class "TodoMappingExtensions\nCLS-010" as MAPPER {
    {static} + AsTodoItem(todo : Todo) : TodoItem
  }
  class "TodoApi\nCLS-020" as API_TODOS <<internal static module>> {
    {static} + MapTodos(routes) : RouteGroupBuilder
    - GET / (db, owner)
    - GET /{id} (db, id, owner)
    - POST / (db, newTodo : TodoItem, owner)
    - PUT /{id} (db, id, todo : TodoItem, owner)
    - DELETE /{id} (db, id, owner)
  }
}

package "Todo.Api · Users — COMP-007" {
  class "TodoUser\nCLS-002" as TODOUSER
  class "UserInfo\nCLS-004" as APIUSERINFO
  class "ExternalUserInfo\nCLS-005" as APIEXTUSER
  class "UsersApi\nCLS-019" as API_USERS <<static module>> {
    {static} + MapUsers(routes) : RouteGroupBuilder
    - POST /token/{provider} (provider, userInfo, userManager, signInManager, dpp)
  }
}

package "Todo.Api · Persistence — COMP-012" {
  class "TodoDbContext\nCLS-011" as DBCTX {
    + Todos : DbSet~Todo~
    # OnModelCreating(builder)
  }
}

package "Todo.Api · Authorization — COMP-009" {
  class "CurrentUser\nCLS-012" as CUR {
    + User : TodoUser?
    + Principal : ClaimsPrincipal
    + Id : string {readOnly}
    + IsAdmin : bool {readOnly}
  }
  class "ClaimsTransformation\nCLS-013" as CLAIMTRANS <<private sealed>> {
    + TransformAsync(principal) : ClaimsPrincipal
  }
  class "CheckCurrentUserAuthHandler\nCLS-014" as AUTHHANDLER <<private>> {
    # HandleRequirementAsync(context, requirement)
  }
}

package "Todo.Api · Cross-cutting — COMP-010, COMP-011, COMP-013" {
  class "RateLimitExtensions\nCLS-015" as RATELIMIT <<static>> {
    {static} + AddRateLimiting(services)
    {static} + RequirePerUserRateLimit(builder)
  }
  class "ValidationFilterExtensions\nCLS-016" as VALIDATION <<static>> {
    {static} + WithParameterValidation~TBuilder~(builder, params Type[])
  }
  class "OpenApiOptionsExtensions\nCLS-017" as OPENAPI <<static>> {
    {static} + AddBearerTokenAuthentication(options)
  }
}

package "Todo.Web.Server · BFF" {
  class "AuthenticationExtensions\nCLS-028" as AUTHEXT <<public static>> {
    - ExternalAuthProvider(builder, configure) {delegate}
    {static} + AddAuthentication(builder) : WebApplicationBuilder
    - SetAuth0SignInScheme(builder) {local}
    - ExternalProviderKey : string = "ExternalProviderName"
    {static} + GetExternalProvider(properties) : string?
    {static} + SetExternalProvider(properties, providerName)
  }
  class "AuthClient\nCLS-018" as AUTHCLIENT {
    + GetTokenAsync(userInfo : UserInfo) : string?
    + CreateUserAsync(userInfo : UserInfo) : string?
    + GetOrCreateUserAsync(provider, userInfo : ExternalUserInfo) : string?
  }
  class "AuthApi\nCLS-021" as WEB_AUTH <<static module>> {
    {static} + MapAuth(routes) : RouteGroupBuilder
    - POST /auth/register (userInfo, client)
    - POST /auth/login (userInfo, client)
    - POST /auth/logout (context) [authorized]
    - GET /auth/login/{provider} (provider)
    - GET /auth/signin/{provider} (provider, client, context, dpp)
    - {static} SignIn(userId, userName, token, providerName)
  }
  class "TodoApi\nCLS-022" as WEB_FWD <<static module>> {
    {static} + MapTodos(routes) : RouteGroupBuilder
    - /todos/{*path} YARP MapForwarder [authorized]
  }
  class "ExternalProviders\nCLS-023" as EXTPROV {
    + GetProviderNamesAsync() : Task~string[]~
  }
  class "HttpAuthenticationStateProvider\nCLS-024" as AUTHSTATE {
    + GetAuthenticationStateAsync() : Task~AuthenticationState~
  }
  class "TokenNames\nCLS-025" as TOKENNAMES {
    {static} + AccessToken : string = "accessToken"
  }
  class "AuthenticationSchemes\nCLS-026" as SCHEMES {
    {static} + ExternalScheme : string = "External"
  }
}

package "Todo.Web.Client — COMP-005" {
  class "TodoClient\nCLS-027" as TODOCLIENT {
    + AddTodoAsync(title : string?) : TodoItem?
    + DeleteTodoAsync(id : int) : bool
    + GetTodosAsync() : (HttpStatusCode, List~TodoItem~?)
    + LoginAsync(email, password) : bool
    + CreateUserAsync(email, password) : bool
    + LogoutAsync() : bool
  }
}

package "Todo.Web.Shared — COMP-006, the web projects' declaration" {
  class "TodoItem\nCLS-006" as WEBDTO
  class "UserInfo\nCLS-007" as WEBUSERINFO
  class "ExternalUserInfo\nCLS-008" as WEBEXTUSER
  class "AuthToken\nCLS-009" as AUTHTOKEN
}

API_TODOS ..> DBCTX
API_TODOS ..> CUR
API_TODOS ..> APIDTO
API_TODOS ..> TODO
API_TODOS ..> MAPPER
API_USERS ..> TODOUSER
API_USERS ..> APIEXTUSER
API_USERS ..> DBCTX
DBCTX ..> TODO
DBCTX ..> TODOUSER
CLAIMTRANS ..> CUR
CLAIMTRANS ..> TODOUSER
AUTHHANDLER ..> CUR
WEB_AUTH ..> AUTHCLIENT
WEB_AUTH ..> TOKENNAMES
WEB_AUTH ..> AUTHEXT : SetExternalProvider
WEB_FWD ..> TOKENNAMES
AUTHCLIENT ..> API_USERS : HTTP users/register,\nusers/login, users/token/{provider}
TODOCLIENT ..> WEB_AUTH : HTTP auth/*
TODOCLIENT ..> WEB_FWD : HTTP todos
AUTHSTATE ..> SCHEMES
EXTPROV ..> SCHEMES
AUTHEXT ..> SCHEMES
AUTHEXT ..> AUTHSTATE : registers
AUTHEXT ..> EXTPROV : registers
WEB_AUTH ..> WEBUSERINFO : serializes
AUTHCLIENT ..> WEBUSERINFO : serializes
AUTHCLIENT ..> WEBEXTUSER : serializes
AUTHCLIENT ..> AUTHTOKEN : reads accessToken
TODOCLIENT ..> WEBDTO

note right of AUTHEXT
  CLS-028 Todo.Web/Server/Authentication/
  AuthenticationExtensions.cs:12-100.
  Registering the cookie scheme is the whole
  of SS-001: AddCookie() for the default scheme
  and AddCookie("External") for the provider hop.
  The provider loop at :40-52 adds GitHub, Google,
  Microsoft and Auth0 only when
  Authentication:Schemes:<provider> exists — no
  shipped settings file carries it, so the four
  schemes are inert (AN-002, EX-001).
  Every other class in this package is reached from
  here: it is the only caller that registers
  CLS-023, CLS-024 and CLS-026.
end note
note right of TODOCLIENT
  CLS-027 Todo.Web/Client/TodoClient.cs:7-71.
  No update method exists — the counterpart of AN-008.
end note
note bottom of WEBDTO
  ADR-011 — the wire shape is declared twice.
  CLS-006..CLS-009 Todo.Web/Shared/SharedClass.cs:5-31
  are the web projects' declarations; CLS-003, CLS-004
  and CLS-005 in the Todo.Api packages are the API's own,
  and no reference edge joins the two (CON-A10).
end note
note bottom of CUR
  CLS-012 Todo.Api/Authorization/CurrentUser.cs:6-15.
  IsAdmin is the dead branch (AN-010, EX-002).
end note
@enduml
```

### Design classes, with the operations the code implements

| ID | Class | Package | Operations, as declared | Anchored dependency | Anchor |
|---|---|---|---|---|---|
| CLS-020 | `TodoApi` | Todo.Api · Todos | `MapTodos(routes) : RouteGroupBuilder`; five handlers: list, read one, create, update, delete | `TodoDbContext`, `CurrentUser`, `TodoItem`, `Todo`, `AsTodoItem` | `Todo.Api/Todos/TodoApi.cs:8-77` |
| CLS-019 | `UsersApi` | Todo.Api · Users | `MapUsers(routes) : RouteGroupBuilder`; the stock `MapIdentityApi<TodoUser>()` group plus one custom handler `POST /token/{provider}` | `TodoUser`, `ExternalUserInfo`, `UserManager`, `SignInManager`, `IDataProtectionProvider` | `Todo.Api/Users/UsersApi.cs:10-64` |
| CLS-011 | `TodoDbContext` | Todo.Api · Persistence | `Todos : DbSet<Todo>`; `OnModelCreating(builder)` declaring the ownership foreign key against `AspNetUsers.Id` | primary constructor over `DbContextOptions<TodoDbContext>`; base `IdentityDbContext<TodoUser>` | `Todo.Api/TodoDbContext.cs:7-21` |
| CLS-012 | `CurrentUser` | Todo.Api · Authorization | `User : TodoUser?` (settable); `Principal : ClaimsPrincipal` (settable); `Id : string` (computed from `NameIdentifier`); `IsAdmin : bool` (computed from the `admin` role claim) | `ClaimsPrincipal`, `TodoUser` | `Todo.Api/Authorization/CurrentUser.cs:6-15` |
| CLS-013 | `ClaimsTransformation` | Todo.Api · Authorization | `TransformAsync(principal) : ClaimsPrincipal` | `CurrentUser`, `UserManager<TodoUser>` | `Todo.Api/Authorization/CurrentUserExtensions.cs:14-35` |
| CLS-014 | `CheckCurrentUserAuthHandler` | Todo.Api · Authorization | `HandleRequirementAsync(context, requirement)` — succeeds only when `CurrentUser.User` is non-null | `CurrentUser` | `Todo.Api/Authorization/CheckCurrentUserAuthHandler.cs:17-39` |
| CLS-015 | `RateLimitExtensions` | Todo.Api · Cross-cutting | `AddRateLimiting(services)`; `RequirePerUserRateLimit(builder) : IEndpointConventionBuilder` | framework rate limiter, `TokenBucketRateLimiterOptions` | `Todo.Api/Extensions/RateLimitExtensions.cs:11-71` |
| CLS-016 | `ValidationFilterExtensions` | Todo.Api · Cross-cutting | `WithParameterValidation<TBuilder>(builder, params Type[]) : TBuilder` | `MiniValidator` | `Todo.Api/Filters/ValidationFilter.cs:7-58` |
| CLS-017 | `OpenApiOptionsExtensions` | Todo.Api · Cross-cutting | `AddBearerTokenAuthentication(options) : OpenApiOptions` | `Microsoft.OpenApi.Models`, `IAuthorizeData` | `Todo.Api/Extensions/OpenApiOptionsExtensions.cs:7-47` |
| CLS-028 | `AuthenticationExtensions` | Todo.Web.Server · BFF | `AddAuthentication(builder) : WebApplicationBuilder`; the private delegate `ExternalAuthProvider`; the local `SetAuth0SignInScheme(builder)`; `ExternalProviderKey = "ExternalProviderName"`; `GetExternalProvider(properties) : string?`; `SetExternalProvider(properties, providerName)` | `AuthenticationSchemes`, `ExternalProviders`, `HttpAuthenticationStateProvider`, `IAuthenticationSchemeProvider`, four provider option types | `Todo.Web/Server/Authentication/AuthenticationExtensions.cs:12-100` |
| CLS-018 | `AuthClient` | Todo.Web.Server · BFF | `GetTokenAsync(UserInfo) : Task<string?>`; `CreateUserAsync(UserInfo) : Task<string?>`; `GetOrCreateUserAsync(string, ExternalUserInfo) : Task<string?>` | `HttpClient` with `BaseAddress = http://todoapi` | `Todo.Web/Server/AuthClient.cs:3-46` |
| CLS-021 | `AuthApi` | Todo.Web.Server · BFF | `MapAuth(routes) : RouteGroupBuilder`; three public POSTs, two provider GETs, one private `SignIn` overload pair | `AuthClient`, `TokenNames`, `AuthenticationSchemes`, `AuthenticationExtensions.SetExternalProvider`, `IDataProtectionProvider` | `Todo.Web/Server/AuthApi.cs:12-128` |
| CLS-022 | `TodoApi` | Todo.Web.Server · BFF | `MapTodos(routes) : RouteGroupBuilder`; one YARP `MapForwarder` at `{*path}` with a request transform | `TokenNames`, `IHttpForwarder` | `Todo.Web/Server/TodoApi.cs:9-28` |
| CLS-023 | `ExternalProviders` | Todo.Web.Server · BFF | `GetProviderNamesAsync() : Task<string[]>` — every scheme that is neither cookie scheme, memoized in a field | `IAuthenticationSchemeProvider` | `Todo.Web/Server/Authentication/ExternalProviders.cs:5-35` |
| CLS-024 | `HttpAuthenticationStateProvider` | Todo.Web.Server · BFF | `GetAuthenticationStateAsync() : Task<AuthenticationState>` — `HttpContext.User`, or an empty principal | `IHttpContextAccessor` | `Todo.Web/Server/Authentication/HttpAuthenticationStateProvider.cs:3-10` |
| CLS-025 | `TokenNames` | Todo.Web.Server · BFF | `static AccessToken : string = "accessToken"` — the one token name the BFF holds | — | `Todo.Web/Server/Authentication/TokenNames.cs:3-6` |
| CLS-026 | `AuthenticationSchemes` | Todo.Web.Server · BFF | `static ExternalScheme : string = "External"` | — | `Todo.Web/Server/Authentication/AuthenticationSchemes.cs:3-7` |
| CLS-027 | `TodoClient` | Todo.Web.Client | `AddTodoAsync(string?) : Task<TodoItem?>`; `DeleteTodoAsync(int) : Task<bool>`; `GetTodosAsync() : Task<(HttpStatusCode, List<TodoItem>?)>`; `LoginAsync`; `CreateUserAsync`; `LogoutAsync` | `HttpClient` with `BaseAddress = HostEnvironment.BaseAddress` | `Todo.Web/Client/TodoClient.cs:7-71` |

`CLS-028` is the class the architecture's component summary does not name and the code holds: the only caller of `AddCookie`, the only caller that registers `CLS-023`, `CLS-024` and `CLS-026`, and the sole site of the provider loop that `EX-001` excludes. It is the whole of mechanism `SS-001` in one static class, and it is a member of COMP-002 because the session authority is defined as the component that owns the cookie scheme.

### What the class model fixes that the requirement statements do not

Four facts belong to the class model because no use-case text can carry them, and each is a constraint the Implementer inherits.

**CLS-027 declares no update operation.** `TodoClient` carries six methods and not one of them issues `PUT`. The absence is a fact of the class, not a gap in a screen — which is why the update use case has an API path and no client path (AN-008). A design that added the method would be adding a capability no requirement declares.

**CLS-012 exposes `IsAdmin` as a computed read-only property with no writer in product code.** `CurrentUser.User` and `Principal` are settable and are written by CLS-013; `Id` and `IsAdmin` are computed and nothing in the product assigns them. `IsAdmin` derives from a claim only CLS-033 mints, so the two disjuncts in `TodoApi.cs:59,69` that read it are unreachable in any delivered run (AN-010, `EX-002`). The member is recovered because the code declares it; it is not evidence of a capability.

**CLS-016 matches on the declared parameter type, and that type is not the credential body.** `WithParameterValidation(typeof(ExternalUserInfo))` is applied to the `/users` group and `WithParameterValidation(typeof(TodoItem))` to `/todos`. `UserInfo` — the body of registration and sign-in — is named by neither call site, so the filter is attached to no endpoint that receives it and CLS-004's `[Required]` attributes are enforced by nothing on the server (BR-032, ADR-004). The `[Required]` attributes on CLS-004 and CLS-007 do take effect in the browser through `DataAnnotationsValidator` on the login form, which is where the only enforcement sits.

**CLS-028 is the model's only cookie registration, and it is static.** The two `AddCookie` calls sit inside `AddAuthentication(this WebApplicationBuilder)`, called once from `Todo.Web/Server/Program.cs:9`. No option, lifetime, sliding-expiry or key-repository value is set here, so the cookie's lifetime is the framework default and `SS-001`'s properties are held by convention rather than by configuration (ADR-002, AN-015, AN-017).

### Ownership trace — every class to the component that holds it

| Package | Component (SAD) | Classes | Project |
|---|---|---|---|
| Todo.Api · Todos | COMP-008 | CLS-001, CLS-003, CLS-010, CLS-020 | `Todo.Api` |
| Todo.Api · Users | COMP-007 | CLS-002, CLS-004, CLS-005, CLS-019 | `Todo.Api` |
| Todo.Api · Persistence | COMP-012 | CLS-011 | `Todo.Api` |
| Todo.Api · Authorization | COMP-009 | CLS-012, CLS-013, CLS-014 | `Todo.Api` |
| Todo.Api · Cross-cutting | COMP-010, COMP-011, COMP-013 | CLS-015, CLS-016, CLS-017 | `Todo.Api` |
| Todo.Web.Server · BFF | COMP-002 (CLS-018, CLS-021, CLS-025, CLS-026, CLS-028); COMP-003 (CLS-022); COMP-001 (CLS-023, CLS-024) | CLS-018, CLS-021, CLS-022, CLS-023, CLS-024, CLS-025, CLS-026, CLS-028 | `Todo.Web/Server` |
| Todo.Web.Client | COMP-005 | CLS-027 | `Todo.Web/Client` |
| Todo.Web.Shared | COMP-006 | CLS-006, CLS-007, CLS-008, CLS-009 | `Todo.Web/Shared` |
| TodoApp.ServiceDefaults | COMP-014 | CLS-029 | `TodoApp.ServiceDefaults` |
| TodoApp.AppHost | COMP-015, COMP-016 | CLS-030 | `TodoApp.AppHost` |
| Todo.Api.Tests | COMP-017 | CLS-031, CLS-032, CLS-033, CLS-034 | `Todo.Api.Tests` |

One component carries no class: COMP-018, the CI pipeline, which is a workflow document with no compilation unit. `TodoApp.AppHost/Program.cs` likewise declares no class — it is top-level statements — so the orchestrator's behaviour is held entirely by CLS-030 across COMP-015 and COMP-016.

### Host configuration, orchestration and verification classes

Five components were recorded as carrying no class of their own. Four of them declare one; the fifth — COMP-018, the CI workflow — declares none because it is a YAML document, not a compilation unit.

```plantuml
@startuml
title The four components the architecture records without a class also declare one — host configuration, orchestration and verification
skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam packageStyle rectangle
hide empty members
hide circle

package "TodoApp.ServiceDefaults — COMP-014" {
  class "Extensions\nCLS-029" as SDExt <<public static, namespace Microsoft.Extensions.Hosting>> {
    {static} + AddServiceDefaults~TBuilder~(builder) : TBuilder
    {static} + ConfigureOpenTelemetry~TBuilder~(builder) : TBuilder
    - {static} + AddOpenTelemetryExporters~TBuilder~(builder) : TBuilder
    {static} + AddDefaultHealthChecks~TBuilder~(builder) : TBuilder
    {static} + MapDefaultEndpoints(app) : WebApplication
  }
}

package "TodoApp.AppHost — COMP-015 and COMP-016" {
  class "Extensions\nCLS-030" as AHExt <<internal static>> {
    {static} + AddTodoDbMigration(builder) : IResourceBuilder~ExecutableResource~?
    {static} + AddEfMigration~TProject~(builder, name) : IResourceBuilder~ExecutableResource~
    {static} + GetProjectDirectory(project) : string
  }
}

package "Todo.Api.Tests — COMP-017" {
  class "TodoApplication\nCLS-031" as TESTAPP <<internal, : WebApplicationFactory~Program~>> {
    - _sqliteConnection : SqliteConnection
    + CreateTodoDbContext() : TodoDbContext
    + CreateUserAsync(username, password) : Task
    + CreateClient(id, isAdmin = false) : HttpClient
    # CreateHost(builder) : IHost
    # Dispose(disposing)
  }
  class "AuthHandler\nCLS-032" as AUTHH <<private sealed, : DelegatingHandler, nested>> {
    # SendAsync(request, cancellationToken) : HttpResponseMessage
  }
  class "TokenService\nCLS-033" as TOKENSVC <<public sealed>> {
    - _options : BearerTokenOptions
    + GenerateTokenAsync(username, isAdmin = false) : Task~string~
  }
  class "DbContextExtensions\nCLS-034" as DBEXT <<internal static>> {
    {static} + AddDbContextOptions~TContext~(services, configure) : IServiceCollection
  }
}

TESTAPP +-- AUTHH : nested
TESTAPP ..> DBEXT : replaces the DbContext options
TESTAPP ..> TOKENSVC : registered scoped
AUTHH ..> TOKENSVC : resolves and mints
TOKENSVC ..> TODOUSER : builds the principal
TESTAPP ..> DBCTX : EnsureCreated over :memory:

class "TodoUser\nCLS-002" as TODOUSER
class "TodoDbContext\nCLS-011\nCOMP-012" as DBCTX

note right of SDExt
  CLS-029 TodoApp.ServiceDefaults/Extensions.cs:16-117.
  AddServiceDefaults is called by both hosts
  (Todo.Api/Program.cs:7, Todo.Web/Server/Program.cs:6),
  which is what makes it COMP-014 rather than a
  library of its own. AddOpenTelemetryExporters is
  private despite being an extension method; the
  OTLP branch at :75-81 is the SS-009 mechanism.
  MapDefaultEndpoints maps /health and /alive inside
  IsDevelopment only — EP-025.
end note

note right of AHExt
  CLS-030 TodoApp.AppHost/Extensions.cs:1-38.
  One class carries both COMP-015's start-up ordering
  and COMP-016's migration: AddTodoDbMigration gates on
  the .db directory's absence, AddEfMigration chains
  WaitForCompletion over the global dotnet-ef install.
  Program.cs:1-28 is top-level statements and declares
  no class, so this is the only class the orchestrator
  authors.
end note

note bottom of TESTAPP
  CLS-031..CLS-034 Todo.Api.Tests/.
  The harness replaces the data-protection provider with
  EphemeralDataProtectionProvider (:53) and the DbContext
  options with a held-open in-memory connection (:37-56),
  which is why AN-020 holds: this proves Todo.Api alone,
  never the assembled topology.
  TokenService mints the admin claim (TokenService.cs:16-21)
  that no product code path can mint (AN-010, EX-002).
end note
@enduml
```

| ID | Class | Package | Operations, as declared | Component | Anchor |
|---|---|---|---|---|---|
| CLS-029 | `Extensions` | TodoApp.ServiceDefaults | `AddServiceDefaults<TBuilder>(builder) : TBuilder`; `ConfigureOpenTelemetry<TBuilder>(builder) : TBuilder`; private `AddOpenTelemetryExporters<TBuilder>(builder) : TBuilder`; `AddDefaultHealthChecks<TBuilder>(builder) : TBuilder`; `MapDefaultEndpoints(app) : WebApplication` | COMP-014 | `TodoApp.ServiceDefaults/Extensions.cs:16-117` |
| CLS-030 | `Extensions` | TodoApp.AppHost | `AddTodoDbMigration(builder) : IResourceBuilder<ExecutableResource>?`; `AddEfMigration<TProject>(builder, name) : IResourceBuilder<ExecutableResource>`; `GetProjectDirectory(project) : string` | COMP-015, COMP-016 | `TodoApp.AppHost/Extensions.cs:1-38` |
| CLS-031 | `TodoApplication` | Todo.Api.Tests | `CreateTodoDbContext() : TodoDbContext`; `CreateUserAsync(username, password) : Task`; `CreateClient(id, isAdmin = false) : HttpClient`; protected `CreateHost(builder) : IHost`; protected `Dispose(disposing)`; private field `_sqliteConnection : SqliteConnection` | COMP-017 | `Todo.Api.Tests/TodoApplication.cs:5-95` |
| CLS-032 | `AuthHandler` | Todo.Api.Tests | `SendAsync(request, cancellationToken) : HttpResponseMessage` — mints a bearer token and writes it onto the outgoing request | COMP-017 | `Todo.Api.Tests/TodoApplication.cs:77-95` |
| CLS-033 | `TokenService` | Todo.Api.Tests | `GenerateTokenAsync(username, isAdmin = false) : Task<string>` — builds the principal, adds the `admin` role claim when asked, protects a bearer ticket | COMP-017 | `Todo.Api.Tests/TokenService.cs:8-33` |
| CLS-034 | `DbContextExtensions` | Todo.Api.Tests | `AddDbContextOptions<TContext>(services, configure) : IServiceCollection` — removes the registered options and re-adds them as singletons | COMP-017 | `Todo.Api.Tests/DbContextExtensions.cs:3-29` |

`CLS-033` is the only class in the whole model that mints the `admin` role claim (`TokenService.cs:16-21`). No product class can: `CLS-012.IsAdmin` reads a claim only this test type writes, and `AspNetRoles`/`AspNetUserRoles` are written by nothing (AN-010, `EX-002`). The claim's existence in the model is evidence of a test fixture, not of a capability.

## Traceability
Every class below is recovered from code, and the anchor cited where it is described is its source. A class the code declares but no recovered use case crosses carries no upstream and none is composed for it: `CLS-005` and `CLS-008` (`ExternalUserInfo` on each side — `EP-011` is an exclusion), `CLS-023` (`ExternalProviders`, whose list no shipped configuration populates), `CLS-026` (`AuthenticationSchemes`, whose only member names the external-cookie scheme the excluded provider flow uses), and `CLS-029` … `CLS-034` — the host-configuration, orchestration and test classes, which lie on no actor's path. The architecture records COMP-014 … COMP-017 as realizing no use case; the classes those components declare inherit that absence.

Three pairs are one fact declared twice, not six facts: `CLS-003`/`CLS-006`, `CLS-004`/`CLS-007` and `CLS-005`/`CLS-008` are the two declarations of one wire shape per ADR-011, and each declaration is traced on its own side because each is a separate class the compiler holds.

`DependsOn` is written only where a class reaches across a package boundary, and it is written by the depending class. Dependencies inside a package are in the class diagram and are not repeated here.

| Element | Traces From | Link Type | Traces To |
|---|---|---|---|
| CLS-001 | UC-004, UC-005, UC-006, UC-007 | Realizes | — |
| CLS-002 | UC-001, UC-002 | Realizes | — |
| CLS-003 | UC-004, UC-005, UC-006 | Realizes | — |
| CLS-004 | UC-001, UC-002 | Realizes | — |
| CLS-005 | — | — | — |
| CLS-006 | UC-004, UC-005, UC-007 | Realizes | — |
| CLS-007 | UC-001, UC-002 | Realizes | — |
| CLS-008 | — | — | — |
| CLS-009 | UC-001, UC-002 | Realizes | — |
| CLS-010 | UC-004, UC-005, UC-006 | Realizes | — |
| CLS-011 | UC-001, UC-002, UC-004, UC-005, UC-006, UC-007 | Realizes | — |
| CLS-012 | UC-004, UC-005, UC-006, UC-007 | Realizes | — |
| CLS-013 | UC-004, UC-005, UC-006, UC-007 | Realizes | CLS-012, CLS-002 |
| CLS-014 | UC-004, UC-005, UC-006, UC-007 | Realizes | CLS-012 |
| CLS-015 | UC-004, UC-005, UC-006, UC-007 | Realizes | — |
| CLS-016 | UC-005, UC-006 | Realizes | — |
| CLS-017 | UC-008 | Realizes | — |
| CLS-018 | UC-001, UC-002 | Realizes | — |
| CLS-019 | UC-001, UC-002 | Realizes | CLS-002, CLS-011 |
| CLS-020 | UC-004, UC-005, UC-006, UC-007 | Realizes | CLS-001, CLS-003, CLS-010, CLS-011, CLS-012 |
| CLS-021 | UC-001, UC-002, UC-003 | Realizes | CLS-018, CLS-025 |
| CLS-022 | UC-004, UC-005, UC-006, UC-007 | Realizes | CLS-025 |
| CLS-023 | — | — | — |
| CLS-024 | UC-001, UC-002, UC-003, UC-004 | Realizes | — |
| CLS-025 | UC-001, UC-002, UC-004, UC-005, UC-006, UC-007 | Realizes | — |
| CLS-026 | — | — | — |
| CLS-027 | UC-001, UC-002, UC-003, UC-004, UC-005, UC-007 | Realizes | — |
| CLS-028 | UC-001, UC-002, UC-003 | Realizes | — |
| CLS-029 | — | — | — |
| CLS-030 | — | — | — |
| CLS-031 | — | — | CLS-011 |
| CLS-032 | — | — | CLS-033 |
| CLS-033 | — | — | CLS-002 |
| CLS-034 | — | — | — |

