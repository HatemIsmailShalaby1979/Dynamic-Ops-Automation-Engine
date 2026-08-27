# Dynamic Ops Automation Engine

Intake-to-operational-readiness pipeline. Transforms raw client requirements into a baseline Erlang C staffing schedule and a pre-built Notion SOP structure in under 60 minutes.

## What it does

1. **Client intake** ? Structured form captures requirements, constraints, volume profiles
2. **Erlang C engine** ? Calculates baseline staffing with shrinkage, occupancy targets, interval granularity
3. **Notion provisioning** ? Auto-creates SOP pages, runbooks, escalation matrices in client's Notion workspace
4. **Output package** ? Staffing model (Excel), SOP structure (Notion), implementation checklist

## Stack

- Python (openpyxl, pydantic, requests)
- Notion API
- YAML for configuration

## Status

**Private precursor to Helix Prime.** This logic was absorbed into Helix Prime's B2B Onboarding engine and WFM engine. Kept private for reference.

## License

Internal use only.