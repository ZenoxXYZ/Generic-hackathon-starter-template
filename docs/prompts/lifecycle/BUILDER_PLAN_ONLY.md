# Builder Plan-Only Prompt

## Use

For one new approved implementation slice.

```text
In a fresh session, read AGENTS.md, the Builder workflow, relevant HADF guides, approved requirements/design, execution checkpoint, code, tests, migrations, configuration, dependencies, phase/review evidence, and Git state. Do not rely on chat memory.

Propose a bounded plan for [WORKSTREAM NAME]: objective, Golden-Path relationship, rules addressed, verified current state, design decisions, scope, deferrals, affected files/layers, data/schema and migration impact, contracts and readiness, services/logic, frontend/backend/persistence/integration N/A decisions, external-service fallback, validation/error behavior, implementation sequence, focused and broader verification, reconstruction topics, risks, completion criteria, and branch/worktree decision. Stop before implementation for Human / Project Owner approval.
```
