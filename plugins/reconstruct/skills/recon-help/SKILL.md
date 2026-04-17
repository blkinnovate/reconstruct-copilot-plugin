---
name: recon-help
description: "Tutorial and quick reference for Reconstruct workflow"
user-invocable: true
disable-model-invocation: false
context: main
version: v0.5
---

# Reconstruct Help

Get help with Reconstruct workflow.

## Usage

```
/recon-help           → Show this quick reference
/recon-help tutorial  → Full tutorial walkthrough
/recon-help [topic]   → Help on specific topic
```

---

## Quick Reference

In this Copilot plugin, workflows are exposed as **skills** (e.g. **recon-manager**, **recon-worker**, **recon-ask-constructor**). Slash-command names below describe the same flows as in Cursor/Claude template commands.

### Commands / skills

| Command / skill | Purpose |
|-----------------|---------|
| `/recon-setup` / **recon-setup** | Connect workspace to project (one-time) |
| `/recon-seed` / **recon-seed** | Onboarding: seed Context Cloud with project knowledge |
| `/recon-manager` / **recon-manager** | Manager agent: plan work, create capsules |
| `/recon-worker` / **recon-worker** | Worker agent: execute plans |
| `/recon-ask-constructor` / **recon-ask-constructor** | Generate capsule + plan via MCP `ask_constructor`, then create/store/link and execute |
| `/recon-help` / **recon-help** | This help |

### Typical Workflow

```
1. /recon-setup      → Connect project (once)
2. /recon-seed       → (Optional) Seed Context Cloud with project knowledge
3. /recon-manager    → Describe work, create capsule + plan
4. Open new chat
5. /recon-worker     → Execute the plan
6. Return to manager chat, say "done"
```

### Ways to Use Reconstruct

**0) Web app Constructor (interactive planning UI)**

- Flow (typical): open Constructor in the Reconstruct web app → enter mission → review capsule + plan → approve/create → then execute in VS Code / Copilot via the worker flow
- **recon-ask-constructor** calls the MCP tool `ask_constructor` to generate a similar “task package” (capsule context + plan) inside the editor

**A) Standard: Manager → Worker**

```
/recon-manager  → creates capsule + stores plan + links session
new chat
/recon-worker   → executes the stored plan with approvals
```

**B) Single-chat: recon-ask-constructor skill**

- Use when: you want “generate plan + execute” in one session for a focused task; confirm scope before edits (same as worker rules)

**C) Onboarding: recon-seed**

```
/recon-seed
```

---

## Tutorial Mode

**If user said `/recon-help tutorial`:**

### Welcome to Reconstruct! 👋

Reconstruct helps you work with AI agents on coding projects with guardrails and context management.

**Key Concepts:**

1. **Project** - Your codebase connected to Reconstruct
2. **Capsule** - A workspace for specific work (has guardrails, allowed paths)
3. **Session** - Active work context (links you to a capsule + plan)
4. **Plan** - Implementation instructions the agent follows

**Two Agents:**

| Agent | Role | Command |
|-------|------|---------|
| Manager | Plans work, creates capsules, reviews results | `/recon-manager` |
| Worker | Executes plans, makes code changes | `/recon-worker` |

**Why Two Agents?**

- Manager has broader context (project overview, planning)
- Implementation is focused (just the current task)
- Clean handoff prevents context pollution
- Human stays in control at transition points

---

### Let's Try It!

```
Step 1: Run /recon-setup to connect your project
Step 2: (Optional) Run /recon-seed to seed project context
Step 3: Run /recon-manager and describe some work
Step 4: The manager will create a capsule and plan
Step 5: Open a new chat window
Step 6: Run /recon-worker to execute
Step 7: Approve each change as it's made
Step 8: Return to manager when done
```

**Ready?** Run `/recon-setup` to begin!

---

## Topic Help

**If user said `/recon-help [topic]`:**

### Topics

**seed** - Onboarding flow for Context Cloud:
- Run `/recon-seed` to populate project context via Q&A rounds and repo scan
- Works for first-time seed or re-seed (update existing)
- User approval required before any write to cloud

**capsules** - Capsules define work scope:
- `allowed_path_patterns` - Where agent CAN work
- `forbidden_path_patterns` - Where agent CANNOT work
- `guardrails` - Rules agent must follow
- `task_summary` - What needs to be done

**sessions** - Sessions track active work:
- Max 2 active sessions per user per project
- Contains reference to current plan
- Archive when work complete

**plans** - Plans guide implementation:
- Created by manager agent
- Single-step or multi-step
- Implementation agent follows exactly

**guardrails** - Safety constraints:
- Path restrictions (allowed/forbidden)
- Operation restrictions (no delete, etc.)
- Content rules (patterns to follow)

**errors** - Common issues:
- "MCP not configured" → Check API key / MCP configuration in VS Code (plugin `.mcp.json`)
- "No session" → Run `/recon-manager` first
- "2 session limit" → Archive an old session
- See `/recon-help recovery` for more

**recovery** - When things go wrong:
- Check state with preferences.json + get_session
- Most issues fixed by re-running setup or manager
- Nuclear option: delete `.reconstruct/` and start fresh

---

## Still Stuck?

```
1. Check reconstruct.app dashboard for project state
2. Review capsule settings in dashboard
3. Try /recon-sync to refresh context
4. Delete .reconstruct/ and run /recon-setup fresh
```
