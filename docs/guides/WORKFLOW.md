# Workflow Concepts

The workflow is designed to make a fast-moving project understandable after chat memory is gone. Repository files, tests, migrations, and Git evidence are durable; a previous conversation is not.

## Requirements, Design, and Evidence

Keep three questions separate:

```text
What must be solved?       authoritative brief -> problem.md
How will we solve it?      approved design -> plan.md
What actually works?       code + tests + migrations + Git + safe verification
```

`execute.md` and `review.md` are useful checkpoints, but they summarize implemented state. They cannot override contradictory code, tests, migrations, or Git evidence.

## Why Builders and Reviewers Are Separate

```text
Builder:  plan -> approved implementation -> debugging -> verification -> phase record
Reviewer: independent read-only audit -> classified findings -> human decision
```

The Builder owns implementation and its local bugs. The Reviewer challenges completion claims with fresh eyes. A Reviewer may correct only human-approved, local, design-preserving findings; architecture, schema, API, or policy corrections become new Builder workstreams.

## Generated Is Not Complete

Generated code becomes a completed checkpoint only after relevant tests, imports, safe runtime/API checks, and any required migration checks pass. A failure should be reproduced, compared with expected behavior, traced to its responsible layer, fixed narrowly, and protected by regression verification.

## Phase and Review Evidence

`docs/phases/` records what a Builder actually implemented and verified. `docs/reviews/` records an independent review scope, evidence, findings, risks, and status. In strict hackathon mode, keep both concise and focused on the demo-critical path.

## Full-Stack Work

Frontend work follows backend contracts instead of copying business rules into the browser:

```text
User -> UI -> API -> validation -> service / logic -> persistence -> response -> UI state
```

Verify the happy path as well as important loading, validation, error, and empty states. Before demo freeze, stop speculative work and focus on startup, the main journey, correctness, integration, and critical failures.

For exact Builder and Reviewer procedures, read [AGENT_WORKFLOW.md](../AGENT_WORKFLOW.md) and [REPO_REVIEW_WORKFLOW.md](../REPO_REVIEW_WORKFLOW.md).
