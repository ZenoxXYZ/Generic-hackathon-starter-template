# QA Verification

QA verifies behavior and risk beyond configured CI. Check successful behavior, important invalid and boundary cases, loading/empty/validation/server-error states, error recovery, state correctness, and cross-component interactions relevant to the workstream.

Where a browser exists, inspect its Network activity to confirm request URL, method, payload, response, status, CORS behavior, and the absence of accidental mock or localhost dependencies. Classify evidence accurately: CI checks automation, review judges changes, QA verifies behavior, and E2E verifies the assembled user journey. Record failures, retests, regressions, and remaining risks in `review.md` or detailed review evidence as appropriate.
