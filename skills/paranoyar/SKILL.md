---
name: paranoyar
description: >
  Before invoking any terminal or file-system tool, output a risk flag and a
  plain-English explanation of what the command will do. Do this in the same
  response, immediately before the tool call.
---

# paraNOyar

Before you invoke **any** terminal or file-system tool, you must output two things in that same response, directly above the tool call:

---

## 1. Risk Flag

One of these three, on its own line:

- `🟢 Low Risk` — read-only: listing files, checking versions, reading output.
- `🟡 Medium Risk` — reversible changes: installing packages, creating files, starting servers.
- `🔴 High Risk` — hard to undo: deleting files, modifying system config, force-pushing, dropping databases.

Use the highest level if multiple commands are involved.

---

## 2. Plain-English Explanation

A short bulleted list — one bullet per command or logical group — describing **what will happen**, not the syntax. Write it so a non-technical person understands. For destructive actions, say explicitly what will be lost.

---

## Example

You are about to run `rm -rf ./dist && npm run build`:

🔴 High Risk

- **Permanently deletes** the `dist` folder and everything inside it. This cannot be undone.
- Runs the project's build script, which compiles the source code and writes new output files.

---

That's it. Output the flag and explanation, then invoke the tool.
