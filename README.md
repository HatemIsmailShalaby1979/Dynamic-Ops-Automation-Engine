# Dynamic Ops Automation Engine

A multi-tenant, async **FastAPI** ingest and automation service — one of four tools
built in the May–June 2026 period, before Helix Prime existed. Its thinking (tenant
isolation, typed ingest contracts, an Erlang C staffing sync, and a webhook fan-out)
was later absorbed into Helix Prime's B2B Onboarding and WFM engines.

It is the only one of the four written as a *service* rather than a script, and the
engineering in it is real: tenant middleware, per-request correlation IDs, typed
exception handling, and a fail-closed configuration model. The code demonstrates a
production-shaped service boundary even though it was a self-directed build.

## What it is

Four POST endpoints, each taking a typed Pydantic payload:

| Endpoint | Payload contract | What happens |
|---|---|---|
| `POST` ingest volume forecast | `VolumeForecastPayload` | Runs the Erlang C staffing sync |
| `POST` ingest KPI health snapshot | `KPIHealthPayload` | `SentinelEngine` evaluates the snapshot and raises a system event on a threshold breach |
| `POST` ingest RTA floor adherence event | `AdherenceEventPayload` | Records the adherence signal for the tenant |
| `POST` dispatch internal event | `SystemEvent` | Fans the event out to the tenant's registered webhooks |

Plus `GET /health`, a deep check that reports on the engine and its dependencies.

**The tenancy model is real, not decorative.** Every endpoint requires an
`X-Tenant-ID` header unless explicitly exempted. `TenantMiddleware` resolves that
header to a `TenantContext` and rejects unknown or inactive tenants with 403/404.
Each tenant carries its own `SLAConfig`, `ErlangThresholds`, `AlertSeverity` levels,
and `WebhookDestination` list with its own `WebhookAuthScheme` — so service-level
targets and staffing thresholds are per-tenant configuration, not constants.
API-key verification is a FastAPI dependency (`app/api/v1/dependencies/security.py`).

**The middleware stack is deliberate**, and the ordering comments explain why: CORS
outermost to catch preflight, then a UUID correlation ID on every request
(`RequestIDMiddleware`), then an `X-Response-Time-Ms` timing header, then tenant
resolution. Typed exception handlers cover validation errors, `HTTPException`,
tenant-not-found, tenant-inactive, and an unhandled catch-all. `/docs`, `/redoc`, and
`/openapi.json` are disabled when `is_production` is set.

**Erlang C is implemented** in `app/services/wfm_engine.py` (`_erlang_b` and
`_erlang_c`), driving the staffing sync behind the forecast endpoint.
`SentinelEngine` monitors KPI health and queues events for background fan-out
through `WebhookDispatcher`.

## Configuration model — fail-closed by design

The service will not boot without database credentials. Importing the app raises a
Pydantic validation error — `DB_PASSWORD: Field required`. That is a **deliberate,
fail-closed default**: the service refuses to start against an unconfigured database
rather than starting half-configured. Point `DB_HOST`, `DB_PORT`, `DB_NAME`,
`DB_USER`, `DB_PASSWORD`, `REDIS_HOST`, `REDIS_PORT` at a real Postgres (or use the
repository's `docker-compose`) and it starts.

## Scope — what is not in this repository

Stated plainly so the README matches the code:

- **No tests.** Zero test files; nothing here is verified by a suite.
- **No Notion integration.** The word "notion" appears only in this README — no
  adapter, no client, no `notion-client` in `requirements.txt`. Earlier revisions
  claimed a "Notion provisioning" stage; it does not exist.
- **No Excel output.** No `openpyxl` or `xlsxwriter`, and no spreadsheet code of any
  kind. Earlier revisions claimed an "Excel output package"; it does not exist.
- **No client-intake form.** What exists is a typed API contract, not the
  "structured intake form" earlier revisions described.
- **`.env.production` and `.env.staging` are tracked**, with placeholder values
  (`DB_PASSWORD=change_me_in_production`,
  `SECRET_KEY=change_me_to_a_secure_random_key_min_32_chars`). No credential is
  exposed, but tracking those filenames is a hygiene problem; they should be replaced
  by `.env.example` and untracked.
- **`Ops_Automation_Hub/requirements.txt` is an oddly nested path** for the only
  requirements file in the repository.

## Run it

```bash
git clone https://github.com/HatemIsmailShalaby1979/Dynamic-Ops-Automation-Engine.git
cd Dynamic-Ops-Automation-Engine
pip install -r Ops_Automation_Hub/requirements.txt

# The service fails closed without these. Point them at a real Postgres,
# or use the docker-compose in the repository root.
export DB_HOST=localhost DB_PORT=5432 DB_NAME=ops_engine \
       DB_USER=postgres DB_PASSWORD=... \
       REDIS_HOST=localhost REDIS_PORT=6379

uvicorn app.main:app --reload
```

Then `GET /health`, and `/docs` for the OpenAPI surface (which is available outside
production). The `Dockerfile` builds on `python:3.10-slim`, installs every
`requirements.txt` it finds, and runs `uvicorn app.main:app`.

## Status

Built May–June 2026 as a standalone service and a learning build; never deployed to a
live workforce-management, CRM, or telephony system, and never connected to one. It has
no external audit, no certified data isolation, and no signed security review. The
engineering it demonstrates — multi-tenant FastAPI, tenant middleware, correlation-ID
tracing, and fail-closed configuration — is real, and it is where Helix Prime's B2B and
WFM engines started.

The GitHub repository description still carries the earlier "under 60 minutes" framing.
That figure was a June 2026 project target with no recorded baseline, sample, or method,
and it is not repeated here.

## Related work

- [Helix Prime](https://github.com/HatemIsmailShalaby1979/Helix-Prime) — the operations core; its B2B and WFM engines are where this thinking ended up
- [Helix Education](https://github.com/HatemIsmailShalaby1979/Helix-Education) — event-sourced learning engine
- [Study Studio](https://github.com/HatemIsmailShalaby1979/Study-Studio) — local-first AI tutor
- [L&D Command Center](https://github.com/HatemIsmailShalaby1979/L-D-Command-Center) — desktop learning and career workstation
- [Blue Waves](https://github.com/HatemIsmailShalaby1979/Blue-Waves-) — content studio
- [Full portfolio](https://github.com/HatemIsmailShalaby1979) — how this fits the wider work

### The other 2026 building attempts

- [WFM Forecasting Calculator](https://github.com/HatemIsmailShalaby1979/wfm-forecasting-calculator)
- [RTA Command Center](https://github.com/HatemIsmailShalaby1979/RTA_command_center)
- [CX Sentiment Sentinel](https://github.com/HatemIsmailShalaby1979/cx-sentiment-sentinel) — the repository name overpromises; the code is a KPI-decay risk scorer

## Author

**Hatem Ismail Shalaby** — Operations Architect · AI Systems Engineer · Founder

- GitHub: [HatemIsmailShalaby1979](https://github.com/HatemIsmailShalaby1979)
- LinkedIn: [hatem-shalaby-202902127](https://www.linkedin.com/in/hatem-shalaby-202902127/)
- Email: hatemshalaby2025@gmail.com
- Education: BSc Managerial Sciences (Computer Section), Sadat Academy for Management Sciences; Business Analytics Nanodegree, Udacity

Based in Al Obour City, Al-Qalyubia Governorate, Egypt.

## Licence

MIT
