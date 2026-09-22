---
name: wrap-up
description: End-of-session ritual for this project - update the learning journey, check docs are consistent, and prepare the commit. Use when the user says they're finishing, closing the session, or types /wrap-up.
---

# Wrap up the session

Close the session so the next one (a different chat, with no memory of this one) can pick up cleanly.

## Steps

1. **Update [docs/learning/journey.md](../../../docs/learning/journey.md)**
   - Move completed items from `## Next` to `## Done`, under a dated session entry.
   - List the **concepts the user learned** this session (they're building an AI-engineering skillset).
   - Rewrite `## Next` so the first item is the very next concrete action.

2. **Check consistency** (report, don't silently fix anything big)
   - Do decisions made this session exist as ADRs? Are statuses right?
   - Does `CLAUDE.md` still match reality (phase, stack, rules)?
   - Are new concepts captured in `docs/learning/`?
   - Do any specs need their status updated?

3. **Summarize for the user**: what we did, what they learned, what's next. Keep it short.

4. **Propose a commit**: show the message, and commit only if the user agrees.
   Message style: `docs: <what changed>` / `feat: <feature>` / `chore: <setup>`.

## Rules

- Never mark anything `Approved`/`Accepted` that the user didn't approve out loud.
- If something is unfinished or unclear, write it down in `journey.md` instead of leaving it in the chat.
