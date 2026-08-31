# Changelog — finance package

All notable changes to the Finance & Legal department package are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.2.0] — 2026-08-26

### Added
- Initial package split from `/opt/data/agents-v2/` mono-repo
- `agents/finance-controller/PROMPT.md` — weekly close + runway + contracts
- `agents/accounting-automation/PROMPT.md` — daily expense categorization + invoice generation
- `agents/tax-receipt-tracker/PROMPT.md` — weekly receipt capture + quarterly tax summary (Paraguay DNIT/SET/IRP/IVA/RUC)
- `agents/procurement-tracker/PROMPT.md` — vendor renewals + new vendor evaluation
- `agents/compliance-monitor/PROMPT.md` — regulatory changes + trademark banlist enforcement
- `schemas/finance.schema.json` — state schema (runway, mrr, deals_open, compliance_flags, renewals)
- `state/finance.json.template` — empty state template
- `playbooks/finance-legal.md` — department charter + roles + SOPs + pricing benchmarks
- `README.md` — install instructions + agent list + skills to load
- `LICENSE` — MIT

### Source provenance
- Constitution: `constitution/02-finance-legal.md` (v0.2.0)
- Playbook: `playbooks/04-finance-legal.md`
- Agent specs: `agents-prompts/{finance-controller,accounting-automation,tax-receipt-tracker,procurement-tracker,compliance-monitor}.md`

### Compliance
- Trademark scan: clean (per `/opt/data/scripts/trademark-scan.py`)
- All `send_*`, `sign_*`, `apply_*` actions hard-stop with `require_approval: true` and `approved_human: ivan` (or `ivan+kiki` for vendor > $50/mo)
- EU client contracts: HARD-STOP until Compliance Officer role filled (per D3)
