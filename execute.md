# Execution Tracker

## Status Model

`PLANNED -> READY -> IN PROGRESS -> VERIFYING -> COMPLETE -> CLOSED`

Completion is refined as:

- **LOCAL COMPLETE** — approved implementation is locally finished and verified.
- **MERGE READY** — PR, configured CI, and required review conditions are satisfied.
- **WORKSTREAM COMPLETE** — merged, synchronized, integrated, QA-verified, and evidenced.

## Current Foundation State

- [x] Generic runtime foundation exists and has recorded verification evidence.
- [x] Generic PostgreSQL Compose, Alembic-baseline, and PostgreSQL CI artifacts exist without product-domain schema.
- [x] Supervisor-verified local PostgreSQL startup, connectivity, migration upgrade/version tracking, and PostgreSQL-backed pytest passed using an alternate host port because native PostgreSQL occupied `5432`.
- [x] Draft PR #3 CI passed its PostgreSQL readiness, migration-upgrade, and pytest path.
- [?] Product-specific work requires approved `problem.md` and `plan.md`.

## Workstream Summary

| ID | Objective | Status | Golden Path | Primary owner | Branch / worktree | Local / PR / CI / review | Merge / sync / QA | Next |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| WS-XX | TBD from approved plan | PLANNED | TBD | TBD | TBD | TBD | TBD | TBD |

## Workstream Card

### WS-XX — Name

- **Objective:**
- **Golden-Path relevance:**
- **Primary owner / Backend owner / Frontend owner / QA owner / Integration owner:**
- **Dependencies:**
- **Approved contract:**
- **Risk level:**
- **Backend / Frontend / Persistence / Integration / Infrastructure:**
- **Branch / worktree:**
- **Builder / Builder status:**
- **Local status:**
- **PR / CI / Reviewer / Review verdict:**
- **Merge status / Post-merge sync / Rendezvous / QA status:**
- **Evidence:**
- **Verification checklist:** focused tests; API/contract check; real frontend/backend request where applicable; persistence check where applicable; slice integration; Golden-Path E2E where applicable; `git diff --check`; `git status`.
- **Blockers:**
- **Next action:**
- **Deferrals:**
- **Overall status:**

Track only evidence-backed state. Use `N/A` for layers that do not belong to the approved workstream.
