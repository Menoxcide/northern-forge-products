# After voice-controlled PCs: what comes next

**Lead thesis (2026-07-29):**  
People will drive their **phones → home PCs → clusters** with **voice + AI**. The winners are not better chat UIs. They are **trusted remote action systems**: hear intent, plan safely, act on *your* machines, prove what happened, get paid for outcomes.

Northern Forge already sits on that path: **S24 voice-adjacent notify**, **Tailscale mesh**, **Hermes/Cognis multi-agent**, **always_on loops**, **MCP**, **local-first**. We do **not** need more Voidmote shells. We need the **control plane for agentic remote work**.

---

## The stack that is forming

```
Voice (phone / earbuds / car)
    → Intent (STT + LLM)
        → Plan (agent)
            → Scoped tools (shell, browser, deploy, k8s, files)
                → Remote runtime (this PC · JUSTIN · cluster · cloud)
                    → Verify (screenshot, logs, diff, receipt)
                        → Memory (what worked on THIS machine)
                            → Money (unlocks, agent labor, ops retainers)
```

Today’s toys: “Hey agent, open Chrome.”  
Tomorrow’s defaults: “Deploy staging, watch the job, text me if GPU OOM, roll back if health fails.”

---

## What comes *after* voice remote control

### 1. Capability scopes (trust, not cleverness)
Voice is dangerous. Next product is **permission envelopes**:
- `read_files` yes · `rm -rf` never without 2FA  
- Time-boxed elevation: “sudo for 5 minutes”  
- Per-machine roles: laptop vs training box vs prod  

**Build:** MCP tools `list_capabilities`, `request_elevation`, `deny_reason` on the mesh host.

### 2. Continuous verification (eyes for ears)
Voice is blind. Next layer is **narrated proof**:
- “I opened the PR. Diff is +120/−40. Tests still running.”  
- Screen/OCR/log tails as first-class tool results  
- Human can barge-in: “stop”, “show me”, “undo”  

**Build:** `describe_session`, `tail_job`, `screenshot_summary` (local).

### 3. Multi-machine orchestration (not one PC)
Users will own a **fleet**: phone, desktop, NAS, 1–N GPUs.
Voice becomes **router**: “Run training on the 4090 box, not the laptop.”

**Build on our mesh:** Tailscale nodes TI/JUSTIN/MEG/S24 as **targets**, not lore.
MCP: `list_nodes`, `run_on(node, cmd)`, `job_status`.

### 4. Machine memory (stigmergy of *this* computer)
Cloud agents forget your weird paths. Next: **per-host memory**
- “On this PC, deploys use `vercel --prod` from `artifacts/…`”  
- Failed commands with fixes that worked  
- Same idea as our stigmergy, scoped to host_id  

**Build:** `host_memory_read/write` in nf-mcp + local sqlite.

### 5. Voice for *ops loops*, not only one-shots
People won’t only say discrete commands. They’ll say:
- “Keep the site green overnight.”  
- “If Stripe webhook fails, page me.”  

That’s **always_on for personal/work machines** — we already run fleet loops; productize a **personal always_on**.

### 6. Skill packs that run *on your metal*
MCP/skills shift from “chat plugins” to **installable labor**:
- “Install the deploy skill on my laptop”  
- Runs with local credentials, not uploaded keys  

**Build:** agent_skill packages that wrap *real* jobs: deploy hub, oil fleet, paste thrift, restart watchdog — **our** ADP as the first customer.

### 7. Money layer
Once voice controls clusters, spend appears:
- GPU minutes, API credits, human review  
- **Pro unlocks** for safer automation (confirm policies, multi-node, audit export)  
- Retainers: “keep my forge green”  

Cash path we already have (Stripe unlocks) maps cleanly to **Pro: multi-node + audit log + voice confirm**.

---

## Northern Forge wedge (useful, not fantasy)

### North-star product (12 months)
**Forge Voice Mesh** — speak to your forge; it acts on your Tailscale machines with scopes, logs, and optional Pro.

### Phase 0 (now — lead) ✅ adjacent
- Mesh + always_on + S24 notify + MCP flagship + usefulness gate  
- Cash links on tools people understand  

### Phase 1 — **Voice Action Queue** (web tool, local-first)
**Job:** Type or paste (later: voice) an intent → get a **reviewable action list** → approve → run locally or via SSH target.

- Free: parse intent → checklist  
- Pro: multi-step plans, saved targets, export audit JSON  

Plain name: **“Remote action checklist”** (passes usefulness gate).

### Phase 2 — **Mesh MCP (flagship expansion)**
On **nf-mcp only** (no new hollow MCP sites):

| Tool | Job | Status |
|------|-----|--------|
| `list_mesh_snapshot` | What’s online (from command-center mesh snapshot) | ✅ shipped (WP-VOICE-001) |
| `forge_loop_status` | always_on / loop_health (read-only) | ✅ shipped (WP-VOICE-001) |
| `queue_action` | Append proposed action to local queue for human review (no execution) | ✅ shipped (WP-VOICE-001) |
| `list_queued_actions` | Read back the queue | ✅ shipped (WP-VOICE-001) |
| `run_safe_cmd` | Allowlisted commands only | ✅ shipped (WP-VOICE-005) |
| `host_memory_get/set` | Per-host notes | ✅ shipped (WP-VOICE-004) |

Read/write local files only, plus `run_safe_cmd`'s fixed-argv status allowlist (`uptime`, `disk_usage`, `mem_usage`, `always_on_status`, `loop_board` — no free-form shell, no mutating commands) — all six ship in `artifacts/nf-mcp/lib/tools.js` and degrade to `available:false` off the operator host (e.g. public Vercel prod), since that deployment doesn't bundle the ADP checkout.

### Phase 3 — **S24 voice in**
- Notification → reply text already exists  
- ✅ Free-text / voice-transcript replies (no KEY=value) → `data/action_queue.jsonl` via `config_inbox.queue_s24_action` (review only)  
- ✅ `s24_notify.notify_action_prompt` + URI to Remote action checklist  
- Next: native voice note → STT → same queue  
- Confirm high-risk with push + biometric  

**Scoped (2026-07-29):** the `REPLY` action's `behavior: textInput` already opens Android's
standard reply box, whose keyboard mic runs OS-level dictation into that same `textInput` field —
so *spoken* intent already reaches `queue_s24_action` today, just via the keyboard's STT, not ours.
"Native voice note → STT" (an actual audio attachment transcribed server-side, e.g. with
faster-whisper) is a materially different feature: HA's `notify.mobile_app_*` actionable
notifications don't support an audio-attach reply action, so it needs either (a) a companion-app
"record audio" notify action (not in stock HA mobile app), or (b) a separate Android-side automation
(Tasker / HA voice assistant shortcut) that records a clip and drops it somewhere this host's
`config_inbox` pipeline can pick up, then this host runs STT and calls `queue_s24_action` on the
transcript. Both paths require configuration *on the S24 / HA companion app itself* — not just repo
code — so this is not a self-contained WP-VOICE-006 package; it needs a human (or Grok, who has the
JUSTIN/HA mesh access) to add the device-side audio-capture hook first. Until then this phase stays
covered by the existing text/dictation path; no further Claude-side code work here.

### Phase 4 — **Cluster targets**
- GPU job submit/status  
- Deploy promote/rollback  
- Cost estimate before run (“this will burn ~$X API”)  

---

## What we will *not* build

- More oracle/sigil/void* MCP landings  
- Unscoped “run anything” shell for agents  
- Cloud-only agents that need all your keys uploaded  
- Voice gimmicks without audit trails  

---

## Competitive frame

| Player | Strength | Gap we can own |
|--------|----------|----------------|
| Big assistants | STT/LLM quality | Your metal, your mesh, your scopes |
| RPA / scripts | Reliable clicks | Language + multi-host + memory |
| DevOps platforms | Clusters | Phone-native voice + sovereign home lab |
| **Us** | Mesh + loops + MCP + phone | Productize **trusted remote action** |

---

## Immediate build order (lead)

1. **Policy** — usefulness gate already freezes fantasy ships.  
2. **Claude WP-VOICE-001** — expand nf-mcp with `forge_loop_status`, `queue_action`, allowlisted status tools (read-first).  
3. **Claude WP-VOICE-002** — web tool: **Remote action checklist** (intent → steps → copy commands / mark done).  
4. **Grok** — wire S24 notify → action queue file; thrift only useful tools.  
5. **Pro unlock** — audit export + multi-target plans on that checklist tool.  

### Success in 30 days
- One tool you use **weekly** to drive the forge by language (typed, then voice)  
- nf-mcp tools a coding agent actually calls for **status + safe actions**  
- Zero new fantasy MCP sites  

---

## One-liner

**Voice remote control is the keyboard of the 2030s.  
What comes next is the OS: scopes, proof, multi-machine memory, and paid reliability.**
