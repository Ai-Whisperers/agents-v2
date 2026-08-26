# Changelog — research package

## [0.2.0] — 2026-08-26

### Added
- Initial package split from `/opt/data/agents-v2/` mono-repo
- `agents/research-tracker/PROMPT.md` — lead agent (Sun 18:00 PYT thesis + publications + courses checkpoint)
- `agents/citation-checker/PROMPT.md` — pre-publication citation verification (on-demand)
- `agents/thesis-tracker/PROMPT.md` — daily 06:00 UTC fine-grained thesis tick
- `agents/course-producer/PROMPT.md` — weekly Sunday 10:00 PYT module production (HITL)
- `agents/okr-tracker/PROMPT.md` — weekly OKR progress + quarterly review
- `agents/funding-coordinator/PROMPT.md` — funding landscape weekly sweep + application tracking
- `schemas/research.schema.json` — state schema (thesis, publications, courses, monetization)
- `state/research.json.template` — empty state template
- `playbooks/research-education.md` — dept charter + 12 roles + monetization paths + knowledge mgmt
- `README.md` — install + agent list + skills to load
- `LICENSE` — MIT

### Source provenance
- Constitution: `constitution/05-research-education.md` (v0.2.0)
- Playbook: `playbooks/05-research-education.md`
- Agent specs: `agents-prompts/{research-tracker,citation-checker,thesis-tracker,course-producer,okr-tracker}.md`
- Funding-coordinator source: `agents/funding-coordinator/PROMPT.md` (cross-cutting Tier 2, kept under research per Q4 decision — Research owns policy, source-curator does mechanical)

### Compliance
- Trademark scan: clean (per `/opt/data/scripts/trademark-scan.py`)
- All `submit_arxiv`, `publish_course_module`, `publish_paper`, `git_force_push` hard-stop with `approved_human: ivan` (or `ivan+kiki` for course module)
