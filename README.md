# IRAS Triage Demo

Interactive proof-of-concept demonstrating an agentic compliance workflow for the Inland Revenue Authority of Singapore (IRAS), built around the ACRA Business Registry dataset.

## What it shows

A three-column dashboard simulating how an AI agent processes new ACRA company registrations and surfaces decisions for a human compliance officer:

| Column | Role |
|---|---|
| **ACRA Registry Feed** | Live intake of new UEN registrations from data.gov.sg |
| **Agent Reasoning Stream** | Timestamped log of the AI agent's tool calls, thoughts, and evaluations |
| **Officer Triage Queue** | Human-in-the-loop review queue — cases the agent escalates for officer sign-off |

## Demo flow

1. Click **Run Daily ACRA Ingest** to trigger the agent
2. Watch the agent process 4 UENs in real time:
   - **Alpha Tech Solutions** → clean profile, routed to onboarding
   - **Apex Shell Logistics / Zenith Trade Singapore / Quantum Holding Group** → same address, same date → flagged as shell network cluster
3. Review cases in the triage queue:
   - Onboarding case → approve a pre-drafted welcome letter to the director
   - High-risk case → read the agent's investigation brief, review and edit two notices (to ACRA Registry + company directors), then dispatch

## Agent logic

The agent applies three deterministic tool calls per entity:

```
get_new_acra_registrations()
check_internal_iras_register(uen)
detect_address_clustering(postal_code)
```

Business rules:
- UEN not in IRAS register → new entity → onboarding pipeline
- 3+ companies at same postal code on same date → shell network flag → halt + escalate

## Stack

Single self-contained `index.html` — no build step, no dependencies. Deploy to any static host (GitHub Pages, Netlify, Vercel).

## Deploy

```bash
# GitHub Pages (after cloning)
# Enable Pages in repo Settings → Pages → Branch: main / root
```
