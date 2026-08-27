# Quickstart

Use this guide when a new hackathon brief arrives. The goal is to establish an evidence-backed MVP path without guessing product requirements.

## 1. Create Your Project

Use GitHub's **Use this template** option if the owner has enabled it, then clone the resulting repository. Alternatively:

```powershell
git clone <template-repository-url> my-hackathon-project
cd my-hackathon-project
```

If you need independent Git history, use the template feature or deliberately reinitialize Git yourself. This template never changes Git history automatically.

## 2. Prepare the Local Foundation

Create the local Python environment before product implementation:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m pytest
uvicorn backend.main:app --reload
```

Confirm `http://127.0.0.1:8000/` returns `{"status":"ok"}`. Add `DATABASE_URL` to your process environment only when approved persistence or Alembic work needs it; do not commit credentials.

Do not add problem-specific dependencies until an approved design justifies them.

## 3. Declare Time Constraints When They Matter

At the opening of an AI or team workstream, explicitly state:

```text
STRICT HACKATHON / TIME-CONSTRAINED MODE
```

This asks the team to protect the MVP, correctness, integration, deployment readiness when needed, verification, and demo readiness before detailed documentation, long teaching sessions, or polish.

## 4. Define the Problem Before Designing

1. Provide the authoritative hackathon statement.
2. Use Problem Statement Intake in the [Prompt Playbook](PROMPT_PLAYBOOK.md).
3. Use Problem Definition and review the proposed `problem.md`.
4. Approve `problem.md`.
5. Run Master System Design and approve `plan.md`.
6. Initialize or reconcile `execute.md` and `review.md` with repository evidence.

Only then begin product implementation.

## 5. Build, Understand, Integrate, and Deploy

The normal flow is:

```text
create repo from template
-> create/activate .venv
-> install dependencies
-> run starter tests
-> verify health endpoint
-> authoritative problem statement
-> Problem Intake
-> problem.md
-> plan.md
-> execution state
-> Builder workstreams
-> workstream reconstruction
-> frontend, when needed
-> local integration
-> deployment, when a remote demo is intended
-> deployed verification
-> final review
-> whole-project reconstruction
-> Demo Freeze
-> demo/submission
```

For each meaningful Builder workstream:
1. Start a fresh Builder workstream in Plan Mode.
2. Approve its plan before implementation.
3. Implement, debug, test, verify, and record the workstream under `docs/phases/`.
4. Run an independent Reviewer workstream for meaningful or risky checkpoints.
5. Reconstruct the verified workstream so the human understands what was built, where it lives, how it runs, what state it touches, and how it was verified.
6. Close the Builder chat only after the human understanding checkpoint is sufficient.

Frontend work should follow approved backend contracts. Local full-stack integration verifies the app on local services. If the MVP must be demoed remotely, add a deployment workstream and verify the deployed golden path before Demo Freeze.

## 6. Compressed Six-Hour Guidance

| Time | Focus |
| --- | --- |
| 0:00-0:30 | Read brief, define scope, approve `problem.md`. |
| 0:30-1:00 | Master design, MVP slice, approve `plan.md`. |
| 1:00-3:00 | Build and verify the primary backend path. |
| 3:00-4:15 | Connect the smallest useful interface to stable contracts. |
| 4:15-5:00 | Exercise the golden path, failures, local integration, and critical fixes. |
| 5:00-5:30 | Deploy if a remote demo is needed; verify public backend, frontend, database, migrations, CORS, and golden path. |
| 5:30-6:00 | Final review, whole-project reconstruction, fallback demo path, and Demo Freeze. |

Learning should be proportional:
- Small reconstruction: 2-3 minutes.
- Meaningful workstream: 5-8 minutes.
- Core business or decision workstream: up to about 8-10 minutes.
- Whole-project reconstruction before demo: about 10-15 minutes.

If time is shorter, reduce scope before reducing verification of the primary flow.
