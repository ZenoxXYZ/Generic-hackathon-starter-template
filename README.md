# Generic Hackathon Starter

A reusable, backend-first foundation for building small, demonstrable projects with AI coding agents while keeping requirements, design decisions, implementation evidence, and review history clear.

Bring an authoritative problem statement. This template supplies repeatable engineering infrastructure; it does not decide the product.

> This is a starting point, not a solution generator.

## What It Is

This repository is a problem-agnostic engineering foundation for hackathons, take-home challenges, rapid prototypes, and other time-constrained exercises. It keeps durable project state in the repository so people and fresh AI sessions can reconstruct what is required, what was designed, what was implemented, and what was verified.

## Why It Exists

Fast projects often lose context between people, chats, and implementation checkpoints. That can produce invented requirements, unverified code, unnecessary infrastructure, and mismatched frontend and backend behavior.

This template provides a repeatable engineering workflow: understand the problem, approve a small design, implement bounded slices, verify them with evidence, review meaningful checkpoints independently, reconstruct enough understanding for humans to supervise and explain the system, deploy when a remote demo is needed, and stabilize the demo-critical path.

## Why Start From a Backend Template?

The starter separates two concerns that should not be conflated.

**Repeatable engineering infrastructure** is setup that is useful across many projects: Python application structure, FastAPI startup, environment configuration, SQLAlchemy foundations, Alembic migration wiring, automated-test foundations, a health endpoint, backend-layer organization, a frontend workspace placeholder, and AI engineering workflows.

**Problem-specific product design** must be derived from the actual brief: domain entities, database schema, business rules, APIs, decision algorithms, product validation, frontend framework, and deployment architecture.

Without a reusable foundation, limited project time is repeatedly spent recreating framework structure, configuration, database wiring, migration setup, and test scaffolding before product work can begin. With this starter, work can move earlier into:

```text
requirements -> design -> domain modeling -> implementation -> integration -> verification
```

This is a deliberate starting point, not a claim that the supplied architecture is optimal for every project.

## Why FastAPI?

**[TEMPLATE DESIGN DECISION]** FastAPI is the default backend framework because Python supports rapid prototyping; FastAPI has relatively low ceremony; Pydantic provides typed request and response contracts; it generates OpenAPI schemas and interactive API documentation; and it works directly with SQLAlchemy, Alembic, Uvicorn, and common Python testing tools. It is also practical when data-processing, optimization, or AI-related logic is written in Python.

FastAPI is **not** a [PROBLEM REQUIREMENT]. A future problem statement may justify another architecture or technology. The template chooses a consistent default for speed and clarity, not universal superiority.

## Engineering Model

The repository uses four state files with distinct purposes:

| File | Engineering role |
| ---- | ---------------- |
| `problem.md` | Normalized requirements model: the approved interpretation of the authoritative brief. |
| `plan.md` | Approved solution architecture and design decisions. |
| `execute.md` | Execution and checkpoint tracker. |
| `review.md` | Concise verified engineering and bug history. |

Requirements and design authority flow from:

```text
authoritative problem statement -> approved problem.md -> approved plan.md
```

Implemented-state truth comes from:

```text
code + tests + migrations + Git evidence + safe runtime verification
```

State files summarize the repository; they do not override contradictory implementation evidence. See [Workflow concepts](docs/guides/WORKFLOW.md) for the detailed model.

## Builder and Reviewer Roles

| Builder | Reviewer |
| ------- | -------- |
| Plans and implements an approved workstream. | Independently reconstructs a checkpoint and audits its evidence. |
| Fixes implementation-time bugs and runs verification. | Searches for defects, regressions, contradictions, missing verification, and requirement drift. |
| Records verified implementation evidence. | Starts read-only and classifies findings before any human-approved correction. |

Separating these roles reduces the risk that an implementation agent merely confirms its own assumptions. Independent review improves scrutiny; it does not guarantee correctness. Humans approve material transitions, design changes, and Git history changes.

## Workstreams

An engineering workstream is a bounded implementation slice with a defined objective, scope, explicit deferrals, affected layers, failure behavior, verification strategy, and completion evidence. A workstream might be a core capability, a persistence slice, a frontend slice, an integration checkpoint, or a targeted correction—depending entirely on the approved problem and plan.

Bounded workstreams reduce context size and make implementation, debugging, documentation, review, and rollback easier to reason about.

```text
Plan -> Human Approval -> Implement -> Debug -> Verify -> Document -> Review -> Understand
```

## Complete Workflow

```text
Authoritative Problem Statement
        |
        v
Problem Statement Intake / Source Analysis
        |
        v
problem.md -> plan.md -> execute.md
        |         |
        |         v
        |   Approved design and workstreams
        v
Builder workstream -> verification -> docs/phases/
        |
        v
Human checkpoint -> independent review -> understand workstream
        |
        v
Next workstream -> frontend / full-stack integration when applicable
        |
        v
Deployment when remote demo is intended
        |
        v
Deployed verification -> final review
        |
        v
Whole-project understanding -> Demo Freeze
```

## Repository Structure

```text
backend/          FastAPI application foundation
frontend/         Placeholder for a future, problem-driven interface
migrations/       Alembic database-schema migration foundation
tests/            Automated verification
docs/guides/      Usage guides and reusable AI prompts
docs/phases/      Builder workstream records
docs/reviews/     Independent review records (created when reviews run)

problem.md        Approved problem interpretation
plan.md           Approved design and roadmap
execute.md        Current engineering checkpoint
review.md         Verified review and bug summary
```

## Technology Foundation

The generic defaults are Python, FastAPI, Pydantic, SQLAlchemy, PostgreSQL-ready configuration, Alembic, Uvicorn, and isolated automated tests. These are template design defaults, not requirements for every future problem.

The current app intentionally exposes only `GET /`, which returns `{"status":"ok"}`. It does not create tables, run migrations at startup, or require a real database connection for the health response.

## Full-Stack Positioning

This is currently a **backend-first, full-stack-capable** starter. Frontend technology is intentionally unspecified because UI choices depend more strongly on real interaction requirements and available constraints than the generic backend foundation does.

When a frontend is in scope, the contract boundary is:

```text
Frontend -> HTTP request -> FastAPI route -> Pydantic validation
-> service / business logic -> SQLAlchemy / persistence
-> response schema -> frontend state and rendering
```

Frontend, local integration, deployment, and deployed end-to-end verification can become separate workstreams. The frontend should use approved backend contracts rather than duplicate backend business or decision logic. See the [full-stack guide](docs/guides/FULL_STACK_GUIDE.md).

## Quick Start

1. Use the repository as a GitHub template, or clone/copy it deliberately.
2. Create and activate a virtual environment.
3. Install dependencies and verify the starter.
4. Provide the authoritative problem statement.
5. Run Problem Statement Intake, then Problem Definition; review and approve `problem.md`.
6. Run Master System Design; review and approve `plan.md`.
7. Initialize execution state.
8. Plan, approve, implement, and verify Builder workstreams.
9. Use independent reviews for meaningful checkpoints.
10. Reconstruct meaningful workstreams so humans understand what was built and verified.
11. Build frontend and local integration work only when the approved problem requires it.
12. Add deployment and deployed end-to-end verification when a remote demo is intended.
13. Run final review, whole-project engineering reconstruction, and Demo Freeze.

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m pytest
uvicorn backend.main:app --reload
```

Confirm [http://127.0.0.1:8000/](http://127.0.0.1:8000/) returns `{"status":"ok"}`. Set `DATABASE_URL` in the process environment only when approved persistence or Alembic work needs it; never commit credentials.

For step-by-step onboarding, read [Quickstart](docs/guides/QUICKSTART.md). For copy/paste lifecycle handoffs, open the [Prompt Playbook](docs/guides/PROMPT_PLAYBOOK.md).

## Hackathon Engineering Priority

```text
working MVP -> correctness -> integration -> verification -> demo readiness -> documentation depth
```

This is an engineering prioritization rule under time pressure. It does not mean skipping validation, ignoring bugs, omitting critical tests, or accepting broken integration. It means not spending scarce time on speculative infrastructure or documentation polish while the critical product path is incomplete.

## What This Template Does Not Predetermine

- Domain entities, database schema, or domain APIs
- Business rules, decision algorithms, or product-specific validation
- A frontend framework or real interface
- Deployment architecture or distributed infrastructure
- ML systems, optimization infrastructure, caches, queues, or background workers

Those choices must come from the authoritative problem statement and approved design.

## Documentation

- [Quickstart](docs/guides/QUICKSTART.md)
- [Workflow concepts](docs/guides/WORKFLOW.md)
- [Prompt Playbook](docs/guides/PROMPT_PLAYBOOK.md)
- [Full-stack guide](docs/guides/FULL_STACK_GUIDE.md)
- [Builder workflow](docs/AGENT_WORKFLOW.md)
- [Reviewer workflow](docs/REPO_REVIEW_WORKFLOW.md)

Reusable methodology lives in `AGENTS.md`, `docs/AGENT_WORKFLOW.md`, `docs/REPO_REVIEW_WORKFLOW.md`, and `docs/guides/`. Project-specific state lives in `problem.md`, `plan.md`, `execute.md`, `review.md`, phase/review records, and the implementation that an approved problem justifies.

## Git Workflow

Agents do not commit or push automatically. Humans review verified work, approve checkpoints, and control history changes.

## License

No license is included yet. Choose one deliberately before publishing the repository.
