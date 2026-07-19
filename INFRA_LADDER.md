# Northern Forge · Infrastructure Ladder

```
thatch → wood → iron → steel → adamantium → titanium
                                              ↓
                         obsidian → nebula → quasar → cosmos
```

## Base metals

| Tier | What you get |
|------|----------------|
| **thatch** | Process + files + manual deploys |
| **wood** | Health, logs, supervised `always_on` |
| **iron** | SQLite stigmergy, deploy drain, hub sync |
| **steel** | Watchdog, metrics, site probes |
| **adamantium** | Thrift market integrity, tokens, evening isolation |
| **titanium** | Diamond config, upgrade orchestrator, self-report |

## Beyond titanium (the Cosmos ladder)

| Tier | What you get |
|------|----------------|
| **obsidian** | Durable `cosmos.sqlite` popular/events; `deploy_quota` awareness; word-safe `_qol_desc` ship path |
| **nebula** | Creation manifesto (makers + agents + MCP); X niche articles; hub analytics; Grok skills |
| **quasar** | Live popular/event APIs; revenue page; unlock ledger; budget-gated deploy drain |
| **cosmos** | Closed loop score: always_on + thrift + oil + exposure + cash without babysitting |

Diamond / diamond_plus is an **infusion** (cash, AI magic, UX) that rides on titanium+; cosmos is the **ladder top**.

## Commands

```bash
python3 infra_tier.py ladder
python3 infra_tier.py status
python3 infra_tier.py upgrade          # base metals + cosmos ladder

python3 cosmos_upgrade.py              # obsidian→…→cosmos only
python3 cosmos_loop.py status          # closed-loop pulse
python3 cosmos_loop.py tick
python3 deploy_quota.py                # Hobby deploy budget
```

## Locks & config

| Artifact | Role |
|----------|------|
| `data/TITANIUM.lock` | Base metal complete |
| `data/OBSIDIAN.lock` … `data/COSMOS.lock` | Beyond-titanium gates |
| `config/diamond.json` | Infusion + money + conversion |
| `config/cosmos.json` | Cosmos tier state |
| `data/cosmos.sqlite` | Durable local popular/events/loop |
| `data/command_center/cosmos_loop.json` | Latest loop report |

## always_on

Cosmos pulse every **4h** (`NF_COSMOS_EVERY`): seed store, reuse niche article pack, thrift tick, rewrite loop score.

## Quasar note

Hobby Vercel still caps **100 API deploys/day**. Quasar/cosmos design **around** that limit (`deploy_quota` + drain skip). True unlimited deploys need **Vercel Pro** (platform), not another code tier.
