# Coaching Package — AI Whisperers Agents

Standalone deployable package for the **Coaching** product line.
Pull this when a customer wants the kiki-coach weekly lesson pipeline,
thesis-active daily ticks, course module production, coaching-customer
lifecycle management, and the coaching conversion funnel — without
pulling in sales/finance/engineering agents.

> **Version**: 0.2.0
> **Source**: split from `/opt/data/agents-v2/` on 2026-08-26
> **License**: MIT
> **Department head**: Ivan + Kiki (co-owned)

---

## What's in this package

### Agents included (5)

| Agent | Class | Schedule | Mission |
|-------|-------|----------|---------|
| `kiki-coach` | CONTENT | Fri 17:00 PYT | Weekly lesson for Kyrian (Spanish by default) |
| `thesis-tracker` | OPERATIONAL | Daily 06:00 UTC | Pick next pending task; advance thesis by 1 task/day |
| `course-producer` | CONTENT | Sun 10:00 PYT | One course module per week (slides + transcript + worksheet) |
| `coaching-customers` | OPERATIONAL | Daily 09:00 PYT | Coaching customer lifecycle (14-agent matrix reference) |
| `conversion-funnel` | OPERATIONAL | Daily 10:00 PYT | Coaching conversion funnel: free resource → 15-min call → Quick-Win |

### Skills to load (18 coaching skills)

The coaching product references these 18 skills (ship with the Hermes skill library):

| # | Skill | Purpose |
|---|-------|---------|
| 1 | `coaching-pitch-kit` | 3-sentence opener + 5 vertical pitches |
| 2 | `coaching-pricing` | S/M/L tiers + PYG/USD/EUR handling |
| 3 | `coaching-tech-stack` | Production stack review for coaching |
| 4 | `coaching-privacy-protocol` | EU data handling for coaching sessions |
| 5 | `coaching-eu-compliance` | EU AI Act + GDPR compliance |
| 6 | `coaching-conversation-framework` | GROW + CLEAR + Sunstein informed-consent backbone |
| 7 | `coaching-agent-debugging` | Diagnostic patterns for misbehaving coaching agents |
| 8 | `coaching-agent-oversight` | Workflow for reviewing coaching agent quality |
| 9 | `coaching-coach-network` | Recruit / train / supervise / pay human coaches |
| 10 | `coaching-onboarding-emails` | Day 1, 3, 7, 10, 30 email templates |
| 11 | `coaching-roi-measurement` | Quantify ROI of AI coaching engagements |
| 12 | `coaching-quality-reviewer-methodology` | Cron reviewer auditing eval-gate brief quality |
| 13 | `coaching-trilingual-glossary` | Trilingual coaching vocab (es/en/nl) — 100+ terms |
| 14 | `coaching-vertical-playbook` | Selling/scoping/delivering AI coaching per vertical |
| 15 | `sunstein-ethics-review` | Informed-consent + nudge + sludge framework |
| 16 | `sunstein-prompt-library` | 15 reusable Sunstein/Solstein prompt templates |
| 17 | `solstein-pipeline-runner` | CLI scoring rubric (1-10) for client fit |
| 18 | `solstein-lite-deploy` | Lightweight coaching deployment template |

### Other skills to load

- `thesis-active-autonomy` — active autonomy protocol
- `thesis-autonomous-tick-discipline` — tick discipline
- `academic-thesis-paper-first` — thesis structure
- `evaluating-llms-harness` — eval methodology
- `data-science` — research data
- `media` — image/audio generation for course slides
- `creative` — design
- `aiw-ops-discipline` — operational discipline

### Files

```
coaching/
├── README.md
├── LICENSE
├── CHANGELOG.md
├── agents/
│   ├── kiki-coach/PROMPT.md
│   ├── thesis-tracker/PROMPT.md
│   ├── course-producer/PROMPT.md
│   ├── coaching-customers/PROMPT.md          ← 14-agent matrix reference
│   └── conversion-funnel/PROMPT.md
├── schemas/
│   └── people.schema.json
├── state/
│   └── people.json.template
└── playbooks/
    └── people-culture.md
```

---

## Install

```bash
# 1. Copy
cp -r packages/coaching/ /opt/data/agents/coaching-package/

# 2. Install all 18 coaching skills
hermes skills install coaching-pitch-kit coaching-pricing coaching-tech-stack   coaching-privacy-protocol coaching-eu-compliance coaching-conversation-framework   coaching-agent-debugging coaching-agent-oversight coaching-coach-network   coaching-onboarding-emails coaching-roi-measurement coaching-quality-reviewer-methodology   coaching-trilingual-glossary coaching-vertical-playbook sunstein-ethics-review   sunstein-prompt-library solstein-pipeline-runner solstein-lite-deploy

# 3. Install supporting skills
hermes skills install thesis-active-autonomy academic-thesis-paper-first

# 4. Init state
cp /opt/data/agents/coaching-package/state/people.json.template /opt/data/agents/state/people.json

# 5. Wire cron
hermes cron add kiki-coach        "0 21 * * 5"   # Fri 17:00 PYT
hermes cron add thesis-tracker    "0 6 * * *"    # Daily 06:00 UTC
hermes cron add course-producer   "0 14 * * 0"   # Sun 10:00 PYT
hermes cron add coaching-customers "0 13 * * *"  # Daily 09:00 PYT
hermes cron add conversion-funnel  "0 14 * * *"  # Daily 10:00 PYT

# 6. Verify
python3 /opt/data/scripts/trademark-scan.py /opt/data/agents/coaching-package/
```

---

## Kiki-coach curriculum (11 topics)

1. Git rebase vs. merge in a 2-person team
2. Reading a Next.js App Router stack trace
3. Writing a CODEOWNERS file that actually owns
4. Env vars: when .env.local vs GitHub Actions secret vs CF Worker
5. Tailwind v4 design tokens vs inline styles
6. Reading a CF Worker trace — KV, R2, subrequest limits
7. Docker Swarm deploy logs: the 5 lines that matter
8. Pre-commit hooks: husky + lint-staged + what to actually lint
9. **Agent ops**: PROMPT.md patterns (hard stops, idempotency)
10. **Eval gates**: golden trajectories for agent testing
11. **Cron schedules**: PYT/UTC, off-hours density

## Coaching conversion funnel

| Stage | Mechanic |
|-------|----------|
| Awareness | Free resource (vertical playbook, glossary) |
| 15-min call | Discovery (Solstein-pipeline-runner scoring rubric 1-10) |
| Pilot | Quick-Win tier (1-3 sessions, $500-1.5K) |
| Standard | Tier 2 ($2-4K setup + $400-800/mo) |
| Premium | Tier 3 ($5K+ setup + $1.5K+/mo) |

## Cultural artifacts (PRESERVE)

Per `06-people-culture.md` lines 68-75:
1. First signed contract in new ICP → LinkedIn post (Sales drafts, Ivan approves)
2. Thesis chapter published → celebration
3. Major deploy win → engineering notes
4. Kiki milestone → kiki-coach notes in next lesson

**These are NOT gamified metrics. They're rituals.**

---

## Burnout signal spec

- **Hours**: 70+ hrs/wk sustained 3 weeks → page Ivan
- **Sentiment**: 2+ burnout keywords in 14d → check-in
- **Deadlines**: 5+ P0/P1 in 1 week → ALERT
- **Latency**: > 4 hrs avg sustained 3 days → ALERT

---

## Hard rules

- **Kiki picks lesson topic**: Kiki
- **Hire contractor > $500/mo**: Ivan + Kiki joint sign-off
- **PTO**: Person themselves
- **Recognize milestone (public post)**: Person being recognized
- **All `publish_module`, `submit_arxiv`, `git_force_push`**: HITL with `approved_human: ivan` (or `ivan+kiki` for module)

---

## Cross-references

- Constitution: `/opt/data/agents-v2/constitution/06-people-culture.md`
- Playbook: `/opt/data/agents-v2/playbooks/06-people-culture.md`
- Burnout spec: `/opt/data/agents-v2/BURNOUT-SIGNAL-SPEC.md`
- Master index: `/opt/data/agents-v2/INDEX.md`
- Package index: `/opt/data/agents-v2/PACKAGE-INDEX.md`
