# Department Taxonomy v1

> DEMIURGE-011 — expands agents-v2 30 functional areas

## Tier 1 — Core (6)

| id | name | status | priority |
|----|------|--------|----------|
| operations | Operations | active | — |
| finance-legal | Finance & Legal | skeleton | — |
| sales | Sales | **active** | P0 |
| engineering | Engineering & Delivery | skeleton | — |
| research | Research & Education | skeleton | — |
| people | People & Culture | skeleton | — |

## Tier 1 sub — Revenue (priority build)

| id | name | status | priority |
|----|------|--------|----------|
| marketing | Marketing | **active** | P0 |
| product-discovery | Product Discovery | **active** | P0 |

## Tier 2 — Cross-cutting (8)

| id | name | status |
|----|------|--------|
| ai-ops | AI Ops | skeleton |
| bizops | BizOps | skeleton |
| compliance | Compliance | skeleton |
| revops | RevOps | skeleton |
| knowledge-mgmt | Knowledge Management | skeleton |
| customer-success | Customer Success | skeleton |
| ai-safety | AI Safety | active (partial) |
| procurement | Procurement | skeleton |

## Tier 3 — Deferred (12)

| id | name | promotion trigger |
|----|------|-------------------|
| marketing-independent | Marketing (standalone dept) | >$2K/mo marketing budget |
| cs-standalone | Customer Success | 5+ recurring clients |
| compliance-standalone | Compliance | first EU client |
| knowledge-standalone | Knowledge Mgmt | >100 source files |
| ai-governance | AI Governance | >15 agents |
| investor-relations | Investor Relations | first external investor |
| chief-of-staff | Chief of Staff | >50 hrs coord/week |
| devrel | Developer Relations | public API launch |
| workplace | Workplace / Facilities | physical office |
| fraud-risk | Fraud & Risk | $500K+ payment volume |
| compensation | Compensation & Benefits | first FTE |
| people-ops | People Operations | 5+ FTEs |

## Tier 4 — Enterprise (4)

Documented in constitution; not in scope at current scale.

## Build order (Ivan directive + DEMIURGE)

1. **Marketing** — demand generation
2. **Product Discovery** — what to build/sell
3. **Sales** — revenue capture
4. Operations + AI Ops (management spine)
5. Engineering
6. Finance + Compliance
7. Research + Knowledge
8. People
9. Tier 3 on trigger

## Skeleton definition

`skeleton` = mission + role inventory + source catalog stub + signal types defined; no active agents until focused session.

## Parent/child

```
sales-growth (playbook)
├── marketing (sub-dept at Tier 1, promotes Tier 3)
├── sales
└── revops (Tier 2)
```
