# Catalog sync status

**Updated:** 2026-07-25

| Field | Value |
|-------|-------|
| Live products | 103 |
| Catalogued | 110 |
| Look | liquid glass (diamond QoL / cosmos / diamond_plus) |
| Design avg | 85.8 (A:76 B:6 D:19 F:7) |
| QoL patched | 107 local sources |
| Brand CSS | https://northern-forge-labs.vercel.app/assets/brand/nf-glass.css |
| Hub | https://northern-forge-labs.vercel.app |
| Conversion | https://nf-conversion.vercel.app |

## GitHub files

- README.md — 103 live · liquid glass look explained
- PRODUCTS.json — counts, look metadata, product_ids
- CATALOG.md — featured tools + associations
- HUB.md / QOL.md / AGENTS.md — continuum docs
- SYNC_STATUS.md — this file

## Source of truth

ADP workspace: `/root/autonomous-digital-products`
- `config/live_products.json`
- `artifacts/northern-forge-hub/catalog.json`
- `python3 github_deploy.py sync` (write needs GitHub MCP OAuth; vault PAT is contents-read only)
