# Generic Hackathon Starter

A reusable full-stack starter and engineering workflow for turning an unknown hackathon challenge into a working, explainable MVP.

This repository gives you a small backend foundation, database/migration wiring, tests, documentation templates, and a practical workflow for building capability by capability. It does not decide your product, your domain, your frontend framework, or your deployment provider.

Official event rules and the actual challenge brief always come first.

## Why This Repository Exists

Hackathons move fast. Teams can lose precious hours to setup, unclear scope, late frontend/backend integration, unverified code, and forgotten decisions.

This starter helps you begin with:

- a runnable backend foundation;
- a place to record requirements, design, execution state, and review history;
- a workflow for building the smallest useful MVP;
- a habit of verifying real behavior before calling work complete.

The goal is not to create the most code. The goal is to build the smallest correct, explainable, demonstrable solution that matches the challenge.

## Who It Is For

This repository is useful for:

- hackathon participants;
- students and learning teams;
- solo builders;
- small teams;
- beginner-to-intermediate full-stack developers;
- people working with or without AI coding agents.

You can use the workflow manually, with human teammates, with agents, or with a mix of both.

## What Is Included

| Area | What exists now |
| ---- | --------------- |
| Backend | Minimal FastAPI app with `GET /` health endpoint. |
| Configuration | Environment-based database URL helper with safe local default. |
| Persistence | SQLAlchemy engine/session/base wiring. |
| Migrations | Alembic configuration and migration environment. |
| Tests | Pytest coverage for app health, imports, OpenAPI, config, and Alembic wiring. |
| Frontend | Placeholder directory only; no framework or real UI has been selected. |
| Workflow docs | Builder, reviewer, full-stack, quickstart, and prompt guidance. |
| State files | Templates for requirements, design, execution tracking, and review history. |

The starter intentionally does not include product entities, product APIs, business rules, domain tables, decision logic, or real frontend functionality.

## Core Philosophy

Use the starter like this:

1. Understand the challenge before coding.
2. Define the smallest meaningful MVP.
3. Identify the Golden Path: the most important successful user journey.
4. Design important API/data contracts early.
5. Build capability by capability.
6. Integrate frontend and backend incrementally.
7. Verify continuously with evidence.
8. Keep the final user journey working.
9. Prefer simplicity under hackathon constraints.

## Development Process Model

This starter uses a hybrid iterative-incremental process with capability-oriented vertical-slice delivery, human-gated important decisions, risk-driven review, and evidence-based verification.

In practice, that means the product is built capability by capability. Each capability is planned, implemented through the layers it actually needs, verified, and then closed before the next useful capability is added. A workstream might cross frontend, API, backend, business logic, persistence, and UI result, but it does not have to touch every layer when the approved scope does not need them.

The model is Agile-style without claiming to be a pure textbook framework. Scope can adapt based on working software, risk, evidence, and remaining time, while the Golden Path stays more important than speculative completeness. Important requirements, design decisions, material implementation plans, release decisions, and major changes can require explicit approval before proceeding.

This fits hackathons because teams need enough upfront requirements and Master System Design to avoid chaos, but not so much planning that implementation starts too late. The practical rhythm is short upfront understanding, small implementation increments, early integration, continuous verification, risk-driven review where it matters, and scope adaptation as the deadline gets closer.

## Workflow At A Glance

```text
Official challenge and rules
-> problem.md
-> MVP + Golden Path
-> plan.md
-> execute.md
-> capability workstreams
-> focused verification
-> Golden Path integration
-> local E2E
-> release/deployment decision
-> final review
-> demo/freeze
```

The exact event rules override this generic workflow. If an event limits starter code, AI assistance, deployment, or submission timing, follow the event.

## Core Repository Files

| File or directory | Purpose |
| ----------------- | ------- |
| `problem.md` | What the product must do: normalized requirements from the official challenge. |
| `plan.md` | How the system is designed: architecture, contracts, workstreams, and release criteria. |
| `execute.md` | What is currently being implemented, verified, blocked, or deferred. |
| `review.md` | Verified review findings and bug/history summary. |
| `README.md` | Project-facing explanation and usage guide. |
| `AGENTS.md` | Repository operating instructions for human or automated agents. |
| `backend/` | FastAPI application foundation. |
| `frontend/` | Placeholder for a future problem-driven interface. |
| `migrations/` | Alembic migration foundation. |
| `tests/` | Automated verification. |
| actual code, tests, migrations, and runtime checks | Implemented truth. |

Project-state files are useful summaries, but the real implementation is proven by code, tests, migrations, Git evidence, and safe runtime checks.

## Capability-Oriented Workstreams

A workstream is one bounded engineering objective, not necessarily one folder or one technical layer.

Generic examples:

- persistence foundation;
- create booking;
- approve request;
- dashboard;
- conflict handling;
- full-stack integration;
- deployment/release preparation.

Some workstreams are backend-heavy. Some are frontend-heavy. Some are full-stack. Some are only verification or hardening. Do not force every workstream through every layer.

## Vertical Slices

Build one meaningful capability through the layers it actually needs.

For example, a full-stack "Create Booking" capability might include:

```text
User
-> frontend form
-> API request
-> backend validation
-> business rule
-> database write
-> response
-> updated frontend state
-> visible result
-> focused verification
```

That is a vertical slice. It proves a real capability, not just isolated files.

Some workstreams may be backend-only or frontend-only. That is fine when the approved plan says those layers are not needed yet.

## Backend-First, Not Backend-Complete-First

This starter is backend-first because a reliable MVP often needs clear data, rules, validation, persistence, and API contracts.

Backend-first does not mean finishing the entire backend before any frontend starts.

A better pattern is:

```text
backend/persistence foundation
-> relevant contract becomes stable enough
-> frontend consumes it
-> slice integration
-> next capability
```

Frontend work should begin when the relevant contracts are stable enough for the approved scope.

## API Contracts

Important request/response interfaces should be designed in `plan.md`, implemented by the backend, consumed by the frontend, and proven during integration.

A useful contract may define:

- method and path;
- route params or query params;
- request body;
- field names and types;
- validation behavior;
- response shape;
- status codes and important errors;
- frontend view or component that consumes it.

If a material contract flaw appears during implementation, stop and update the approved design instead of silently letting frontend and backend drift apart.

## Getting Started

Clone or create a new repository from this starter, then run the local foundation:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m pytest
uvicorn backend.main:app --reload
```

Open [http://127.0.0.1:8000/](http://127.0.0.1:8000/). The starter health endpoint should return:

```json
{"status":"ok"}
```

Database notes:

- The app can import and serve the health endpoint without a real database.
- `DATABASE_URL` is read from the process environment when persistence work needs it.
- The default local database URL is in-memory SQLite.
- Alembic is wired, but product migrations should be created only after an approved problem and design require real persistence changes.
- Do not commit real credentials or `.env` files.

Frontend notes:

- `frontend/` is a placeholder.
- No frontend framework has been selected.
- Add real frontend functionality only after the challenge and approved plan require it.

## Starting A New Hackathon Challenge

Recommended sequence:

1. Read the official challenge and rules.
2. Normalize requirements into `problem.md`.
3. Define the MVP and Golden Path.
4. Design the system in `plan.md`.
5. Initialize `execute.md`.
6. Transition this README from generic starter documentation to challenge-specific project documentation.
7. Start the first workstream.
8. Build and verify capabilities incrementally.
9. Use independent review for meaningful or risky checkpoints.
10. Reconcile final docs and prepare the demo.

## README Lifecycle

This README starts as generic starter documentation. It should not stay generic forever after a real challenge begins.

Early transition:

- after `problem.md` is approved;
- after `plan.md` is approved;
- after `execute.md` is initialized;
- rewrite README.md so it describes the actual challenge, MVP, Golden Path, architecture, setup, and current status.

Final reconciliation:

- near the end of the project;
- compare README.md against actual code, tests, migrations, runtime behavior, and selected release path;
- update implemented features, setup, demo flow, deployment notes if used, known limitations, and explicit deferrals.

Do not claim planned functionality as implemented.

## Testing And Verification

Use verification that matches the risk of the workstream:

- unit tests for pure logic;
- schema/API tests for request and response behavior;
- service tests for application workflow;
- migration checks when persistence changes;
- focused workstream verification for one capability;
- integration checks when frontend and backend meet;
- Golden-Path E2E before demo/freeze.

Generated code is not complete until relevant behavior is verified.

## Local E2E Before Deployment

Prove the application locally before treating it as demo-ready.

```text
local browser/app
-> local frontend if present
-> local backend
-> local/test database
-> visible result
```

Deployment is conditional unless the rules or demo require it. If you deploy, run deployed E2E afterward because hosted runtime changes URLs, environment variables, CORS, database connectivity, migrations, startup behavior, and failure modes.

## AI-Assisted Development

This repository works for human-only, AI-assisted, or mixed development workflows.

When using agents, keep the responsibilities clear:

| Role | Responsibility |
| ---- | -------------- |
| Human / project owner | Understands requirements, approves decisions, prioritizes scope, and remains accountable. |
| Control / supervisor role | Helps analyze requirements, architecture, plans, debugging, explanations, and workflow control. |
| Builder role | Implements bounded workstreams, tests, debugs, and records evidence. |
| Reviewer role | Independently checks correctness, integration, contract drift, and missing verification. |
| Repository | Remains the engineering source of truth. |

These roles may be filled by humans, AI agents, or a combination of both. No specific tool or model is required.

## Documentation

- [Quickstart](docs/guides/QUICKSTART.md)
- [Workflow concepts](docs/guides/WORKFLOW.md)
- [Prompt Playbook](docs/guides/PROMPT_PLAYBOOK.md)
- [Full-stack guide](docs/guides/FULL_STACK_GUIDE.md)
- [Builder workflow](docs/AGENT_WORKFLOW.md)
- [Reviewer workflow](docs/REPO_REVIEW_WORKFLOW.md)

Use the README for orientation. Use the detailed docs when you need exact operating rules.

## Adapting The Starter

When a real challenge starts:

- keep reusable infrastructure that is allowed by the official rules;
- replace placeholder/generic language with challenge-specific facts;
- keep requirements in `problem.md`;
- keep design decisions in `plan.md`;
- keep implementation progress in `execute.md`;
- keep review history in `review.md`;
- avoid carrying domain assumptions from previous projects.

## Hackathon Priorities

Under time pressure, prioritize:

1. working Golden Path;
2. correctness;
3. persistence and integrity;
4. frontend/backend integration;
5. verification;
6. explainability;
7. demo reliability;
8. optional polish.

## What This Template Does Not Predetermine

- Domain entities, database schema, or domain APIs
- Business rules, decision algorithms, or product-specific validation
- A frontend framework or real interface
- Deployment architecture or distributed infrastructure
- ML systems, optimization infrastructure, caches, queues, or background workers

Those choices must come from official event rules, the official challenge/problem statement, and approved design.

## Git Workflow

Agents do not commit or push automatically. Humans review verified work, approve checkpoints, and control history changes.

## License

No license is included yet. Choose one deliberately before publishing the repository.
