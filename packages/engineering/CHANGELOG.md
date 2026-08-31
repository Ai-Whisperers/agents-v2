# Changelog — engineering package

## [0.2.0] — 2026-08-26

### Added
- Initial package split from `/opt/data/agents-v2/` mono-repo
- `agents/engineering-roster/PROMPT.md` — lead agent (Tue+Fri 17:00 PYT)
- `agents/devops-monitor/PROMPT.md` — Docker Swarm + Traefik + CF Worker health (every 30 min)
- `agents/qa-automation-runner/PROMPT.md` — PR-triggered test suite + coverage gate
- `agents/security-watchdog/PROMPT.md` — credential exposure + auth log monitoring (every 30 min)
- `agents/ai-safety-engineer/PROMPT.md` — OWASP LLM Top 10 + hard-stop verification (every 30 min)
- `agents/chaos-test-runner/PROMPT.md` — weekly chaos tests CT-1/CT-2/CT-3
- `schemas/engineering.schema.json` — state schema (deploys_7d, open_prs, incidents, kiki_commits)
- `state/engineering.json.template` — empty state template
- `playbooks/engineering-delivery.md` — dept charter + role matrix + stack reality + AI Safety protocol
- `README.md` — install + agent list + skills to load (18 skills)
- `LICENSE` — MIT

### Source provenance
- Constitution: `constitution/04-engineering-delivery.md` (v0.2.0)
- Playbook: `playbooks/03-engineering-delivery.md`
- Agent specs: `agents-prompts/{engineering-roster,devops-monitor,qa-automation-runner,security-watchdog,ai-safety-engineer,chaos-test-runner}.md`

### Compliance
- Trademark scan: clean (per `/opt/data/scripts/trademark-scan.py`)
- All `merge_pr`, `deploy_prod`, `rotate_credential`, `disable_hardstop`, `modify_eval_gates` hard-stop with `approved_human: kiki` or `ivan+kiki`
