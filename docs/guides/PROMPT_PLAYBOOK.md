# Prompt Playbook

Use these prompts as copy/paste lifecycle handoffs. Replace bracketed placeholders. Each agent must read `AGENTS.md` and the governing workflow before acting. Planning prompts use Plan Mode; implementation begins only after explicit human approval.

## Essential Set Under Time Pressure

Use the smallest sequence that protects the critical path:

1. Starter Check
2. Problem Statement Intake / Source Analysis
3. Problem Definition
4. Master System Design
5. Plan Pre-Implementation Review
6. New Builder Workstream
7. Approve and Implement Workstream
8. Independent Repository Review for meaningful checkpoints
9. Frontend or Full-Stack Integration when applicable
10. Final End-to-End Review
11. Demo Freeze

Not every tiny workstream needs a separate long review during a severely time-constrained event. Do not compress away verification of the critical path.

## 1. Starter Check

### Role

Repository maintainer.

### When to Use

Before accepting a new problem statement or starting a new project from the template.

### Mode

Plan Mode / read-only.

### Prompt

```text
Read AGENTS.md, docs/AGENT_WORKFLOW.md, docs/REPO_REVIEW_WORKFLOW.md, problem.md, plan.md, execute.md, review.md, relevant phase/review records, code, tests, migrations, configuration, and Git evidence. Verify that this starter is problem-agnostic and report its actual readiness, drift, existing worktree changes, and decisions required. Do not modify files, install dependencies, commit, or push.
```

## 2. Problem Statement Intake / Source Analysis

### Role

Requirements analyst.

### When to Use

When the authoritative brief arrives as a PDF, document, image, pasted text, webpage, presentation, or multiple supplied artifacts.

### Mode

Plan Mode / read-only.

### Prompt

```text
Read AGENTS.md and inspect the supplied source material: [AUTHORITATIVE PROBLEM STATEMENT OR ARTIFACTS]. Identify which supplied sources are authoritative. Produce an intake analysis for human review that extracts only explicit evidence: objectives, actors, inputs, outputs, constraints, mandatory capabilities, evaluation criteria, stated technology constraints, ambiguities, contradictions, and missing information.

For every material conclusion, cite its source and distinguish [PROBLEM REQUIREMENT] from [UNSPECIFIED]. Do not design architecture, choose entities, APIs, schema, algorithms, or frontend technology. Do not edit repository files. Stop for human review.
```

### Expected Output

An evidence-backed requirements analysis suitable as input to `problem.md`.

## 3. Problem Definition

### Role

Requirements analyst.

### When to Use

After source intake is reviewed, or when a clear authoritative text brief is supplied directly.

### Mode

Plan Mode.

### Prompt

```text
Read AGENTS.md, docs/AGENT_WORKFLOW.md, the authoritative source or approved intake analysis, and current repository state. Produce a proposed problem.md only; do not edit it.

Use sections appropriate to the brief, including as applicable: problem objective; actors/users; required capabilities; entities or concepts explicitly implied by the brief; inputs; outputs; constraints; stated validation or business requirements; stated external systems; evaluation or success criteria; ambiguities; unspecified decisions; and explicit deferrals only where the brief supports them.

Mark every important conclusion as [PROBLEM REQUIREMENT], [UNSPECIFIED], or [DESIGN DECISION]. Avoid [DESIGN DECISION] at this stage unless it is clearly identified as unapproved. Do not design architecture, APIs, persistence, algorithms, or frontend behavior. Stop for human review and approval.
```

### Expected Output

A proposed, source-grounded `problem.md` interpretation with no invented product requirements.

## 4. Approve and Write `problem.md`

### Role

Builder.

### When to Use

After the proposed interpretation is explicitly approved.

### Mode

Implementation.

### Prompt

```text
The proposed problem interpretation is approved. Update problem.md exactly to the approved interpretation. Preserve the distinction between [PROBLEM REQUIREMENT], [UNSPECIFIED], and [DESIGN DECISION]. Do not begin product design or implementation. Do not modify unrelated files, commit, or push.
```

## 5. Master System Design

### Role

Lead Builder.

### When to Use

After `problem.md` is approved.

### Mode

Plan Mode.

### Prompt

```text
Read AGENTS.md, docs/AGENT_WORKFLOW.md, approved problem.md, plan.md, execute.md, review.md, relevant phase/review records, code, tests, migrations, dependencies, configuration, and Git evidence. Reconstruct the current repository state before designing.

Produce the smallest coherent MVP plan that covers only approved requirements. Address, where applicable: system boundary; actors; architecture; major components; domain model; database schema and relationships; API endpoints and request/response contracts; validation; service boundaries; business or decision logic; state transitions; error behavior; frontend requirements; frontend/backend contracts; migration strategy; testing and integration strategy; workstream sequencing; dependency decisions; problem-justified security requirements; explicit deferrals; demo-critical golden path; risks; and unresolved decisions.

Label each non-obvious choice [DESIGN DECISION], never as a problem requirement. Do not implement or edit files. Stop for human approval.
```

### Expected Output

An approved-plan candidate that is feasible for the available time and traceable to `problem.md`.

## 6. Plan Pre-Implementation Review

### Role

Senior architecture reviewer.

### When to Use

Before implementation begins on a proposed master plan.

### Mode

Plan Mode / read-only.

### Prompt

```text
Read AGENTS.md, docs/AGENT_WORKFLOW.md, approved problem.md, the proposed plan, current repository evidence, and relevant guidance. Review the proposed plan without editing files.

Check requirement coverage, invented requirements, unnecessary complexity, missing entities or relationships, API and schema consistency, frontend/backend contract completeness, failure behavior, migration implications, testability, feasibility for the available time, workstream ordering, critical path, explicit deferrals, overengineering, under-design, and unresolved design decisions.

Report strengths, contradictions, missing decisions, overengineering, under-design, and recommended corrections. Produce a revised plan only if requested. Stop for human approval.
```

### Expected Output

An evidence-based plan review, not implementation.

## 7. Initialize Execution State

### Role

Builder.

### When to Use

After the master plan is approved.

### Mode

Implementation.

### Prompt

```text
Read AGENTS.md, docs/AGENT_WORKFLOW.md, approved problem.md and plan.md, current state files, and repository evidence. Initialize or reconcile execute.md and review.md only where verified evidence supports it. Record the next workstream and explicit deferrals. Do not implement product behavior, change architecture, commit, or push.
```

## 8. New Builder Workstream

### Role

Builder.

### When to Use

For each new approved implementation slice.

### Mode

Plan Mode.

### Prompt

```text
In a fresh session, read AGENTS.md and docs/AGENT_WORKFLOW.md. Reconstruct authoritative requirements, approved design, the execution checkpoint, relevant code, tests, migrations, configuration, dependencies, phase/review records, and Git evidence. Do not rely on prior chat memory.

Propose a bounded plan for [WORKSTREAM NAME] with: objective; requirements addressed; verified current state; design decisions; scope; explicit deferrals; files and layers likely affected; data/schema changes; API changes; service or logic changes; frontend impact; validation and error behavior; migration implications; tests; verification commands; risks; and completion criteria. Stop before implementation for human approval.
```

### Expected Output

A plan conforming to the Builder workflow’s planning requirements.

## 9. Approve and Implement Workstream

### Role

Builder.

### When to Use

Only after the workstream plan is explicitly approved.

### Mode

Implementation.

### Prompt

```text
Exit Plan Mode and implement exactly the approved [WORKSTREAM NAME] scope. Follow AGENTS.md and docs/AGENT_WORKFLOW.md. Preserve layer boundaries and existing compatible behavior unless the approved plan says otherwise. Create migrations for approved persistence changes; do not run migrations automatically at startup or mutate real databases.

Reproduce and fix implementation-time bugs with evidence, add regression coverage, run focused checks during implementation and broader relevant verification at closeout. Create proportional docs/phases documentation and reconcile execute.md/review.md only with verified evidence. Under strict hackathon mode, keep documentation concise.

Report changed files, database changes, request/data flow, verification results, remaining deferrals, and anything not verified. Stop before commit or push for human review.
```

### Expected Output

Verified implementation evidence and a human-review handoff.

## 10. Implementation-Time Bug Investigation

### Role

Builder.

### When to Use

When a failure is discovered while implementing an approved workstream.

### Mode

Implementation.

### Prompt

```text
For [SYMPTOM], reproduce or verify the failure, record expected and actual behavior, inspect repository evidence, locate the responsible layer, and identify the root cause. Propose the smallest design-preserving fix. Add regression coverage, run focused and broader relevant verification, and record a stable BUG-ID only after the bug is verified. Escalate any material architecture, schema, API, policy, or scope change for human approval before implementing it.
```

## 11. Builder Closeout

### Role

Builder.

### When to Use

At a verified workstream checkpoint.

### Mode

Implementation.

### Prompt

```text
Audit [WORKSTREAM NAME] against AGENTS.md and docs/AGENT_WORKFLOW.md. Reconcile completion claims against code, tests, migrations, safe runtime checks, documentation, and Git evidence. Report changed files, implementation, request/data flow, verification, verified bugs, deferrals, risks, and exact checkpoint scope. Update only repository records that the evidence supports. Do not commit or push.
```

## 12. Independent Repository Review

### Role

Independent Reviewer.

### When to Use

After a meaningful workstream or named checkpoint.

### Mode

Read-only initial review.

### Prompt

```text
Read AGENTS.md and docs/REPO_REVIEW_WORKFLOW.md. Establish the exact [CHECKPOINT] and diff scope, including the baseline commit and uncommitted changes if applicable. Independently reconstruct requirements and implemented state from repository evidence; do not rely on Builder claims.

Trace requirement coverage and inspect architecture, schema/migration consistency, API contracts, validation, business or decision logic, failure handling, tests, regression risk, configuration/security concerns relevant to scope, documentation drift, and frontend/backend compatibility where applicable. Classify each finding exactly as a verified bug, design issue, documentation drift, missing verification, deferred feature, or optional improvement, following the Reviewer workflow. The initial pass is read-only: do not fix, commit, or push. End with the required review status and stop.
```

### Expected Output

A review report with evidence, correctly classified findings, and no unapproved changes.

## 13. Approve Local Review Fixes

### Role

Reviewer.

### When to Use

After a human accepts specific local, design-preserving findings.

### Mode

Implementation.

### Prompt

```text
Human approval: correct only [FINDING IDs]. Follow docs/REPO_REVIEW_WORKFLOW.md: reproduce each accepted finding, identify the root cause, make the smallest design-preserving correction, add regression coverage where appropriate, verify it, and update accepted review evidence. Do not widen scope, redesign architecture, commit, or push.
```

## 14. Corrective Builder Workstream

### Role

Builder.

### When to Use

For a human-approved correction that materially affects architecture, data, API, policy, or scope.

### Mode

Plan Mode.

### Prompt

```text
Read AGENTS.md, docs/AGENT_WORKFLOW.md, the approved review finding [FINDING IDs OR EVIDENCE], approved requirements/design, and repository evidence. Produce a corrective Builder plan covering the violated invariant, affected architecture/data/API/policy, decisions required, scope, explicit deferrals, migration and compatibility implications, tests, verification, and risks. Do not implement until the human approves the plan.
```

## 15. Frontend Workstream

### Role

Frontend Builder.

### When to Use

After UI requirements and backend contracts are approved.

### Mode

Plan Mode.

### Prompt

```text
Read AGENTS.md, docs/AGENT_WORKFLOW.md, docs/guides/FULL_STACK_GUIDE.md, approved problem.md and plan.md, current backend contracts, tests, and repository evidence. Plan the smallest frontend slice for the actual user workflow: required pages/views/components, frontend state model, API calls, loading, empty, success, validation, failure, recovery, demo-critical path, and minimal visual polish.

Keep business and decision logic in the backend. Identify any missing or incompatible contract before implementation. State scope, deferrals, affected files, tests, verification, and risks. Stop for human approval.
```

### Expected Output

A frontend plan grounded in approved requirements and actual backend contracts.

## 16. Full-Stack Integration Workstream

### Role

Integration Builder.

### When to Use

When the approved frontend and backend slices exist.

### Mode

Plan Mode.

### Prompt

```text
Read AGENTS.md, docs/AGENT_WORKFLOW.md, approved problem.md and plan.md, frontend and backend code, contracts, tests, migrations, configuration, and Git evidence. Plan verification of the actual user journey:

User action -> frontend state -> HTTP request -> FastAPI route -> validation -> service -> business logic -> persistence -> response -> frontend rendering.

Identify each contract boundary, error propagation path, loading/empty/success/failure state, mismatch risk, test approach, affected files, scope, deferrals, verification commands, and completion criteria. Stop before implementation for human approval.
```

### Expected Output

An end-to-end integration plan with explicit contract and error checks.

## 17. Integration Debugging

### Role

Integration Builder.

### When to Use

When an approved end-to-end path fails.

### Mode

Implementation.

### Prompt

```text
Reproduce [INTEGRATION SYMPTOM] across user action, frontend state, request, route, validation, service/logic, persistence, response, and rendering. Compare expected and actual behavior at each boundary, isolate the root cause, and implement only an approved design-preserving correction. Verify the full path, contract compatibility, error propagation, and relevant regression checks. Escalate material contract or architecture changes for approval. Do not commit or push.
```

## 18. Final End-to-End Review

### Role

Independent Reviewer.

### When to Use

Before a demonstration or delivery checkpoint.

### Mode

Read-only initial review.

### Prompt

```text
Read AGENTS.md and docs/REPO_REVIEW_WORKFLOW.md. Reconstruct the current verified state and run the final repository review for [CHECKPOINT]. Prioritize startup, the approved golden user flow, core correctness, persistence/state, frontend/backend compatibility, critical validation and error behavior, test evidence, configuration relevant to the demo, and P0/P1 findings. The initial review is read-only. Classify evidence and findings under the Reviewer workflow, report the required review status, and stop without fixing, committing, or pushing.
```

## 19. Demo Freeze

### Role

Release coordinator.

### When to Use

When preparing the final demonstration or delivery.

### Mode

Implementation.

### Prompt

```text
Enter STRICT HACKATHON / TIME-CONSTRAINED MODE. Read AGENTS.md, the governing workflows, approved requirements/design, current state files, code, tests, migrations, configuration, and Git evidence to reconstruct what is verified. Identify the golden demo path and freeze optional feature development.

Identify P0/P1 blockers. Verify startup; required database and migrations; backend behavior; frontend behavior; full-stack integration; seed/demo data if applicable; environment configuration; and critical validation and error behavior. Record known limitations and appropriate fallback or demo-recovery steps. Do not perform speculative refactoring, commit, or push. Stop for human approval of the checkpoint.
```

### Expected Output

A demo-readiness report with verified paths, blockers, limitations, and recovery notes.

## 20. Optional Post-Hackathon Hardening

### Role

Maintainer.

### When to Use

After the time-constrained event.

### Mode

Plan Mode.

### Prompt

```text
Read repository evidence, approved requirements/design, review findings, and demo risks. Propose a prioritized hardening roadmap for reliability, security, maintainability, and deployment. Do not reclassify design decisions as problem requirements. Stop for approval before implementation.
```
