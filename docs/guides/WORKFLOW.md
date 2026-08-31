# Workflow Concepts

The workflow is designed to make a fast-moving project understandable after chat memory is gone. Repository files, tests, migrations, and Git evidence are durable; a previous conversation is not.

## Requirements, Design, and Evidence

Keep three questions separate:

```text
What may be done?          official event rules / official clarifications
What must be solved?       official challenge / problem statement -> problem.md
How will we solve it?      approved design -> plan.md
What actually works?       code + tests + migrations + Git + safe verification
```

`execute.md` and `review.md` are useful checkpoints, but they summarize implemented state. They cannot override contradictory code, tests, migrations, or Git evidence.

Official event rules and organizer clarifications outrank the template workflow for competition constraints. Reusable/prebuilt infrastructure, challenge-specific implementation, AI-assisted development, deployment, and submission/code-freeze behavior must comply with those official rules.

Document roles:
- `problem.md` is the normalized WHAT the complete product must do. It may include frontend, backend, persistence/data, business rules, invariants, user workflows, inputs/outputs, assumptions, constraints, and MVP boundaries, but it should not become an implementation design document.
- `plan.md` is the approved HOW / Master System Design. It records Golden Path, architecture, frontend/backend structure, entities, database design, invariants, important API contracts, business/decision logic, workstream map, dependencies, integration strategy, verification strategy, and release/deployment criteria.
- `execute.md` is live implementation/workstream state with capability, Golden-Path relevance, dependencies, contracts, layer tasks, verification, evidence, status, blockers, next step, and deferrals. N/A layers are valid.
- `review.md` is verified review findings/history, not a duplicate implementation tracker.
- `README.md` is project-facing documentation for the actual repository.
- Actual code, migrations, tests, Git evidence, and safe runtime checks are implemented truth.

`plan.md` and the Builder Planning Phase / Plan Mode are different. `plan.md` is the persistent whole-system Master Design. Builder Planning Phase / Plan Mode is a repo-grounded implementation plan for one bounded workstream.

## Human, Supervisor, Builder, Reviewer, and Repository Roles

```text
Human / Project Owner: approves, understands, prioritizes, decides, explains
Control / Supervisor: requirements reasoning, architecture supervision, Builder task/prompt preparation, Builder-plan critique, teaching, reconstruction, debugging supervision, scope/time control, judge readiness
Builder: repo reconstruction, workstream planning, implementation, tests, debugging, execute.md/evidence updates, concise implementation report
Reviewer: independent verification, findings, severity, verdict
Repository: engineering truth
```

These roles may be filled by humans, AI agents, or a combination of both. The workflow should not depend on any specific tool as the primary long-form teaching agent; the Control / Supervisor may reconstruct workstream understanding after Builder evidence exists.

## Why Builders and Reviewers Are Separate

```text
Builder:  plan -> approved implementation -> debugging -> verification -> phase record
Reviewer: independent read-only audit -> classified findings -> human decision
```

The Builder owns implementation and its local bugs. The Reviewer challenges completion claims with fresh eyes. A Reviewer may correct only human-approved, local, design-preserving findings; architecture, schema, API, or policy corrections become new Builder workstreams.

## Generated Is Not Complete

Generated code becomes a completed checkpoint only after relevant tests, imports, safe runtime/API checks, and any required migration checks pass. A failure should be reproduced, compared with expected behavior, traced to its responsible layer, fixed narrowly, and protected by regression verification.

## Why Post-Implementation Reconstruction Exists

When official rules permit AI-assisted development, AI can produce working code faster than a human can internalize it.

```text
verified code != human understanding
```

Post-implementation reconstruction bridges that gap. It translates verified repository evidence into enough human understanding to supervise, debug, modify, and explain the system.

The learning stage comes after verification because the best teaching source is the actual implementation, not a hypothetical design that may have changed during debugging.

## Three Levels of Understanding

After a meaningful workstream, the human should understand:

1. Why the workstream exists.
2. How it is implemented.
3. How it connects to the rest of the repository.

This does not mean memorizing every line. It means knowing the requirement, design, important files, runtime flow, data flow, dependencies, verification evidence, and judge-level explanation.

## Workstreams and Builder Chats

One fresh Builder chat normally maps to one meaningful workstream. The repository persists context; the chat is temporary.

A workstream is a bounded engineering objective that creates or strengthens meaningful system behavior. It may be backend-only, backend-heavy, frontend-only, frontend-heavy, a full-stack vertical slice, business/decision-logic oriented, integration/hardening oriented, specialized verification, or release/deployment oriented. The boundary follows the capability, not a technology folder.

Golden Path means the most important successful user journey that demonstrates the core value of the MVP. It is identified before implementation during problem intake and Master System Design, then used to drive MVP scope, workstream priority, architecture, data/API contracts, frontend views, integration order, E2E verification, and demo preparation.

A meaningful Builder chat normally closes after:

```text
plan.md / execute.md
-> next workstream
-> fresh Builder session or agent where useful
-> repository reconstruction
-> Builder Planning Phase / Plan Mode
-> bounded implementation plan
-> Control / Supervisor + Human review
-> human approval
-> implementation
-> debugging
-> focused verification
-> evidence
-> execute.md update
-> implementation report
-> Control / Supervisor workstream reconstruction
-> optional risk-driven Reviewer
-> human understanding checkpoint
-> close workstream
```

Multiple small tasks may form one workstream and should usually receive one combined reconstruction. Do not require a long teaching session after every microscopic edit.

A workstream is complete only when its relevant path reaches: DESIGNED -> PLANNED -> APPROVED -> IMPLEMENTED -> INTEGRATED where relevant -> VERIFIED -> EVIDENCE RECORDED -> EXIT CRITERIA SATISFIED -> CLOSED.

Reviewers are selective and risk-driven. Useful checkpoints include complex business/decision logic, concurrency/integrity, critical state transitions, important DB constraints, major API changes, significant integration, and final product checkpoints.

## Phase and Review Evidence

`docs/phases/` records what a Builder actually implemented and verified. `docs/reviews/` records an independent review scope, evidence, findings, risks, and status. In strict hackathon mode, keep both concise and focused on the demo-critical path.

## Stable Methodology vs Project State

The stable reusable methodology lives in:
- AGENTS.md
- docs/AGENT_WORKFLOW.md
- docs/REPO_REVIEW_WORKFLOW.md
- docs/guides/

These files evolve when the generic engineering method improves.

Project-specific state lives in:
- problem.md
- plan.md
- execute.md
- review.md
- README.md inside an adapted hackathon solution repository
- docs/phases/
- docs/reviews/
- code, tests, migrations, frontend, and configuration justified by the approved problem

Do not contaminate reusable methodology with product-specific rules. Do not treat project-state summaries as stronger evidence than the real implementation.

## Full-Stack Work

Backend-first does not mean backend-complete-first. Backend-first establishes authoritative domain foundations, persistence, major invariants, critical backend capabilities, and sufficiently stable API/data contracts. Frontend work may begin once the relevant contract/capability is stable enough for the approved scope.

Master System Design should identify the important API/data contracts needed by the MVP and Golden Path. Workstreams may refine the relevant details, but material contract changes must be propagated to all affected layers.

Frontend work follows backend contracts instead of copying business rules into the browser:

```text
User -> UI -> API -> validation -> service / logic -> persistence -> response -> UI state
```

Verify the happy path as well as important loading, validation, error, and empty states. Before demo freeze, stop speculative work and focus on startup, the main journey, correctness, integration, and critical failures.

Integration evidence grows in stages:

1. Level 1 - Contract integration: frontend expectations and backend design agree.
2. Level 2 - Feature / slice integration: a real frontend capability communicates with the real corresponding backend capability.
3. Level 3 - Systematic full-stack integration: the assembled Golden Path is checked and hardened across boundaries.
4. Level 4 - E2E verification: a real user journey proves the system works through required layers and produces the intended outcome.

Systematic full-stack integration is a later hardening/reconciliation pass, not the first time frontend and backend meet.

## Deployment Lifecycle

The workflow supports two release paths.

Release decision starts after local evidence:

```text
Golden Path assembled
-> systematic full-stack hardening
-> local Golden-Path E2E
-> Feature Freeze
-> release decision
```

Local release path:

```text
Feature Freeze
-> local final runtime
-> chosen-runtime E2E
-> P0/P1 fixes
-> final README reconciliation
-> final review
-> required critical corrections
-> whole-project engineering reconstruction
-> internal Demo Freeze
-> Git/source checkpoint
-> official event freeze/submission
```

Deployed release path:

```text
-> Feature Freeze
-> deployment decision
-> deployment
-> deployed E2E verification
-> P0/P1 fixes
-> final README reconciliation
-> final review
-> required critical corrections
-> whole-project engineering reconstruction
-> internal Demo Freeze
-> Git/source checkpoint
-> official event freeze/submission
```

Public deployment is not universally mandatory. Deploy when deployment is officially required, necessary for the demo, or reliable and valuable within remaining time. Otherwise, reliable local demonstration with local E2E/final verification remains valid.

Local success is not deployment success. A deployed app has different URLs, environment variables, origins, database connectivity, migrations, build commands, startup behavior, and failure modes.

Conceptually:

```text
LOCAL:
frontend localhost
-> backend localhost
-> local/test DB

DEPLOYED:
hosted frontend
-> HTTPS
-> hosted backend
-> hosted PostgreSQL
```

Deploy the smallest architecture that reliably demonstrates the critical path. Do not add infrastructure merely to look production-grade.

## Demo Freeze vs Official Freeze

Demo Freeze is an internal stability gate chosen by the team. It means optional feature work stops and the team protects startup, the primary flow, correctness, integration, verification, known fallback paths, and explanation readiness.

Official Code Freeze or submission deadline is an external competition boundary. The official rules always take precedence over the template workflow.

## README Lifecycle

README.md starts as generic starter documentation, then transitions with the project.

Pass 1 - early challenge transition: after `problem.md` is approved, `plan.md` is approved, and `execute.md` is initialized, README.md should become a challenge-specific project README. It may include project/challenge name, concise problem summary, approved MVP, Golden Path, architecture overview, tech stack, frontend/backend/persistence structure, local setup/run instructions, environment variables, migration commands, test commands, and current implementation status. It must not claim planned but unimplemented features as completed.

Pass 2 - final README reconciliation: once the Golden Path and implementation are stable, reconcile README.md against actual verified code, migrations, tests, runtime behavior, selected release path, demo flow, deployment if used, known limitations, and explicit deferrals. Remove stale generic-starter wording and inaccurate claims.

The Control / Supervisor decides when README transition/reconciliation is required and prepares the bounded Builder task/prompt. The Builder performs the edit and verifies README.md against repository reality.

## Starter, AI, and External Service Policy

Reusable code, boilerplate, starter infrastructure, authentication components, UI libraries, AI-assisted development, deployment, and submission behavior are governed by official event rules and organizer clarifications. Do not assume every event permits the same starting point or assistance model.

Challenge-specific implementation boundaries also come from the official event rules. The generic template should not claim when every event requires challenge-specific code to be created.

When external, cloud, or third-party services are used:
- Justify why they are needed.
- Verify credentials and access before relying on them.
- Understand failure modes.
- Avoid unnecessary single points of failure.
- Preserve a local or degraded fallback where practical.

## Whole-Project Engineering Reconstruction

After major workstreams and before the final demo, reconstruct the whole application:
- Architecture
- Domain relationships
- Database
- API
- Service and business logic
- Decision engine, when present
- Frontend
- Dynamic updates, when present
- Deployment
- Verification
- Limitations
- Engineering tradeoffs

The final reconstruction should leave the human able to explain the project as:

```text
Problem
-> Requirements
-> Architecture
-> Data model
-> API
-> Services
-> Business/Decision Logic
-> Persistence
-> Frontend
-> Dynamic Updates
-> Deployment
-> Verification
-> Limitations / Tradeoffs
```

## Time-Constrained Learning

During a six-hour hackathon, the goal is not line-by-line code memorization, complete theory mastery, or long lectures after each edit.

The goal is to understand major engineering decisions, meaningful workstream execution, file and layer connections, important state/data flow, verification, and how the whole application can be explained to judges.

Suggested timing:
- Small workstream reconstruction: 2-3 minutes.
- Meaningful workstream: 5-8 minutes.
- Core business or decision workstream: up to about 8-10 minutes.
- Whole-project reconstruction before demo: about 10-15 minutes.

These are guidance, not rigid timers.

For exact Builder and Reviewer procedures, read [AGENT_WORKFLOW.md](../AGENT_WORKFLOW.md) and [REPO_REVIEW_WORKFLOW.md](../REPO_REVIEW_WORKFLOW.md).
