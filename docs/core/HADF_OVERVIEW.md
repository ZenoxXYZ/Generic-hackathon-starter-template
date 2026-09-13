# HADF Overview

HADF, the Hackathon Agentic Development Framework, is a lightweight operating model for turning an approved challenge into a small, correct, explainable MVP with humans and agents working from repository evidence.

It is not a product architecture, a domain template, an AI product, or enterprise process overhead. Official event rules and the approved challenge always override this generic framework.

The repository holds durable engineering memory after a chat ends: requirements, design, live execution state, reviews, code, tests, migrations, and Git history. Builders implement and verify bounded work; Reviewers independently challenge evidence; the Human / Project Owner remains accountable for decisions and understanding. Post-implementation reconstruction turns verified repository evidence into the human understanding needed to supervise, debug, modify, and explain the system.

## Governing Principles

- Parallelize implementation, not architecture.
- One bounded change uses one branch.
- One concurrent implementation agent uses one mutable workspace.
- Inspect before modifying; generated code is not completed work.
- Do not silently change architecture, public API, shared schema, invariants, major dependencies, MVP, Golden Path, or another owner's scope.
- Frontend work waits for contract clarity, not total backend completion.
- Merge changes shared source; integration proves dependent components cooperate.
- CI, PR review, QA, and E2E are distinct forms of evidence.

## Canonical Guides

- [Project truth and authority](PROJECT_TRUTH_MODEL.md)
- [Decision authority](DECISION_AUTHORITY.md)
- [Golden Path](GOLDEN_PATH.md)
- [Workstreams](WORKSTREAMS.md)
- [API contracts](API_CONTRACTS.md)
- [Definition of Done](DEFINITION_OF_DONE.md)
- [Git operating model](../git/GIT_MENTAL_MODEL.md)
- [Operational runbooks](../runbooks/CHALLENGE_INTAKE.md)
- [Full-stack flow](FULL_STACK_FLOW.md)
- [Time-compressed operation](../runbooks/TIME_COMPRESSION.md)
