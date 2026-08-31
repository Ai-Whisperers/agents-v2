# Operations Package — AI Whisperers Agents

Standalone deployable package for the **Operations** department.
Pull this when a customer wants cross-repo work tracking, daily business
snapshots, AI-ops monitoring, OKR rollups, source-materials curation, and
founder-bandwidth monitoring without the rest of the org.

> **Version**: 0.2.0
> **Source**: split from `/opt/data/agents-v2/` on 2026-08-26
> **License**: MIT
> **Department head**: Ivan

---

## What's in this package

### Agents included (6)

| Agent | Class | Schedule | Mission |
|-------|-------|----------|---------|
| `management-coordinator` | OPERATIONAL | Mon+Thu 17:00 PYT | Cross-repo stuck/stale/PR review |
| `business-analyst` | OPERATIONAL | Daily 06:30 PYT | Pipeline / revenue / sites snapshot |
| `ai-ops-coordinator` | OPERATIONAL | Daily 09:00 PYT | Agent-layer health, eval gates, drift |
| `bizops-tracker` | OPERATIONAL | Sun 17:00 PYT | Cross-functional analytics, OKRs |
| `source-curator` | OPERATIONAL | Sun 09:00 PYT | source-materials/ freshness sweep |
| `founder-bandwidth-watchdog` | OPERATIONAL | Sun 18:00 PYT | Burnout signal detection |

### Skills to load

- `aiw-ops-discipline` — operational tone, validation discipline
- `aiw-git-safety` — git safety rules
- `diagramming` — architecture diagrams for OKR viz
- `github-auto-merge-permissive-protection` — branch protection
- `org-repo-audit` — repo inventory
- `trademark-compliance-scrub` — public output safety
- `research-integrity-protocol` — citation discipline (for source-curator)

### Files

```
operations/
├── README.md
├── LICENSE
├── CHANGELOG.md
├── agents/
│   ├── management-coordinator/PROMPT.md
│   ├── business-analyst/PROMPT.md
│   ├── ai-ops-coordinator/PROMPT.md
│   ├── bizops-tracker/PROMPT.md
│   ├── source-curator/PROMPT.md
│   └── founder-bandwidth-watchdog/PROMPT.md
├── schemas/
│   └── coord.schema.json
├── state/
│   └── coord.json.template
└── playbooks/
    └── operations.md
```

---

## Install

```bash
# 1. Copy
cp -r packages/operations/ /opt/data/agents/operations-package/

# 2. Install skills
hermes skills install aiw-ops-discipline
hermes skills install aiw-git-safety
hermes skills install github-auto-merge-permissive-protection
hermes skills install org-repo-audit
hermes skills install trademark-compliance-scrub
hermes skills install research-integrity-protocol

# 3. Init state
cp /opt/data/agents/operations-package/state/coord.json.template /opt/data/agents/state/coord.json

# 4. Wire cron
hermes cron add management-coordinator     "0 21 * * 1,4"   # Mon+Thu 17:00 PYT
hermes cron add business-analyst           "30 10 * * *"    # Daily 06:30 PYT
hermes cron add ai-ops-coordinator         "0 13 * * *"     # Daily 09:00 PYT
hermes cron add bizops-tracker             "0 21 * * 0"     # Sun 17:00 PYT
hermes cron add source-curator             "0 13 * * 0"     # Sun 09:00 PYT
hermes cron add founder-bandwidth-watchdog "0 22 * * 0"     # Sun 18:00 PYT

# 5. Verify
python3 /opt/data/scripts/trademark-scan.py /opt/data/agents/operations-package/
```

---

## Hard rules

- **Operations is the "objetivo-department"**: it doesn't ship products, it makes sure every other dept can ship.
- **Edit `ORG-AGENTS.md`**: Ivan only
- **Force-push any repo**: Ivan only
- **All `comment_on_issue`, `close_issue`, `add_source`, `retire_source`**: HITL with `approved_human: ivan`
- **Caps**: `open_stuck ≤ 10`, `decisions_for_ivan ≤ 3` (rolling)

---

## Cron cadence (PYT, UTC-4)

| Time | What |
|------|------|
| 06:00 | morning-brief |
| 06:30 | business-analyst |
| Every 15 min | health.sh watchdog |
| Every 15 min | site-health (live HTTP checks) |
| Every 15 min (off) / 30 min (on) | cron-heartbeat |
| Every 15 min | validate-state.py |
| Every 6 hours | state-snapshot.sh |
| Hourly | cost-cap |
| 09:00 | ai-ops-coordinator |
| Mon+Thu 17:00 | management-coordinator |
| Tue+Fri 17:00 | engineering-roster (handoff) |
| Fri 17:00 | kiki-coach |
| Sat/Sun weekly | bizops-tracker, source-curator, founder-bandwidth-watchdog |

---

## Cross-references

- Constitution: `/opt/data/agents-v2/constitution/01-operations.md`
- Playbook: `/opt/data/agents-v2/playbooks/01-operations.md`
- Master index: `/opt/data/agents-v2/INDEX.md`
- Package index: `/opt/data/agents-v2/PACKAGE-INDEX.md`
