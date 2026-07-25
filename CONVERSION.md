# Diamond+ conversion layer

**Live API:** https://nf-conversion.vercel.app  
**Manifest:** `config/system_manifest.json`  
**Tier:** cosmos / diamond_plus

## Endpoints

| Endpoint | Purpose |
|----------|---------|
| `POST /api/stripe/webhook` | `checkout.session.completed` fulfillment |
| `GET /api/unlock/verify?session_id=` | Paid check → unlock key (Stripe truth) |
| `GET /api/unlock/verify?invoice_id=` | Invoice paid path (OOB / bridged) |
| `GET /api/unlock/ledger?session_id=` | Single session status (no PII) |
| `GET /api/unlock/ledger` | Recent paid list (**admin secret** required) |
| `POST /api/event` | Analytics beacon (+ optional Bearer user) |
| `GET /api/event?stats=1` | Aggregate event counts |
| `GET /api/analytics/popular?limit=` | **Hot / popular products** for hub |
| `POST /api/checkout` | Create Checkout Session (**per-product catalog** · contextual name/price) |
| `GET /api/checkout` | List pro catalog (product_id, benefit, amount) |
| `POST /api/ai/generate` | AI magic (NVIDIA primary · 8b first) |
| `POST /api/auth/session` | Guest / email identity (HMAC) |
| `GET /api/auth/session` | Bearer → current user |
| `POST /api/scores` · `GET /api/scores` | Scores / leaderboards |
| `POST /api/trackers` · `GET /api/trackers` | Progress blobs |

## Customer flow

1. Unlock on **that product** (CTA is contextual: name, benefit, price) or [hub /revenue](https://northern-forge-labs.vercel.app/revenue)  
2. `POST /api/checkout` with `product_id` → Stripe Checkout line item for **that** tool (not a shared golden-hour link)  
3. Redirect → `/unlock/success?session_id={CHECKOUT_SESSION_ID}&product_id=…`  
4. Verify API → `localStorage` unlock key for that product → return URL from catalog  

**Catalog:** `data/stripe_catalog.json` · `lib/pro_catalog.js` · Payment Links only for `mi-golden-hour` + snow; everyone else uses dynamic `price_data`.

## Durable unlock ledger

- Stripe (source of truth)  
- SQLite `data/unlock_ledger.sqlite`  
- JSON backup  
- Sync: `python3 scripts/sync_unlocks_from_stripe.py`

## Analytics / popular

- Hub client: `js/nf-hub-analytics.js`  
- Beacons `product_open` / `card_click` / `product_view`  
- Local durable: `data/cosmos.sqlite` (agents)  
- Live popular: `GET /api/analytics/popular`

## AI magic

```http
POST /api/ai/generate
{ "task": "sample_goal|expand_notes|forge_prompts|polish_copy|freeform|…",
  "product_id": "…",
  "input": { } }
```

Provider order: **Moonshot/Kimi Code** (`kimi-k2.7-code` …) → NVIDIA (8b → gemma → 70b) · optional xAI / OpenAI / Groq.  
Env: `MOONSHOT_API_KEY` (or `KIMI_API_KEY`), optional `MOONSHOT_MODEL`, `MOONSHOT_BASE_URL` (default `https://api.moonshot.ai/v1`).  
Client: `js/nf-magic.js` on Prompt Forge, Copy Forge, MailForge (+ more as wired).  
`forge_prompts` returns **claude + gpt + grok** (three distinct model-ready prompts; client rebuilds any missing/duplicate panel locally).

## Identity

See skill `/nf-identity`. Guest and email sessions; scores and trackers optional.

## Security & rate limits

All public endpoints go through `lib/http_guard.guard` + `lib/rate_limit` (per-IP sliding windows).  
Details, profile table, and env knobs: **`artifacts/nf-conversion/SECURITY.md`**.

Highlights:

- AI: 12/min + 80/hr · checkout: 8/min · auth: 20/min · events: 120/min  
- CORS allowlist (not open `*`) · security headers via `vercel.json`  
- Checkout URL host allowlist · ledger list admin-gated · webhook signature  

## Deploy

```bash
# conversion project
cd artifacts/nf-conversion && vercel deploy --prod --yes
# or identity+hub helper when quota allows
bash scripts/deploy_identity_layer.sh
```

## E2E note

Live Stripe rejects test cards; e2e unlock path validated via invoice `paid_out_of_band` bridge when needed (see diamond.json e2e block).
