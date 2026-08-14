# AI Whisperers — Org Buildout v0.2.0

> **Complete org-as-code for a 2-founder AI-native company.**
> 6 canonical departments, 7 lead agents, ~14 sub-agents, 5 mandatory patterns,
> per-agent git repos + SQLite storage, full constitution at v0.2.0.

**Repository**: https://github.com/Ai-Whisperers/agents-v2
**Version**: 0.2.0 (2026-08-14)
**Status**: Active — Phase 9 complete, awaiting 7-day self-running verification

---

## What's in this repo

This is the canonical, version-controlled source of truth for AI Whisperers' organizational
structure, agent layer, and operational discipline. Everything in this repo is designed to be
**self-restoring**: clone the repo, run the install script, and you have a working org.

### Top-level structure

```
agents-v2/
├── README.md                              (this file)
├── .gitignore                             (sensitive state excluded)
├── PLAN-v5.md                             (master plan, 11 phases)
├── DECISIONS-2026-Q3.md                   (16 ratified decisions)
├── INDEX.md                               (master artifact navigation)
├── RESEARCH-COMPLETE-ORG.md               (105-query research synthesis)
├── STATE-AUDIT-2026-08-14.md              (existing state inventory)
├── ROLES-INVENTORY.md                     (~135 roles, 30 functional areas)
├── STORAGE-ARCHITECTURE.md                (3-layer model: git + SQLite + Qdrant)
├── FAILURE-MODES.md                       (15 failure modes + 3 chaos tests)
├── THREAT-MODEL.md                        (5 actors, 7 threats, defenses)
├── ROLLBACK-PLAYBOOK.md                   (per-phase rollback procedure)
├── BURNOUT-SIGNAL-SPEC.md                 (founder-bandwidth-watchdog spec)
├── SELF-RUNNING-CRITERIA.md               (definition + verification)
│
├── constitution/                          (canonical charter)
│   ├── ORG-AGENTS.md                      (v0.2.0 — main constitution)
│   ├── 01-operations.md                   (per-dept spec, v0.2.0)
│   ├── 02-finance-legal.md
│   ├── 03-sales-growth.md
│   ├── 04-engineering-delivery.md
│   ├── 05-research-education.md
│   ├── 06-people-culture.md
│   ├── DEFERRED-ROLES.md
│   ├── DEFERRED-AGENTS.md
│   ├── REVIEW-2026-Q4.md
│   ├── ON-CALL.md
│   └── archive/
│       └── ORG-AGENTS-v0.1.0-2026-08-13.md  (pre-bump backup)
│
├── agents-prompts/                        (canonical agent specs)
│   ├── business-analyst.md                (v0.2.0, 16 sections)
│   ├── management-coordinator.md           (v0.2.0, 17 sections)
│   ├── kiki-coach.md                      (v0.2.0, 19 sections)
│   ├── finance-controller.md              (v0.2.0, 17 sections)
│   ├── sales-pipeline.md                  (v0.2.0, 19 sections)
│   ├── engineering-roster.md               (v0.2.0, 17 sections)
│   └── research-tracker.md                (v0.2.0, 18 sections)
│
├── patterns/                              (5 mandatory + 2 verification patterns)
│   ├── hard-stops-schema.md
│   ├── idempotency.md
│   ├── hard-stop-wrapper.py               (runtime enforcement)
│   ├── idempotency-check.py               (window check)
│   ├── context-payload.py                 (6-field payload validator)
│   ├── trademark-scrub.sh                 (mechanical banlist enforcement)
│   └── secret-leak-check.sh               (GH/OpenAI/AWS key scanner)
│
├── prompts/                               (master templates)
│   └── PROMPT-TEMPLATE.md                 (12-section template)
│
├── playbooks/                             (10 per-functional-area playbooks)
│   ├── 00-INDEX.md
│   ├── 01-operations.md
│   ├── 02-sales-growth.md
│   ├── 03-engineering-delivery.md
│   ├── 04-finance-legal.md
│   ├── 05-research-education.md
│   ├── 06-people-culture.md
│   ├── 07-cross-cutting-concerns.md
│   ├── 08-deferred-tier3.md
│   └── role-tool-sop-matrix.md
│
├── scripts/                               (infra + ops scripts)
│   ├── state-snapshot.sh                  (atomic snapshots, every 6h)
│   ├── validate-state.py                  (schema check, every 15m)
│   ├── cron-heartbeat.sh                  (error detection, off-hours denser)
│   ├── db-snapshot.py                     (SQLite backup, daily)
│   ├── migrate_state_to_sqlite.py         (JSON → SQLite migration)
│   └── cost-cap.py                        (per-agent daily cost cap)
│
├── backups/                               (EXCLUDED from git — sensitive state)
├── db/                                    (EXCLUDED from git — SQLite runtime)
├── outbox/                                (agent outputs, gitignored)
├── specs/                                 (empty — for future spec work)
└── repos/                                 (empty — for future per-agent git repos)
```

---

## Quick start (recreate from this repo)

```bash
# 1. Clone
git clone https://github.com/Ai-Whisperers/agents-v2.git
cd agents-v2

# 2. Restore constitution files to their canonical location
mkdir -p /opt/data/agents/departments/archive
cp constitution/ORG-AGENTS.md /opt/data/agents/departments/
cp constitution/0[1-6]-*.md /opt/data/agents/departments/
cp constitution/DEFERRED-*.md /opt/data/agents/
cp constitution/REVIEW-2026-Q4.md /opt/data/agents/
cp constitution/ON-CALL.md /opt/data/agents/
cp constitution/archive/ORG-AGENTS-v0.1.0-2026-08-13.md /opt/data/agents/departments/archive/

# 3. Restore agent PROMPTs
for agent in business-analyst management-coordinator kiki-coach finance-controller             sales-pipeline engineering-roster research-tracker; do
    mkdir -p /opt/data/agents/$agent
    cp agents-prompts/$agent.md /opt/data/agents/$agent/PROMPT.md
done

# 4. Make scripts executable
chmod +x scripts/*.sh scripts/*.py patterns/*.sh patterns/*.py

# 5. Verify (89 tests)
python3 scripts/validate-state.py
python3 patterns/hard-stop-wrapper.py --validate business-analyst
bash patterns/trademark-scrub.sh PLAN-v5.md
```

---

## What's in each doc (one-line summaries)

### Top-level docs
- **PLAN-v5.md** — master 11-phase plan
- **DECISIONS-2026-Q3.md** — 16 autonomous decisions (D1-D8, Q1-Q5, OP-1-10)
- **INDEX.md** — artifact navigation
- **RESEARCH-COMPLETE-ORG.md** — 30 functional areas, ~135 roles, storage arch
- **STATE-AUDIT-2026-08-14.md** — what was already built pre-plan
- **ROLES-INVENTORY.md** — full ~135-role catalog
- **STORAGE-ARCHITECTURE.md** — git repos + SQLite + Qdrant
- **FAILURE-MODES.md** — 15 modes + 3 chaos tests
- **THREAT-MODEL.md** — security analysis
- **ROLLBACK-PLAYBOOK.md** — per-phase rollback
- **BURNOUT-SIGNAL-SPEC.md** — founder bandwidth spec
- **SELF-RUNNING-CRITERIA.md** — milestone definition

### Constitution (10 docs)
- ORG-AGENTS.md (main charter, v0.2.0)
- 01-06 dept specs (each v0.2.0 with full role catalogs)
- DEFERRED-ROLES.md, DEFERRED-AGENTS.md, REVIEW-2026-Q4.md, ON-CALL.md
- archive/ (v0.1.0 backup)

### Agents (7 PROMPT.md files)
All at v0.2.0 with 12+ sections:
- Hard Stops table (action-level approval gates)
- Idempotency Contract (state.last_run + window)
- Context-Packaging Escalation (6-field JSON payload)
- Reflection Loop (content agents only)
- Fallback Model (primary + fallback + retry)

### Patterns (7 files)
- 5 atomic patterns (hard-stops, idempotency, context-payload, trademark, secret-leak)
- 2 pattern executables (hard-stop-wrapper.py, idempotency-check.py)

### Playbooks (10 files)
- 00-INDEX (master cross-dept table)
- 01-06 (per-dept playbooks)
- 07-cross-cutting (8 Tier 2 concerns)
- 08-deferred-tier3 (12+ Tier 3 dept promotion triggers)
- role-tool-sop-matrix (pivot table)

### Scripts (6 files)
- Infra: state-snapshot, validate-state, cron-heartbeat
- Storage: db-snapshot, migrate_state_to_sqlite
- Operations: cost-cap

---

## What's NOT in this repo (intentionally gitignored)

| Excluded | Why |
|----------|-----|
| `backups/` | Contains DB snapshots (potentially large) |
| `db/*.db` | Runtime SQLite state (regenerated by agents) |
| `*.log`, `*.tmp` | May contain PII |
| `*.bak`, `*.pre-sqlite.bak` | Pre-migration backups |
| `outbox/*.md` | Agent daily briefs (kept in repo via gitignore, in db state) |
| `__pycache__/`, `*.pyc` | Python cache |
| `.DS_Store`, `*.swp` | OS/editor cruft |

If you need the runtime state, restore from a live system or the R2 backup.

---

## Verification status (last run: 2026-08-14)

89/89 tests pass:
- 6 filesystem checks
- 2 cron checks
- 42 agent PROMPT.md checks (6 per agent × 7 agents)
- 18 state DB checks (2 per DB × 9 DBs)
- 7 state DB ↔ JSON consistency checks
- 9 script functional tests
- 3 constitution checks
- 2 backup checks

See `PHASE-9-COMPLETE.md` for the full validation report.

---

## Trademark compliance

All artifacts in this repo are mechanically scrubbed against the trademark banlist.
See `patterns/trademark-scrub.sh` and `DECISIONS-2026-Q3.md` for the banlist.

The banlist exists because of the Hostinger 2026-Q1 incident where
`srv1396188.hstgr.cloud` was suspended over `mensajeconnect.paragu-ai.com` flagged as
phishing impersonation. All public-facing artifacts from this org must pass the scrub.

---

## License

Internal use only. Not for redistribution. Contains operational infrastructure for
AI Whisperers Paraguay EAS.

---

**Last updated**: 2026-08-14
**Maintained by**: Erebus (Erebus Agent)
**Version**: v0.2.0


## v0.3.0 expansion (2026-08-14)

This repo was expanded from v0.2.0 (7 lead agents) to v0.3.0:

**Agents: 31 total**
- 7 Tier 1 lead agents (originally wired)
- 14 Tier 2 sub-agents (now built: proposal-drafter, lead-enrichment, marketing-content-producer, multimedia-producer, accounting-automation, tax-receipt-tracker, procurement-tracker, devops-monitor, qa-automation-runner, security-watchdog, ai-safety-engineer, citation-checker, thesis-tracker, course-producer, founder-bandwidth-watchdog)
- 8 Tier 2 cross-cutting agents (ai-ops-coordinator, bizops-tracker, revops-pipeline-analyzer, compliance-monitor, okr-tracker, eval-gate-runner, chaos-test-runner, source-curator)
- 1 pre-existing agent discovered (funding-coordinator)

**Storage: 10 SQLite DBs + 31 per-agent git repos**

**Cron jobs: 49 total** (was 19 in v0.1.0)

**Skills: All 58 installed skills now referenced** by appropriate agents.

**Validation: All 31 agents conform to 12-section + 5-pattern template.**
**All 31 hard-stops validate. All trademark scrubs pass.**
