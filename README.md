# HADF Generic Hackathon Starter

HADF (the **Hackathon Agentic Development Framework**) is a reusable FastAPI starter and human-AI engineering workflow for turning an unknown hackathon challenge into a scoped, integrated, tested, explainable MVP.

It gives a team a safe starting point before the challenge is known: technical scaffolding, shared project-truth files, and an operating model that keeps humans accountable for important decisions. Humans interpret requirements and approve material decisions; agents perform bounded planning, implementation, testing, debugging, review, and evidence work.

The repository remains challenge-neutral until the official challenge is understood and its requirements and design are approved. It is not a product or a preselected domain; it is the controlled engineering system used to build one.

## This repository contains two things

### Included software foundation

A challenge-neutral FastAPI, testing, database, migration, and CI starting point.

### Engineering operating system

A structured way for humans and AI agents to understand, design, implement, integrate, verify, and explain the resulting project.

## What problem does this solve?

| Common Hackathon Problem | HADF Response |
| --- | --- |
| Team starts coding before understanding the challenge | `problem.md` + challenge intake |
| Everyone imagines a different architecture | Shared `plan.md` |
| Scope becomes too large | MVP boundary |
| Team builds the wrong things first | Golden Path |
| AI agents make unrelated changes | Bounded tasks + `AGENTS.md` |
| Frontend and backend drift | Approved API contracts |
| Multiple agents overwrite each other | Branches + conditional worktrees |
| “Agent says done” but code is unverified | Tests + evidence + review |
| PR merges but teammates still have old code | Post-merge synchronization |
| Features work separately but not together | Rendezvous + QA + E2E |
| Integration happens too late | Incremental vertical-slice integration |
| Nobody understands the final system | Reconstruction + README reconciliation |

## Why does HADF exist?

Hackathons move quickly, so teams can begin coding before they share an interpretation of the challenge. That leads to oversized scope, competing architectures, AI-generated assumptions, incompatible frontend/backend work, late integration, and a demo made from isolated features.

HADF is the response: it turns challenge understanding into an approved MVP, a Golden Path, one shared design, bounded workstreams, explicit contracts, verified integration, and an explainable final system.

## Why is this repository generic?

Real hackathons often begin with an unknown challenge. A starter that pre-builds product entities, domain APIs, database tables, authentication assumptions, workflows, or frontend behavior may solve the wrong problem before the event begins.

This starter therefore provides application bootstrap, configuration, tests, database/migration wiring, CI, Git/PR workflow, agent rules, project-truth files, workstream guidance, QA/integration process, prompts, and runbooks. The actual challenge determines the domain, actors, entities, business rules, API contracts, schema, frontend UX, security, external services, and deployment needs.

```text
GENERIC STARTER
→ reusable engineering foundation

ACTUAL CHALLENGE
→ product requirements

APPROVED DESIGN
→ challenge-specific architecture

IMPLEMENTATION
→ real application
```

**The reusable part is the engineering system. The product is still designed from the actual challenge.**

## Why start from this template?

The goal is not to pre-solve a hackathon. It is to avoid repeatedly rebuilding generic infrastructure under time pressure: application bootstrap, tests, Alembic, CI, project-truth files, Git controls, and agent boundaries.

That gives teams faster startup, less architecture drift, safer AI assistance, earlier integration, and a reusable process without assuming a domain.

## What this repository gives you

### Software foundation

- ✓ FastAPI, Pydantic, SQLAlchemy, and Alembic
- ✓ SQLite development fallback and PostgreSQL-ready configuration
- ✓ pytest + httpx test foundation
- ✓ GitHub Actions CI and a pull-request template
- ✓ Frontend placeholder until the challenge selects a stack

### Engineering system

- ✓ `AGENTS.md`, `problem.md`, `plan.md`, `execute.md`, and `review.md`
- ✓ MVP, Golden Path, workstream, and contract guidance
- ✓ Solo, 2-, 3-, and 4-member operating modes
- ✓ Git branch, worktree, PR, merge, and post-merge guidance
- ✓ QA, E2E, and deployment-readiness runbooks
- ✓ Reusable role and lifecycle prompts
- ✓ Challenge-neutral architecture

## HADF in one diagram

```text
Challenge
   ↓
problem.md
   ↓
MVP + Golden Path
   ↓
plan.md
   ↓
Workstreams + Contracts
   ↓
Branch / Worktree
   ↓
Builder Plan
   ↓
Human Approval
   ↓
Implementation
   ↓
Tests + Evidence
   ↓
PR + CI
   ↓
Merge + Sync
   ↓
Integration + QA + E2E
   ↓
Verified MVP
```

The Golden Path is the most important successful user journey that proves the MVP’s value. Work from approved requirements and design, then integrate and verify each relevant capability before calling the MVP complete. This sequence converts shared understanding into bounded work, then bounded work into a verified system rather than a collection of isolated features.

## Who this is for

This repository is useful for:

- solo hackathon developers;
- small hackathon teams;
- students learning backend and project workflow;
- developers using coding agents;
- teams that want AI assistance without losing architecture and control; and
- engineers who want a reusable project-control template.

## Tech stack at a glance

| Area | Current Starter |
| --- | --- |
| Backend | FastAPI |
| Validation | Pydantic |
| ORM | SQLAlchemy |
| Database | SQLite fallback / local PostgreSQL development path |
| Migrations | Alembic |
| Testing | pytest + httpx |
| CI | GitHub Actions |
| Version control | Git |
| Collaboration | GitHub Pull Requests |
| Agent governance | `AGENTS.md` |
| Frontend | Intentionally unselected placeholder |

## Current technical foundation

| Layer | Current implementation |
| --- | --- |
| Application entry | `backend/main.py` |
| API framework | FastAPI with `GET /` health endpoint |
| Configuration | Environment-driven `DATABASE_URL` with a safe fallback |
| Database access | SQLAlchemy engine, session factory, base, and dependency helper |
| Migration system | Alembic environment with an infrastructure-only baseline |
| Default development DB | In-memory SQLite fallback |
| PostgreSQL development | Optional host-run PostgreSQL through Compose and `DATABASE_URL` |
| Testing | pytest + httpx application/configuration/database-connectivity tests |
| CI | Python 3.12 runs PostgreSQL readiness, migration upgrade, then tests |
| Frontend | Placeholder only; no framework or UI selected |

The starter intentionally contains no product-specific routers, services, entities, domain tables, authentication, business rules, or real frontend behavior. Those are introduced only after the challenge is understood and the design is approved.

## Architecture at a glance

```text
Browser / Client
 ↓
Frontend Event Handler
 ↓
API Client
 ↓
HTTP / JSON
 ↓
FastAPI Router
 ↓
Pydantic Validation
 ↓
Service / Use Case
 ↓
Business Rules / Invariants
 ↓
SQLAlchemy Session
 ↓
Database Transaction
 ↓
Response Schema
 ↓
JSON Response
 ↓
Frontend State
 ↓
Rendered UI
```

The generic starter currently provides only the foundation. Challenge-specific routers, schemas, services, invariants, models, and frontend behavior are introduced after `problem.md` and `plan.md` are approved.

An **invariant** is a rule that must always remain true. A **transaction** is a group of database changes that succeeds or fails together.

A **route** receives an HTTP request, a **schema** validates/serializes the request or response shape, a **service** coordinates an application operation, and an **ORM** maps application objects to database operations.

## Quick start

Create a repository from this template when official rules allow reusable starter code, then clone it.

1. Use Python 3.12, then create and activate a virtual environment. It isolates this project’s Python packages.

   **Windows PowerShell**

   ```powershell
   python -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```

   **macOS/Linux**

   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

2. Install the declared project dependencies.

   ```powershell
   python -m pip install -r requirements.txt
   ```

3. Run the automated foundation tests. Without `DATABASE_URL`, the database-connectivity check uses the in-memory SQLite fallback.

   ```powershell
   python -m pytest
   ```

4. Start the local FastAPI development server.

   ```powershell
   uvicorn backend.main:app --reload
   ```

5. Open [http://127.0.0.1:8000/](http://127.0.0.1:8000/). The health endpoint should return `{"status":"ok"}`.

### Optional local PostgreSQL foundation

The application and tests run on the host. Docker Compose runs only PostgreSQL.

1. Copy [.env.example](.env.example) to `.env`. `POSTGRES_PORT` defaults to `5432` and is overridable; when it changes, update the port in `DATABASE_URL` to match.
2. Start PostgreSQL and wait until its health status is healthy.

   ```powershell
   docker compose up -d
   docker compose ps
   ```

3. Set the same URL in the host shell before running Alembic, pytest, or FastAPI.

   ```powershell
   $env:DATABASE_URL = "postgresql+psycopg://hadf:hadf_local_password@127.0.0.1:5432/hadf_dev"
   python -m alembic upgrade head
   python -m pytest
   uvicorn backend.main:app --reload
   ```

The initial Alembic revision is infrastructure-only: it creates no product tables and is immutable after merge. It proves migration execution on a fresh database, not real-model autogeneration. Future challenge-specific models must be registered in `backend.models` and added through new revisions. `DATABASE_URL` remains optional for the health-only SQLite fallback. Never run migrations against a real database without explicit approval.

When several clones or worktrees share one Docker host, optionally set a distinct `COMPOSE_PROJECT_NAME`, `POSTGRES_DB`, and `POSTGRES_PORT` in each local `.env`. Separate developers on separate machines can use the identical defaults.

## What do I do after cloning?

### First 30 minutes

1. [Confirm official challenge and event rules](docs/runbooks/CHALLENGE_INTAKE.md).
2. [Verify the starter locally](#quick-start).
3. [Read the repository operating rules](AGENTS.md).
4. [Write the approved problem interpretation](problem.md).
5. [Define the MVP and Golden Path](docs/core/GOLDEN_PATH.md).
6. [Approve the Master System Design](plan.md).
7. [Initialize execution state](execute.md).
8. [Split work into capability-oriented workstreams](docs/core/WORKSTREAMS.md).
9. [Assign owners and dependencies](docs/runbooks/WORKSTREAM_START.md).
10. [Start the first bounded branch](docs/git/BRANCH_WORKFLOW.md).

Use [Challenge Intake](docs/runbooks/CHALLENGE_INTAKE.md), [Master Design](docs/runbooks/MASTER_DESIGN.md), and [time-compressed guidance](docs/runbooks/TIME_COMPRESSION.md) when the event clock is tight.

## Repository map

```text
backend/        FastAPI application foundation and future backend layers
frontend/       Placeholder for a frontend selected by the actual challenge
tests/          Isolated automated checks for the starter
migrations/     Alembic migration environment for approved schema changes
.github/        CI workflow and pull-request template
docs/core/      HADF concepts, truth model, contracts, and completion gates
docs/git/       Branch, worktree, PR, conflict, and post-merge guidance
docs/modes/     Solo and team responsibility allocations
docs/runbooks/  Practical execution, QA, E2E, and release checklists
docs/prompts/   Reusable role and lifecycle prompts

AGENTS.md       Stable rules for humans and agents in this repository
problem.md      What must be built after the challenge is understood
plan.md         How the approved system is designed
execute.md      What work is active, blocked, or verified
review.md       What has been independently verified or found wrong
```

## Project truth model

| Artifact | Plain-English purpose |
| --- | --- |
| `AGENTS.md` | How agents should behave |
| `problem.md` | What must be built |
| `plan.md` | How the team decided to build it |
| `execute.md` | What is being worked on right now |
| `review.md` | What has been verified or found wrong |
| Code, tests, and Git | What actually exists |

```text
DESIGN → IMPLEMENTATION → SHARED SOURCE → RUNTIME
```

Read the [Project Truth Model](docs/core/PROJECT_TRUTH_MODEL.md) for authority, evidence, and the difference between these states.

## Beginner-friendly Git model

| Term | Meaning |
| --- | --- |
| Branch | A separate line of Git history for one bounded change |
| Worktree | A separate physical project folder checked out on another branch |
| PR | A proposal to merge a branch into `main` |
| CI | Automated checks run for configured changes |

```text
One human + one active task
→ normal branch

One human + multiple concurrent coding agents
→ separate branches + separate worktrees

Different humans
→ normally separate clones
```

Worktrees are conditional, not a team-size ritual. See the [worktree workflow](docs/git/WORKTREE_WORKFLOW.md).

## Three levels of done

```text
LOCAL COMPLETE
→ code works locally and focused verification passed

MERGE READY
→ PR, CI, and required review passed

WORKSTREAM COMPLETE
→ merged, synchronized, integrated, and QA-verified
```

Generated code is not completed work. Read the [Definition of Done](docs/core/DEFINITION_OF_DONE.md) for the exact evidence required at each gate.

## CI vs review vs QA vs E2E

| Check | Question it answers |
| --- | --- |
| CI | What configured automated checks passed? |
| PR review | Is the change safe, scoped, and architecturally correct? |
| QA | Does behavior satisfy requirements and important edge cases? |
| E2E | Does the real assembled user journey work? |

None replaces the others.

## Worked example

This is illustrative only; it is not a built-in product requirement.

```text
Requirement
→ a resource must be creatable

plan.md
→ defines POST /resources

execute.md
→ WS-02 Resource Creation

Backend
→ implements the approved endpoint

Frontend
→ builds a form against the approved contract

Backend PR merges
→ frontend synchronizes latest main

Mock removed
→ browser calls the real API

QA verifies persistence
→ workstream closes
```

## Choose your path

### I want to...

| Goal | Start here |
| --- | --- |
| Understand HADF | [HADF Overview](docs/core/HADF_OVERVIEW.md) |
| Start a challenge | [Challenge Intake](docs/runbooks/CHALLENGE_INTAKE.md) |
| Plan the system | [Master Design](docs/runbooks/MASTER_DESIGN.md) |
| Use an AI Builder | [Builder prompt](docs/prompts/BUILDER.md) |
| Run multiple agents | [Worktree workflow](docs/git/WORKTREE_WORKFLOW.md) |
| Open or review a PR | [Pull-request workflow](docs/git/PULL_REQUEST_WORKFLOW.md) |
| Integrate frontend and backend | [Rendezvous runbook](docs/runbooks/RENDEZVOUS.md) |
| Debug a failure | [Debugger prompt](docs/prompts/DEBUGGER.md) |
| Run QA | [QA verification](docs/runbooks/QA_VERIFICATION.md) |
| Prepare deployment | [Deployment readiness](docs/runbooks/DEPLOYMENT_READINESS.md) |

## Team modes

| Mode | Concise allocation | Detailed guide |
| --- | --- | --- |
| Solo | Human owns architecture, integration, and release; agents provide bounded support | [Solo](docs/modes/SOLO.md) |
| 2-member | A leads architecture/backend/integration; B leads frontend/UX/QA/E2E | [Team of 2](docs/modes/TEAM_2.md) |
| 3-member | A leads architecture/integration; B owns backend/data; C owns frontend/QA | [Team of 3](docs/modes/TEAM_3.md) |
| 4-member | A integrates; B owns backend/data; C owns frontend; D owns QA/reliability | [Team of 4](docs/modes/TEAM_4.md) |

## How the agentic workflow works

HADF separates authority from execution. Humans interpret official rules and the challenge, approve requirements, define the MVP and Golden Path, approve architecture, approve material API/schema/invariant/security changes, and decide when work may merge or release.

AI agents inspect repository state, propose bounded plans, implement approved workstreams, test, debug, review, generate evidence, and support documentation or reconstruction. They do not silently redefine the product or shared architecture.

### Humans own

- official challenge interpretation and requirements approval;
- MVP, Golden Path, architecture, contracts, and major schema decisions;
- security, merge, and release decisions.

### Agents may perform

- repository inspection, bounded planning, implementation, testing, debugging, review, evidence generation, documentation, and reconstruction assistance.

```text
Official Challenge
      ↓
Human + Control Room
      ↓
problem.md
      ↓
MVP + Golden Path
      ↓
Master System Design
      ↓
plan.md
      ↓
Workstreams
      ↓
Bounded AI Builders
      ↓
Tests + Evidence
      ↓
Human / Reviewer Gate
      ↓
PR + CI
      ↓
Merge
      ↓
Sync + Integration
      ↓
QA + E2E
      ↓
Verified MVP
```

**Parallelize implementation, not architecture.** Different people and agents may implement simultaneously, but they work against one approved architecture and shared contracts. Read [Decision Authority](docs/core/DECISION_AUTHORITY.md) and [AGENTS.md](AGENTS.md) before assigning implementation work.

```text
Human defines and approves
↓
Agent plans
↓
Human approves the plan
↓
Agent implements and self-verifies
↓
Human / Reviewer verifies
↓
Accepted result
```

## Why agent tasks are bounded

Coding agents are more reliable when they receive a clear objective, approved contract, exact scope, relevant files, exit criteria, test expectations, and stop/escalation conditions.

```text
Bad:    "Build the backend."

Better: "Implement WS-03 Resource Creation using the approved POST /resources
         contract. Do not change shared schema or unrelated endpoints. Run
         focused tests and stop if the approved contract must change."
```

Bounded tasks reduce architecture drift, unrelated edits, hidden assumptions, integration conflicts, and accidental scope growth.

## 1. MVP — What actually needs to exist?

MVP means **Minimum Viable Product**: the smallest integrated version of the system that proves the solution works.

An MVP is not every feature, production completeness, maximum polish, or every optional edge case. It is enough functionality to prove core value, enough integration to demonstrate the main workflow, and enough correctness to support the critical demo journey. HADF defines it early to protect the event from uncontrolled scope growth.

Once the team knows what must exist, it can decide what must work first.

## 2. Golden Path — What must work end to end?

The Golden Path is the most important end-to-end user journey that demonstrates the MVP’s value.

```text
User enters system
→ submits important input
→ backend validates and processes it
→ database state changes
→ response returns
→ frontend displays the result
```

```text
MVP         = what must exist
Golden Path = the critical journey through it
Workstreams = bounded capabilities needed to build it
```

If the Golden Path does not work end-to-end, the project is not demo-ready even if many isolated features exist.

## 3. Workstreams — How the system is divided

A workstream is a bounded capability, not simply a technical folder.

```text
Less useful: frontend / backend / database

Better:      user entry / resource creation / recommendation / allocation / dashboard
```

A vertical slice may cross frontend → API → service → database → response → UI. It crosses only the layers needed to deliver one useful capability.

**Backend-first does not mean backend-complete-first.** Backend foundations may start earlier, while frontend work can begin as soon as shared contracts are design-stable.

## 4. Contracts — How parallel work stays compatible

An API contract is an agreed method, path, request, response, status behavior, and important error behavior. This example is illustrative only; it does not add an endpoint or domain requirement to the starter.

```text
POST /resources

Request
{
  "name": "Example"
}

Success: 201 Created
{
  "id": "generated-id",
  "name": "Example"
}

Validation failure: 422
```

A design-stable contract lets frontend and backend work independently without inventing incompatible fields or behavior. When the real backend dependency is available, temporary mocks are removed and the team performs a real integration rendezvous.

## What process model does HADF use?

**HADF is a human-governed hybrid iterative-incremental software process with Golden-Path-driven scope control, capability-oriented vertical-slice delivery, shared-contract-based parallel implementation, human-gated important decisions, risk-driven review, evidence-based verification, and incremental integration.**

| Process idea | Plain-English meaning |
| --- | --- |
| Human-governed | Humans retain important authority. |
| Hybrid | Structured planning is followed by iterative implementation. |
| Iterative | Work is reviewed, tested, and corrected. |
| Incremental | The product grows capability by capability. |
| Golden-Path-driven | The core user journey drives priority. |
| Capability-oriented | Work is divided by behavior, not only folders. |
| Vertical-slice delivery | A capability may cross UI, API, service, and database layers. |
| Shared-contract parallelism | Teams and agents build safely against agreed interfaces. |
| Human-gated decisions | Material architecture, API, schema, and security changes require approval. |
| Risk-driven review | Riskier work receives deeper scrutiny. |
| Evidence-based verification | “Done” requires proof, not a claim. |
| Incremental integration | Pieces are combined continuously rather than only at the end. |

HADF is not pure Waterfall, uncontrolled Agile, Scrum by another name, or “let several coding agents loose and hope integration works.” It borrows useful ideas from iterative development, incremental delivery, Agile feedback, vertical slicing, continuous integration, and human-in-the-loop agentic workflows.

## Full HADF hackathon process

```text
Official Rules + Challenge
↓
Challenge Intake → problem.md → MVP → Golden Path
↓
Master System Design → plan.md → workstreams + dependencies
↓
Design-stable contracts → branches/worktrees → Builder planning → human approval
↓
Parallel implementation → local verification → commit + push → PR → CI + review
↓
Merge → post-merge synchronization → frontend/backend rendezvous → integrated QA
↓
Regression → Golden-Path E2E → Feature Freeze → P0/P1 corrections
↓
Deployment decision → final independent review → README reconciliation
↓
Project reconstruction → demo rehearsal → Demo Freeze → submission
```

Each stage creates the evidence needed for the next. A merge changes shared source; it does not by itself prove that dependent components now work together.

## How this template becomes a real project

The generic starter begins with `backend/`, `frontend/`, `tests/`, `migrations/`, `problem.md`, `plan.md`, and `execute.md`. After a challenge arrives, the team derives the actual actors, entities, MVP, Golden Path, contracts, and workstreams from that challenge, then implements the approved system in those locations.

For example, a hypothetical resource-allocation challenge might lead to Request, Resource, and Allocation entities; request creation, recommendation, allocation, and dashboard workstreams; and one integrated allocation journey. This is illustrative only. The template contains none of these domain assumptions.

## Example: from requirement to verified capability

```text
Challenge requirement
↓
problem.md → MVP relevance → Golden Path relevance → plan.md
↓
POST /resources contract → WS-02 → feature branch → Builder plan → human approval
↓
backend implementation + frontend contract-based implementation → local tests
↓
PR + CI + review → merge → frontend sync → remove mock
↓
real browser/API/database flow → QA → WORKSTREAM COMPLETE
```

This is how a requirement becomes a verified capability rather than merely generated code.

## README evolves with the project

```text
Challenge Intake
→ problem, users, and MVP
→ Master Design
→ architecture and stack
→ Implementation
→ real setup, environment, and features
→ Integration
→ actual full-stack behavior
→ Feature Freeze
→ supported features and limitations
→ Final Review
→ reconcile README with runtime evidence
→ Demo Freeze
→ lock setup and demo instructions
```

**README describes the system that actually exists, not the system the team originally intended to build.** See the [README lifecycle runbook](docs/runbooks/README_LIFECYCLE.md).

## How to read this repository as an engineer or recruiter

This is not primarily a feature-rich product demo. It is a reusable engineering-system project.

| Area | What to inspect |
| --- | --- |
| Backend engineering | FastAPI structure, configuration, SQLAlchemy, Alembic, testing, and CI |
| Architecture thinking | Requirements/design separation, contracts, capability decomposition, vertical slices, invariants, and Definition of Done |
| Git and collaboration | Branch isolation, conditional worktrees, PRs, CI, post-merge synchronization, and integration ownership |
| Agentic engineering | Bounded responsibilities, human decision gates, plan-before-implementation, repository-held context, evidence, and review |
| Delivery engineering | MVP scope control, Golden Path priority, incremental integration, QA, E2E, freezes, reconstruction, and README reconciliation |

The repository demonstrates the ability to design not only software, but also the process by which humans and AI reliably build software together.

## What this repository demonstrates

### Software engineering

- FastAPI, Pydantic, SQLAlchemy, Alembic, testing, CI, and a deliberate architecture direction.

### Agentic engineering

- Human/AI authority, bounded agents, project truth, Git isolation, contract-driven parallelism, review, evidence, and incremental integration.

## What this repository is not

It is not a finished SaaS product, a domain-specific backend, a set of prebuilt hackathon answers, a huge enterprise framework, an autonomous AI system that makes product decisions, or a replacement for understanding software engineering.

It is a generic software foundation, a human-AI engineering operating system, an agentic workflow template, and a reusable hackathon starting environment.

## Detailed documentation

- [Core HADF guides](docs/core/HADF_OVERVIEW.md)
- [Git operating guides](docs/git/GIT_MENTAL_MODEL.md)
- [Operational runbooks](docs/runbooks/CHALLENGE_INTAKE.md)
- [Role prompts](docs/prompts/CONTROL_ROOM.md)
- [Lifecycle prompts](docs/prompts/lifecycle/CHALLENGE_INTAKE.md)
- [Full-stack flow](docs/core/FULL_STACK_FLOW.md)
- [Builder procedure](docs/AGENT_WORKFLOW.md)
- [Reviewer procedure](docs/REPO_REVIEW_WORKFLOW.md)

## Intentional limitations

This starter stays generic until an authoritative challenge and approved design justify product work. It does not choose a domain, frontend stack, deployment provider, external services, or persistence model. Official event rules and organizer clarifications always override HADF guidance.
