# Northern Forge · Creation Manifesto

We build **useful surfaces** for three audiences — and keep them **separate**:

1. **Makers & freelancers** — free-core web tools that solve one job (default hub)  
2. **Any agent / builder** — portable skills, personas, and MCP tools that work *outside* our stack  
3. **Forge operators** — ADP loops, thrift, fleet oil (backend only; not the public product line)  

## How people should choose a surface

Every product answers three questions in plain language:

| Question | On the card / hero |
|----------|--------------------|
| **Who is this for?** | Named person (UP hiker, solo freelancer, agent runtime…) |
| **When should they open it?** | Named moment (before trail, launch day, token debug…) |
| **How do they use it?** | Browser page · install SKILL.md · call flagship MCP |

Hub cards show **Best for … · when …**. App chrome loads the same line. Agents page maps human vs agent paths. If a ship candidate cannot fill those three fields honestly, it is not ready.

## Future tech we want to invent

Not more generic dashboards. **Cutting-edge useful systems** people would open weekly:

| Lane | Promise | Examples to push |
|------|---------|------------------|
| **Agent interfaces** | Tools agents call like APIs — schemas, not chat theater | Flagship MCP cores, prompt routing, skill packs, human-review queues |
| **Local field systems** | Hyper-local outdoor / place intelligence, offline-first | Golden hour, snow depth, trail kits, pack weight, field checklists |
| **Builder cores** | Sharp developer utilities with free cores | JSON→TS, regex, JWT, cron, contrast, typed converters |
| **Maker operations** | Freelance & launch ops without SaaS bloat | Invoices, copy packs, mail HTML, rate cards, meeting cost |
| **Local-first trust** | Data stays in browser unless exported | No-account free cores, device unlocks, export paths |

**Ship rule:** prefer a tool that teaches a *new default* for agents or field work over another clone invoice. Fantasy brands and hollow MCP shells stay frozen.

## What we create

### Public product apps
- Single-purpose pages: prompts, regex, invoices, packs, streaks, dice, contrast, mail HTML  
- Free core by default; optional Stripe unlocks  
- Public voice: user-facing only (no thrift/self-promo chrome)  
- UX shell: steps, help, loading, movable modals (`nf-ui.js`)  
- Optional identity: sign-in, scores, trackers (`nf-identity.js`)  
- Optional AI magic: generate buttons (`nf-magic.js` → `/api/ai/generate`)  

### Portable agent products (public · Skills & MCP)

**Rule:** a catalog `agent_skill` or `mcp_server` must be useful to *any* agent without owning Northern Forge.

- **Installable skills / personas** — SKILL.md workflows (invoices, prompts, trail kits, …)  
- **Flagship MCP** — one strong server agents actually add, not twenty hollow shells  
- **Hub path** — `/agents` is the install surface; catalog category **Skills & MCP**  
- **Gate** — `usefulness_gate` rejects fantasy brands, hollow MCP, and **ops_only** skills  

| First-party product | URL |
|---------------------|-----|
| **Northern Forge MCP** (flagship) | https://nf-mcp.vercel.app — `/mcp` JSON-RPC · `/tools` REST |

Free core tools today: `list_live_products`, `get_product`, `popular_tools`, `post_event`, `get_payment_link`, `forge_status`, `golden_hour_windows`, `pack_weight_sum`, `prompt_variants` (+ job tools as they land).

Ship weights (~80% `web_tool`, ~10% `mcp_server`, ~10% `agent_skill`). MCP only when ≥2 real callable tools do work. Override: `NF_PRODUCT_KIND=mcp`.

### Forge ops (backend · not catalog)

- **ADP loops** — `always_on.py` dream→ship→market→maintain  
- **Fleet oil** — `fleet_maintain.py` QoL, design audit, unlocks, AI smoke  
- **Thrift market** — paste packs always; rare X API posts  
- **Local Grok skills** — `/northern-forge-ops`, `/nf-fleet-oil`, `/nf-qol-fleet`, `/nf-thrift-cash`, `/nf-ai-magic`, `/nf-identity`, `/nf-ux-shell`  
- **Ship path** — design → diamond QoL → NFUI → deploy → thrift → stigmergy  
- **Command center / metrics** — health, infra tier, design scores  

These stay in AGENTS.md, local skills, and a collapsed operator section on `/agents` — never primary hub nav or product cards.

Third-party MCP we *use* to operate the forge (not the product line):

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

### Observe the loop

```bash
python3 scripts/loop_status.py          # dense one-screen status
python3 scripts/loop_status.py --watch  # live refresh
bash scripts/loop_watch.sh -f           # status + always_on log
```

Full guide: [OBSERVE.md](./OBSERVE.md).

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

## Brand · liquid glass (CC0)

Public design system for hub and apps:

- Glassmorphism CSS + hover effects (`nf-glass.css`)  
- Atmosphere, mark, banner, OG card (Grok Imagine)  
- Free use: **CC0** — see [BRAND.md](./BRAND.md)  
- Live: https://northern-forge-labs.vercel.app/assets/brand/

## Non-goals

- Fake waitlists for vaporware  
- Dark patterns / forced accounts for free cores  
- Product UIs that are internal thrift dashboards  
- Shipping without steps/help when the flow is non-obvious  
- Public catalog cards for forge ops (always_on, thrift, fleet oil, deploy quota)  
- Hollow MCP landing pages without callable job tools  

## Infrastructure ladder

```
thatch → … → titanium → obsidian → nebula → quasar → cosmos
```

Cosmos = closed loop (ship → thrift → oil → exposure → cash) with durable local store, deploy-budget awareness, and agent/MCP surfaces. See `INFRA_LADDER.md`.

## North star

> Specific problems. Short pages. Free cores. Fair unlocks. Agents that keep shipping. MCP servers that stay callable. Niche writing that earns attention. Loop that funds the next ship.
