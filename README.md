# HADF Generic Hackathon Starter

HADF, the **Hackathon Agentic Development Framework**, is a challenge-neutral repository and operating model for building a small, verified, explainable hackathon MVP with humans and agents.

This repository is a generic FastAPI scaffold, a repository-held engineering control system, a human-plus-agent workflow template, and a Git/PR/integration operating environment. It is not a product, a preselected domain, a frontend framework, an enterprise platform, or a substitute for official event rules.

## Generic Runtime Scaffold

The current scaffold intentionally contains only:

- a FastAPI application with `GET /` health endpoint returning `{"status":"ok"}`;
- environment-based database URL configuration with a safe in-memory SQLite default;
- SQLAlchemy and Alembic wiring for future approved persistence work;
- isolated tests for application and configuration behavior; and
- a placeholder `frontend/` directory with no selected framework or UI.

It does not include product entities, APIs, business rules, domain tables, decision logic, product data, or real frontend behavior.

## Quick Start

Create a repository from this template when official rules allow reusable starter code, then clone it. If independent Git history is required, use the template feature or reinitialize Git deliberately; this repository never changes Git history automatically.

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m pytest
uvicorn backend.main:app --reload
```

Open [http://127.0.0.1:8000/](http://127.0.0.1:8000/). The health endpoint should return `{"status":"ok"}`.

`DATABASE_URL` is optional for the health-only foundation. Set it from `.env.example` only when approved persistence work requires a real database. Alembic migrations require `DATABASE_URL`; do not run them against a real database without explicit approval.

Before product work, confirm official rules, verify the local foundation, normalize the challenge in `problem.md`, approve Master System Design in `plan.md`, and initialize `execute.md`. Use [Challenge Intake](docs/runbooks/CHALLENGE_INTAKE.md), [Master Design](docs/runbooks/MASTER_DESIGN.md), and [time-compressed guidance](docs/runbooks/TIME_COMPRESSION.md).

## Project Truth

| Source | Purpose |
| --- | --- |
| `AGENTS.md` | Stable agent operating policy. |
| `problem.md` | Normalized requirements. |
| `plan.md` | Approved system design. |
| `execute.md` | Live workstream state. |
| `review.md` | Verification, findings, and risk state. |
| Code, tests, and Git history | Implementation and historical truth. |

Detailed precedence and the four repository states are in the [Project Truth Model](docs/core/PROJECT_TRUTH_MODEL.md).

## Main Workflow

```text
challenge intake -> approved problem -> MVP + Golden Path -> Master Design
-> workstream -> branch/worktree decision -> Builder plan -> human approval
-> implementation -> local verification -> PR + CI + review -> merge
-> post-merge sync -> rendezvous -> QA/E2E -> closed
```

The Golden Path is the most important successful user journey that demonstrates the core MVP value. Build and integrate capabilities that prove it before speculative features. See the [HADF overview](docs/core/HADF_OVERVIEW.md) and [Golden Path guide](docs/core/GOLDEN_PATH.md).

## Team And Workspace Choice

Choose [Solo](docs/modes/SOLO.md), [Team of 2](docs/modes/TEAM_2.md), [Team of 3](docs/modes/TEAM_3.md), or [Team of 4](docs/modes/TEAM_4.md) according to people and responsibilities—not rigid technical silos.

Use a normal feature branch for one human's one active mutable task. Use separate branches and worktrees only when that same human runs multiple concurrent mutable tasks or agents. Different humans normally use separate clones. See [worktree workflow](docs/git/WORKTREE_WORKFLOW.md).

## PRs, Integration, And Agents

One bounded change belongs on one branch and in one PR. CI runs configured automated checks; PR review judges scope, architecture, contracts, and code; QA verifies behavior and risk; E2E proves the real assembled user journey. A merge changes shared source, but integration proves components cooperate.

Agents inspect repository evidence before modifying anything and must escalate material changes to architecture, public APIs, shared schemas, invariants, major dependencies, MVP, Golden Path, or another owner's scope. The human remains accountable. Start with [Decision Authority](docs/core/DECISION_AUTHORITY.md), [PR workflow](docs/git/PULL_REQUEST_WORKFLOW.md), and the [Builder workflow](docs/AGENT_WORKFLOW.md).

## Detailed Documentation

- [Core HADF guides](docs/core/HADF_OVERVIEW.md)
- [Git operating guides](docs/git/GIT_MENTAL_MODEL.md)
- [Team modes](docs/modes/SOLO.md)
- [Operational runbooks](docs/runbooks/CHALLENGE_INTAKE.md)
- [Role prompts](docs/prompts/CONTROL_ROOM.md)
- [Lifecycle prompts](docs/prompts/lifecycle/CHALLENGE_INTAKE.md)
- [Full-stack flow](docs/core/FULL_STACK_FLOW.md)
- [Deployment readiness](docs/runbooks/DEPLOYMENT_READINESS.md)
- [README lifecycle](docs/runbooks/README_LIFECYCLE.md)
- [Builder procedure](docs/AGENT_WORKFLOW.md)
- [Reviewer procedure](docs/REPO_REVIEW_WORKFLOW.md)

## Intentional Limitations

This starter stays generic until an authoritative challenge and approved design justify product work. It does not choose a domain, frontend stack, deployment provider, external services, or persistence model. Official event rules and organizer clarifications always override HADF guidance.
