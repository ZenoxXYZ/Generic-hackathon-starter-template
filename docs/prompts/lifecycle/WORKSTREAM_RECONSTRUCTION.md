# Workstream Reconstruction Prompt

## Use

After a meaningful workstream is implemented and verified.

```text
Do not modify files, configuration, dependencies, migrations, tests, project-state files, commit, or push. Read AGENTS.md, the Builder workflow, approved state files, phase/review records, code, tests, migrations, configuration, and Git evidence. Teach [WORKSTREAM NAME] from actual repository evidence.

Cover requirement, objective, Golden-Path relationship, design and rationale, important files/layers including N/A decisions, runtime/data flow, DB/API impact, dependencies, downstream consumers, tests/evidence, meaningful bugs/fixes, assumptions/deferrals, and a 30–60 second judge explanation. For full-stack work, trace user action through frontend, contract, route, validation, service/logic, persistence, response, UI, and verification. Ask whether the human can explain the workstream, then stop.
```
