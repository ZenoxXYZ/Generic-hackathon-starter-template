# Definition Of Done

Generated code is not complete work. Use three distinct completion gates.

## Local Complete

The approved bounded implementation is finished locally and relevant focused verification has passed. Evidence, limitations, and unverified items are recorded.

## Merge Ready

The change is Local Complete, its diff is human-reviewed, the PR describes scope and contracts, configured CI passes, and required review findings are resolved or explicitly accepted.

## Workstream Complete

The change is merged, dependent owners synchronize, temporary mocks are removed where relevant, required rendezvous and integration occur, QA and applicable E2E pass, regression evidence is recorded, and `execute.md` is closed accurately.

CI runs configured automated checks. PR review judges scope, architecture, contracts, and code. QA verifies behavior and risk. E2E proves a real assembled user journey. None replaces the others.
