# HADF Generic Hackathon Starter

HADF (the **Hackathon Agentic Development Framework**) is a reusable FastAPI starter and human-AI engineering workflow for building hackathon MVPs with controlled architecture, Git isolation, AI-agent supervision, testing, review, and incremental integration.

It gives a team a safe starting point before the challenge is known: technical scaffolding, shared project-truth files, and an operating model that keeps humans accountable for important decisions.

## What problem does this solve?

| Common Hackathon Problem | HADF Response |
| --- | --- |
| Team starts coding before understanding the challenge | `problem.md` + challenge intake |
| Everyone imagines a different architecture | Shared `plan.md` |
| AI agents make unrelated changes | Bounded tasks + `AGENTS.md` |
| Frontend and backend drift | Approved API contracts |
| Multiple agents overwrite each other | Branches + conditional worktrees |
| “Agent says done” but code is unverified | Tests + evidence + review |
| PR merges but teammates still have old code | Post-merge synchronization |
| Features work separately but not together | Rendezvous + QA + E2E |
| Team builds too much | MVP + Golden Path |
| Nobody understands the final system | Reconstruction + documentation |

## What this repository gives you

- ✓ Generic FastAPI backend foundation
- ✓ SQLAlchemy + Alembic database readiness
- ✓ pytest test foundation
- ✓ GitHub Actions CI and a pull-request template
- ✓ Agent governance through `AGENTS.md`
- ✓ `problem` / `plan` / `execute` / `review` workflow
- ✓ Solo, 2-, 3-, and 4-member operating modes
- ✓ Git branch, worktree, PR, merge, and post-merge guidance
- ✓ QA, E2E, and deployment-readiness runbooks
- ✓ Reusable role and lifecycle prompts
- ✓ Challenge-neutral architecture

## How it works

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
AI Builder
   ↓
Tests + Review
   ↓
PR + CI
   ↓
Merge + Sync
   ↓
Integration + QA + E2E
   ↓
Verified MVP
```

The Golden Path is the most important successful user journey that proves the MVP’s value. Work from approved requirements and design, then integrate and verify each relevant capability before calling the MVP complete.

## Who this is for

This repository is useful for:

- solo hackathon developers;
- small hackathon teams;
- students learning backend and project workflow;
- developers using Codex or other coding agents;
- teams that want AI assistance without losing architecture and control; and
- engineers who want a reusable project-control template.

## Tech stack at a glance

| Area | Current Starter |
| --- | --- |
| Backend | FastAPI |
| Validation | Pydantic |
| ORM | SQLAlchemy |
| Database | SQLite fallback / PostgreSQL-ready |
| Migrations | Alembic |
| Testing | pytest + httpx |
| CI | GitHub Actions |
| Version control | Git |
| Collaboration | GitHub Pull Requests |
| Agent governance | `AGENTS.md` |
| Frontend | Intentionally unselected placeholder |

## Architecture at a glance

```text
User
 ↓
Frontend
 ↓
HTTP / JSON
 ↓
FastAPI Route
 ↓
Pydantic Validation
 ↓
Service / Business Logic
 ↓
SQLAlchemy
 ↓
Database
 ↓
Response
 ↓
Frontend State
```

The current starter contains the foundation only. Product-specific routes, services, entities, tables, and frontend behavior are added only after an actual challenge is understood and approved.

## Quick start

Create a repository from this template when official rules allow reusable starter code, then clone it.

1. Create and activate a virtual environment. It isolates this project’s Python packages.

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

3. Run the automated foundation tests.

   ```powershell
   python -m pytest
   ```

4. Start the local FastAPI development server.

   ```powershell
   uvicorn backend.main:app --reload
   ```

5. Open [http://127.0.0.1:8000/](http://127.0.0.1:8000/). The health endpoint should return `{"status":"ok"}`.

`DATABASE_URL` is optional for this health-only foundation. Use the placeholders in [.env.example](.env.example) only when approved persistence work requires a real database. Alembic migrations require `DATABASE_URL`; never run them against a real database without explicit approval.

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

## AI agent governance

AI may inspect, implement, test, debug, review, and document within an approved bounded task.

Humans retain authority for requirement interpretation, architecture, contracts, major data decisions, security decisions, and merge or release decisions.

```text
Agent says done
→ evidence
→ tests
→ diff
→ review
→ human approval
```

Read [Decision Authority](docs/core/DECISION_AUTHORITY.md) and [AGENTS.md](AGENTS.md) before assigning implementation work.

## What this repository demonstrates

This repository demonstrates reusable backend scaffolding, repository governance, AI-agent task boundaries, Git branching and worktrees, pull-request workflow, CI, structured testing, contract-first integration, project-state documentation, multi-agent engineering, and human-in-the-loop verification.

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
