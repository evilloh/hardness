# Learning Journey

> The progress log of this project as a learning path. Claude reads this at the start of every session
> to know where we are. Update it whenever a step is completed.

## Done

- [x] **Session 1 (2026-09-22): Foundations**
  - Repo skeleton: `CLAUDE.md`, vision, specs templates, ADRs, research policy, first skill (`/new-spec`)
  - Concepts learned: agent & agent loop, harness, tools, context engineering vs prompt engineering,
    CLAUDE.md / skills / subagents / hooks / MCP, workflow patterns (menu, not checklist), SDD, EARS, ADRs,
    chat resume vs files, human-in-the-loop collaboration model
  - Decided: **ADR-0002 — React PWA** (SPA vs PWA explained)
  - Vision v0.2 written with the user: the name (harness + hard, Nessie logo), the **four lists**
    (Drains / Restores / Lifts / Longings), the **1% continuous progress** idea, the photo/notes journal
  - Ethical stance added: **no engagement hooks**, "reward the return, not the streak"
    (vision non-goals + principles 4–6, `CLAUDE.md` domain rules, spec-template checklist)
  - **First real research cycle**: the user challenged an unsourced claim Claude had written into the
    vision → web research → [note](../research/notes/rewarding-returns-vs-streaks.md) + SRC-001…005,
    with an explicit "what the evidence does NOT say" section and a rejected-techniques table
  - Skills created: `/new-spec`, `/wrap-up`, `/research-topic`
  - Lessons: a rule added to `CLAUDE.md` does **not** retroactively fix text written earlier;
    instructions ≠ guarantees (that's what hooks are for); **skills are discovered at session start**,
    so a skill created mid-session only becomes invocable in the next one
  - Commit: `dd4a22c` (foundations)

## Next

1. [ ] **User vets SRC-001…005** in [`sources.md`](../research/sources.md) (status `pending` → `vetted`)
      and reads the note [rewarding-returns-vs-streaks](../research/notes/rewarding-returns-vs-streaks.md)
2. [ ] User reviews [`docs/product/vision.md`](../product/vision.md) v0.2 and answers its open questions
      (how to log low moments, daily mood check-in?, languages, which pillar first)
3. [ ] Commit the anti-gamification + research changes
4. [ ] Run `/new-spec` → spec **001 — The four lists** (first full SDD cycle: requirements → design → tasks)
5. [ ] Scaffold the Vite + React + TS PWA, then the testing-stack ADR
6. [ ] First **hook**: typecheck + tests after every edit

## Later (concepts waiting for their moment)

- Subagents (first: a reviewer), `/code-review`, CI with GitHub Actions
- Layer 2 (AI inside the app): Claude API, RAG over our sources, guardrails, evals
