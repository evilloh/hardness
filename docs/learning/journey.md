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
  - Skills created: `/new-spec`, `/wrap-up`

## Next

1. [ ] User reviews [`docs/product/vision.md`](../product/vision.md) v0.2 and answers its open questions
      (how to log low moments, daily mood check-in?, languages, which pillar first)
2. [ ] First git commit (the foundations)
3. [ ] Run `/new-spec` → spec **001 — The four lists** (first full SDD cycle: requirements → design → tasks)
4. [ ] Scaffold the Vite + React + TS PWA, then the testing-stack ADR
5. [ ] First **hook**: typecheck + tests after every edit

## Later (concepts waiting for their moment)

- Subagents (first: a reviewer), `/code-review`, CI with GitHub Actions
- Research workflow for medical sources (web search + user vetting)
- Layer 2 (AI inside the app): Claude API, RAG over our sources, guardrails, evals
