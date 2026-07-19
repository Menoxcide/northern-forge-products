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
| `GET /api/unlock/ledger` | Recent paid sessions (Stripe) |
| `POST /api/event` | Analytics beacon (+ optional Bearer user) |
| `GET /api/event?stats=1` | Aggregate event counts |
| `GET /api/analytics/popular?limit=` | **Hot / popular products** for hub |
| `POST /api/checkout` | Create Checkout Session for known products |
| `POST /api/ai/generate` | AI magic (NVIDIA primary · 8b first) |
| `POST /api/auth/session` | Guest / email identity (HMAC) |
| `GET /api/auth/session` | Bearer → current user |
| `POST /api/scores` · `GET /api/scores` | Scores / leaderboards |
| `POST /api/trackers` · `GET /api/trackers` | Progress blobs |

## Customer flow

1. Unlock on product or [hub /revenue](https://northern-forge-labs.vercel.app/revenue)  
2. Stripe Payment Link / Checkout  
3. Redirect → `/unlock/success?session_id={CHECKOUT_SESSION_ID}`  
4. Verify API → `localStorage` unlock key → product  

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

Provider order: NVIDIA (8b → gemma → 70b) · optional xAI / OpenAI / Groq env keys.  
Client: `js/nf-magic.js` on Prompt Forge, Copy Forge, MailForge (+ more as wired).

## Identity

See skill `/nf-identity`. Guest and email sessions; scores and trackers optional.

## Deploy

```bash
# conversion project
cd artifacts/nf-conversion && vercel deploy --prod --yes
# or identity+hub helper when quota allows
bash scripts/deploy_identity_layer.sh
```

## E2E note

Live Stripe rejects test cards; e2e unlock path validated via invoice `paid_out_of_band` bridge when needed (see diamond.json e2e block).
