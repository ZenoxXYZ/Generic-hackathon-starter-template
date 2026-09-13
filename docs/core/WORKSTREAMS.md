# Workstreams

A workstream is one bounded engineering objective that creates or strengthens meaningful system behavior. It is not automatically a folder, role, or fixed set of technical layers.

Workstreams may be backend-only, frontend-only, full-stack vertical slices, data/logic work, integration/hardening, QA, or release work. Prioritize work that unlocks or protects the Golden Path, while recognizing that foundations, hardening, and release work may also be necessary.

Each workstream must record its objective, Golden-Path relationship, owner, dependencies, relevant contract, risks, verification expectation, exit criteria, and explicit deferrals in `plan.md` and `execute.md`.

One bounded change normally uses one branch. A Builder may work only within its approved scope; shared architecture, contracts, schemas, invariants, and other owners' scope require approval before change.

Use the [workstream start](../runbooks/WORKSTREAM_START.md) and [Builder launch](../runbooks/BUILDER_LAUNCH.md) runbooks.
