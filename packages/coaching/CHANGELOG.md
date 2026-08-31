# Changelog — coaching package

## [0.2.0] — 2026-08-26

### Added
- Initial package split from `/opt/data/agents-v2/` mono-repo
- `agents/kiki-coach/PROMPT.md` — weekly Friday 17:00 PYT lesson for Kyrian (Spanish by default)
- `agents/thesis-tracker/PROMPT.md` — daily 06:00 UTC thesis progress tick
- `agents/course-producer/PROMPT.md` — weekly Sunday 10:00 PYT module producer (HITL)
- `agents/coaching-customers/PROMPT.md` — coaching customer lifecycle (14-agent matrix reference)
- `agents/conversion-funnel/PROMPT.md` — coaching conversion funnel (free resource → 15-min call → Quick-Win)
- `schemas/people.schema.json` — state schema (kiki lesson streak, founder bandwidth, milestones)
- `state/people.json.template` — empty state template
- `playbooks/people-culture.md` — dept charter + 11-topic curriculum + burnout signal spec
- `README.md` — install + agent list + 18 coaching skills reference
- `LICENSE` — MIT

### Skills to load (18 total)
See README for the full list of 18 coaching skills (pitch-kit, pricing, EU compliance, conversation-framework, etc.).

### Source provenance
- Constitution: `constitution/06-people-culture.md` (v0.2.0)
- Playbook: `playbooks/06-people-culture.md`
- Agent specs: `agents-prompts/{kiki-coach,thesis-tracker,course-producer}.md`

### Compliance
- Trademark scan: clean (per `/opt/data/scripts/trademark-scan.py`)
- `publish_module`, `git_force_push`, `submit_arxiv` hard-stop with `approved_human: ivan` (or `ivan+kiki` for module publish)
