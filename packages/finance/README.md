# Finance & Legal Package — AI Whisperers Agents

Standalone deployable package for the **Finance & Legal** department of AI Whisperers.
Pull this package when a customer wants the cash-tracking, contract-management, tax,
procurement, and compliance-monitoring agents without the rest of the org.

> **Version**: 0.2.0
> **Source**: split from `/opt/data/agents-v2/` on 2026-08-26
> **License**: MIT
> **Department head**: Ivan

---

## What's in this package

### Agents included (5)

| Agent | Class | Schedule | Mission |
|-------|-------|----------|---------|
| `finance-controller` | OPERATIONAL | Fri 18:00 PYT | Weekly close, runway, contracts |
| `accounting-automation` | OPERATIONAL | Daily 07:00 PYT | Expense categorization, invoice generation |
| `tax-receipt-tracker` | OPERATIONAL | Sun 08:00 PYT | Receipt capture, Paraguay DNIT/SET quarterly summary |
| `procurement-tracker` | OPERATIONAL | Mon 09:00 PYT | Vendor renewals, new vendor evaluation |
| `compliance-monitor` | OPERATIONAL | Mon 08:00 PYT | Regulatory watch, trademark banlist enforcement |

### Skills to load

Install these skills from the Hermes skill library before running the package:

- `paraguai-proposal-pricing` — invoice templates + pricing multipliers
- `trademark-compliance-scrub` — public artifact compliance
- `prospect-dossier-pii-sanitization` — PII handling
- `aiw-ops-discipline` — completion + validation discipline

### Files

```
finance/
├── README.md                                  ← this file
├── LICENSE                                    ← MIT
├── CHANGELOG.md                               ← version history
├── agents/
│   ├── finance-controller/PROMPT.md           ← lead agent
│   ├── accounting-automation/PROMPT.md
│   ├── tax-receipt-tracker/PROMPT.md
│   ├── procurement-tracker/PROMPT.md
│   └── compliance-monitor/PROMPT.md
├── schemas/
│   └── finance.schema.json                    ← state schema
├── state/
│   └── finance.json.template                  ← empty state template
└── playbooks/
    └── finance-legal.md                       ← dept charter + SOPs + pricing
```

---

## Install

### 1. Copy the package

```bash
cp -r packages/finance/ /opt/data/agents/finance-package/
cd /opt/data/agents/finance-package/
```

### 2. Install required skills

```bash
# From the Hermes skills library
hermes skills install paraguai-proposal-pricing
hermes skills install trademark-compliance-scrub
hermes skills install prospect-dossier-pii-sanitization
hermes skills install aiw-ops-discipline
```

### 3. Initialize state

```bash
cp state/finance.json.template /opt/data/agents/state/finance.json
# Edit deals_open, mrr_usd, burn_usd_monthly with your actuals
```

### 4. Wire cron jobs

Each agent has its schedule in its `PROMPT.md` YAML frontmatter. Register with:

```bash
hermes cron add finance-controller   "0 21 * * 5"   # Fri 18:00 PYT
hermes cron add accounting-automation "0 11 * * *"  # Daily 07:00 PYT (PYT=UTC-4)
hermes cron add tax-receipt-tracker  "0 12 * * 0"   # Sun 08:00 PYT
hermes cron add procurement-tracker  "0 13 * * 1"   # Mon 09:00 PYT
hermes cron add compliance-monitor   "0 12 * * 1"   # Mon 08:00 PYT
```

### 5. Verify

```bash
python3 /opt/data/scripts/trademark-scan.py /opt/data/agents/finance-package/
# Expected: ✓ CLEAN
```

---

## Hard rules (re-stated from the playbook)

- **Currency**: USD primary; PYG when contract is in Guaraníes (note FX rate)
- **Trademark scrub**: run on every external-facing artifact before publish
- **EU client contracts**: HARD-STOP until Compliance Officer role filled (per D3)
- **New vendor > $50/mo**: requires Ivan + Kiki joint approval
- **Sign any contract**: Ivan only

---

## Pricing benchmarks (Paraguay dental / legal)

| Tier | Dental (Gs.) | Legal multiplier | Legal (USD) |
|------|--------------|------------------|-------------|
| Quick-Win | 500K setup + 150K/mo | ~3x | 1.5K setup + 550/mo |
| Standard | 1.2M setup + 400K/mo | ~3x | 2K setup + 1.3K/mo |
| Premium | 2.5M setup + 900K/mo | ~3x | 4.5K setup + 2.5K/mo |
| Enterprise | — | bespoke | 9K setup + 2.5K/mo |

---

## Cross-references

- Constitution source: `/opt/data/agents-v2/constitution/02-finance-legal.md`
- Playbook source: `/opt/data/agents-v2/playbooks/04-finance-legal.md`
- Master index: `/opt/data/agents-v2/INDEX.md`
- Package index: `/opt/data/agents-v2/PACKAGE-INDEX.md`
