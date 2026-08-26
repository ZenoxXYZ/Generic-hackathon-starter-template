# Generic Hackathon Starter

This repository is a problem-agnostic starter for hackathon work. It contains a minimal FastAPI backend foundation, database configuration hooks, Alembic migration wiring, tests, and project-state documents.

No product domain, entities, tables, APIs, frontend behavior, business rules, or decision logic are defined yet. Those must come from an authoritative problem statement, then an approved `problem.md`, then an approved `plan.md`.

## Workflow

- `AGENTS.md` contains stable repository rules.
- `Docs/AGENT_WORKFLOW.md` defines the builder workflow.
- `Docs/REPO_REVIEW_WORKFLOW.md` defines the independent review workflow.
- `problem.md` should capture the approved interpretation of the hackathon problem before product work begins.
- `plan.md`, `execute.md`, and `review.md` should be updated from repository evidence as implementation proceeds.

## Backend

The backend currently exposes only:

```text
GET / -> {"status":"ok"}
```

Database objects are configured for SQLAlchemy and PostgreSQL-compatible URLs, but the application does not create tables, run migrations at startup, or connect to a real database for the health endpoint.

## Local Setup

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
Copy-Item .env.example .env
uvicorn backend.main:app --reload
```

Set `DATABASE_URL` in `.env` or the shell before database or migration work. Do not put real credentials in committed files.

## Tests

```powershell
python -m pytest
```

Current tests verify app import, the root health response, OpenAPI construction, and safe configuration behavior without touching a real PostgreSQL database.
