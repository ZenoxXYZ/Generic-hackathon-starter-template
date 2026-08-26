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

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m pytest
uvicorn backend.main:app --reload
```

Confirm `http://127.0.0.1:8000/` returns `{"status":"ok"}`. Add `DATABASE_URL` to your process environment only when approved persistence or Alembic work needs it; do not commit credentials.

## 3. Declare Time Constraints When They Matter

At the opening of an AI or team workstream, explicitly state:

```text
STRICT HACKATHON / TIME-CONSTRAINED MODE
```

This asks the team to protect the MVP, correctness, integration, verification, and demo readiness before detailed documentation or polish.

## 4. Define the Problem Before Designing

1. Provide the authoritative hackathon statement.
2. Use the Problem Definition prompt in the [Prompt Playbook](PROMPT_PLAYBOOK.md).
3. Review and approve `problem.md`.
4. Run Master System Design and approve `plan.md`.
5. Initialize or reconcile `execute.md` and `review.md` with repository evidence.

Only then begin product implementation.

## 5. Build, Review, and Integrate

1. Start a fresh Builder workstream in Plan Mode.
2. Approve its plan before implementation.
3. Implement, debug, test, verify, and record the workstream under `docs/phases/`.
4. Ask for a human-approved Git checkpoint when appropriate.
5. Run an independent Reviewer workstream for meaningful or risky changes.
6. Build frontend work from approved backend contracts.
7. Run a full-stack, end-to-end review before freezing the demo.

## Compressed Six-Hour Example

| Time | Focus |
| --- | --- |
| 0:00–0:30 | Read brief, define scope, approve `problem.md`. |
| 0:30–1:00 | Master design, MVP slice, approve `plan.md`. |
| 1:00–3:00 | Build and verify the primary backend path. |
| 3:00–4:30 | Connect the smallest useful interface to stable contracts. |
| 4:30–5:15 | Exercise the golden path, failures, and integration. |
| 5:15–6:00 | Independent review, fixes approved by a human, demo freeze. |

If time is shorter, reduce scope before reducing verification of the primary flow.
