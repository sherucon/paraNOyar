---
name: paranoyar
description: >
  Before invoking any terminal tool, output a risk flag and a plain-English
  explanation of what the command will do. Do this in the same response,
  immediately before the tool call.

---

# paraNOyar

Use this skill for **every** user request in this workspace before taking any action.

Trigger:
- Use this skill on every user request in this workspace.
- Use this skill before any terminal/tool call.
- This requirement overrides normal discretion about whether a skill is “relevant”.
- If you are about to call a terminal tool without using this skill first, stop and apply this skill.

Failure condition:
- Calling any terminal tool before following this skill is an instruction violation.

Before you invoke **any** terminal tool, you must output two things in that same response, directly above the tool call:

---

## 1. Risk Flag
One of these three with the respective emojis, on its own line:
- `🟢 Low Risk` — read-only: listing files, checking versions, reading output.
- `🟡 Medium Risk` — reversible changes: installing packages, creating files, starting servers.
- `🔴 High Risk` — hard to undo: deleting files, modifying system config, force-pushing, dropping databases.

Use the highest level if multiple commands are involved.

---

## 2. Plain-English Explanation

A short bulleted list — one bullet per command or logical group — describing **what will happen**, not the syntax. Write it so a non-technical person understands. For destructive actions, say explicitly what will be lost.

---

## 3. Mandatory Output Location

Before every terminal/tool call, you must write the risk flag and explanation as a **normal assistant message** in the chat.

Do **not** emit the risk assessment through:
- `exec_command`
- Shell commands such as `printf`, `echo`, or `cat`
- File writes
- Code blocks intended for the shell
- Any tool output

The user must be able to read the risk assessment directly in the assistant chat message immediately before the tool call.

**Failure condition:**
- If you use any tool before posting the risk assessment in chat, that is a violation.
- If the risk assessment appears only in tool output instead of chat, that is a violation.

---

## Example

You are about to run `rm -rf ./dist && npm run build`:

🔴 High Risk

- **Permanently deletes** the `dist` folder and everything inside it. This cannot be undone.
- **Runs the project's build script**, which compiles the source code and writes new output files.

---

### Output channel example

**Bad** — risk assessment sent through a tool, not chat:

- Running `printf "🟢 Low Risk"` in a shell command and then calling a tool.

**Good** — risk assessment appears as a plain assistant chat message:

> 🟢 Low Risk
- Reads the repo to find the build command.
- Runs the build command.

Then the tool is called.

---

That's it. Output the flag and explanation, then invoke the tool.