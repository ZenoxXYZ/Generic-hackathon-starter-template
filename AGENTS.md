AGENTS.md
Stable engineering rules for this repository.
1. Repository Purpose
This is a reusable hackathon engineering repository intended to be adapted to an authoritative problem statement.
- The authoritative problem statement defines what must be solved.
- problem.md captures the approved interpretation of that problem.
- The repository must not inherit domain assumptions from previous projects.
- Design choices must remain distinguishable from problem requirements.
2. Requirements and Implemented-State Evidence
Use two separate axes. Do not treat a project-state summary as requirements authority or as more authoritative than contradictory repository evidence.
Requirements / Design Authority
1. Authoritative external problem statement
2. Approved problem.md interpretation
3. Approved plan.md design decisions
The authoritative problem statement is the ultimate source for what the project must solve. problem.md is the repository's approved interpretation of those requirements. plan.md records approved engineering and design choices for satisfying them. A design choice must not be presented as a problem requirement.
Implemented-State Evidence
Determine implemented state from repository evidence, including:
- Actual code
- Automated tests
- Migrations and schema evidence
- Git history and status
- Safe runtime or API verification, where applicable
execute.md, review.md, docs/phases/, and docs/reviews/ summarize implemented state and verified engineering history. Reconcile them to repository evidence; they must not override contradictory code, tests, migrations, or Git evidence.
If implementation evidence conflicts with project-state documentation:
1. Do not silently choose either side.
2. Verify the repository evidence.
3. Report the inconsistency.
4. Correct stale documentation only after the actual state is understood.
3. Default Technology Direction
The preferred default stack for fast hackathon MVP development is:
- Python
- FastAPI
- Pydantic
- SQLAlchemy
- PostgreSQL
- Alembic
- Uvicorn
- Isolated automated testing
These are default design choices, not problem requirements. If the authoritative problem statement or approved plan justifies a different technology, the plan may override a default after documenting that decision. No frontend framework is mandatory.
4. Default Architecture
Prefer a modular monolith unless requirements justify another architecture. Common responsibilities are:
- backend/main.py — application composition and app entry point
- backend/routes/ — HTTP concerns
- backend/schemas/ — request and response validation contracts
- backend/services/ — application operations and orchestration
- backend/models/ — SQLAlchemy persistence mappings
- backend/logic/ — pure reusable decision or business algorithms when separation is useful
- backend/database.py — database engine, session, base, and dependency setup
- backend/config.py — environment-based configuration
- tests/ — automated verification
- migrations/ — database schema evolution
- frontend/ — user interface when the problem requires one
Do not create unnecessary layers merely because they are theoretically clean.
5. Coding Principles
- Inspect the real repository before making assumptions.
- Read before editing.
- Do not invent requirements.
- Clearly label conclusions as appropriate:
  - [PROBLEM REQUIREMENT]
  - [DESIGN DECISION]
  - [IMPLEMENTATION]
- Prefer minimal, focused, reversible changes.
- Preserve verified behavior unless the approved plan intentionally changes it.
- Favor readable, explicit code over clever abstractions.
- Solve root causes rather than symptoms.
- Avoid unrelated refactoring during feature work.
- Keep the application runnable whenever practical.
6. API Layer Rules
- Routes handle paths, HTTP methods, dependencies, status codes, request and response wiring, and translation of application outcomes into HTTP behavior.
- Routes should delegate application and business work to services or logic modules.
- Routes must not contain major business or decision algorithms.
- Avoid duplicate endpoints.
- Use stable response contracts.
- Handle validation failures through schemas where appropriate.
7. Schema Rules
- Pydantic schemas own request and response contracts.
- Distinguish required, optional, nullable, and omitted values carefully.
- PATCH semantics must distinguish omitted fields from explicit null.
- Use validation constraints where they are part of the API contract.
- Do not duplicate schema definitions in route or app modules.
- Response schemas should support serialization from ORM objects when needed.
8. Service and Business Logic Rules
- Services own application operations, persistence orchestration, and transactional workflow.
- Reusable pure algorithms may live in logic/.
- Services should not depend on FastAPI request or response objects.
- Services may use SQLAlchemy sessions and models.
- Business and decision logic must not be buried in routes.
- Transaction failures must roll back appropriately.
- Make deterministic behavior explicit when ordering or ranking matters.
9. Database Rules
- SQLAlchemy models represent persistence.
- Alembic is the default schema-evolution mechanism.
- Do not casually use create_all() as a replacement for versioned schema changes after migrations exist.
- Do not run migrations automatically at app startup unless explicitly approved.
- Database credentials must come from environment-based configuration.
- Do not hardcode secrets.
- Automated tests must not mutate production or externally important databases.
- Use isolated temporary databases when appropriate.
- Do not modify real PostgreSQL data without explicit approval.
10. Dependency Rules
- Prefer the existing stack.
- Do not install dependencies without a concrete approved need.
- Explain what problem a new dependency solves.
- Update the dependency manifest.
- Avoid infrastructure complexity unless required.
Do not add the following prematurely unless actual requirements or an approved design decision justify them:
- Microservices
- Kafka
- RabbitMQ
- Celery
- Kubernetes
- Service meshes
- Distributed caches
- Vector databases
- ML systems
- Background workers
- WebSockets
11. Security and Configuration Rules
- Never commit credentials, tokens, passwords, private keys, or .env files.
- Provide safe .env.example placeholders.
- Validate external inputs.
- Avoid sensitive logging.
- Treat local database and administrative scripts as potentially destructive.
- Use environment-based configuration.
- Do not disable security checks merely to make tests pass.
12. Testing Requirements
A task is not complete because code was generated. Relevant behavior must be verified.
Prefer:
- Unit tests for pure logic
- Service tests
- Schema validation tests
- HTTP/API tests
- Migration tests when persistence changes
- Integration tests for important user flows
- Regression tests for verified bugs
Test:
- Normal behavior
- Important invalid inputs
- Missing entities
- Boundary conditions
- Failure cases relevant to the feature
Existing tests must not be deleted merely to obtain a green suite.
13. Debugging Requirements
Use this debugging workflow:
1. Reproduce or verify the failure when feasible.
2. Record the observed symptom.
3. Determine expected behavior.
4. Inspect actual evidence.
5. Locate the responsible architectural layer.
6. Identify the root cause.
7. Make the smallest appropriate fix.
8. Run focused verification.
9. Run relevant regression verification.
10. Record meaningful bug history.
Do not repeatedly change unrelated code based on guesses.
Use disciplined bug classification:
- A missing future feature is not automatically a bug.
- An optional improvement is not automatically a bug.
- A design limitation is not automatically a bug.
For verified bugs, use stable BUG-IDs and record:
- Component
- Symptom
- Expected behavior
- Actual behavior
- Root cause
- Fix
- Focused verification
- Regression verification
- Status
14. Verification and Task Completion
Use these execution markers:
- [ ] Pending
- [~] In progress
- [x] Completed and verified
- [!] Blocked by a known issue or bug
- [?] Requires clarification or an engineering/design decision
Rules:
- Generated code alone never qualifies for [x].
- Mark [x] only after relevant verification passes.
- If verification is impossible, mark the task incomplete or not verified.
- Never hide known failures.
After implementation, report:
- Files changed
- Verification performed
- What passed
- What failed
- What was not verified
- What remains incomplete
15. Git and Change Safety
- Inspect git status before significant work when the repository has Git metadata.
- Do not reset, discard, or revert unrelated user changes.
- Do not rewrite unrelated files.
- Do not delete files unless justified.
- Keep logical changes reviewable.
- Do not create commits unless explicitly requested.
- Do not push unless explicitly requested.
- Before a commit, report what changed and what was verified.
- Prefer clear logical commit boundaries.
16. Anti-Overengineering Rules
- Build the smallest solution satisfying verified requirements.
- Optimize for a working, explainable MVP under hackathon constraints.
- Do not introduce architecture only for hypothetical future scale.
- Prefer a modular monolith by default.
- Avoid unnecessary factories, wrappers, and layers.
- Do not prematurely optimize.
- Distinguish demo-critical requirements from polish.
17. Builder Agent Operating Rules
Builder Agents must:
- Read docs/AGENT_WORKFLOW.md.
- Reconstruct project state from repository evidence, not previous-chat memory.
- Read problem.md, plan.md, execute.md, review.md, relevant phase and review documents, Git history, tests, migrations, and code.
- Begin meaningful new workstreams with planning.
- Require human approval before implementing major plans.
- Stop for approval if implementation requires a material architecture, schema, API, or policy change.
- Create phase documentation under docs/phases/ appropriate to the workstream's complexity and available time.
- Update project-state summaries at workstream closeout to match verified repository evidence.
18. Independent Reviewer Agent Rules
Reviewer Agents must:
- Read docs/REPO_REVIEW_WORKFLOW.md.
- Use a fresh, independent repository-evidence review.
- Perform the initial review read-only.
- Distinguish bugs, design issues, missing verification, documentation drift, deferred features, and improvements.
- Not automatically fix review findings before human approval.
- Allow approved local, design-preserving fixes in the review chat.
- Escalate major architecture, schema, API, or policy corrections to a dedicated corrective workstream.
- Never commit or push without explicit approval.
19. Documentation Responsibilities
- problem.md — authoritative approved problem interpretation
- plan.md — high-level system design and engineering roadmap
- execute.md — summary execution and checkpoint tracker
- review.md — concise summary of verified engineering and bug history
- docs/AGENT_WORKFLOW.md — Builder Agent workflow
- docs/REPO_REVIEW_WORKFLOW.md — Reviewer Agent workflow
- docs/phases/ — detailed implementation and learning documentation
- docs/reviews/ — detailed independent repository-review evidence
Avoid duplicating full phase documentation into review.md.
20. Hackathon Priority Rule
When time is constrained, prioritize in this order:
1. Primary user journey works
2. Core decision or business behavior is correct
3. Persistence and state are correct
4. Backend/frontend contract works
5. Important failure cases are handled
6. Tests protect the demo-critical path
7. Explainability
8. Maintainability
9. Polish
Near submission or demo freeze, do not add speculative features.
Keep documentation concise enough that it does not delay the higher-priority working MVP, correctness, integration, verification, or demo readiness.
21. AI Agent Final Rule
The agent's objective is not to generate the most code.
The objective is to produce the smallest correct, verified, understandable, demonstrable solution consistent with the authoritative problem statement.