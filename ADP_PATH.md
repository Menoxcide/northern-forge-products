# ADP ship path

```
persona + visual → design_product → diamond_qol.patch_html (+ glass)
  → deploy_vercel (or queue) → thrift_after_ship → stigmergy
```

## Modules

| Step | Code |
|------|------|
| Personas / visuals | `personas.py` |
| HTML design | `product_designer.py` (`_qol_desc`, glass body) |
| QoL + glass | `diamond_qol.py` |
| Deploy | `deploy_vercel.py` (API → CLI fallback → queue) |
| Market | `thrift_market.py` |
| Articles | `x_articles.py` |
| Agent | `autonomous_digital_product_agent.py` |
| Always-on | `always_on.py` (product tick isolated, 7m timeout) |

## Guardrails

- Public voice scrub  
- Deploy budget gate  
- No mid-word descriptions  
- Cosmos loop measures the closed path  

## Related

`INFRA_LADDER.md` · `CREATION_MANIFESTO.md` · `AGENTS.md`

## Daily product cycle

Scheduled Grok task **adp-daily-product-cycle** must run on **this host**.

```bash
export ADP_ROOT=/root/autonomous-digital-products
bash "$ADP_ROOT/scripts/adp_daily_cycle.sh"
# or:
cd /root/autonomous-digital-products && python3 run_full_cycle.py
```

If a cloud sandbox reports `dir missing`, that runner is not the control plane —
re-run on the always_on host (this tree), do not recreate the repo elsewhere.
