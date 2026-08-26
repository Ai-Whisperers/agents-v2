# Customer Template — Reusable Deployment Skeleton

> **Last updated:** 2026-08-26 (v0.1.0)
> **Companion to:** `TOOLING-TIERS.md`. Read that first to understand what the customer is buying.
> **Source docs:** `/opt/data/agents/ORG-AGENTS.md`, `/opt/data/agents-v2/PHASE-13-COMPLETE-UPDATED-PLAN.md`,
> `/opt/data/agents/research/200-ai-coaching-companies.md`,
> `/opt/data/agents-v2/docs/COMPLETE-EXPLANATION.md`,
> `paraguayan-client-preengagement` skill, `client-site-kickoff` skill,
> `vertical-client-extension-playbook` skill.
> **Why this exists:** the August 13, 2026 transcription surfaced the missing piece — *"Should be a
> template that customers can use later. 'Oh, you want to have marketing? Okay, you want to have these
> roles, which one do you want to have automated?' And then AI does its best."* This doc is that template.

---

## 1. How the template fits in the deploy pipeline

```
Customer signs Tier (1, 2, or 3)
            │
            ▼
1. INTAKE  ──►   200-question structured form (this doc §2)
            │     - identity, profile, services, ops, web, content, SEO, marketing, security
            │
            ▼
2. CONFIG  ──►   Configuration knobs (this doc §3)
            │     - which agents on/off
            │     - vertical preset (legal / dental / beauty / RE / e-commerce)
            │     - trilingual bundle
            │
            ▼
3. VERTICAL ──►  Vertical profiles (this doc §4)
            │     - role selection decision tree (this doc §5)
            │     - which roles per vertical are default-on
            │
            ▼
4. PRICING ──►   Pricing calculator (this doc §6)
            │     - input: headcount + verticals + add-ons
            │     - output: tier + setup fee + monthly
            │
            ▼
5. TIMELINE ──►  Onboarding timeline (this doc §7)
            │     - week 1 / month 1 / month 3
            │     - self-running milestone target
            │
            ▼
6. LIMITS  ──►   Customization limits (this doc §8)
                    - what's in scope, what's a separate SKU
```

---

## 2. Intake checklist (200-question pattern)

Mirrors the `client-site-kickoff` skill (10 sections × ~30 questions = 300 questions; AIW customer
template = 200 questions across 9 sections to avoid the casual "tell me everything" intake).

The schema for every question:

```json
{
  "id": "<SECTION>-<NN>",
  "category": "<sub-category>",
  "question": "<full question text>",
  "type": "text|textarea|select|boolean|tags|file|url|email|tel|range|number|date",
  "required": true,
  "default": null,
  "options": ["a", "b"],
  "example": "<example answer>",
  "hint": "<guidance for the client>",
  "accepted_formats": ["pdf", "jpg"]
}
```

### Section A — Identidad corporativa + perfil del fundador (20 Qs)

Identity, brand, founder profile. Drives the trilingual voice + the founder-as-Person JSON-LD.

| ID range | Topic | Count |
|----------|-------|-------|
| ID-01 to ID-08 | Razón social, denominaciones, marca, paleta, idioma operativo | 8 |
| ID-09 to ID-13 | Bio del fundador, matrículas, formación, idiomas | 5 |
| ID-14 to ID-20 | Visión, misión, valores, tagline, voz de marca | 7 |

### Section B — Servicios / oferta (25 Qs)

Vertical-specific services + pricing tier (per `TOOLING-TIERS.md` §5).

| ID range | Topic | Count |
|----------|-------|-------|
| SV-01 to SV-10 | Listado completo de servicios/productos | 10 |
| SV-11 to SV-15 | Pricing público (o "solicitar cotización"), descuentos, bundles | 5 |
| SV-16 to SV-20 | Garantías, SLA, política de devolución | 5 |
| SV-21 to SV-25 | Roadmap de servicios (próximos 6 meses) | 5 |

### Section C — Operaciones + equipo (25 Qs)

Drives the people-hr + ai-ops-coordinator setup + the cron schedule.

| ID range | Topic | Count |
|----------|-------|-------|
| OP-01 to OP-08 | Horarios, ubicación, canales de atención | 8 |
| OP-09 to OP-14 | Equipo actual: roles, headcount, nombres (opcional) | 6 |
| OP-15 to OP-20 | Herramientas ya en uso (Notion / Linear / Trello / Sheets / WA / etc.) | 6 |
| OP-21 to OP-25 | Pain points diarios que el customer quiere automatizar | 5 |

### Section D — Web, audiencia, KPIs (20 Qs)

Drives the static-site Worker + lead API per `client-site-kickoff` Step 4.

| ID range | Topic | Count |
|----------|-------|-------|
| WB-01 to WB-08 | URL actual, hosting, TLS, dominio | 8 |
| WB-09 to WB-13 | Audiencia objetivo, KPIs de negocio | 5 |
| WB-14 to WB-20 | Sitemap deseado, secciones prioritarias | 7 |

### Section E — Contenido + UX + microcopy (20 Qs)

Drives the marketing-content + multimedia-producer agents.

| ID range | Topic | Count |
|----------|-------|-------|
| CT-01 to CT-08 | Hero copy candidates, eslogan, prueba social | 8 |
| CT-09 to CT-13 | Testimonios disponibles, fotos (placeholders marcados) | 5 |
| CT-14 to CT-20 | Idioma del contenido (ES/EN/NL), tono de voz | 7 |

### Section F — SEO + legal + compliance (25 Qs)

Drives the compliance-monitor + trademark scrub at deploy time.

| ID range | Topic | Count |
|----------|-------|-------|
| SE-01 to SE-08 | Keywords objetivo, schema.org markup, sitemap.xml | 8 |
| SE-09 to SE-13 | LGPD / GDPR / EU AI Act / Ley 1682/01 (PY) — qué compliance aplica | 5 |
| SE-14 to SE-20 | Política de cookies, privacidad, disclaimers | 7 |
| SE-21 to SE-25 | Marca registrada, nombres protegidos, banlist propio del cliente | 5 |

### Section G — Marketing + comercial + conversión (20 Qs)

Drives the sales-pipeline + lead-enrichment + proposal-drafter agents.

| ID range | Topic | Count |
|----------|-------|-------|
| MK-01 to MK-08 | Tono, claims prohibidos, embudo | 8 |
| MK-09 to MK-13 | Automation permitido (emails / reminders / follow-ups) | 5 |
| MK-14 to MK-20 | Conversión objetivo (lead-to-customer %), ventana de tiempo | 7 |

### Section H — Seguridad + operaciones de TI (20 Qs)

Drives the security-auditor + eval-gate-runner + cron-secret hygiene.

| ID range | Topic | Count |
|----------|-------|-------|
| SC-01 to SC-08 | Hosting, TLS, backups, uptime SLA | 8 |
| SC-09 to SC-13 | 2FA, gestión de secretos, rotación de claves | 5 |
| SC-14 to SC-20 | Monitoring, alerting, runbook de incidentes | 7 |

### Section I — Roles del AI-employee (25 Qs)

Drives the role-selection decision tree (§5 below). The most productised section.

| ID range | Topic | Count |
|----------|-------|-------|
| AR-01 to AR-08 | ¿Qué departamentos querés activar? (financiero/ventas/ops/etc.) | 8 |
| AR-09 to AR-13 | Por cada departamento: ¿qué roles querés automatizar? | 5 |
| AR-14 to AR-20 | Por cada rol: ¿humano-en-loop o auto-run? | 7 |
| AR-21 to AR-25 | Coaching-as-producto: ¿se lo querés revender a tus clientes? | 5 |

**Total: 200 questions, 9 sections.** Stored under `customers/<slug>/intake/01-09-*.json` per the
`client-site-kickoff` schema.

---

## 3. Configuration knobs

After intake is submitted, these knobs control what ships. All knobs are version-pinned in
`customers/<slug>/config.yaml`.

```yaml
# customers/<slug>/config.yaml — customer deployment config (v0.1.0 schema)

# Tier selection (mutually exclusive)
tier: micro                # micro | small | medium

# Vertical preset (one or more; compound = +15% on price, see §6)
verticals:
  - legal                  # legal | dental | beauty | real_estate | ecommerce

# Language bundle
languages:
  primary: es              # es | en | nl
  secondary: en            # optional, included in Tier 2+
  tertiary: nl             # optional, included in Tier 3 only by default

# Agent-by-agent override (default: tier rule set)
agents:
  business-analyst:        # Tier 1 lead
    enabled: true
    class: HITL_AGENT      # FULL_AGENT | HITL_AGENT | CRON_WORKFLOW | HUMAN_ONLY
    cron: "30 10 * * *"    # daily 06:30 PYT (PYT = UTC-4)
    model: reasoning
    provider: litellm
    toolsets: [notion, whatsapp, sheets]
  sales-pipeline: { enabled: true, class: HITL_AGENT, cron: "0 13,16 * * *" }
  lead-enrichment: { enabled: true, class: CRON_WORKFLOW, cron: "30 9 * * *" }
  ai-ops-coordinator: { enabled: true, class: FULL_AGENT, cron: "0 8 * * *" }
  # ... etc. Each tier's agent manifest is templated from /opt/data/agents/ORG-AGENTS.md §1.

# Self-running target (per SELF-RUNNING-CRITERIA.md)
self_running:
  target_date: 2026-09-30  # 30 days post-deploy for micro, 14 for small, 7 for medium
  observation_window_days: 7

# Hard stops (always-on, inherited from vertical-client-extension-playbook)
hard_stops:
  trademark_banlist: enforce
  price_privacy: enforce
  no_fabrication: enforce
  pii_hard_stop: enforce
  no_private_repo_writes: enforce
  # Customer-specific additions go here (e.g. no_paid_social: enforce)

# Auth + secret storage
secrets:
  backend: bws             # bws (Bitwarden Secrets) | env-injected | vault
  rotation_days: 90

# Output channels
output_channels:
  morning_brief: email
  weekly_brief: whatsapp
  escalation_target: founder_email

# Eval-gate strictness (strict | warn | off)
eval_gate_strictness: strict

# Customisation limits (template — see §8)
limits:
  max_custom_agents: 0     # tier 1
  # tier 2: 2, tier 3: 10
  max_trilingual_content: true
  custom_branding: true
```

### 3.1 What changes per tier (config knobs)

| Knob | Tier 1 (default) | Tier 2 (adds) | Tier 3 (adds) |
|------|------------------|----------------|----------------|
| `agents.*.enabled` | 4 true, 43 false | 12 true, 35 false | 47 all true |
| `self_running.target_date` | deploy + 30d | deploy + 14d | deploy + 7d |
| `eval_gate_strictness` | strict | strict (cron-driven) | strict + trending |
| `secrets.backend` | env-injected | bws | bws + customer-VPC |
| `output_channels.escalation_target` | founder_email | founder_email + WhatsApp | founder_email + dedicated operator |
| `limits.max_custom_agents` | 0 | 2 | 10 |
| `languages.tertiary` | — | available | included |

---

## 4. Five vertical profiles

Each vertical presets default agent behaviour, KPI priorities, and tone. Compound verticals
(+15% per stack level) — e.g. `legal+dental` is one vertical at full price, plus 50% of a vertical
add-on.

### 4.1 Legal (PY + NL + EU)

**Source of authority:** Lex/RP legal site style (per `client-site-kickoff` §1 personas).

| Default-on | Default-off | Notes |
|------------|-------------|-------|
| `business-analyst`, `sales-pipeline`, `lead-enrichment`, `proposal-drafter` | `marketing-content` (tone restriction — legal cannot use ad copy) | |
| `compliance-monitor` (always-on) | `multimedia-producer` | |
| `citation-checker` (always-on legal citations) | | |
| `compliance-monitor` escalation: **URGENT** for `penal` practice areas (per `client-site-kickoff` §6.1 lead API Worker pattern — `URGENT <30 min, NORMAL <24h`) |

**KPI priority:** lead response time, scholarship-of-process, compliance incidents.

**Voice:** formal, restrained, evidence-first. Optional NL copy for Dutch-speaking clients.

### 4.2 Dental (PY + BR + AR)

**Source of authority:** clinical reference sites (Ometzdental weekly refresh in
`ORG-AGENTS.md` §1.6 — first client site shipped).

| Default-on | Default-off | Notes |
|------------|-------------|-------|
| `marketing-content` (always-on — content calendar) | `funding-coordinator` | |
| `multimedia-producer` (always-on — patient education videos) | `proposal-drafter` (SOWs rare) | |
| `lead-enrichment` (3 mins SLA on inbound) | | |
| `bizops-tracker` (recall + patient lifetime KPI) | | |

**KPI priority:** appointments booked, recall rate, patient reviews, treatment-plan conversion.

**Voice:** warm, educational, multilingual (ES/PT/EN).

### 4.3 Beauty / wellness (PY + BO + BR)

**Source of authority:** content-driven verticals (social-feed-driven).

| Default-on | Default-off | Notes |
|------------|-------------|-------|
| `marketing-content` (M-W-F cadence) | `compliance-monitor` (less regulatory load) | |
| `multimedia-producer` (always-on) | `funding-coordinator` | |
| `lead-enrichment` | `proposal-drafter` | |
| `coach-*` (optional — wellness verticals often buy coaching alongside) | | |

**KPI priority:** content engagement, booking conversion, repeat customer rate.

**Voice:** aspirational, sensory, before/after evidence.

**Restriction (NEW 2026-08-26):** beauty verticals must not auto-post to trademark-banned social
platforms. Marketing content drafted to customer's CMS for manual approval only.

### 4.4 Real estate (PY + AR + NL — Mark NL active prospect)

**Source of authority:** transaction-heavy vertical (closing-focused).

| Default-on | Default-off | Notes |
|------------|-------------|-------|
| `proposal-drafter` (heavy SOW volume) | `compliance-monitor` (in-house closer handles disclosures) | |
| `lead-enrichment` (high cadence) | `coach-*` | |
| `marketing-content` (listing descriptions) | `funding-coordinator` | |
| `citation-checker` (legal citations on listings) | | |

**KPI priority:** listings posted, qualified leads, transactions closed, average days-on-market.

**Voice:** direct, location-specific, evidence-led. NL copy required for Dutch-speaking prospects
(Mark NL per `200-ai-coaching-companies.md` preface).

### 4.5 E-commerce (PY + BR + global)

**Source of authority:** operational vertical (lots of catalog data, returns, refunds).

| Default-on | Default-off | Notes |
|------------|-------------|-------|
| `accounting-automation` (always-on — refund-heavy) | `coach-*` | |
| `lead-enrichment` | `proposal-drafter` (catalog-driven, not SOW) | |
| `marketing-content` (M-W-F product highlights) | | |
| `tax-receipt-tracker` (weekly) | | |
| `bizops-tracker` (LTV, AOV, refund rate KPI) | | |

**KPI priority:** AOV, refund rate, repeat customer %, cart-abandon recovery rate.

**Voice:** transactional, scannable, plain language. Heavily localised ES/PT depending on
primary market.

---

## 5. Decision tree — "What roles do you want automated?"

This is the **core template interaction** from the August 13 quote: *"you want to have marketing,
which roles do you want automated?"* Below is the flow per department.

```
START — Customer has selected a department
        │
        ▼
Q1. ¿Cuántas horas por semana gasta el customer en este departamento?
   ├─ <2h/wk   → RESPUESTA = "Skip this department"
   ├─ 2-10h/wk → Q2
   └─ >10h/wk  → Q2 + suggest Tier ≥ 2

Q2. ¿Hay variabilidad semanal en el trabajo?
   ├─ Alta (cada cliente es distinto) → Q3 HUMAN-IN-LOOP
   └─ Baja (rutina repetible)        → Q4 AUTO-RUN

Q3. ¿Quién aprueba el output? (humano-en-loop)
   ├─ Founder                              → class: HITL_AGENT
   ├─ Department manager                   → class: HITL_AGENT + assign approver
   └─ Cliente final (no approval step)     → class: FULL_AGENT + disclaimer

Q4. ¿Qué pasa si el agent falla?
   ├─ Sales-blocking → class: HITL_AGENT + escalation=HIGH
   ├─ Compliance-blocking → class: HITL_AGENT + escalation=CRITICAL
   └─ Cosmetic-only → class: FULL_AGENT + escalation=LOW
```

### 5.1 Department-specific role-selections

Once the customer has answered Q1-Q4 per department, they get a per-role checklist drawn from
`/opt/data/agents-v2/ROLES-INVENTORY.md` (~135 roles; default-on per vertical in §4):

#### Marketing department (6 roles — choose 1-6)

- ☐ **Content Marketing Manager** (Marketing Manager de contenido) — editorial calendar
- ☐ **Marketing Manager** — estrategia y mix de canales
- ☐ **SEO Specialist** — keyword research + technical SEO
- ☐ **Email Marketing Specialist** — lifecycle email + drip
- ☐ **Brand Manager** — brand identity, voice
- ☐ **Growth Marketer** — experimentation, A/B

#### Sales department (6 roles — choose 1-6)

- ☐ **SDR (Sales Development Rep)** — outbound, qualification
- ☐ **Account Executive (AE)** — closing
- ☐ **Proposal Writer** — SOWs y cotizaciones
- ☐ **Sales Engineer** — technical pre-sales
- ☐ **Customer Success Manager (CSM)** — post-sale retention
- ☐ **Channel Sales Manager** — referral + integrations

#### Finance department (4 roles — choose 1-4)

- ☐ **Bookkeeper** — AP/AR, expense categorization
- ☐ **Tax Specialist** — quarterly filings
- ☐ **Procurement Officer** — vendor sourcing
- ☐ **FP&A Analyst** — forecasting + budgets

#### Engineering department (4 roles — choose 1-4)

- ☐ **DevOps / SRE** — infrastructure, CI/CD
- ☐ **QA Engineer** — testing + eval
- ☐ **Frontend / Backend / Full-stack** (pick one) — client-side / server-side / both
- ☐ **AI Safety Engineer** — hard-stop enforcement (recommended Tier 3)

#### People department (3 roles — choose 1-3)

- ☐ **Performance Coach** — coaching individual
- ☐ **Recognition Lead** — milestone rituals
- ☐ **Head of People / VP HR** — hiring + comp

#### Operations department (4 roles — choose 1-4)

- ☐ **Operations Lead** — day-to-day
- ☐ **Repo Steward** — GitHub hygiene
- ☐ **Watchdog Engineer** — cron liveness + alerting
- ☐ **Compliance Watchdog** — regulatory + trademark

#### Legal department (3 roles — choose 1-3)

- ☐ **Legal Counsel** — contract review, IP (external contractor)
- ☐ **Compliance Officer** — GDPR / LGPD / EU AI Act
- ☐ **Contract Drafter** — NDAs, MSAs, SOWs

#### Multimedia department (3 roles — choose 1-3)

- ☐ **Multimedia Producer** — image / video / audio
- ☐ **Brand Manager** — voice + visual identity
- ☐ **Performance Marketing Manager** — *NOT available on trademark-banned platforms*

### 5.2 Default-on per vertical (covers ≥3 roles by default)

| Vertical | Default-on departments + roles |
|----------|--------------------------------|
| **Legal** | Operations + Legal + Finance (compliance + tax) — 4 roles default-on |
| **Dental** | Marketing + Sales + Multimedia — 4 roles default-on |
| **Beauty** | Marketing + Multimedia + Sales — 4 roles default-on |
| **RE** | Sales + Operations + Legal — 4 roles default-on |
| **E-commerce** | Finance + Marketing + Sales + Operations — 5 roles default-on |

After default-on, customer is asked: *"Anything else?"* — every additional role is at the per-role
rate from the calculator (§6).

---

## 6. Pricing calculator

Inputs the customer provides in the intake form:

| Input | Type | Example |
|-------|------|---------|
| `headcount` | int | 8 |
| `verticals[]` | enum list | `[legal]` |
| `selected_roles[]` | enum list | `[content_marketing, sdr, lead_enrichment, compliance_monitor]` |
| `tier` | enum | `small` |
| `languages[]` | enum list | `[es, en]` |
| `addons[]` | enum list | `[trilingual_content, dedicated_operator]` |
| `billing_cycle` | enum | `monthly` \| `annual` |

Output the calculator returns:

```yaml
result:
  tier: small
  base_price_usd: 600               # from TOOLING-TIERS.md §3.7
  vertical_multiplier: 1.0          # single vertical: 1.0; +0.15 per additional
  trilingual_addon_usd: 0           # bundled in Tier 2+
  selected_role_count: 4
  role_overage_usd: 0               # 4 roles included in Tier 2; overage @ $40/role/mo in Tier 1 only
  addons_usd: 0
  billing_discount_pct: 0           # 10% / 15% / 20% for annual
  setup_fee_usd: 500                # from TOOLING-TIERS.md §3.7
  monthly_total_usd: 600
  setup_total_usd: 500
  year_1_total_usd: 7700            # 500 + 12*600
  year_1_arr_usd: 7200              # 12*600 (operational ARR only)
```

### 6.1 Calculator rules

1. **Base price** = tier base × billing cycle (annual = 0.85 / 0.80 of monthly).
2. **Vertical multiplier** = 1.0 + 0.15 × max(0, len(verticals) − 1). Two verticals +15%, three +30%.
3. **Role overage** (Tier 1 only): each role beyond the 4 included = $40/mo USD / €50 / ₲250K.
   Tier 2 includes 6 roles; Tier 3 includes all 47 (no overage).
4. **Trilingual add-on**: $0 in Tier 2+, $50/mo USD in Tier 1, €60 / ₲300K.
5. **Dedicated operator add-on**: $300/mo / €350 / ₲1,800K (Tier 3 only).
6. **Custom agent authoring add-on**: $400/agent one-time setup + $50/agent/mo.
7. **Annual discount**: 10% (Micro), 15% (Small), 20% (Medium).
8. **Hard cap**: setup fee never exceeds 1× monthly at the same tier.

### 6.2 Worked examples

**Example 1: PY law firm, 8 employees, ES only, Tier 2, single legal vertical:**
- base $600 × 1.0 × 1.0 = $600/mo
- 4 selected roles, included
- 12-month discount 15% → $6120/yr (vs $7200 undiscounted)
- setup $500 one-time

**Example 2: NL dental practice, 12 employees, NL+EN, Tier 2, dental + beauty compound:**
- base $600 × 1.15 × 1.0 (NL included) = $690/mo
- trilingual addon $0 (already Tier 2)
- 8 roles selected, included (Tier 2 has 6 default + 2 overage-free)
- annual − 15% → $7038/yr
- setup $500

**Example 3: PY e-commerce, 35 employees, ES+PT, Tier 3, e-commerce only:**
- base $2000 × 1.0 × 1.0 = $2000/mo
- 12 roles selected, all included (Tier 3 has 47 included)
- annual − 20% → $19,200/yr
- setup $1000
- + 2 custom agents × ($400 + $50/mo × 12) = $2000 setup extra + $1200/yr

---

## 7. Onboarding timeline

### Week 1 — Foundation

| Day | Activity | Owner |
|-----|----------|-------|
| D1 | Intake form submitted (200 Qs filled) | Customer + AIW operator |
| D1 | Vertical preset + tier recommendation auto-emailed | Calculator (§6) |
| D2 | Contract signed, setup fee invoiced | Customer + AIW |
| D2-3 | VPS / CF account / OAuth credentials collected | Customer |
| D3 | PROMPT.md files seeded, state schemas instantiated | AIW Erebus |
| D4-5 | Agents wired to customer's data sources (Notion / WA / Sheets) | AIW Erebus |
| D5 | First cron tick fires for every agent in tier | AIW Erebus |
| D6 | First morning-brief delivered; eval-gate runs on the brief | AIW Erebus |
| D7 | Trademark scrub + 12-factor audit + custom-config validation | AIW Erebus + customer |
| D7 | **Week 1 gate**: customer can review their first week's briefs | Customer |

### Month 1 — Stabilisation

| Week | Activity | Owner |
|------|----------|-------|
| W2 | Eval-gate tuning; cron schedule reviewed | AIW Erebus |
| W2 | Customer feedback round-1 (5 questions from operator) | Customer |
| W3 | HARD/HIGH decisions routed to founder per `ROLLBACK-PLAYBOOK.md` §1.2 | AIW + customer |
| W3 | First weekly brief + bizops-tracker readout | AIW |
| W4 | Self-running check #1 — Tier 1 + 2 eligible for declaration | AIW |
| W4 | Review monthly KPIs vs original intake | AIW + customer |
| W30 | **Month 1 gate**: customer should have 0 escalation blockers; org-state fresh every <5 min | AIW |

### Month 3 — Self-running declaration

| Week | Activity | Owner |
|------|----------|-------|
| W5-8 | Coaching phase opt-in (Tier 3 only): `coach-onboarding`, `coach-practitioner`, `coach-lead-finder` | AIW Erebus + customer |
| W8 | Chaos test runner opt-in (Tier 3 only) | AIW Erebus |
| W9-12 | Eval-gate trending review; quality drift detection | AIW |
| W12 | Self-running declaration + v1.0.0 lock | AIW + customer + Iván |
| W12 | **Final gate**: handover to customer-led ops | AIW |

### 7.1 Self-running declaration (per `SELF-RUNNING-CRITERIA.md`)

For each tier, the declaration lands at:

| Tier | Days post-deploy | What's required |
|------|------------------|-----------------|
| **Micro** | Day 30 | 0 cron errors in 30d window + 0 founder "is X live?" messages |
| **Small** | Day 14 | Same + eval-gate trending clean |
| **Medium** | Day 7 (after Foundation gates F1/F2/F3 from `PHASE-13` §4.2) | All of: 0 errors + 0 messages + chaos test A pass + 12-factor ≥ 9.0 |

After declaration:
- AIW stops touching customer PROMPTs and cron schedules.
- Customer takes ownership of state rollback per `ROLLBACK-PLAYBOOK.md`.
- AIW retains kill-switch access (one cron `hermes cron disable` away).

---

## 8. Customisation limits

### 8.1 In scope (per `vertical-client-extension-playbook` pattern)

- **Pick which agents are enabled.** Per `agents.*.enabled` in §3 config.
- **Pick the cadence** (cron schedule per agent).
- **Pick the tools** (`toolsets` per agent).
- **Pick the language bundle** (`languages[]`).
- **Pick the vertical preset** (single or compound).
- **Brand colours, fonts, copy voice** (per-vertical defaults, overrideable).
- **Webhook destinations** (Email / WhatsApp / Linear / Notion — customer's choice).
- **Output channels** (where morning-brief + escalation land).

### 8.2 Out of scope (separate SKUs)

- **Custom agent authoring** beyond the 47-agent matrix — billed per agent (see §6.1 #6).
- **Multi-tenant SSO** beyond Notion + Workspace — separate project.
- **EU AI Act + GDPR + LGPD turnkey compliance pack** — bundled Tier 3 only, separate SKU otherwise.
- **Real-human 1:1 coaching sessions** — the AI agents write the briefs; humans run the sessions.
  Customer pays AIW-referred coaches separately.
- **Trademark-banned paid acquisition channels** (paid social / paid search / paid video-placement) — never sold.
- **Mobile native apps** — Web Workers only at this SKU.

### 8.3 Hard-stop ceiling (per `vertical-client-extension-playbook` §"Rejection Patterns")

The template will refuse configurations that violate org-constitution rules:

| Rejection | Why |
|-----------|-----|
| Add 7+ Tier-1 departments | Org constitution hard-caps at 6 Tier-1 (per `vertical-client-extension-playbook` table) |
| Use `model: fast` for P1 hygiene agents | Single-tool only; multi-tool batch fails |
| Use `model: primary` for cron jobs | Subscription expired risk; silent 402 |
| Use `provider: minimax-oauth` for any agent | Rate-limited; not reliable for 7-day self-running |
| Auto-commit to customer's private repo | Per `no_private_repo_writes` hard stop |
| Wire WhatsApp automated personalised replies | Template acks only (per `COMPLETE-EXPLANATION.md` §3) |
| Publish prices / fabricate testimonials on public surfaces | Daily guard agent (`compliance-monitor`) blocks |
| Skip Phase 0 foundations (canonical host cutover + orphan routes + redirects) | 2 hours of code; saves months of drift |
| Build trademark-banned marketing channels | Banlist applies to OUR surfaces; we don't ship them |
| L3 git repos in early phases | Defer until self-running criteria met (Phase 6 only) |

---

## 9. Validation gates (run on every deploy)

Before "week 1 gate" (§7):

- [ ] Intake form complete (200 Qs, 0 unanswered required)
- [ ] Trademark scan clean on `customers/<slug>/config.yaml` and all seeded PROMPT.md files
- [ ] All cron jobs registered with `provider=litellm, model=reasoning`
- [ ] `eval-gate.py` runs end-to-end on at least 1 seeded brief
- [ ] Morning-brief cron delivered at least once before customer-facing kickoff
- [ ] `state/org-state.json` mtime < 5 min (sanity check on heartbeat)
- [ ] 12-factor audit score ≥ 9.0 (`PHASE-21-12-FACTOR-COMPLETE.md` reference)
- [ ] Disaster-recovery runbook handed to customer (`ROLLBACK-PLAYBOOK.md` §3)
- [ ] Hard-stops profile signed by customer (5 mechanical + tier-specific)
- [ ] Escalation route tested end-to-end (founder receives a test page)

If any fails, the deploy is **not done**. Fix first, then re-validate.

---

## 10. Open questions for Iván

1. **Do we offer a "free quick-win" tier as a marketing funnel?** Per the existing coaching
   conversion flow (`COMPLETE-EXPLANATION.md` §3), the 30-min free session is the conversion
   trigger. Should the customer template offer a 30-min "AI scan of your workflow" instead?
2. **Per-vertical pricing tiers — does each vertical deserve its own setup fee?** Currently
   the setup fee is flat per tier. Legal verticals need more intake rigor; e-commerce needs more
   catalog data. Per-vertical setup fees would price that risk in.
3. **Multi-currency pricing**: does the ₲ / € / $ conversion track parallel-market rate, or
   fixed business rates? The current doc uses parallel rate (₲7,200/USD), which is more
   customer-friendly but exposes AIW to FX volatility.
4. **EU AI Act + GDPR turnkey compliance pack** — bundle Tier 3 or separate SKU?
5. **Customer-portal self-serve tier upgrade/downgrade** — required before scaling, or
   manual-conversation-only is fine for the first 10 customers?

---

## 11. Cross-references

- **Companion:** `TOOLING-TIERS.md` — three pricing tiers, what's included/excluded.
- **Agent matrix:** `/opt/data/agents/ORG-AGENTS.md` — 47-agent roster.
- **Roles inventory:** `/opt/data/agents-v2/ROLES-INVENTORY.md` — 135 roles this template draws from.
- **Vertical extension:** `vertical-client-extension-playbook` — single-client extension pattern.
- **Customer-site kickoff:** `client-site-kickoff` skill — 200-question intake + sample demo.
- **Plan:** `/opt/data/agents-v2/PHASE-13-COMPLETE-UPDATED-PLAN.md` §4 (six phases, 90-day build order).
- **Rollback:** `/opt/data/agents/ROLLBACK-PLAYBOOK.md` — per-state + per-cron + per-deploy.
- **Self-running milestone:** `/opt/data/agents-v2/SELF-RUNNING-CRITERIA.md`.
- **Trademark banlist:** `/opt/data/scripts/trademark-scan.py`.
- **Trilingual context:** `/opt/data/skills/coaching/coaching-trilingual-glossary/` —
  es/en/nl coaching vocabulary + AIW positioning.
- **Market context:** `/opt/data/agents/research/200-ai-coaching-companies.md` — BetterUp/CoachHub/Valence
  spend anchors ($4-15K/employee/year).
- **Coaching research continuation:** `/opt/data/agents/research/coaching-continuation-plan.md` —
  5-track plan.

---

**End of CUSTOMER-TEMPLATE.md** — see `TOOLING-TIERS.md` for the pricing side of the same SKU.
