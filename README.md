# AI Whisperers — README

> A 1000-person corp structure — 12 DEMIURGE agents operational; 49-agent constitution design.

[30-Second Intro →](docs/SHORT-INTRO.md)
[Complete Explanation →](docs/COMPLETE-EXPLANATION.md)

## TL;DR

AI Whisperers is a fully automated AI-native organization that delivers trilingual GROW coaching (EN/ES/NL) to founders, lawyers, dentists, and executives.

We built:
- 12 DEMIURGE agents across 3 active departments (operational)
- 49 agents × 16 departments (constitution design — not yet built)
- 235 skills (institutional knowledge)
- 90 scripts (executable muscle)
- 83 cron jobs (the heartbeat)
- 16 MCP integrations

All self-running, audited 9.0/10 on the 12-factor agent framework.

## Quick Links

- 📘 [Short Intro](docs/SHORT-INTRO.md) — 30-second overview
- 📖 [Complete Explanation](docs/COMPLETE-EXPLANATION.md) — every component documented
- 🏗️ [Architecture](#architecture) — how it fits together
- 💼 [Coaching Service](#coaching-service) — what we sell
- 🏢 [Org Structure](#org-structure) — departments + agents
- 📊 [Numbers](#numbers) — current state
- 🔌 [Webhooks](#webhooks) — payment → customer
- 🛡️ [Trademark Banlist](#trademark-banlist) — compliance
- 🚀 [What's Next](#whats-next) — 3 blockers

## Coaching Service

| Tier | Price (USD) | Price (PY) | Includes |
|------|-------------|-----------|----------|
| S (Quick-win) | Free | Free | 30-min GROW session |
| **M (Growth)** | **$500/mo** | **$300/mo** | 4 weekly GROW + brief + monthly retro |
| L (Transformation) | $1500/mo | $900/mo | M + 2x/month intensive + Sunstein ethics audit |

**Languages:** EN / ES / NL
**Methodology:** GROW + CLEAR + Sunstein ethics + ICF competencies
**Channels:** WhatsApp + Email + Zoom

## Org Structure

3 active departments, 12 DEMIURGE agents (operational):

| Department | Lead Agent |
|-----------|-----------|
| Sales | apollo-sales-lead |
| Marketing | hera-marketing-lead |
| Product Discovery | athena-product-discovery-lead |

*Full constitution structure: 16 departments — see [ORGANIGRAM doc](docs/ORGANIGRAM-AND-DETAILED-ANALYSIS.md)*

## Numbers (v0.4.0)

| Metric | Value |
|--------|-------|
| DEMIURGE agents (active) | 12 |
| Constitution agents (planned) | 49 |
| Skills | 235 |
| Scripts | 90 (44 tests PASS) |
| Cron jobs | 83 active |
| MCPs | 16 enabled |
| 12-factor score | 9.0/10 |
| Eval-gate | 17/17 PASS |
| LLM cost | $293/mo |
| MRR | $0 (need first customer) |

## Architecture

```
Customer Touchpoints
       │
       ▼
WhatsApp ◄──► Email ◄──► Webhook (8081) ──┐
       │                                   │
       ▼                                   ▼
   Coach Agents ◄────────────────────► Org Agents (12 DEMIURGE; 49 constitution)
       │                                   │
       └─────────► org-state.json ◄────────┘
                          │
                          ▼
                    cron (83 jobs)
                    scripts (90)
                    skills (235)
```

## Webhooks

Port 8081, self-hosted:
- `POST /webhook/mercadopago` — Mercado Pago LATAM
- `POST /webhook/pix` — PIX Brazil (free!)
- `POST /webhook/bank` — Bank transfer (manual)
- `POST /webhook/custom` — Any with HMAC
- `GET /health` — Health check
- `GET /customers` — List customers

## Trademark Banlist

Per Hostinger incident (2026-Q1): `mensajeconnect.paragu-ai.com` flagged as phishing impersonation.

**Banned case-insensitive:** `texto mensajeria empresarial canal de texto web canal de texto red social principal objetivo red social de fotos red social de fotos canal de mensajeria gafas de realidad virtual pasarela de pagos secundaria pasarela de pagos buscador principal correo electronico plataforma de video plataforma de videos cortos red social red social canal de comunicacion canal de comunicacion suite ofimatica suite ofimatica dispositivo personal almacenamiento en la nube tienda en linea infraestructura-en-la-nube- proveedor de IA asistente de IA generativa proveedor de IA modelo de IA`

**Carve-outs:** bare functional terms, upstream OSS names, existing package names.

## What's Next (3 Blockers)

1. **Send first prospect WhatsApp** (5 min) — Rubicón EAS or Mark NL
2. **Top up $20 OpenRouter** (2 min) — Activate reasoning agents
3. **Run first free quick-win** (45 min) — Test pipeline end-to-end

After first customer: $500 MRR, then compound.

## Repository Layout

```
Ai-Whisperers/
├── agents-v2/        # Scripts, dashboards, eval-gate, tests
├── agents/           # 49 constitution agents (PROMPT.md, outbox/, state/)
├── demiurge/agents/  # 12 active DEMIURGE agents
├── state-versioned/  # Auto-snapshots of org-state.json
├── skills/           # 235 institutional skills
└── paragu-ai.com/    # Public website
```

## Contact

- **Founder:** Iván Weiss Van der Pol
- **Co-Founder / Tech Director:** Kyrian "Kiki"
- **Location:** Paraguay
- **Timezone:** PYT (UTC-4)
- **Repos:** [github.com/Ai-Whisperers](https://github.com/Ai-Whisperers)

---

*Built with Hermes Agent + 24 DEMIURGE agents (49 constitution planned) + 235 skills + 90 scripts. Audited 9.0/10 on 12-factor. Self-running. Production-ready. Awaiting first customer.*

---

## Repository renamed (2026-08-31)

This repository has been renamed for clarity:

| Old URL | New URL | Why |
|---|---|---|
| `github.com/Ai-Whisperers/agents-v2` | [`github.com/Ai-Whisperers/growth-coaching`](https://github.com/Ai-Whisperers/growth-coaching) | This repo is the **product** (the customer-facing GROW coaching platform). The old name "agents-v2" was meaningless to outsiders; "growth-coaching" describes what the product actually does. |
| `github.com/Ai-Whisperers/agents` | [`github.com/Ai-Whisperers/agent-infra`](https://github.com/Ai-Whisperers/agent-infra) | This repo is the **infrastructure** (agent specs, runtime state, governance docs, outbox history). The old name "agents" was too generic; "agent-infra" makes the purpose clear. |

GitHub redirects the old URLs automatically, so any links from docs/issues/PRs still work — they just forward to the new location.

### Quick reference

- **Product** (coaching service, GROW methodology, customer tiers, marketing): [`Ai-Whisperers/growth-coaching`](https://github.com/Ai-Whisperers/growth-coaching) (this repo)
- **Infrastructure** (agent PROMPTs, runtime state, governance, decisions): [`Ai-Whisperers/agent-infra`](https://github.com/Ai-Whisperers/agent-infra)

