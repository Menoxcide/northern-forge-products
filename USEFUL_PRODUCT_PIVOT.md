# Useful product pivot (honest postmortem)

**Date:** 2026-07-29  
**Problem:** Fleet feels too specific / fantasy-branded; MCP products feel useless.

## Diagnosis (evidence)

| Fact | Detail |
|------|--------|
| Scale | ~122 live products |
| Kinds | ~87 web_tool, ~26 mcp_server, ~9 agent_skill |
| Naming | “Voidmote Oracle”, “Echoweave Sigils”, “Symbiont Weaver”, “Synthesis Mind” — brand theater, not jobs |
| Ship weights (was) | **45% mcp_server** — flooded catalog with landing pages |
| MCP scaffold default | Often `hello_forge` / describe_product — not a job an agent needs daily |
| Flagship MCP tools that *are* real | `golden_hour_windows`, `pack_weight_sum`, `prompt_variants`, catalog helpers |
| Most “MCP products” | Separate Vercel apps that are **marketing shells**, not tools Claude/Gemini would install |

### What *is* useful in the fleet (keep / double down)

- **MI Golden Hour Planner** — clear outdoor job  
- **Trailhead Snow Depth** — clear outdoor job  
- **Prompt Context Forge / X Copy Forge** — daily creator jobs  
- **JSON→TS, regex, streaks, gear pack, contrast** — classic free-tool jobs  
- **nf-mcp** flagship — one server with real schemas (needs more *job* tools)

### What failed

Autonomous loop optimized for **ship cadence + uniqueness + agent theater**, not **“would I open this tomorrow?”**

## Pivot rules (now)

1. **Default ship = useful web_tool** (weight ~80%).  
2. **MCP only when** there are ≥2 real callable tools that do work (not hello/ping).  
3. **Titles in plain English** describing the job (no fantasy brands by default).  
4. **Flagship MCP gets stronger** — one server agents actually add, not 26 shells.  
5. **Freeze promoting hollow MCP** in thrift (prefer tools with clear free job).  

## Seed / weight changes (shipped in code)

- `DEFAULT_KIND_WEIGHTS`: web 0.80 · mcp 0.10 · skill 0.10  
- `DEFAULT_SEEDS` + `mesh_seeds` diversifiers: job language only  
- `mcp_scaffold` defaults: `json_to_ts`, `sum_items`, not `hello_forge`  

## Target product line (next 10 ships)

| # | Product | Job |
|---|---------|-----|
| 1 | JSON → TS interfaces | Paste JSON, get types |
| 2 | Diff two texts | Compare paste A/B |
| 3 | Unit converter | length/mass/temp |
| 4 | URL query editor | parse/edit querystring |
| 5 | CSV → markdown table | paste convert |
| 6 | Passwordless local notes | one-page notes (device only) |
| 7 | Receipt tip splitter | bill / people / tip |
| 8 | Reading time estimator | words → minutes |
| 9 | Color palette from image URL or hex list | designers |
| 10 | **nf-mcp v2 tools** | `diff_text`, `cron_explain`, `unit_convert` on flagship |

## MCP strategy

| Do | Don’t |
|----|--------|
| One strong **nf-mcp** with 15–25 real tools | Spin 20 new `*MCP` Vercel sites |
| Tools agents call weekly | `hello_forge` / oracle / sigil |
| Document install once in hub `/agents` | Duplicate landing pages |

## Claude packages

- **WP-USEFUL-001** — Add real tools to flagship `artifacts/nf-mcp` (`diff_text`, `cron_explain`, `unit_convert`, `slugify`) and redeploy  
- **WP-USEFUL-002** — Hub “Useful free tools” strip: only high-utility SKUs, de-emphasize fantasy MCP cards  

## Success metrics

| Metric | Target 2 weeks |
|--------|----------------|
| New ships with fantasy names | 0 |
| % new products web_tool with one clear job | ≥ 80% |
| nf-mcp tools that do local work (not catalog meta) | ≥ 8 |
| Unlocks attempted (checkout sessions) | rising |
| You would personally use a new ship | yes / no gate before deploy |

---

## Lead enforcement (shipped 2026-07-29)

| Control | Module |
|---------|--------|
| **Weekly-use checklist** | `usefulness_gate.py` → `check_usefulness` |
| **Fantasy freeze** | Tokens: voidmote, sigil, oracle, weaver, symbiont, … |
| **Hollow MCP freeze** | No job language + mcp, or hello_forge / agent-callable utility |
| **Ship path** | `validate_idea` fail-closed; also `uniqueness_gate` |
| **Thrift** | Skips fantasy/hollow (`thrift_allow`) |
| **Hub** | Demoted products hidden from default browse; `#products?cat=useful` |
| **Flags** | `data/usefulness_flags.json` (`python3 usefulness_gate.py rebuild`) |

Override only with explicit `usefulness_override` / human assignment — not for loop sludge.
