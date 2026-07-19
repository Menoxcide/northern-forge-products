# Northern Forge · Creation Manifesto

We build **useful surfaces** for three audiences at once:

1. **Makers & freelancers** — free-core web tools that solve one job  
2. **Agents** — agent-oriented utilities, skills, and thrift ops that ship without babysitting  
3. **MCP-connected systems** — tools that agents and humans call through Model Context Protocol  

## What we create

### Public product apps
- Single-purpose pages: prompts, regex, invoices, packs, streaks, dice, contrast, mail HTML  
- Free core by default; optional Stripe unlocks  
- Public voice: user-facing only (no thrift/self-promo chrome)  
- UX shell: steps, help, loading, movable modals (`nf-ui.js`)  
- Optional identity: sign-in, scores, trackers (`nf-identity.js`)  
- Optional AI magic: generate buttons (`nf-magic.js` → `/api/ai/generate`)  

### Agent-oriented tools
- **ADP loops** — `always_on.py` dream→ship→market→maintain  
- **Fleet oil** — `fleet_maintain.py` QoL, design audit, unlocks, AI smoke  
- **Thrift market** — paste packs always; rare X API posts  
- **Grok skills** — `/northern-forge-ops`, `/nf-fleet-oil`, `/nf-qol-fleet`, `/nf-thrift-cash`, `/nf-ai-magic`, `/nf-identity`, `/nf-ux-shell`  
- **Ship path** — design → diamond QoL → NFUI → deploy → thrift → stigmergy  
- **Command center / metrics** — health, infra tier, design scores  

### MCP servers (first-class creation surface)
We treat MCP servers as products agents use, not side notes:

| MCP / integration | Use in the forge |
|-------------------|------------------|
| **Vercel** | Deploy apps, env, logs |
| **Stripe** | Checkout, invoices, customers as identity backbone |
| **Linear** | Epics (e.g. NOR-5 conversion) |
| **GitHub** | Catalog / product archive |
| **Mixpanel** | Analytics project (when token set) |
| **Figma / Canva / Excalidraw** | Design systems & assets |
| **X / x-docs** | Publishing & platform docs |
| **Neon / Cloudflare / Railway** | When provisioned for durable data |
| **Grok/xAI tools** | Reasoning, Imagine brand, tasks |

New agent tools should expose **clear tool schemas**, **idempotent actions**, and **public vs ops boundaries**.

## Exposure: X articles (niche, in-depth)

We publish **long-form niche articles** on X for exposure—not slogan sludge:

- Upper Peninsula trail kit science  
- Lake-effect snow depth heuristics  
- Golden hour for northern latitudes  
- Local-first freelancing tooling  
- Prompt routing between models without accounts  
- Agent thrift marketing economics (ops threads, not product UI)  

Pipeline: `x_articles.py` → `data/articles/` → thrift tick / manual paste / rare API post.

## Popularity & hub analytics

The public hub shows **what people actually open**:

- Client tracks `product_open` / `card_click`  
- Server aggregates via `/api/event` + `/api/analytics/popular`  
- Hub sorts and badges **Hot** / **Popular** tools  

## Non-goals

- Fake waitlists for vaporware  
- Dark patterns / forced accounts for free cores  
- Product UIs that are internal thrift dashboards  
- Shipping without steps/help when the flow is non-obvious  

## Infrastructure ladder

```
thatch → … → titanium → obsidian → nebula → quasar → cosmos
```

Cosmos = closed loop (ship → thrift → oil → exposure → cash) with durable local store, deploy-budget awareness, and agent/MCP surfaces. See `INFRA_LADDER.md`.

## North star

> Specific problems. Short pages. Free cores. Fair unlocks. Agents that keep shipping. MCP servers that stay callable. Niche writing that earns attention. Loop that funds the next ship.
