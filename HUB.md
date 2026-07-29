# Northern Forge Labs · Hub

**Public hub:** https://northern-forge-labs.vercel.app

## Counts

- **51 browsable live** (default hub count — same as public explorer)
- 40 useful · 65 registered · 14 demoted fantasy/hollow (hidden by default)

## Look

Liquid glass fleet chrome (diamond QoL):

- https://northern-forge-labs.vercel.app/assets/brand/nf-glass.css
- Atmosphere + mark + banner under `/assets/brand/`

## Sections

- Live products + **Popular** hot strip (analytics)
- **Useful** category (weekly-use gate)
- **Creation manifesto** · makers, agents, MCP
- **Agents & MCP** pillars
- Pay · Unlocks · Terms · Privacy

## Conversion API

Base: `https://nf-conversion.vercel.app`

| Endpoint | Purpose |
|----------|---------|
| `POST /api/event` | Analytics beacons |
| `GET /api/analytics/popular` | Hot / popular products |
| `POST /api/ai/generate` | AI magic (NVIDIA primary) |
| `POST /api/auth/session` | Guest / email identity |
| `POST /api/scores` · `GET /api/scores` | Leaderboards |
| `POST /api/checkout` · Stripe webhook | Unlocks |
| `GET /api/unlock/verify` · `GET /api/unlock/ledger` | Entitlements |

## Social

- X: https://x.com/NForge26
- GitHub catalog: this repo (51 browsable live products)
- MCP: https://nf-mcp.vercel.app

## Fleet

See [PRODUCTS.json](./PRODUCTS.json) · [CATALOG.md](./CATALOG.md)
