# Diamond-fused titanium QoL (+ liquid glass)

Module: `diamond_qol.py` · Report: `data/qol_apply_report.json`  
Enforced on every ship via `autonomous_digital_product_agent` + fleet oil.

## Standard (every product)

1. **Complete copy** — never cut mid-word (`_qol_desc` / `smart_truncate`)  
2. **Responsive media** — canvas/img `max-width: 100%`  
3. **Benefits strip** — Free now / Pro unlock / More tools / Privacy  
4. **Hub bar** — Hub · Pro unlocks · catalog tools (no thrift self-promo)  
5. **Analytics** — beacon to `nf-conversion` `/api/event`  
6. **Unlock CTA** — Stripe Payment Link when paid tier exists  
7. **Touch targets** — min 44px  
8. **Public access** — SSO-blocked apps mirrored under hub `/tools/*`  
9. **Liquid glass** — `nf-glass.css` + `body.nf-glass` + glass cards (hover lift)  
10. **A11y basics** — `role="main"` / contentinfo on new shells  

## Public voice (required)

Product UIs are for **end users**, not internal thrift workflow.

Never ship public copy like:

- “Built for @NForge26”  
- “paste them yourself / post manually (cheap)”  
- “thrift-market / zero API burn”  
- stigmergy / diamond-titanium / autonomous-agent scaffolding language  

OK:

- Northern Forge Labs brand  
- “More tools” hub links  
- Free / Pro pricing  
- Clear steps and help  

## Liquid glass brand (CC0)

| Asset | URL path |
|-------|----------|
| CSS | `/assets/brand/nf-glass.css` |
| Atmosphere | `/assets/brand/atmosphere.jpg` |
| Mark | `/assets/brand/mark.jpg` |
| Banner | `/assets/brand/banner.jpg` |
| OG card | `/assets/brand/og-card.jpg` |
| JS boot | `/js/nf-glass.js` |

Live CDN: `https://northern-forge-labs.vercel.app/assets/brand/`  
Inject: `diamond_qol._inject_glass` · skill `/nf-ux-shell`

## Apply

```bash
python3 diamond_qol.py all            # local sources
python3 fleet_maintain.py oil         # coordinated
# deploy products only when deploy_quota allows
```

## Design health

`python3 design_audit.py` → `data/design_audit.json`  
Target: fleet average high-90s with A grades; fix thin subcopy and missing ARIA over time.
