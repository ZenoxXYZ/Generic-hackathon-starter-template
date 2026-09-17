# HADF Generic Hackathon Starter

HADF is a human-governed framework for turning an approved challenge into a
bounded, verified, explainable submission. This repository combines reusable
HADF methodology with one included, verified software starter.

```text
Universal HADF methodology
!= Product Build specialization
!= optional FastAPI/PostgreSQL Product Build starter
!= historical implementation and review evidence
```

HADF does not require FastAPI, PostgreSQL, a browser, or a software product.
The included FastAPI/PostgreSQL stack is an optional verified Product Build
starter: a convenience when it fits the approved challenge, not a methodology
requirement or an automatic choice for every Product Build challenge.

## Choose Your Path

| If you need to... | Start here |
| --- | --- |
| Understand and classify a challenge | [START_HERE.md](START_HERE.md) |
| Use universal HADF methodology | [HADF Overview](docs/core/HADF_OVERVIEW.md) |
| Define proof, workstreams, completion, timebox, or team allocation | [Core guides](docs/core/HADF_OVERVIEW.md) and [runbooks](docs/runbooks/CHALLENGE_INTAKE.md) |
| Build a user-facing product or service | [Product Build playbook](docs/playbooks/product-build.md) |
| Use the included software starter | [FastAPI/PostgreSQL starter guide](docs/starters/software-fastapi-postgres.md) |

Start with challenge classification, not a stack choice. Product Build applies
when the Challenge Profile and evaluation contract describe a user-facing
product or service. A fixed-schema hidden-checker API, hardware, simulation,
or other challenge may follow universal HADF without using this starter.

## Repository Layers

### Universal HADF

The reusable methodology lives in `docs/core/`, generic `docs/runbooks/`,
`docs/prompts/`, `docs/modes/`, and the root project records. It covers
challenge classification, proof, workstreams, accountability, completion,
timebox selection, Git safety, verification, and human/agent authority.

### Product Build specialization

[Product Build](docs/playbooks/product-build.md) applies universal HADF to
user-facing software products and services. MVP, Golden Path, API contracts,
full-stack flow, browser E2E, Feature Freeze, and deployment guidance apply
only when that specialization is selected.

### Optional verified software starter

The existing `backend/`, `frontend/`, `tests/`, `migrations/`, Compose,
Alembic, and CI paths provide a challenge-neutral FastAPI/PostgreSQL Product
Build starter. It includes FastAPI, SQLAlchemy, Alembic, pytest, Docker Compose
PostgreSQL, and PostgreSQL-backed CI without product-domain models or tables.

Use [the starter guide](docs/starters/software-fastapi-postgres.md) for setup,
run, test, migration, PostgreSQL, and health-check instructions.

### Historical evidence

`docs/phases/` and `docs/reviews/` preserve implementation and review history.
They are evidence and learning records, not required onboarding material.

## Universal Project Records

| Record | Purpose |
| --- | --- |
| `AGENTS.md` | Stable operating policy for humans and agents |
| `problem.md` | Approved interpretation of the actual challenge |
| `plan.md` | Approved system and timebox strategy |
| `execute.md` | Active workstream and checkpoint state |
| `review.md` | Verified findings, risks, and quality state |
| Code, tests, migrations, and Git | Active implementation evidence |

These records remain universal: they are not FastAPI starter files. Read the
[Project Truth Model](docs/core/PROJECT_TRUTH_MODEL.md) for authority and
evidence boundaries.

## Repository Map

```text
START_HERE.md       Methodology-first challenge router
docs/core/          Universal HADF concepts and authority
docs/runbooks/      Universal operating guidance and checklists
docs/prompts/       Reusable role and lifecycle handoffs
docs/modes/         Solo and team coordination patterns
docs/playbooks/     Selected specializations, including Product Build
docs/starters/      Guides for verified optional starters
docs/phases/        Historical implementation evidence
docs/reviews/       Historical independent-review evidence

backend/            Optional FastAPI/PostgreSQL starter implementation
frontend/           Optional starter placeholder for a selected UI stack
tests/              Starter verification
migrations/         Starter schema-evolution environment
compose.yaml        Optional local PostgreSQL service
```

## Starter Status

The included software starter is intentionally health-only. It has no
product-specific routes, services, entities, tables, authentication, business
rules, or real frontend behavior. Its verified foundation includes an
environment-driven database configuration, SQLite fallback, optional local
PostgreSQL, an infrastructure-only Alembic baseline, pytest, and CI that checks
PostgreSQL readiness, migration execution, and tests.

For the exact verified commands, limitations, and safe database guidance, use
the [FastAPI/PostgreSQL starter guide](docs/starters/software-fastapi-postgres.md).

## Adapting This Repository

After official rules and the challenge are understood, classify the work,
record the approved interpretation in `problem.md`, define the design in
`plan.md`, initialize `execute.md`, and select only the methodology,
specialization, and starter components the challenge justifies.

When the repository becomes a real project, reconcile this README with actual
verified behavior. See the [README lifecycle](docs/runbooks/README_LIFECYCLE.md).

## Intentional Boundaries

This repository does not preselect a domain, product, frontend framework,
deployment provider, external service, persistence model, or event schedule.
Official event rules and organizer clarifications always override HADF
guidance.
