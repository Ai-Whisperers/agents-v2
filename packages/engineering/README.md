# Engineering & Delivery Package — AI Whisperers Agents

Standalone deployable package for the **Engineering & Delivery** department.
Pull this when a customer wants deploy health monitoring, PR review,
QA automation, security scanning, AI safety, and chaos testing without
the rest of the org.

> **Version**: 0.2.0
> **Source**: split from `/opt/data/agents-v2/` on 2026-08-26
> **License**: MIT
> **Department head**: Kiki (CTO)

---

## What's in this package

### Agents included (6)

| Agent | Class | Schedule | Mission |
|-------|-------|----------|---------|
| `engineering-roster` | OPERATIONAL | Tue+Fri 17:00 PYT | Deploy health, PR review queue, Kiki workload |
| `devops-monitor` | OPERATIONAL | Every 30 min | Docker Swarm + Traefik + CF Worker health (silent on green) |
| `qa-automation-runner` | OPERATIONAL | on-PR | Run test suite + coverage gate (95% lines / 90% branches) |
| `security-watchdog` | OPERATIONAL | Every 30 min | Credential exposure + auth log monitoring |
| `ai-safety-engineer` | OPERATIONAL | Every 30 min | OWASP LLM Top 10 + hard-stop verification + weekly chaos test |
| `chaos-test-runner` | OPERATIONAL | Sun 03:00 PYT | Weekly chaos tests CT-1 (LLM down), CT-2 (corrupt state), CT-3 (bad tool response) |

### Skills to load (18 skills)

- `aiw-deploy-discipline` — verify topology before deploy
- `aiw-git-safety` — git safety discipline
- `client-site-deploy` — single site deploy
- `client-site-build-workflow` — greenfield site build
- `cloudflare-tunnel-zero-trust-expose` — CF tunnels
- `code-hygiene-ci-gardening` — lint/format/CI
- `devops` — general DevOps
- `evolution-api-destructive-ops` — bridge security
- `github-pr-workflow` — PR lifecycle
- `github-code-review` — review PRs
- `github-auto-merge-permissive-protection` — GH admin
- `live-site-triage` — site outage triage
- `mcp` — MCP server setup
- `red-teaming` — adversarial testing
- `supabase-2026-secret-proxy` — Supabase edge proxy
- `vps-aiw-autonomous-ops` — VPS ops
- `vps-aiw-client-sites` — audit live sites
- `vps-aiw-deploy-pipeline` — CF Worker + R2
- `vps-aiw-dns-fix` — DNS troubleshooting
- `vps-aiw-static-deploy` — static sites
- `vps-knowledge` — VPS knowledge

### Files

```
engineering/
├── README.md
├── LICENSE
├── CHANGELOG.md
├── agents/
│   ├── engineering-roster/PROMPT.md
│   ├── devops-monitor/PROMPT.md
│   ├── qa-automation-runner/PROMPT.md
│   ├── security-watchdog/PROMPT.md
│   ├── ai-safety-engineer/PROMPT.md
│   └── chaos-test-runner/PROMPT.md
├── schemas/
│   └── engineering.schema.json
├── state/
│   └── engineering.json.template
└── playbooks/
    └── engineering-delivery.md
```

---

## Install

```bash
# 1. Copy
cp -r packages/engineering/ /opt/data/agents/engineering-package/

# 2. Install skills (the deployment-critical ones first)
hermes skills install aiw-deploy-discipline aiw-git-safety
hermes skills install vps-aiw-deploy-pipeline vps-aiw-static-deploy vps-aiw-dns-fix
hermes skills install github-pr-workflow github-code-review github-auto-merge-permissive-protection
hermes skills install cloudflare-tunnel-zero-trust-expose live-site-triage
hermes skills install red-teaming evolution-api-destructive-ops
hermes skills install code-hygiene-ci-gardening devops mcp
hermes skills install supabase-2026-secret-proxy vps-knowledge vps-aiw-autonomous-ops
hermes skills install vps-aiw-client-sites client-site-deploy client-site-build-workflow

# 3. Init state
cp /opt/data/agents/engineering-package/state/engineering.json.template /opt/data/agents/state/engineering.json

# 4. Wire cron
hermes cron add engineering-roster    "0 21 * * 2,5"   # Tue+Fri 17:00 PYT
hermes cron add devops-monitor        "*/30 * * * *"    # Every 30 min
hermes cron add qa-automation-runner  "on-pr"           # GH webhook
hermes cron add security-watchdog     "*/30 * * * *"    # Every 30 min
hermes cron add ai-safety-engineer    "*/30 * * * *"    # Every 30 min
hermes cron add chaos-test-runner     "0 7 * * 0"       # Sun 03:00 PYT

# 5. Verify
python3 /opt/data/scripts/trademark-scan.py /opt/data/agents/engineering-package/
```

---

## Stack reality

| Layer | Tech |
|-------|------|
| Primary VPS | Hostinger (38.9.96.179) — 32GB RAM, 387GB disk |
| Secondary VPS | Servarica Host A |
| Reverse proxy | Traefik v3.5.3 (auto-LE) |
| Orchestrator | Docker Swarm (NOT K8s) |
| Static deploys | CF Worker + R2 |
| Forbidden | Vercel 403 — DO NOT attempt deploys |

## AI Safety protocol (per OWASP LLM Top 10 2026)

- **Hard stops** — enforced via `hard-stop-wrapper.py` at runtime
- **Eval gates** — golden trajectories + auto-eval
- **Prompt injection** — all untrusted input sanitized
- **Excessive agency** — LLM cannot bypass hard stops
- **Chaos tests**: CT-1 (LLM down), CT-2 (corrupt state), CT-3 (bad tool response)

---

## Hard rules

- **Merge PR (no breaking changes)**: Kiki or designated reviewer
- **Merge PR (schema change, infra)**: Kiki + Ivan
- **Hotfix deploy to prod**: Kiki (logged, Ivan notified)
- **Rollback**: Kiki (logged)
- **New tool < $50/mo**: Kiki
- **New tool > $50/mo**: Kiki + Ivan
- **Disable hard-stop wrapper**: require Ivan + Kiki
- **Modify eval-gate ground truth**: require Ivan
- **Force-push any repo**: Ivan only

---

## Cross-references

- Constitution: `/opt/data/agents-v2/constitution/04-engineering-delivery.md`
- Playbook: `/opt/data/agents-v2/playbooks/03-engineering-delivery.md`
- Threat model: `/opt/data/agents-v2/THREAT-MODEL.md`
- Failure modes: `/opt/data/agents-v2/FAILURE-MODES.md`
- Master index: `/opt/data/agents-v2/INDEX.md`
- Package index: `/opt/data/agents-v2/PACKAGE-INDEX.md`
