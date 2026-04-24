# paraNOyar 🔐

**Informed consent for AI coding agents.**

> Stop blindly approving AI commands. paraNOyar forces your AI assistant to explain every terminal action in plain English — and wait for your *explicit* green light before touching anything.

---

## The Problem

AI coding agents are powerful. They're also terrifying when they silently run `rm -rf`, install unknown packages, or reset your database — all while you're nodding along to a code explanation you only half-understood.

paraNOyar puts you back in control. Not by slowing the AI down, but by making it *speak human* before it acts.

---

## How It Works

Whenever your AI agent is about to run a command — any command, even a simple `ls` — paraNOyar forces it to output this 3-step block **immediately before** invoking the tool:

**Step 1 — Risk Badge**
The AI opens with a risk classification:
- `🟢 Low Risk` — read-only (listing files, checking status)
- `🟡 Medium Risk` — state-changing (installing packages, writing files)
- `🔴 High Risk` — destructive (deleting files, running scripts, resetting databases)

**Step 2 — Exact Command Preview**
The AI shows you the exact, unmodified commands it wants to run.

**Step 3 — ELI5 Translation**
The AI explains each command in plain English — what it does, what changes, and what could be lost.

Then the agent **immediately invokes the tool**, and the native **Run / Skip** button appears. That button is your approval gate — no need to type Y or N. Read the explanation, then click Run or Skip.

---

## Full Example

Here's what you'll see when your AI wants to set up a database:

> 🔴 **High Risk**
>
> ```bash
> npm install sqlite3
> rm -rf temp_data
> ```
>
> **paraNOyar Translation:**
> - Downloads a third-party tool called "sqlite3" from the internet to manage your database.
> - **Permanently deletes** the folder named "temp_data". This cannot be undone.

↓ The agent immediately invokes the tool, and the native **Run / Skip** prompt appears. That's it — no need to type anything. Click **Run** to approve or **Skip** to cancel.

---

## Installation

Install into your project for any agent with a single command:

**Cursor**
```bash
npx skills add sherucon/paranoyar -a cursor
```

**Windsurf**
```bash
npx skills add sherucon/paranoyar -a windsurf
```

**Cline / RooCode**
```bash
npx skills add sherucon/paranoyar -a cline
```

**Claude Code**
```bash
npx skills add sherucon/paranoyar -a claude-code
```

**Codex CLI**
```bash
npx skills add sherucon/paranoyar -a codex
```

**Antigravity**
```bash
npx skills add sherucon/paranoyar -a antigravity
```

**All agents at once**
```bash
npx skills add sherucon/paranoyar -a cursor -a windsurf -a cline
```

The skill is installed into your project's agent directory (e.g., `.cursor/skills/paranoyar/`). It only affects the project it's installed in.

---

## What paraNOyar Does NOT Do

- ❌ It does **not** block commands — you always have the final say.
- ❌ It does **not** see your code or files.
- ❌ It does **not** log anything or phone home.
- ❌ It does **not** slow the AI down — it only changes *how* the AI communicates before acting.
- ✅ It simply requires the AI to be transparent and wait for your approval.

---

## Who Is This For?

- **Non-technical founders** building apps with AI who are terrified of raw terminal commands.
- **Security-conscious developers** who want an audit trail and an "air gap" before an AI runs destructive commands.
- **Students and junior devs** who want to learn *why* the AI is doing what it's doing, not just watch it happen.

---

## Uninstalling

To remove the skill from a specific agent, delete the skill directory:

```bash
# Cursor example
rm -rf .cursor/skills/paranoyar
```

Once removed, the protocol no longer applies.

---

## License

MIT © [sherucon](https://github.com/sherucon)
