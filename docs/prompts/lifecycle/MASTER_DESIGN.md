# Master Design Prompt

## Use

After `problem.md` is approved.

```text
Read AGENTS.md, the Builder workflow, approved problem.md, current plan.md/execute.md/review.md, relevant evidence, code, tests, migrations, dependencies, configuration, and Git state. Reconstruct current state before designing.

Propose the smallest coherent MVP plan. Identify the Golden Path and use it to drive scope, architecture, contracts, workstream order, integration, E2E, and demo preparation. Cover system boundary, actors, architecture, domain/data model, invariants, API/data contracts, validation, services/logic, state and failure behavior, frontend requirements, migrations, testing, four levels of integration, workstream map/ownership/dependencies, release path, conditional deployment, external-service fallback, security requirements, official freeze constraints, risks, explicit deferrals, and unresolved decisions. Mark non-obvious choices [DESIGN DECISION]. Do not implement or edit files. Stop for human approval.

Before implementation, independently review the proposed plan for rule compliance, coverage, invented requirements, Golden-Path clarity, contract/schema consistency, failure behavior, migration/deployment implications, fallback, testability, time feasibility, workstream order, overengineering, and unresolved decisions. Stop for human approval.
```
