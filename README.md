# Dynamic Ops Automation Engine

> **Status: building attempt.** The intake, Erlang C, and Notion-provisioning stages
> run. The "under 60 minutes" end-to-end figure is a project target from June 2026,
> not a measured benchmark. Snapshot 2026-08-27.

A precursor to Helix Prime, from the May–June 2026 build period. The thinking
here was later absorbed into Helix Prime.

## What it does

An intake-to-operational-readiness pipeline. It turns raw client requirements into
a baseline Erlang C staffing schedule and a pre-built Notion SOP structure.

1. **Client intake**: structured form captures requirements, constraints, and volume profiles
2. **Erlang C engine**: baseline staffing with shrinkage, occupancy targets, and interval granularity
3. **Notion provisioning**: creates SOP pages, runbooks, and escalation matrices in a client Notion workspace
4. **Output package**: staffing model (Excel), SOP structure (Notion), and an implementation checklist

## What is verified, and what is not

| Item | Status |
|---|---|
| Client intake and Erlang C staffing calculation | Runs locally. |
| Notion provisioning | Runs against a Notion workspace with valid API credentials. |
| Excel output package | Runs locally. |
| "Under 60 minutes" end-to-end figure | Project target from June 2026. No recorded baseline, sample, or method. Not a measured benchmark. |
| External audit | None. |

## Stack

- Python (openpyxl, pydantic, requests)
- Notion API
- YAML configuration

## Run locally

Local setup steps are not recorded in this file. The repository contains a
Dockerfile and a GitHub Actions build-and-push workflow; the pipeline needs a
Notion API token to run the provisioning stage.

## Honest boundary

The pipeline needs a Notion API token and a workspace to do anything beyond the
staffing calculation. It produces a plan, not a running operation: nothing in it
delivers service, and the output is only as good as the requirements captured at
intake. It has no authentication layer of its own.

The environment templates `.env.production` and `.env.staging` are tracked. Every value in them is a placeholder, so no credential is
exposed, but tracking files with those names is a hygiene problem. It is listed as
outstanding in the portfolio security audit.

This is not a production deployment claim. There is no external audit, no
certified data isolation, and no signed security review. No revenue has been
realised.

## Related work

- [Helix Prime](https://github.com/HatemIsmailShalaby1979/Helix-Prime) — the operations core
- [Helix Education](https://github.com/HatemIsmailShalaby1979/Helix-Education) — event-sourced learning engine
- [Study Studio](https://github.com/HatemIsmailShalaby1979/Study-Studio) — local-first AI tutor
- [L&D Command Center](https://github.com/HatemIsmailShalaby1979/L-D-Command-Center) — desktop learning and career workstation
- [Blue Waves](https://github.com/HatemIsmailShalaby1979/Blue-Waves-) — content studio
- [LIVE Support Assistant](https://github.com/HatemIsmailShalaby1979/LIVE-Support-Assistant) — explainable support prototype
- [Full portfolio](https://github.com/HatemIsmailShalaby1979) — how this project fits the wider work

### The 2026 building attempts

- [WFM Forecasting Calculator](https://github.com/HatemIsmailShalaby1979/wfm-forecasting-calculator)
- [RTA Command Center](https://github.com/HatemIsmailShalaby1979/RTA_command_center)
- [CX Sentiment Sentinel](https://github.com/HatemIsmailShalaby1979/cx-sentiment-sentinel)

## Author

**Hatem Ismail Shalaby** — Operations Architect · AI Systems Engineer · Founder

- GitHub: [HatemIsmailShalaby1979](https://github.com/HatemIsmailShalaby1979)
- LinkedIn: [hatem-shalaby-202902127](https://www.linkedin.com/in/hatem-shalaby-202902127/)
- Email: hatemshalaby2025@gmail.com
- Education: BSc Managerial Sciences (Computer Section), Sadat Academy for Management Sciences; Business Analytics Nanodegree, Udacity

Based in Al Obour City, Al-Qalyubia Governorate, Egypt.

## Licence

MIT
