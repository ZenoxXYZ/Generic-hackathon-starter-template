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

| ID | Objective | Status | Critical Proof Path | Primary owner | Dependencies | Verification / evidence | Next |
| --- | --- | --- | --- | --- | --- | --- | --- |
| WS-XX | TBD from approved plan | PLANNED | TBD | TBD | TBD | TBD | TBD |

## Workstream Card

### WS-XX — Name

- **Objective:**
- **Critical-Proof-Path relevance:**
- **Primary owner:**
- **Contributors / optional specialist owners:**
- **Dependencies:**
- **Governing interfaces / assumptions:**
- **Risk level:**
- **Implementation / construction state:**
- **Integration state:**
- **Verification state:**
- **Required evidence:**
- **Current evidence:**
- **Branch / worktree:**
- **Builder / Builder status:**
- **Local status:**
- **PR / CI / Reviewer / Review verdict:**
- **Merge status / synchronization / rendezvous where applicable:**
- **Exit criteria:**
- **Blockers:**
- **Decision needed:**
- **Next action:**
- **Deferrals:**
- **Overall status:**

Track only evidence-backed state. Use `N/A` for layers that do not belong to the approved workstream.
