# Sales & Growth Package — AI Whisperers Agents

Standalone deployable package for the **Sales & Growth** department.
Pull this when a customer wants lead capture, enrichment, ICP scoring,
outreach drafting, proposal generation, and pipeline analytics without
the rest of the org.

> **Version**: 0.2.0
> **Source**: split from `/opt/data/agents-v2/` on 2026-08-26
> **License**: MIT
> **Department head**: Ivan

---

## What's in this package

### Agents included (6)

| Agent | Class | Schedule | Mission |
|-------|-------|----------|---------|
| `sales-pipeline` | CONTENT | Daily 12:00 PYT | Inbound triage + ICP scoring + outreach drafts (HITL) |
| `proposal-drafter` | CONTENT | On-demand | Drafts proposals after discovery call (HITL) |
| `lead-enrichment` | OPERATIONAL | Daily 08:00 PYT | Adds intent signals + scores ICP match |
| `marketing-content-producer` | CONTENT | Mon/Wed/Fri | Blog posts, LinkedIn content, case studies (HITL) |
| `multimedia-producer` | CONTENT | On-demand | Video scripts, podcast outlines, graphics (HITL) |
| `revops-pipeline-analyzer` | OPERATIONAL | Daily 11:00 PYT | Funnel metrics + bottleneck detection |

### Skills to load

- `b2b-cold-outreach-pitch` — ICP definitions + outreach templates
- `paraguai-proposal-pricing` — pricing benchmarks + multipliers
- `prospect-dossier-pii-sanitization` — PII handling on lead dossiers
- `trademark-compliance-scrub` — public output safety
- `social-media` — content frameworks
- `creative` — diagrams, ASCII art for content
- `media` — image/audio generation

### Files

```
sales/
├── README.md
├── LICENSE
├── CHANGELOG.md
├── agents/
│   ├── sales-pipeline/PROMPT.md
│   ├── proposal-drafter/PROMPT.md
│   ├── lead-enrichment/PROMPT.md
│   ├── marketing-content-producer/PROMPT.md
│   ├── multimedia-producer/PROMPT.md
│   └── revops-pipeline-analyzer/PROMPT.md
├── schemas/
│   └── sales.schema.json
├── state/
│   └── sales.json.template
└── playbooks/
    └── sales-growth.md
```

---

## Install

```bash
# 1. Copy
cp -r packages/sales/ /opt/data/agents/sales-package/

# 2. Install skills
hermes skills install b2b-cold-outreach-pitch
hermes skills install paraguai-proposal-pricing
hermes skills install trademark-compliance-scrub
hermes skills install prospect-dossier-pii-sanitization

# 3. Init state
cp /opt/data/agents/sales-package/state/sales.json.template /opt/data/agents/state/sales.json

# 4. Wire cron
hermes cron add sales-pipeline           "0 16 * * *"   # 12:00 PYT
hermes cron add proposal-drafter         "on-demand"
hermes cron add lead-enrichment          "0 12 * * *"   # 08:00 PYT
hermes cron add marketing-content-producer "0 13 * * 1,3,5"  # Mon/Wed/Fri 09:00 PYT
hermes cron add multimedia-producer      "on-demand"
hermes cron add revops-pipeline-analyzer "0 15 * * *"   # 11:00 PYT

# 5. Verify
python3 /opt/data/scripts/trademark-scan.py /opt/data/agents/sales-package/
```

---

## ICPs (3 segments)

| ICP | Budget (USD) | Pain | Conversion path |
|-----|--------------|------|-----------------|
| Solo entrepreneur | $500-5K | Time poverty, no hire budget | Free resource → 15-min call → Quick-Win ($1.5K) |
| SME ops manager | $10K-100K | Process inefficiency, ROI pressure | Complimentary audit → 30-min strategy → Pilot ($10-25K) |
| Corporate innovation lead | $100K-500K+ | Legacy systems, board pressure | Confidential briefing → exec workshop → Enterprise |

## Conversion funnel targets

| Stage | Target |
|-------|--------|
| leads → calls | > 40% |
| calls → proposals | > 60% |
| proposals → signed | > 30% |
| Pipeline coverage | 3x quarterly target |

---

## Hard rules

- **Inbound-first** (D2): outbound deferred until 20+ inbound leads/week sustained 4 weeks
- **Trademark scrub** on every external-facing artifact before send
- **All `send_proposal`, `publish_post`, `apply_discount`, `send_external`**: HITL with `approved_human: ivan`
- **Proposal > $5K**: Ivan + Kiki together
- **Discount > 15% off list**: Ivan only

---

## Cross-references

- Constitution: `/opt/data/agents-v2/constitution/03-sales-growth.md`
- Playbook: `/opt/data/agents-v2/playbooks/02-sales-growth.md`
- Master index: `/opt/data/agents-v2/INDEX.md`
- Package index: `/opt/data/agents-v2/PACKAGE-INDEX.md`
