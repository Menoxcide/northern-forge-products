# Autonomous continuance

The machine oils itself. Coordinated via `fleet_maintain` + `always_on` (maintain + **cosmos** ticks).

## Process

| Artifact | Path |
|----------|------|
| always_on pid | `data/always_on.pid` |
| watchdog | `scripts/watchdog.sh` + `watchdog_supervisor.sh` |
| oil report | `data/fleet_maintain.json` |
| design scores | `data/design_audit.json` |
| health | `data/command_center/health.json` |
| metrics | `data/command_center/infra_metrics.json` |
| cosmos loop | `data/command_center/cosmos_loop.json` |
| infra tier | `data/infra_tier.json` |
| deploy budget | `data/deploy_quota.json` |
| manifest | `config/system_manifest.json` |
| cosmos config | `config/cosmos.json` |

## Loops

| Loop | Interval | Module |
|------|----------|--------|
| mesh | 15m | mesh_context + command_center |
| thrift | 45m | thrift_market + **x_articles** |
| revenue | 2h | revenue_tracker + rails |
| maintain | 3h | fleet_maintain.run_once |
| **cosmos** | **4h** | cosmos_loop.tick |
| product | 90m | AutonomousDigitalProductAgent (timeout 7m) |
| evening | ~20h | scripts/evening_remeasure.sh (isolated) |

## Continuance checklist

```bash
ps -p $(cat data/always_on.pid) -o pid,etime,cmd
tail -40 data/logs/always_on.log
python3 scripts/healthcheck.py
python3 cosmos_loop.py status
python3 infra_tier.py status
python3 deploy_quota.py
python3 fleet_maintain.py oil
```

## Oil steps (fleet_maintain)

1. vercel_env  
2. drain_queue (skipped if deploy budget empty)  
3. qol (includes liquid glass inject)  
4. design_audit  
5. thrift  
6. unlocks  
7. hub_sync (local write always; deploy may queue)  
8. conversion smoke  
9. health_metrics  

## Escalation

| Symptom | Action |
|---------|--------|
| always_on dead | `bash scripts/watchdog.sh` |
| product hang | fixed: subprocess + `NF_PRODUCT_TIMEOUT` |
| deploy 402 | wait budget / Vercel Pro; `deploy_quota.py` |
| REST token 403 | use CLI session (`vercel deploy --prod --yes`) |
| AI timeout | conversion uses fast NVIDIA 8b first |
| GitHub write 403 | use GitHub MCP OAuth or PAT with contents:write |

## North star

Ship → thrift → oil → exposure → cash → ship again. **Cosmos** = that loop measured and durable.
