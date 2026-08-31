# Changelog — operations package

## [0.2.0] — 2026-08-26

### Added
- Initial package split from `/opt/data/agents-v2/` mono-repo
- `agents/management-coordinator/PROMPT.md` — cross-repo stuck/stale/PR review (Mon+Thu 17:00 PYT)
- `agents/business-analyst/PROMPT.md` — daily 06:30 PYT one-page brief (pipeline / revenue / sites)
- `agents/ai-ops-coordinator/PROMPT.md` — agent-layer health, eval gates, drift (daily 09:00 PYT)
- `agents/bizops-tracker/PROMPT.md` — weekly OKR progress + cross-functional snapshot
- `agents/source-curator/PROMPT.md` — weekly source-materials/ freshness sweep
- `agents/founder-bandwidth-watchdog/PROMPT.md` — weekly burnout signal detection
- `schemas/coord.schema.json` — state schema (open_stuck, stale_repos, decisions_for_ivan)
- `state/coord.json.template` — empty state template
- `playbooks/operations.md` — dept charter + role matrix + cron cadence + handoff matrix
- `README.md` — install instructions + agent list + skills to load
- `LICENSE` — MIT

### Source provenance
- Constitution: `constitution/01-operations.md` (v0.2.0)
- Playbook: `playbooks/01-operations.md`
- Agent specs: `agents-prompts/{management-coordinator,business-analyst,ai-ops-coordinator,bizops-tracker,source-curator,founder-bandwidth-watchdog}.md`

### Compliance
- Trademark scan: clean (per `/opt/data/scripts/trademark-scan.py`)
- All `comment_on_issue`, `close_issue`, `add_source`, `retire_source` actions hard-stop with `require_approval: true` and `approved_human: ivan`
