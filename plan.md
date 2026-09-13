# Engineering Plan / Master System Design

## Status

[?] Requires approved `problem.md` before product-specific design.

## MVP And Golden Path

Record the smallest viable MVP and the Golden Path: the most important successful user journey that demonstrates its core value.

## Architecture And Service Boundaries

Record approved runtime components, technology choices, frontend/backend boundaries, persistence, service/logic responsibilities, and reasons for each design decision.

## Entities, Schema, And Invariants

Record only approved domain entities, relationships, state transitions, validation, integrity, security, and business/decision invariants.

## API And Data Contracts

| Producer / consumer | Contract | Request/input | Response/output | Validation / errors | Owner |
| --- | --- | --- | --- | --- | --- |
| TBD | TBD | TBD | TBD | TBD | TBD |

Material contract changes require explicit approval, propagation to all affected consumers and producers, updated tests, and an execution-state record.

## Risks, Testing, And Integration

Record architecture and delivery risks, focused tests, and the selected release path. Distinguish these integration stages:

1. Contract integration — frontend expectations and backend design agree.
2. Feature/slice integration — a real frontend capability reaches the corresponding backend capability.
3. Systematic full-stack integration — the assembled Golden Path is hardened across boundaries.
4. Golden-Path E2E — a real user journey proves the intended outcome.

Record local or deployed E2E expectations, important failure paths, browser/API evidence where applicable, and persistence/refresh expectations.

## Release, Deployment, And Documentation Reconciliation

After Golden-Path assembly, systematic hardening, local E2E, and Feature Freeze, choose a local final-runtime path or an approved deployment workstream. For deployment, record hosting, environment-variable names, migrations, production API URL, CORS, external-service fallback, and deployed E2E criteria.

Record the early README transition after approved requirements/design and execution initialization, then final README reconciliation against verified implementation and the selected release path.

## Workstream Map

| ID | Objective | Golden-Path relevance | Owners | Dependencies | Contract | Risk | Verification / exit criteria |
| --- | --- | --- | --- | --- | --- | --- |
| WS-XX | TBD | TBD | TBD | TBD | TBD | TBD | TBD |

## Parallel Execution Policy

Parallelize approved implementation, not architecture. One bounded change uses one branch. One concurrent implementation agent uses one mutable workspace.

- Use a normal feature branch when one human has one active mutable task.
- Use separate branches and worktrees only when that same human has multiple concurrent mutable tasks.
- Different humans normally use separate clones.
- Frontend work starts when its relevant contract is stable enough; it does not wait for total backend completion.

## Explicit Deferrals And Assumptions

Record intentionally postponed work and unverified assumptions so they are not mistaken for bugs or requirements.
