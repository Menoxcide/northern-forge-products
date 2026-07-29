# Claude Code — Northern Forge ADP

@AGENTS.md
@CLAUDE_MEMORY.md
@data/claude_memory/SYNCED.md

## Desk

- **Root:** this directory (`/root/autonomous-digital-products` in proot)
- **MCP:** `.mcp.json` → `northern-forge` @ https://nf-mcp.vercel.app/mcp
- **Skills:** `.claude/skills/` (northern-forge-ops, nf-thrift-cash, nf-qol-fleet, …)
- **Board:** `python3 agentic_loop.py package --agent claude`
- **Handoff:** `data/handoff/LATEST.md` · inbox `data/claude_memory/HANDOFF_INBOX.md`
- **Cash:** `data/promote_now/CASH_SPRINT.md` · `CASH_LINKS.md`
- **Auth:** `source scripts/claude_load_env.sh` (vault → env; never print values)

## Team loop

Grok hosts always_on + board. You claim packages, implement, handoff back.

```bash
python3 scripts/claude_sync_memory.py
python3 agentic_loop.py package --agent claude
# claim → work → complete → handoff.py write --from claude
```

## Hard rules

- No thrift/self-promo in product UIs
- Do not restart always_on unless dead
- Never dump secrets into chat or git

## Autonomous watcher

```bash
bash scripts/claude_desk_bootstrap.sh   # once
bash scripts/claude_handoff_loop_start.sh
```
