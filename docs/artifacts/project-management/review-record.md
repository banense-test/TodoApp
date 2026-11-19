## Document Control
### Reviewer lens
<!-- review: Survey I1 -->

- Phase: Survey
- Status: Draft — technical lens of the end-of-Survey milestone review
- Milestone Target: end of Survey (SBC) — not yet achieved
- Review type: Milestone review (SBC), technical lens — formal inspection against the artifact-type checklists
- Reviewed: Development Case, System Inventory, Risk List, Iteration Plan — all Survey, Draft, iteration 1
- SCM evidence: no pull request in any state; no IARI build on `main`

## Review Scope and Criteria
### Reviewer lens
<!-- review: Survey I1 -->

SBC asks one question: is the material the whole recovery will rest on adequate? Four artifacts answer it, and they are the only four anything in Excavation, Consolidation and Inception will cite. Nothing was built in this iteration — no code, no pull request, no build — so the review is entirely an evidence review: does each claim rest on what it cites.

Three lenses of the SBC review follow this one; this block records the technical lens only.

| Artifact | Author | Checklist applied | Version reviewed |
|---|---|---|---|
| Development Case | Process Engineer | DC baseline conformance; optional-trigger justification; validity of every referenced path | Survey, Draft, iteration 1 |
| System Inventory | Software Archaeologist | Anchor verification (each anchor opened and read against its claim); UML/notation correctness of the perimeter and coverage diagrams; internal consistency; Coverage arithmetic | Survey, Draft, iteration 1 |
| Risk List | Project Manager | The declared magnitude scale used and not replaced; every anomaly scored; acceptance verbatim for High; owning roles at work in the phase each action names | Survey, Draft, iteration 1 |
| Iteration Plan | Project Manager | Exit criteria against evidence; no forecast before a measured actual; resource roster; the plan not exercising a verdict it disclaims | Survey, Draft, iteration 1 |

#### What was opened, not merely read

An anchor that does not say what the artifact claims is the defect every later role inherits, so each high-consequence row was checked against its file:

| Anchor opened | Claim it carries | Verdict |
|---|---|---|
| `Todo.Web/Server/Authentication/AuthenticationExtensions.cs` | Four provider schemes registered only when `Authentication:Schemes:<provider>` exists | Confirmed — the exclusion of external provider sign-in rests on code |
| `Todo.Api/Program.cs` | Scalar mapped only in Development, `MapOpenApi()` unguarded, root redirects to `/scalar/v1` | Confirmed — AN-016 accurate |
| `Todo.Web/Server/TodoApi.cs` | Forwarder targets the literal `http://todoapi`; bearer re-signed from the stored token | Confirmed — AN-012 and the BFF description accurate |
| `Todo.Web/Client/TodoClient.cs` | No update method; five calls only | Confirmed — AN-008 accurate |
| `Todo.Web/Client/Components/TodoList.razor` | Checkbox carries no `@bind` and no handler | Confirmed — AN-008 accurate |
| `Todo.Api/Todos/TodoApi.cs` | `owner.IsAdmin` widens read, update and delete | Confirmed — AN-010 accurate |
| `Todo.Api/Users/UsersApi.cs` | `/users` group carries no authorization; provider key unprotected before identity | Confirmed — AN-018 accurate |
| `.github/workflows/ci.yaml` | `actions/setup-dotnet@v3` with no `dotnet-version` | Confirmed — AN-006 accurate |
| `.devcontainer/devcontainer.json` | Base image `sdk:8.0` against a `net9.0` target | Confirmed — AN-005 accurate |
| `Todo.Web/Server/AuthApi.cs` | Register, login and logout call the API; provider challenge and callback present | Confirmed — but see below on refresh |
| `Todo.Api/TodoDbContext.cs`, `Todo.Api/Users/TodoUser.cs` | `IdentityDbContext<TodoUser>` plus `Todos` = 8 entities | Confirmed — the Data Model trigger genuinely does not hold |
| `TodoApp.AppHost/Program.cs` | Two project services plus a container, gated on a migration | Confirmed — the Deployment Model trigger genuinely holds |
| `CONTRIBUTING.md` | Named by the Development Case as the home of three convention families | **Not found** — Development Case#F1 |

One claim did not survive: the Inventory's Perimeter says the delivered product uses token refresh, and nothing in the delivery redeems a refresh token. That is System Inventory#F2.

The UML content was checked as notation, not as illustration: the perimeter diagram types its components and systems and labels each dependency with its mechanism; the coverage diagram separates read from declared-unread and gives each unread set a reason; the Risk List's classification diagram states the scale, the band arithmetic and the acceptance rule. None is a prose summary drawn as arrows. The Inventory's History diagram is the one place a diagram asserts a count that the accompanying table repeats rather than derives — noted, not recorded as a defect, because the per-area commit lists are given in full.

No SCM evidence bears on this milestone. `scm_list_pull_requests` returns nothing in any state, so there is no scaffolding to approve, no code to request changes on, and nothing to defer out of phase; `scm_get_build_status("main")` reports no IARI pipeline yet, which is correct for a phase that builds nothing. The Implementation and Test disciplines have no Survey stage.

## Findings


## Resolutions and Actions


## Disposition

