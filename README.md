# AI Whisperers — GROW Coaching Product (`growth-coaching`)

> **This repo is the customer-facing GROW coaching product.**
> AI Whisperers delivers trilingual GROW coaching (EN/ES/NL) to founders, lawyers, dentists, and executives.
> The internal AIW org layer (departments, ops, monitoring, DEMIURGE framework) lives in
> [`Ai-Whisperers/aiw-org`](https://github.com/Ai-Whisperers/aiw-org) — the sister repo.

---

## What this repo is

The **sellable** AI Whisperers product line — 6 distributable packages that customers can pull:

| Package | Department head | Status |
|---|---|---|
| [`packages/coaching/`](packages/coaching/) | Ivan + Kiki (co-owned) | **Active** — kiki-coach, course-producer, conversion-funnel, coaching-customers, thesis-tracker |
| [`packages/finance/`](packages/finance/) | Ivan | Distributable |
| [`packages/sales/`](packages/sales/) | Ivan | Distributable |
| [`packages/operations/`](packages/operations/) | Ivan | Distributable |
| [`packages/engineering/`](packages/engineering/) | Kiki | Distributable |
| [`packages/research/`](packages/research/) | Ivan | Distributable |

## Service tiers

| Tier | Price (USD) | Price (PY) | Includes |
|---|---|---|---|
| S (Quick-win) | Free | Free | 30-min GROW session |
| **M (Growth)** | **$500/mo** | **$300/mo** | 4 weekly GROW + brief + monthly retro |
| L (Transformation) | $1500/mo | $900/mo | M + 2x/month intensive + Sunstein ethics audit |

**Languages:** EN / ES / NL
**Methodology:** GROW + CLEAR + Sunstein ethics + ICF competencies
**Channels:** WhatsApp + Email + Zoom

## What's NOT in this repo

| Concern | Repo | Why |
|---|---|---|
| Internal AIW org (departments, ops, monitoring) | [`Ai-Whisperers/aiw-org`](https://github.com/Ai-Whisperers/aiw-org) | Different audience (internal), different lifecycle (continuous) |
| DEMIURGE agent framework | [`Ai-Whisperers/aiw-org`](https://github.com/Ai-Whisperers/aiw-org) | Org framework, not product framework |
| Production cron jobs + state files | (live at runtime, not in repo) | Must never leak into the product code |
| Customer PII | (never in repo) | Privacy |

## Repo layout

```
README.md                  ← you are here
packages/                  ← 6 distributable packages (per-dept)
community/                 ← 3 LATAM-targeted customer-facing files
dashboard/                 ← 1 dashboard config
state/                     ← 9 runtime state mirrors (read-only)
plans/                     ← 0 files (reserved for future plans)
backups/                   ← 1 historical backup
```

## Sister repo

[`Ai-Whisperers/aiw-org`](https://github.com/Ai-Whisperers/aiw-org) — the internal AIW org layer. It contains:
- 47 production agents (T1 leads + T2 sub + T3 cross-cutting + T4 monitoring + T5 coaching)
- 6 Tier-1 dept charters + 16-dept taxonomy
- DEMIURGE framework + 24 named agent souls
- 81 DEMIURGE tickets
- 25 production scripts (cron-sync, eval-gate, build-org-state, webhook-receiver, coach-onboarding-poller, etc.)
- 25 tests, 9 patterns, 13 playbooks

The two repos share infrastructure (cron sync, BWS secrets, Hermes runtime).

---

## How to deploy a package for a customer

1. **Pick the right package** — see the table above; pick one that matches their use case
2. **Copy the package directory** — `cp -r packages/<dept> ~/customer-deploy/`
3. **Configure** — set `WHATSAPP_TOKEN`, `BWS_*` env vars per the package's `README.md`
4. **Deploy** — `./install-hooks.sh`, then start the cron daemon
5. **Monitor** — see the package's `playbooks/` for operational runbook

---

## See also

- [`Ai-Whisperers/aiw-org`](https://github.com/Ai-Whisperers/aiw-org) — sister repo (internal org layer)
- Each package's `README.md` — package-specific deployment guide
- Each package's `playbooks/` — operational runbook