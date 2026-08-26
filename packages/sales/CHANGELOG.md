# Changelog — sales package

## [0.2.0] — 2026-08-26

### Added
- Initial package split from `/opt/data/agents-v2/` mono-repo
- `agents/sales-pipeline/PROMPT.md` — lead agent (daily inbound triage + ICP scoring)
- `agents/proposal-drafter/PROMPT.md` — drafts proposals after discovery call (HITL)
- `agents/lead-enrichment/PROMPT.md` — daily enrichment + ICP scoring
- `agents/marketing-content-producer/PROMPT.md` — Mon/Wed/Fri content drafts (HITL)
- `agents/multimedia-producer/PROMPT.md` — video/podcast/graphic specs (HITL)
- `agents/revops-pipeline-analyzer/PROMPT.md` — funnel metrics + bottleneck detection
- `schemas/sales.schema.json` — state schema (leads_in_flight, funnel_30d, outreach_queue, stalled_deals)
- `state/sales.json.template` — empty state template
- `playbooks/sales-growth.md` — dept charter + ICPs + conversion funnel targets + tooling
- `README.md` — install instructions + agent list + skills to load
- `LICENSE` — MIT

### Source provenance
- Constitution: `constitution/03-sales-growth.md` (v0.2.0)
- Playbook: `playbooks/02-sales-growth.md`
- Agent specs: `agents-prompts/{sales-pipeline,proposal-drafter,lead-enrichment,marketing-content-producer,multimedia-producer,revops-pipeline-analyzer}.md`

### Compliance
- Trademark scan: clean (per `/opt/data/scripts/trademark-scan.py`)
- All `send_*`, `publish_*`, `apply_discount`, `modify_pricing` actions hard-stop with `require_approval: true`
- Inbound-first per D2 (outbound DEFERRED until 20+ inbound leads/week sustained 4 weeks)
