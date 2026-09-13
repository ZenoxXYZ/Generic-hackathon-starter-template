# Rendezvous

A rendezvous is an explicit cross-owner integration checkpoint after dependent work becomes available. It is not satisfied by a merge alone.

Confirm the real contract, endpoint/path/method, request and response shapes, error behavior, configuration, state updates, persistence where relevant, and mock removal. Record whether the result is contract agreement, a real slice integration, systematic hardening, or E2E evidence.

Use this checklist where relevant:

- [ ] Endpoint path and HTTP method agree.
- [ ] Request fields, types, validation, and error format agree.
- [ ] Response structure and status handling agree.
- [ ] Client API base URL and CORS configuration are correct.
- [ ] Loading, success, empty, validation, and server-error states are visible.
- [ ] Mutation/refetch and stale-state behavior are correct.
- [ ] Refresh/reload preserves required persistent state.
- [ ] Temporary mocks are removed when the real dependency is available.
- [ ] Browser Network evidence confirms the real request and response when a browser exists.
