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
