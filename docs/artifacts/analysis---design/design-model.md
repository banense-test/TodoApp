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
| `Todo` → `TodoUser` on `OwnerId` | many-to-one, required (`[Required]` on `OwnerId`; `IsRequired` by the non-nullable `string` under `Nullable enable`) | Every todo belongs to exactly one account, and no todo can exist unattached. Every read, update and delete carries the column in its predicate, so a row is never fetched by id alone and then checked — a non-owner's item answers `404`, never `403` | `Todo.Api/TodoDbContext.cs:11-15`; `Todo.Api/Todos/Todo.cs:9-11`; `Todo.Api/Todos/TodoApi.cs:33,59,69` |
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
| Incomplete | `POST /todos` on a new row | `Title` non-empty (CLS-016 validation on the group; `TodoItem` is the declared body type, ADR-004) | `OwnerId` is the caller's `NameIdentifier` and cannot be supplied by the body, because `TodoItem` carries no `OwnerId` member |
| Complete | `PUT /todos/{id}` with `IsComplete = true` | Route id equals body id, owner matches, single `UPDATE ... WHERE` | — |
| Deleted | `DELETE /todos/{id}` | Owner matches, single `DELETE ... WHERE` | No restore path exists |

## Design Packages and Classes
The classes group by the component that declares them, and the grouping is not the project grouping: five packages sit inside `Todo.Api`'s one project because each mechanism is a registration applied to route groups rather than a folder, and three sit inside `Todo.Web.Server` because they share a host and a pipeline. The decomposition is held by the interfaces the Software Architecture Document names (`INT-001` … `INT-012`), not by the `.csproj` files.

```plantuml
@startuml
title Design Packages — the recovered classes grouped by the component that holds them, with the references the code declares
skinparam shadowing false
skinparam classAttributeIconSize 0
skinparam packageStyle rectangle
hide empty members
hide circle

package "Todo.Api · Todos" {
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
    - GET / (db : TodoDbContext, owner : CurrentUser)
    - GET /{id} (db, id : int, owner)
    - POST / (db, newTodo : TodoItem, owner)
    - PUT /{id} (db, id, todo : TodoItem, owner)
    - DELETE /{id} (db, id, owner)
  }
}

package "Todo.Api · Users" {
  class "TodoUser\nCLS-002" as TODOUSER
  class "UserInfo\nCLS-004" as APIUSERINFO
  class "ExternalUserInfo\nCLS-005" as APIEXTUSER
  class "UsersApi\nCLS-019" as API_USERS <<static module>> {
    {static} + MapUsers(routes) : RouteGroupBuilder
    - POST /token/{provider} (provider,\n  userInfo : ExternalUserInfo,\n  userManager, signInManager,\n  dataProtectionProvider)
  }
}

package "Todo.Api · Persistence" {
  class "TodoDbContext\nCLS-011" as DBCTX {
    + Todos : DbSet~Todo~
    # OnModelCreating(builder)
  }
}

package "Todo.Api · Authorization" {
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

package "Todo.Api · Cross-cutting" {
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
  class "AuthClient\nCLS-018" as AUTHCLIENT {
    + GetTokenAsync(userInfo : UserInfo) : string?
    + CreateUserAsync(userInfo : UserInfo) : string?
    + GetOrCreateUserAsync(provider : string, userInfo : ExternalUserInfo) : string?
  }
  class "AuthApi\nCLS-021" as WEB_AUTH <<static module>> {
    {static} + MapAuth(routes) : RouteGroupBuilder
    - POST /auth/register (userInfo : UserInfo, client : AuthClient)
    - POST /auth/login (userInfo : UserInfo, client : AuthClient)
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

package "Todo.Web.Client" {
  class "TodoClient\nCLS-027" as TODOCLIENT {
    + AddTodoAsync(title : string?) : TodoItem?
    + DeleteTodoAsync(id : int) : bool
    + GetTodosAsync() : (HttpStatusCode, List~TodoItem~?)
    + LoginAsync(email, password) : bool
    + CreateUserAsync(email, password) : bool
    + LogoutAsync() : bool
  }
}

API_TODOS ..> DBCTX : resolves per request
API_TODOS ..> CUR : resolves per request
API_TODOS ..> APIDTO : validates / projects
API_TODOS ..> TODO
API_TODOS ..> MAPPER
API_USERS ..> TODOUSER
API_USERS ..> APIEXTUSER
API_USERS ..> DBCTX : via UserManager
DBCTX ..> TODO
DBCTX ..> TODOUSER
CLAIMTRANS ..> CUR : fills
CLAIMTRANS ..> TODOUSER : FindByIdAsync
AUTHHANDLER ..> CUR : reads
WEB_AUTH ..> AUTHCLIENT
WEB_AUTH ..> TOKENNAMES
WEB_FWD ..> TOKENNAMES
AUTHCLIENT ..> API_USERS : HTTP users/register,\nusers/login, users/token/{provider}
TODOCLIENT ..> WEB_AUTH : HTTP auth/*
TODOCLIENT ..> WEB_FWD : HTTP todos
AUTHSTATE ..> SCHEMES : default scheme
EXTPROV ..> SCHEMES : skips both cookie schemes

note right of TODOCLIENT
  CLS-027 Todo.Web/Client/TodoClient.cs:7-71.
  No update method exists — the counterpart of AN-008.
  GetTodosAsync:14-24 returns (200, empty list) when
  BaseAddress is null, which is the prerender pass.
end note

note right of WEB_FWD
  CLS-022 Todo.Web/Server/TodoApi.cs:9-28.
  The request transform reads the cookie's accessToken
  and writes it into ProxyRequest.Headers.Authorization
  unchecked (BR-034): no presence test, no freshness test.
end note

note bottom of CUR
  CLS-012 Todo.Api/Authorization/CurrentUser.cs:6-15.
  IsAdmin is the dead branch (AN-010, EX-002).
  CLS-013 / CLS-014 Todo.Api/Authorization/
  CurrentUserExtensions.cs:8-35 and
  CheckCurrentUserAuthHandler.cs:8-40.
end note

note bottom of RATELIMIT
  CLS-015 Todo.Api/Extensions/RateLimitExtensions.cs:11-71.
  One policy, partitioned on NameIdentifier.
  CLS-016 Todo.Api/Filters/ValidationFilter.cs:7-58 — matched
  on the declared parameter type, which is why UserInfo is on
  no validated endpoint (BR-032, ADR-004).
  CLS-017 Todo.Api/Extensions/OpenApiOptionsExtensions.cs:7-47.
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
| CLS-018 | `AuthClient` | Todo.Web.Server · BFF | `GetTokenAsync(UserInfo) : Task<string?>`; `CreateUserAsync(UserInfo) : Task<string?>`; `GetOrCreateUserAsync(string, ExternalUserInfo) : Task<string?>` | `HttpClient` with `BaseAddress = http://todoapi` | `Todo.Web/Server/AuthClient.cs:3-46` |
| CLS-021 | `AuthApi` | Todo.Web.Server · BFF | `MapAuth(routes) : RouteGroupBuilder`; three public POSTs, two provider GETs, one private `SignIn` overload pair | `AuthClient`, `TokenNames`, `AuthenticationSchemes`, `IDataProtectionProvider` | `Todo.Web/Server/AuthApi.cs:12-128` |
| CLS-022 | `TodoApi` | Todo.Web.Server · BFF | `MapTodos(routes) : RouteGroupBuilder`; one YARP `MapForwarder` at `{*path}` with a request transform | `TokenNames`, `IHttpForwarder` | `Todo.Web/Server/TodoApi.cs:9-28` |
| CLS-023 | `ExternalProviders` | Todo.Web.Server · BFF | `GetProviderNamesAsync() : Task<string[]>` — every scheme that is neither cookie scheme, memoized in a field | `IAuthenticationSchemeProvider` | `Todo.Web/Server/Authentication/ExternalProviders.cs:5-35` |
| CLS-024 | `HttpAuthenticationStateProvider` | Todo.Web.Server · BFF | `GetAuthenticationStateAsync() : Task<AuthenticationState>` — `HttpContext.User`, or an empty principal | `IHttpContextAccessor` | `Todo.Web/Server/Authentication/HttpAuthenticationStateProvider.cs:3-10` |
| CLS-025 | `TokenNames` | Todo.Web.Server · BFF | `static AccessToken : string = "accessToken"` — the one token name the BFF holds | — | `Todo.Web/Server/Authentication/TokenNames.cs:3-6` |
| CLS-026 | `AuthenticationSchemes` | Todo.Web.Server · BFF | `static ExternalScheme : string = "External"` | — | `Todo.Web/Server/Authentication/AuthenticationSchemes.cs:3-7` |
| CLS-027 | `TodoClient` | Todo.Web.Client | `AddTodoAsync(string?) : Task<TodoItem?>`; `DeleteTodoAsync(int) : Task<bool>`; `GetTodosAsync() : Task<(HttpStatusCode, List<TodoItem>?)>`; `LoginAsync`; `CreateUserAsync`; `LogoutAsync` | `HttpClient` with `BaseAddress = HostEnvironment.BaseAddress` | `Todo.Web/Client/TodoClient.cs:7-71` |

### What the class model fixes that the requirement statements do not

Three facts belong to the class model because no use-case text can carry them, and each is a constraint the Implementer inherits.

**CLS-027 declares no update operation.** `TodoClient` carries six methods and not one of them issues `PUT`. The absence is a fact of the class, not a gap in a screen — which is why the update use case has an API path and no client path (AN-008). A design that added the method would be adding a capability no requirement declares.

**CLS-012 exposes `IsAdmin` as a computed read-only property with no writer.** `CurrentUser.User` and `Principal` are settable and are written by CLS-013; `Id` and `IsAdmin` are computed and nothing assigns them. `IsAdmin` derives from a claim no endpoint in the model can mint, so the two disjuncts in `TodoApi.cs:59,69` that read it are unreachable (AN-010, EX-002). The member is recovered because the code declares it; it is not evidence of a capability.

**CLS-016 matches on the declared parameter type, and that type is not the credential body.** `WithParameterValidation(typeof(ExternalUserInfo))` is applied to the `/users` group and `WithParameterValidation(typeof(TodoItem))` to `/todos`. `UserInfo` — the body of registration and sign-in — is named by neither call site, so the filter is attached to no endpoint that receives it and CLS-004's `[Required]` attributes are enforced by nothing on the server (BR-032, ADR-004). The `[Required]` attributes on CLS-004 and CLS-007 do take effect in the browser through `DataAnnotationsValidator` on the login form, which is where the only enforcement sits.

### Ownership trace — every class to the component that holds it

| Package | Component (SAD) | Classes | Project |
|---|---|---|---|
| Todo.Api · Todos | COMP-008 | CLS-001, CLS-003, CLS-010, CLS-020 | `Todo.Api` |
| Todo.Api · Users | COMP-007 | CLS-002, CLS-004, CLS-005, CLS-019 | `Todo.Api` |
| Todo.Api · Persistence | COMP-012 | CLS-011 | `Todo.Api` |
| Todo.Api · Authorization | COMP-009 | CLS-012, CLS-013, CLS-014 | `Todo.Api` |
| Todo.Api · Cross-cutting | COMP-010, COMP-011, COMP-013 | CLS-015, CLS-016, CLS-017 | `Todo.Api` |
| Todo.Web.Server · BFF | COMP-002 (CLS-018, CLS-021, CLS-025, CLS-026); COMP-003 (CLS-022); COMP-001 (CLS-023, CLS-024) | CLS-018, CLS-021, CLS-022, CLS-023, CLS-024, CLS-025, CLS-026 | `Todo.Web/Server` |
| Todo.Web.Client | COMP-005 | CLS-027 | `Todo.Web/Client` |
| Todo.Web.Shared | COMP-006 | CLS-006, CLS-007, CLS-008, CLS-009 | `Todo.Web/Shared` |

Two components carry no class of their own, and that is correct rather than incomplete: COMP-014 (`TodoApp.ServiceDefaults`) is registered by builder extensions with no class the product authored, COMP-015/COMP-016 are an orchestration program and a CLI invocation, and COMP-017/COMP-018 are the test harness and the pipeline. A class diagram recovers the classes the product declares; those five components declare none.

## Traceability
Every class below is recovered from code, and the anchor cited where it is described is its source. A class the code declares but no recovered use case crosses carries no upstream and none is composed for it: `CLS-005` and `CLS-008` (`ExternalUserInfo` on each side — `EP-011` is an exclusion), `CLS-023` (`ExternalProviders`, whose list no shipped configuration populates), `CLS-026` (`AuthenticationSchemes`, whose only member names the external-cookie scheme the excluded provider flow uses). Four elements of one fact are not four facts: `CLS-003`/`CLS-006`, `CLS-004`/`CLS-007` and `CLS-005`/`CLS-008` are the two declarations of one wire shape per ADR-011, and each declaration is traced on its own side because each is a separate class the compiler holds.

`DependsOn` is written only where a class reaches across a package boundary. Dependencies inside a package are in the class diagram and are not repeated here.

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

