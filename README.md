# Dynamic Ops Automation Engine

> **Status: building attempt.** The intake, Erlang C, and Notion-provisioning stages
> run. The repository is public on GitHub. The "under 60 minutes" end-to-end figure
> is a project target from June 2026, not a measured benchmark. Snapshot
> 2026-08-27.

One of the four building attempts from May–June 2026 — the period when I left a
twenty-eight-year operations career and started building full time, alone, while
teaching myself to write software. The thinking here was later absorbed into
Helix Prime.

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

## Visibility and licence correction

An earlier version of this file described the repository as "Kept private for
reference" and licensed "Internal use only". Both statements were inaccurate. The
repository is public on GitHub and returns HTTP 200 to unauthenticated requests.
The private and internal-use labels have been removed. The canonical licence for
this portfolio is MIT, stated below.

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

The environment templates `.env.production` and `.env.staging` are tracked in this
public repository. Every value in them is a placeholder, so no credential is
exposed, but tracking files with those names is a hygiene problem. It is listed as
outstanding in the portfolio security audit.

This is not a production deployment claim. There is no external audit, no
certified data isolation, and no signed security review. No revenue has been
realised.

## The founder's story

I spent twenty-eight years in operations. The first fourteen were the
foundation: ground operations and real-time traffic management at Hurghada
International Airport, then Air Berlin, where I directed ground operations
through the 2011 regional transition and held SLA compliance under conditions
that had no playbook. Alongside that, international logistics at Shorouk
International Bookshop and hybrid IT operations at Nefertari American School.

The second fourteen were about automation. I built AI-driven automation for
contact centres at ByteDance, Vodafone and Uber: NLP pipelines that turn
unstructured customer language into signal, Erlang C forecasting that turns
volume into staffing, and the reporting layers that made both usable by people
on the floor. The hard part was never the model. It was the handover — who owns
the decision, what evidence supports it, and what happens when the system is
wrong.

In April 2026 I left that career and started building full time — alone, and
teaching myself to write software as I went. The first four tools were published
six weeks later, in May and June 2026. Each one took a single operational problem
and solved it properly. They were not impressive. They were correct.

Those four tools converged into one idea: **Helix Codex**, an accountable AI
operating organization. Not an autonomous agent. An organization with a
constitution, named roles with bounded authority, evidence trails, and a human at
every consequential boundary. Helix Prime is its operations core.

Dynamic Ops Automation Engine is one of the four building attempts. It is
maintained by one person, with no team and no funding. It has not been externally
audited and it has not made revenue. Where it is unfinished, this document says
so.

## Related work

- [Helix Prime](https://github.com/HatemIsmailShalaby1979/Helix-Prime) — the operations core
- [Helix Education](https://github.com/HatemIsmailShalaby1979/Helix-Education) — event-sourced learning engine
- [Study Studio](https://github.com/HatemIsmailShalaby1979/Study-Studio) — local-first AI tutor
- [L&D Command Center](https://github.com/HatemIsmailShalaby1979/L-D-Command-Center) — desktop learning and career workstation
- [Blue Waves](https://github.com/HatemIsmailShalaby1979/Blue-Waves-) — content studio
- [LIVE Support Assistant](https://github.com/HatemIsmailShalaby1979/LIVE-Support-Assistant) — explainable support prototype
- [Full portfolio](https://github.com/HatemIsmailShalaby1979) — the front door

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
