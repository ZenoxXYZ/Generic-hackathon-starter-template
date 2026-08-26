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

## Workstreams and Review

A frontend Builder workstream should first inspect the approved problem, plan, API contracts, and current backend behavior. It plans UI scope and states, receives human approval, then implements and verifies the interface. A full-stack workstream verifies the actual path from user input through backend behavior and back to rendering.

An independent Reviewer checks contract compatibility, loading/error/empty behavior, stale state risks, and accidental duplication of backend decision logic. It does not invent a framework or redesign the product without approval.

## Demo-First UI Priorities

1. Main input or action
2. Current system state
3. Core decision or output
4. Explanation
5. Error and recovery
6. Polish

Protect the first five before spending time on visual refinement.
