# Research & Education Package — AI Whisperers Agents

Standalone deployable package for the **Research & Education** department.
Pull this when a customer wants thesis progress tracking, citation verification,
course module production, publication pipeline, funding program tracking, and
OKR rollups — without pulling in sales/finance/engineering agents.

> **Version**: 0.2.0
> **Source**: split from `/opt/data/agents-v2/` on 2026-08-26
> **License**: MIT
> **Department head**: Ivan

---

## What's in this package

### Agents included (6)

| Agent | Class | Schedule | Mission |
|-------|-------|----------|---------|
| `research-tracker` | CONTENT | Sun 18:00 PYT | Thesis + publications + courses weekly checkpoint |
| `citation-checker` | CONTENT | On-demand | Verifies every citation before external publication |
| `thesis-tracker` | OPERATIONAL | Daily 06:00 UTC | Fine-grained thesis progress (autonomous tick) |
| `course-producer` | CONTENT | Sun 10:00 PYT | One course module per week (slides + transcript + worksheet) |
| `okr-tracker` | OPERATIONAL | Sun 17:00 PYT | Weekly OKR progress + quarterly review |
| `funding-coordinator` | OPERATIONAL | Mon 09:00 UTC | Funding landscape weekly sweep + application tracking |

### Skills to load

- `thesis-active-autonomy` — active autonomy protocol
- `thesis-autonomous-tick-discipline` — tick discipline
- `academic-thesis-paper-first` — thesis structure
- `evaluating-llms-harness` — eval methodology
- `data-science` — research data
- `research` — research methods
- `research-integrity-protocol` — methodology rigor + citation grounding
- `grounded-citations` — citation discipline
- `media` — image/audio generation for course slides
- `creative` — design
- `aiw-ops-discipline` — operational discipline

### Files

```
research/
├── README.md
├── LICENSE
├── CHANGELOG.md
├── agents/
│   ├── research-tracker/PROMPT.md
│   ├── citation-checker/PROMPT.md
│   ├── thesis-tracker/PROMPT.md
│   ├── course-producer/PROMPT.md
│   ├── okr-tracker/PROMPT.md
│   └── funding-coordinator/PROMPT.md
├── schemas/
│   └── research.schema.json
├── state/
│   └── research.json.template
└── playbooks/
    └── research-education.md
```

---

## Install

```bash
# 1. Copy
cp -r packages/research/ /opt/data/agents/research-package/

# 2. Install skills
hermes skills install thesis-active-autonomy academic-thesis-paper-first
hermes skills install grounded-citations research-integrity-protocol
hermes skills install evaluating-llms-harness data-science
hermes skills install research aiw-ops-discipline

# 3. Init state
cp /opt/data/agents/research-package/state/research.json.template /opt/data/agents/state/research.json

# 4. Wire cron
hermes cron add research-tracker    "0 22 * * 0"   # Sun 18:00 PYT
hermes cron add citation-checker    "on-demand"
hermes cron add thesis-tracker      "0 6 * * *"    # Daily 06:00 UTC
hermes cron add course-producer     "0 14 * * 0"   # Sun 10:00 PYT
hermes cron add okr-tracker         "0 21 * * 0"   # Sun 17:00 PYT
hermes cron add funding-coordinator "0 9 * * 1"    # Mon 09:00 UTC (weekly sweep)

# 5. Verify
python3 /opt/data/scripts/trademark-scan.py /opt/data/agents/research-package/
```

---

## Monetization paths

| Asset | Path | Status |
|-------|------|--------|
| 20-pattern agentic framework | MIT license → GitHub stars → consulting leads | Live (agentic-schemas repo) |
| Thesis (P1 GeoData v2) | arXiv preprint → journal → academic consulting | In flight |
| ParaguAI Builder | SaaS product | 5+ live tenants |
| Agent org framework | Open-source template → 1-person-AI-company course | Drafted |
| Multi-agent BPM research | Position paper at 2026 Workshop on AI for BPM | Drafted |

---

## Knowledge Management sub-function

- **Owner**: Research dept owns the policy
- **Mechanical curator**: `source-curator` agent (Tier 2) — lives in operations package
- **Cadence**: Weekly freshness sweep
- **Trigger to ship source-curator**: source-materials/ > 50 files (currently ~30)
- **Trigger to promote KM to standalone dept**: > 100 files OR second knowledge-heavy vertical

---

## Hard rules

- **Thesis chapter sign-off**: Ivan
- **Submit to arXiv / conference**: Ivan (research-tracker drafts cover letter)
- **Publish course module**: Ivan + Kiki (technical review)
- **Open-source the agentic framework updates**: Ivan
- **Accept invited talk / podcast**: Ivan
- **License research IP to external party**: Ivan + Kiki
- **Add/retire source-materials**: Ivan (per source-curator recommendation)
- **Modify curriculum**: require Kiki (charter)
- **All `submit_arxiv`, `publish_course_module`, `publish_paper`, `git_force_push`**: HITL with `approved_human: ivan` (or `ivan+kiki` for module)

---

## Cross-references

- Constitution: `/opt/data/agents-v2/constitution/05-research-education.md`
- Playbook: `/opt/data/agents-v2/playbooks/05-research-education.md`
- Master index: `/opt/data/agents-v2/INDEX.md`
- Package index: `/opt/data/agents-v2/PACKAGE-INDEX.md`
