Independent Repository Review Workflow
1. Purpose
Independent repository review is a quality gate after meaningful implemented workstreams. The Reviewer Agent evaluates:
A. the newly completed workstream; and
B. the resulting repository for regressions or inconsistencies affecting previously completed behavior.

The Reviewer must not depend on Builder chat memory. Its purpose is to independently validate completion claims, review new work, detect regressions, classify findings correctly, and protect the next Builder workstream from building on broken assumptions.

2. When Review Runs
A full review is recommended when a workstream introduces:
- Meaningful executable behavior
- Database or schema changes
- Business or decision logic
- Cross-domain integration
- Frontend/backend integration
- Deployment or production configuration
- Significant state transitions
- Important infrastructure or configuration behavior

Do not automatically require a full review after trivial documentation-only changes.

Review should normally occur after the Builder workstream has been implemented, implementation-debugged, verified, documented, human-reviewed, committed, and preferably pushed so the Reviewer audits a stable checkpoint. A committed checkpoint is preferred, not mandatory when a human explicitly authorizes review of an identified uncommitted checkpoint.

3. Reviewer Bootstrap
A fresh Reviewer must inspect, when relevant:
- AGENTS.md
- docs/AGENT_WORKFLOW.md
- docs/REPO_REVIEW_WORKFLOW.md
- problem.md
- plan.md
- execute.md
- review.md
- Newly completed phase documentation
- Relevant earlier phase documentation
- Previous repository reviews
- Git status
- Recent Git history
- Actual code
- Tests
- Migrations
- Dependency and configuration files
- Frontend code and contracts, if present
- Deployment configuration and public URLs, if deployment is in scope

Apply the two-axis model in AGENTS.md: use the authoritative problem statement, approved problem.md, and approved plan.md for requirements and design authority; use code, tests, migrations, Git history/status, and safe runtime verification for implemented-state evidence. execute.md, review.md, phase documentation, and review documentation are summaries, not overriding evidence.

Reconstruct state from evidence. Do not assume project-state files are accurate.

4. Identify Review Scope
Determine the most recently completed meaningful workstream from:
- Git history
- execute.md
- plan.md
- Phase documentation
- Implementation
- Deployment records, if applicable

Normally verify that the expected review target exists and is committed. A human may authorize review of a clearly identified uncommitted checkpoint when commit or push is deliberately deferred, pre-commit independent review is desired, or time constraints make it useful.

For an authorized uncommitted review, record the exact Git status and diff scope, distinguish the baseline commit from uncommitted changes, and do not assume the changes are approved. Initial review remains read-only, and the Reviewer must not commit or push automatically. If scope is ambiguous, report it before reviewing.

5. Initial Review Is Read-Only
The first review pass is read-only: it must not intentionally modify tracked repository implementation files, approved configuration, dependencies, migrations, or project-state files. It must not commit, push, or mutate real/external databases or production state.

Do not:
- Fix code
- Update documentation
- Install dependencies
- Add migrations
- Change APIs
- Commit or push
- Mutate real or external databases or production state

Safe verification is permitted when it uses isolated temporary databases, disposable temporary files or directories, ignored cache or artifact locations, local application startup, automated tests, compile or import checks, non-destructive Git inspection, public deployed smoke checks, or other checks that do not intentionally persist changes to tracked repository state or external data. Incidental ignored artifacts such as __pycache__, temporary database files, or test caches should be cleaned or ignored appropriately and do not alone violate this rule.

First inspect, verify, reproduce where appropriate, classify, report, and stop for human review. This clarification does not authorize the Reviewer to fix code during the initial review pass.

6. Requirement Traceability Review
For implemented behavior, trace:

```text
[PROBLEM REQUIREMENT]
-> [DESIGN DECISION]
-> [IMPLEMENTATION]
-> [VERIFICATION]
```

Check that:
- Implementation actually addresses the requirement.
- The design decision matches approved documentation.
- No design choice is falsely presented as a problem requirement.
- No important approved requirement was silently omitted.

7. Architecture Review
Inspect separation and responsibilities across:
- Routes or controllers
- Schemas and contracts
- Services and application operations
- Models and persistence
- Logic and decision algorithms
- Database and configuration
- Frontend/backend boundaries

Identify concrete architectural violations. Do not report stylistic preferences as defects.

8. API Review
For each relevant endpoint, verify:
- Method
- Path
- Request schema
- Response schema
- Service or logic called
- Status codes
- Missing-entity behavior
- Validation behavior
- PATCH semantics
- Deterministic ordering where specified
- Public API compatibility
- No accidental or prototype endpoints

9. Schema / Validation Review
Inspect:
- Required versus optional values
- Nullable versus omitted values
- Explicit null semantics
- PATCH behavior
- Bounds
- Enums and statuses
- Duplicate handling
- Normalization
- List and object validation
- Response serialization

Cross-check against approved design.

10. Service / Business Logic Review
Inspect:
- Application operations
- Persistence orchestration
- Transaction handling
- Rollback
- Query behavior
- Ordering
- Update semantics
- Missing entities
- Pure algorithm correctness
- Explainability where required
- Accidental HTTP concerns in services
- Accidental business logic in routes

11. Database / Migration Review
Inspect:
- Model and migration consistency
- Migration ordering
- Metadata registration
- Upgrade and downgrade behavior
- Baseline or adoption assumptions
- Destructive changes
- Schema drift
- Test migration flow
- Automatic startup schema behavior

Do not mutate real or external databases.

12. Decision / Algorithm Review
When a workstream includes decision logic, verify:
- Formula or algorithm matches approved policy
- Boundary behavior
- Deterministic tie-breaking
- Rounding versus ranking semantics
- Filtering and eligibility
- State assumptions
- Explainability
- No unsupported inference from contextual fields

Distinguish an incorrect implementation from a deliberate MVP policy limitation.

13. Cross-Domain Regression Review
Check whether the new workstream broke:
- Application startup
- Previously verified APIs
- Migrations
- Database behavior
- Ordering
- Validations
- State transitions
- Earlier decision logic
- Frontend/backend contracts
- Deployment configuration, if applicable
- Tests

Run relevant regression checks safely.

14. Test Quality Review
Inspect:
- Unit tests
- Schema tests
- Service tests
- API tests
- Migration tests
- Integration tests
- Regression tests
- Deployed smoke or end-to-end checks, when deployment is in scope

Determine:
- What is actually proven
- Important success and failure cases
- Missing critical coverage
- Accidental external database use
- Dependence on environment or state
- Whether fixed bugs have regression protection
- Whether deployed verification is distinct from local verification

15. Frontend / Full-Stack Review
When a frontend exists, inspect:

```text
User
-> UI interaction
-> request
-> backend route
-> validation
-> service/business logic
-> database/decision logic
-> response
-> UI state
```

Review:
- Request and response compatibility
- Loading, error, and empty states
- Important validation display
- Stale data or state
- Duplicated business logic in the frontend
- Golden demo flow

16. Deployment Review
When deployment is in scope, distinguish local verification from deployed verification. Review:
- Public backend startup
- Public health endpoint
- Frontend production API URL
- Absence of hard-coded localhost dependencies
- CORS for real deployed origins
- Hosted database connectivity
- Applied migrations
- Critical request/response contracts against the deployed backend
- Deployed golden user flow
- Environment-variable and secret hygiene
- Fallback demo paths, if documented

Classify missing deployed verification as [MISSING VERIFICATION] unless evidence shows a true implemented defect.

17. Configuration / Security / Repository Hygiene Review
Inspect:
- Secrets
- Environment variables
- .env
- Dependency manifest
- Generated files
- Unsafe scripts
- Debug code
- Destructive startup behavior
- Accidental local files
- Configuration inconsistencies
- Dependency breakage

18. Documentation / Project State Review
Treat execute.md, review.md, phase documentation, and review documentation as summaries. Cross-check them against Git history, code, tests, migrations, and actual verification; do not let them override contradictory implemented-state evidence.

If evidence conflicts, verify repository state, report the inconsistency, and correct stale documentation only after the actual state is understood. Detect stale checkpoint wording or false completion claims.

Human understanding documentation and reconstruction may be checked for documentation drift or contradiction, but the Reviewer should not turn learning completeness into a product correctness bug.

19. Finding Classification
Every finding must be exactly one of the following:

[BUG]
Verified implemented behavior is incorrect.

[DESIGN ISSUE]
Concrete design or architecture concern requiring an engineering decision.

[MISSING VERIFICATION]
Implementation may be correct, but evidence is insufficient.

[DOCUMENTATION DRIFT]
Project-state documentation disagrees with repository reality.

[DEFERRED FEATURE]
Intentionally postponed functionality.

[IMPROVEMENT]
Non-blocking enhancement.

Do not classify deferred work, style preferences, hypothetical scale issues, optional polish, or incomplete learning narration as bugs.

20. Bug Evidence Standard
Before assigning a BUG-ID, establish where feasible:
- Expected behavior
- Actual behavior
- Reproduction or evidence
- Component
- Impact

Use stable BUG-IDs. Record:
- BUG-ID
- Workstream
- Component
- Severity
- Symptom
- Expected behavior
- Actual behavior
- Evidence
- Root cause once confirmed
- Proposed fix
- Focused verification
- Regression verification
- Status

Suspicion alone is not enough for a bug.

21. Severity
Use:

P0
Blocks primary operation or demo, creates major safety, security, or data risk, or prevents MVP functioning.

P1
Material correctness, regression, or integration issue that should normally be fixed before dependent development.

P2
Non-blocking issue, improvement, or missing verification that may be deferred.

Do not inflate severity.

22. Initial Review Report
Produce:
A. Overall Repository Health
B. Workstream Reviewed
C. Repository State Reviewed
D. Requirement Traceability
E. Architecture Assessment
F. API Assessment
G. Schema / Validation Assessment
H. Service / Business Logic Assessment
I. Database / Migration Assessment
J. Decision / Algorithm Assessment when relevant
K. Cross-Domain Regression Assessment
L. Test / Verification Assessment
M. Frontend Integration Assessment when relevant
N. Deployment Assessment when relevant
O. Configuration / Security Assessment
P. Documentation / Project-State Assessment
Q. Verified Strengths
R. Bugs
S. Design Issues
T. Missing Verification
U. Documentation Drift
V. Deferred Features Correctly Left Untouched
W. Improvements
X. Recommended Action Order
Y. Whether repository is safe to continue building on

Then stop. Do not fix findings during the initial review.

23. Review Status
End with exactly one:

REVIEW STATUS: PASS

or

REVIEW STATUS: PASS WITH NON-BLOCKING FINDINGS

or

REVIEW STATUS: BLOCKED

Definitions:

PASS
No blocking correctness concern.

PASS WITH NON-BLOCKING FINDINGS
No blocking issue, but P2, design, improvement, or missing-verification items remain.

BLOCKED
Verified P0 or P1 prevents safe dependent development.

24. Human Approval Before Fixes
The Reviewer must not automatically fix findings. Initial findings remain in the review report until human review. A human must first approve specific findings for correction.

25. Local Review-Fix Ownership
Approved small, local, design-preserving bugs may be fixed in the same Reviewer chat. Examples include:
- Validation bug
- Incorrect query or order
- Missing rollback
- Incorrect approved formula implementation
- Route wiring issue
- Missing regression test
- Documentation drift

Reviewer workflow:
1. Reproduce.
2. Identify root cause.
3. Make the smallest fix.
4. Add or update a regression test.
5. Run focused verification.
6. Run broader relevant regression verification.
7. Rerun the affected review area.
8. Update review evidence.
9. Stop for human review.

Do not commit or push automatically.

After a finding is accepted or verified and a local fix is approved, record the accepted review result and verified BUG-ID/history in the appropriate repository-review document and concise review.md history. Documentation drift may be corrected only after explicit human approval. Major corrective findings remain escalated to a corrective Builder workstream.

26. Major Corrective Workstream Escalation
Do not silently fix findings requiring material change to:
- Architecture
- Persisted schema or data model
- Public API contract
- Major business or decision policy
- Workstream scope or order
- Major dependency or infrastructure

Instead produce a corrective-workstream handoff containing:
- Verified evidence
- Violated requirement or invariant
- Affected design
- Why a local fix is insufficient
- Affected components
- Decisions required
- Tests required after correction

Then open a fresh corrective Builder workstream in Plan Mode.

27. New Functionality
Missing future functionality is not a review fix. It remains a Builder workstream according to plan.md and execute.md.

28. Review Documentation
After human acceptance or fixes as appropriate, create:
docs/reviews/<workstream-slug>-review.md

Use:

# <Workstream> Repository Review

## Review Scope
## Repository State Reviewed
## Workstream Reviewed
## Requirement Traceability
## Architecture Assessment
## API Assessment
## Schema / Validation Assessment
## Service / Business Logic Assessment
## Database / Migration Assessment
## Decision / Algorithm Assessment
## Cross-Domain Regression Assessment
## Test Coverage And Verification
## Frontend Integration Assessment
## Deployment Assessment
## Configuration / Security Assessment
## Documentation / Project-State Assessment
## Bugs
## Design Issues
## Missing Verification
## Documentation Drift
## Deferred Features
## Improvements
## Fixes Performed
## Regression Verification
## Remaining Risks
## Final Repository Health

End with the final review status. Do not duplicate the entire review into review.md.

In strict hackathon or time-constrained mode, use a concise review record by default: review scope, evidence checked, relevant findings by classification and severity, verification performed, remaining risks or deferrals, and final review status. Use the detailed structure above when risk, complexity, deployment, or learning value justifies it. Omit irrelevant sections or mark them not applicable; do not create empty sections solely to satisfy a template.

29. Project State Updates
- review.md - concise project-level accepted review and verified bug history; do not add unconfirmed suspicions
- execute.md - update only when review changes actual execution state or checkpoint
- plan.md - update only if review creates an approved roadmap or design change

Do not rewrite project-state files unnecessarily.

30. Git Rules
Initial review is read-only. Approved fixes and review documentation should be committed separately when practical. The Reviewer never commits or pushes unless explicitly requested.

31. Quality Gate
Do not recommend beginning dependent major work while a P0 remains. A P1 should normally be resolved when it creates material correctness or integration risk. P2 may remain documented or deferred.

The purpose is safe MVP progress, not perfection.

32. Hackathon Review Compression
Under severe time constraints, prioritize review of:
1. Application startup
2. Golden user flow
3. Core decision correctness
4. Persistence and state correctness
5. Frontend/backend compatibility
6. Deployed access and deployed integration when the demo is remote
7. P0 and P1 bugs
8. Critical validation and security issues

Do not spend final hackathon time fixing low-value style, polish, or learning-completeness findings.

Prioritize working MVP, correctness, integration, deployed verification when needed, and demo readiness before documentation depth. Use the concise review record in Section 28 unless risk or complexity justifies the detailed structure.

33. Final Principle
The Reviewer Agent's job is to independently challenge completion claims using repository evidence.

It should try to detect real correctness and regression problems without manufacturing bugs, turning intentional MVP limitations into defects, or treating local success as deployed success.
