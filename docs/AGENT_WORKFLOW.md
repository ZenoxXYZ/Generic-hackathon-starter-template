Builder Agent Engineering Workstream Workflow
1. Purpose
This workflow enables a fresh Builder Agent chat to reconstruct project state from repository evidence and safely continue the next engineering workstream without depending on previous chat context. It defines the procedure for planning, implementing, debugging, verifying, documenting, and handing off work. Stable repository rules remain in AGENTS.md.
2. Repository State Reconstruction
Every fresh Builder workstream begins by reading or inspecting the following when present and relevant:
- AGENTS.md
- docs/AGENT_WORKFLOW.md
- problem.md
- plan.md
- execute.md
- review.md
- Relevant docs/phases/
- Relevant docs/reviews/
- Current Git status
- Recent Git history
- Actual repository structure
- Implementation
- Tests
- Migrations
- Dependency and configuration files
Apply the two-axis model in AGENTS.md: use the authoritative problem statement, approved problem.md, and approved plan.md for requirements and design authority; use code, tests, migrations, Git history/status, and safe runtime verification for implemented-state evidence. execute.md, review.md, phase documentation, and review documentation are summaries, not overriding evidence.
Do not trust execute.md or other documentation blindly. Cross-check important completion claims against code, tests, migrations, Git history, and review evidence.
If repository evidence conflicts with project-state files, do not silently choose either side. Verify the repository evidence, report the inconsistency, and correct stale documentation only after the actual state is understood. Stop before starting a new workstream when the inconsistency affects its prerequisites or scope.
3. Determine the Next Engineering Workstream
Use the repository sources for their distinct purposes:
- The authoritative problem statement, problem.md, and approved plan.md — requirements and approved design direction
- execute.md, review.md, and phase/review documentation — implementation-state summaries
- Git, code, tests, migrations, and safe verification — implementation-state evidence
Determine the next incomplete, meaningful workstream and verify its prerequisites. Do not blindly implement whatever text appears next in a stale checklist.
4. Workstream Size
A workstream represents one meaningful engineering objective, not one tiny checkbox. Generic workstream types may include:
- Core domain or state
- Secondary domain capability
- Core business or decision logic
- Allocation, scheduling, or optimization logic
- Dynamic state handling
- Frontend integration
- Operational hardening
- Integration or debugging
Group tightly related subtasks when they belong to one coherent engineering objective. Do not make every file edit its own workstream.
5. Planning Phase
Meaningful workstreams begin in Plan Mode. Plan Mode is read-only.
Before proposing a plan:
- Inspect the current architecture.
- Verify existing behavior.
- Inspect related tests and migrations.
- Derive requirements from problem.md.
- Identify relevant design decisions.
The plan must contain the following sections:
Verified Current State
What actually exists and works?
Requirements Addressed
Which [PROBLEM REQUIREMENT] does this workstream solve?
Design Decisions
Which choices are ours?
Scope
What this workstream will implement.
Explicit Deferrals
What it will not implement.
Entity/Data Changes
Models, fields, and relationships affected.
API Changes
Endpoints, contracts, and status behavior.
Service/Business/Decision Logic
Computation or workflow introduced.
Persistence/Migration Changes
Database impact.
Validation
Required, optional, nullable, omitted, and boundary behavior.
Request/Data Flow
How the feature flows through the system.
Failure Behavior
Important invalid, missing, and error cases.
Implementation Sequence
Meaningful engineering subtasks.
Testing Strategy
How correctness will be proven.
Verification Strategy
Commands and checks needed.
Files Likely To Change
Expected repository scope.
Commit Boundaries
Logical change groups, if commits are later requested.
Risks / Open Decisions
Questions, dependencies, assumptions, and decision points.
Do not implement before human approval.
6. Human Plan Approval Gate
A produced plan is not automatically approved. Wait for explicit human approval before implementation.
If the human adds clarifications, incorporate them as approved constraints. Only after approval should Plan Mode be exited.
7. Implementation Phase
After approval:
- Re-check Git status when Git metadata exists.
- Verify the repository has not materially changed.
- Implement only the approved scope.
- Preserve verified existing behavior.
- Make minimal, focused changes.
- Follow the architecture responsibilities in AGENTS.md.
Work through meaningful implementation subtasks efficiently. Prefer vertical slices where practical, for example:
Persistence
→ schema/validation
→ service/logic
→ route/API
→ test
or:
Input state
→ filter/eligibility
→ score/rank/decision
→ explanation
→ API response
→ test
Do not add unrelated functionality.
8. Execution Tracker
Maintain execute.md using:
- [ ] Pending
- [~] In progress
- [x] Completed and verified
- [!] Blocked
- [?] Requires decision
Rules:
- Never mark generated-but-unverified work [x].
- Use meaningful checkpoint updates, not constant edits after every line.
- Final workstream closeout must update execution state accurately.
- Treat execute.md as a summary and reconcile it to verified repository evidence before updating it.
9. Implementation-Time Debugging
The Builder Agent owns implementation-time bugs discovered while building its approved workstream when they can be fixed without materially changing the approved design.
For every failure:
1. Reproduce or verify it.
2. Record expected versus actual behavior.
3. Inspect evidence.
4. Locate the architectural layer.
5. Identify root cause.
6. Make the smallest appropriate fix.
7. Add or update a regression test.
8. Run focused verification.
9. Run broader relevant regression verification.
Record meaningful verified Builder bugs in review.md during workstream closeout using stable BUG-IDs. Do not invent bugs or treat missing deferred functionality as a bug.
10. Design-Change Escalation
Stop before implementing a material unapproved change to:
- Architecture
- Persisted data model
- Migration strategy
- Public API contract
- Major business or decision policy
- Workstream scope
- Major dependency or infrastructure
- Phase ordering
Report:
1. What was discovered
2. Why the approved plan is affected
3. Options
4. Tradeoffs
5. Recommendation
6. Decision required
Return to planning and obtain human approval before proceeding. Small implementation corrections that preserve the approved design do not require re-planning.
11. Verification Ladder
After implementation, run relevant checks such as:
1. Targeted tests
2. Full automated test suite
3. Migration upgrade or check, when applicable
4. Import or application-startup check
5. API smoke tests
6. Compile or static sanity checks
7. Dependency consistency check
8. Frontend/backend integration test, where applicable
9. git diff --check
10. git status
Only run checks relevant to the repository. Do not claim unperformed verification. Clearly classify results as:
- VERIFIED
- FAILED
- NOT VERIFIED
- DEFERRED
12. Full-Stack Verification
When a frontend exists, verify the primary user journey:
User
→ frontend interaction
→ HTTP request
→ route
→ schema validation
→ service/business logic
→ persistence/decision logic
→ response
→ frontend rendering
Test at minimum:
- Golden successful flow
- Important invalid input
- Missing or empty state
- Important boundary condition
- Major state-changing operation
- Backend/frontend schema compatibility
13. Phase Documentation
After successful verification of a meaningful workstream, document it under:
docs/phases/<workstream-slug>/
In normal or learning mode, create:
- README.md
- Numbered .md documents for meaningful implementation subtasks when useful
Do not create separate documents for trivial edits.
Strict Hackathon / Time-Constrained Mode
By default, create only docs/phases/<workstream-slug>/README.md with a concise record of the objective, requirements addressed, important design decisions, key files and architecture, API or data flow, core logic or algorithm, verification, important bugs, deferred work, and a concise study or demo explanation.
Create numbered subtask documents only when a non-obvious engineering decision, complex algorithm, meaningful bug/debugging story, migration or integration issue needs preservation, or the human explicitly requests detailed learning documentation. Do not require empty or irrelevant sections; omit them or mark them not applicable.
The detailed README and subtask guidance below applies in normal or learning mode, or when the workstream's risk or complexity justifies it.
Phase README Must Explain
- Objective
- Starting state
- Ending state
- Problem requirements addressed
- Design decisions
- Actual implementation subtasks
- Architecture after the phase
- Files added, modified, or deleted
- API behavior
- Request and data flow
- Database and migration changes
- Validation
- Service, business, or decision logic
- Formulas or algorithms when relevant
- Tests
- Verification results
- Meaningful bugs and fixes
- Explicit deferrals
- Remaining limitations
- Concepts the learner should understand
- VS Code code-reading order
- Concise hackathon or judge explanation
Subtask Docs
For meaningful subtasks, explain:
- Problem solved
- Files changed
- Important code
- Why it changed
- Backend flow
- Database impact
- Validation and failure behavior
- Tests
- Bugs
- Remaining work
- Concepts
- VS Code study guide
- Judge explanation
Clearly distinguish:
- [PROBLEM REQUIREMENT]
- [DESIGN DECISION]
- [IMPLEMENTATION]
Phase documentation must describe actual verified implementation, not merely repeat the plan.
14. review.md Closeout
Keep review.md concise. Record:
- Workstream status
- Implemented behavior
- Verification performed
- Test results
- Meaningful bug history
- Deferred work
- Not-verified items
- Important limitations
Do not duplicate entire phase documentation into review.md.
Builder closeout records Builder-owned, verified implementation-time bugs. Reviewer findings remain in the review report until human review; accepted or verified review findings are recorded by the Reviewer only after the applicable human approval.
15. plan.md Closeout
Update plan.md only if:
- Workstream completion status needs reflecting.
- The high-level roadmap changed.
- An approved design change materially affects future phases.
Do not rewrite the plan after every implementation detail.
16. Human Review Gate
After implementation, debugging, verification, phase documentation, and project-state updates, stop for human review. Do not automatically commit or push.
Report:
- IMPLEMENTATION
- VERIFICATION
- BUGS
- DOCUMENTATION
- PROJECT STATE
- GIT STATUS
- REMAINING / DEFERRED
17. Commit and Push
Commits happen only when explicitly requested. Prefer logical boundaries such as:
- Implementation and tests
- Documentation and project state
- Review or corrective fixes
Before committing:
- Inspect the staged diff.
- Confirm intended scope.
- Confirm tests and verification.
Push only when explicitly requested.
18. Independent Repository Review Handoff
After a meaningful executable or cross-domain workstream is implemented, debugged, verified, documented, human-reviewed, and normally committed and pushed, an independent Reviewer Agent may run the quality gate in docs/REPO_REVIEW_WORKFLOW.md when practical before dependent major development continues. A human may explicitly authorize review of a clean, identified uncommitted checkpoint under that workflow.
Tiny documentation-only changes do not automatically require a full independent review.
19. Builder vs Reviewer Ownership
Builder Agent:
- Plans
- Implements
- Fixes implementation-time bugs
- Verifies
- Documents
- Updates project state
- Prepares commits
Reviewer Agent:
- Independently audits stable committed work
- Starts read-only
- Classifies findings
- May fix approved local, design-preserving bugs
- Does not silently redesign architecture
Major review-discovered corrective design changes become a separate corrective Builder workstream.
20. Review Result Handling
If independent review returns:
PASS
Proceed to the next workstream.
PASS WITH NON-BLOCKING FINDINGS
Record or defer findings appropriately and proceed if no dependency risk exists.
BLOCKED
Do not begin dependent major development. P0 must be resolved. P1 should normally be resolved before dependent development when it creates material correctness or integration risk.
21. Next-Chat Handoff
After the Builder and Reviewer cycle is complete, and any requested commits or pushes are completed, the next fresh Builder chat must reconstruct state from repository evidence. The user should not need to manually restate the previous workstream.
The repository is the persistent memory.
22. Hackathon Time Compression
Under strict time limits, prioritize:
1. Problem understanding
2. Primary user journey
3. Core domain or state
4. Core decision or business logic
5. Frontend/backend integration
6. Verification and debugging
7. Demo readiness
Compress workstreams when useful. Do not allow process documentation to consume time needed for a working MVP.
Prioritize working MVP, correctness, integration, verification, and demo readiness before documentation depth. Use the strict documentation mode in Section 13 when appropriate.
Near demo freeze:
- Stop speculative feature development.
- Fix only issues threatening startup, primary flow, correctness, persistence, integration, or critical validation.
23. Final Principle
The Builder Agent's job is not to maximize code volume.
It is to convert approved requirements and design decisions into the smallest correct, verified, understandable MVP while leaving enough repository evidence for another fresh agent to continue safely.