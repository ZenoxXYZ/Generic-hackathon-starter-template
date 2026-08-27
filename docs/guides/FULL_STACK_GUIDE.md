# Full-Stack Guide

The template does not choose a frontend framework. Choose the smallest UI stack that matches the approved problem, team skills, and available time.

## Contract-First Integration

Define the API request and response contracts before connecting the interface. Backend routes, Pydantic contracts, services, and logic remain the source of backend behavior; the frontend should not duplicate core business or decision logic.

```text
User
  -> Frontend
  -> Fetch / API Client
  -> FastAPI Route
  -> Pydantic
  -> Service
  -> Logic
  -> SQLAlchemy
  -> Database
  -> Response
  -> Frontend Rendering
```

Configure backend URLs through environment-aware frontend configuration when appropriate. Do not hardcode deployment-specific URLs or credentials into a public client.

## Minimum UI States

For each real interaction, design and verify:

- Loading
- Successful result
- Request or server error
- Validation feedback
- Empty or unavailable state

## Local vs Deployed Full-Stack Integration

Local integration proves the system works across local services:

```text
LOCAL:
frontend dev server
-> local backend
-> local/test DB
```

Deployed integration proves the public demo path works across hosted services:

```text
DEPLOYED:
hosted frontend
-> production API base URL
-> hosted FastAPI
-> hosted PostgreSQL
```

When deployment is in scope, verify both. Local success does not prove deployed success.

Deployment-specific integration should cover:
- `API_BASE_URL` or equivalent environment configuration.
- No hard-coded localhost dependency in production frontend code.
- CORS for the real deployed frontend origin.
- HTTPS origin and protocol differences.
- Public backend health.
- Hosted persistence.
- Production error behavior.
- Deployed contract testing.
- Deployment-specific integration failures such as missing environment variables, unapplied migrations, blocked cross-origin requests, wrong route prefixes, or frontend builds pointing at local services.

## Integration Checklist

- [ ] Frontend API base URL is the production URL when deployed.
- [ ] Endpoint path matches.
- [ ] HTTP method matches.
- [ ] Request fields and types match.
- [ ] Response structure matches.
- [ ] Status codes are handled.
- [ ] Error format is handled.
- [ ] CORS works.
- [ ] No localhost dependency remains in deployed code.
- [ ] Hosted DB persists state.
- [ ] Deployed golden request tested.

## Workstreams and Review

A frontend Builder workstream should first inspect the approved problem, plan, API contracts, and current backend behavior. It plans UI scope and states, receives human approval, then implements and verifies the interface. A full-stack workstream verifies the actual path from user input through backend behavior and back to rendering.

If the MVP must be demoed remotely, a deployment workstream follows local integration. It should configure hosted services, environment variables, migrations, production API URL, CORS, and deployed end-to-end verification.

An independent Reviewer checks contract compatibility, loading/error/empty behavior, stale state risks, accidental duplication of backend decision logic, and deployed integration evidence when deployment is in scope. It does not invent a framework or redesign the product without approval.

## Demo-First UI Priorities

1. Main input or action
2. Current system state
3. Core decision or output
4. Explanation
5. Error and recovery
6. Deployed access, when the demo is remote
7. Polish

Protect the first six before spending time on visual refinement.
