# Decision Authority

The Human / Project Owner remains accountable for requirements, priorities, risk acceptance, major design choices, and source-history actions.

| Role | Primary responsibility |
| --- | --- |
| Human / Project Owner | Approves, prioritizes, decides, and explains. |
| Control / Supervisor | Requirements reasoning, architecture supervision, scope/time control, and reconstruction. |
| Builder | Bounded implementation, debugging, verification, and evidence recording. |
| Reviewer | Independent evidence-based findings and verdict. |
| QA / Integration owner | Behavioral, cross-boundary, and assembled-flow verification. |

Agents must stop and escalate before materially changing architecture, public API, shared schema, invariants, MVP, Golden Path, major dependencies, execution order, or another owner's approved scope. See [AGENTS.md](../../AGENTS.md) and [decision runbooks](../runbooks/MASTER_DESIGN.md).
