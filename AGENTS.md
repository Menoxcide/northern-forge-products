# Northern Forge · Agent Continuum (coordinated)

**Source of truth:** `config/system_manifest.json` + `config/diamond.json` + `config/cosmos.json`  
**Tier:** **cosmos** (base titanium · infusion diamond_plus)

Product UIs are for **end users**. Internal thrift/ops language stays out of public pages.

## Architecture map

| Layer | Module | Role |
|-------|--------|------|
| Always-on | `always_on.py` | 24/7 loops: mesh, thrift, revenue, maintain, **cosmos**, product, evening |
| Fleet oil | `fleet_maintain.py` | QoL, design audit, unlocks, hub sync, AI smoke, health |
| QoL | `diamond_qol.py` | Public chrome, word-safe copy, benefits, hub bar, **liquid glass inject** |
| Design | `design_audit.py` | Live score + persona/visual diversity |
| Ship | `autonomous_digital_product_agent.py` | design → QoL → deploy → thrift |
| Agent surfaces | `agent_surface_template.py` · `AGENT_SURFACE.md` | MCP/skill landings (not empty web tools) |
| Market | `thrift_market.py` | Paste packs always; ≤1 X API/day |
| Articles | `x_articles.py` | Niche long-form X exposure (wired into thrift tick) |
| Cosmos | `cosmos_loop.py` · `cosmos_store.py` · `cosmos_upgrade.py` | Closed-loop pulse + durable popular/events |
| Deploy budget | `deploy_quota.py` | Hobby 100/day awareness; drain skips when empty |
| Conversion | `artifacts/nf-conversion` | Stripe, identity, scores, popular, AI generate · **rate-limited + CORS hardened** (`SECURITY.md`) |
| Brand | `assets/brand/nf-glass.css` + Imagine pack | Liquid glass / glassmorphism (CC0) |
| Analytics | `/api/event` + hub `nf-hub-analytics.js` | Opens → popular strip |

## Loops (always_on)

| Tick | Cadence | Action |
|------|---------|--------|
| mesh | 15m | mesh context + command center |
| thrift | 45m | thrift packs + **x_articles** tick |
| revenue | 2h | revenue tracker / rails |
| maintain | 3h | `fleet_maintain` oil (no full redeploy by default) |
| cosmos | 4h | seed store, article reuse, thrift pulse, loop score |
| product | 90m | ship cycle (**7m hard timeout** so hangs can’t freeze the world) |
| evening | ~20h | isolated remeasure |

## Skills (load these)

| Skill | Use |
|-------|-----|
| `/northern-forge-ops` | Full stack ops |
| `/nf-fleet-oil` | Fleet maintain |
| `/nf-qol-fleet` | QoL / public voice |
| `/nf-thrift-cash` | Thrift + Stripe cash |
| `/nf-ai-magic` | ✨ generate buttons |
| `/nf-identity` | Sign-in, scores, trackers |
| `/nf-ux-shell` | UX shell + **liquid glass brand** |

## Commands

```bash
python3 scripts/healthcheck.py
python3 fleet_maintain.py oil
python3 infra_tier.py status
python3 cosmos_loop.py status
python3 thrift_market.py tick
python3 x_articles.py generate
python3 design_audit.py
bash scripts/watchdog.sh
# hub deploy (CLI session when API token stale):
cd artifacts/northern-forge-hub && vercel deploy --prod --yes
```

## Public voice

Never in product UIs: thrift self-promo, `@NForge26` “built for”, stigmergy/ops chrome.  
OK: brand name, hub links, free/pro pricing, steps/help.

## Brand · liquid glass

- Live: https://northern-forge-labs.vercel.app/assets/brand/  
- CSS: `nf-glass.css` · JS: `js/nf-glass.js`  
- Auto-injected by `diamond_qol._inject_glass` on fleet QoL  
- License: **CC0** (Grok Imagine pack)


## Polish · uniqueness · agent surfaces

- Uniqueness map: `UNIQUENESS.md` · `data/uniqueness_map.json` · freeze invoice clones
- **Ship gate:** `uniqueness_gate.py` blocks saturated JTBD clones in `validate_idea`
- **Apply roles:** `python3 uniqueness_gate.py apply` stamps kill/merge on `live_products.json`
- Agent surfaces: `AGENT_SURFACE.md` · `agent_surface_template.py` for MCP/skill landings
- Hot polish: `python3 polish_hot_tools.py` (top-10 job lines + empty states)
- Deploy: Vercel **Pro CLI** via `deploy_via_cli` / `--scope menoxcides-projects` (API token may be stale)

## Catalog (GitHub)

https://github.com/Menoxcide/northern-forge-products — live fleet catalog + manifesto + ladder · `PRODUCTS.json` (sync: `python3 github_deploy.py sync`)

## Identity

- Client `js/nf-identity.js` · API auth/session, scores, trackers  
- Skill `/nf-identity`  
- Popular: `GET /api/analytics/popular`

## Deploy notes

- Vercel **Pro** — prefer CLI session (`deploy_via_cli`); vault `VERCEL_TOKEN` may 403  
- Scope: `--scope menoxcides-projects` · team `team_FUzvh15z3pvgTzB7DGHE9jPv`  
- GitHub write: vault PAT (rotated) works for `python3 github_deploy.py sync`
