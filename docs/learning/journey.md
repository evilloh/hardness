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

- [x] **Session 2 (2026-09-24): Vision v0.4 + first spec requirements**
  - Session-start ritual explained: `CLAUDE.md` → `journey.md` → verify against files/git → reconcile → act
  - Concepts: `CLAUDE.md` (always loaded) vs skills (on demand) vs hooks (guaranteed); plan mode vs specs;
    **information altitude** (vision / design / evidence / decision); release (v1) vs spec vs task vs session;
    a change to an approved doc = new version + new approval; "what did the agent add on its own?" when reviewing
  - SRC-001 vetted. Research cycle 2: [compound-learning-little-often](../research/notes/compound-learning-little-often.md)
    (spacing beats cramming; "37× better" is not how learning curves work) → SRC-006…010 pending
  - Vision v0.3 → **v0.4 approved**: diary + mantras, meditation, mood check-in, statistics, release plan
    (v1 = lists, 1%, journal, mood), EN/ES/IT, **two axes** (Energy: Drains↔Recharges, Mood: Lifts↔Drags) + Longings
  - First real use of `/new-spec`: **spec 001 — The lists, requirements approved**
  - Commit: pending (user is switching the GitHub account in VS Code)

## Next

1. [ ] **Commit session 2** (after the GitHub account switch)
2. [ ] Spec 001 **`design.md`**: screens, colours per end/level, the split pill, data model
3. [ ] User vets **SRC-002…010** in [`sources.md`](../research/sources.md) (homework, not blocking spec 001)
4. [ ] Research + vet **help resources** for EN / ES / IT (spec 001 AC-6.6, needed before release)
5. [ ] Spec 001 `tasks.md`, then scaffold the Vite + React + TS PWA and the testing-stack ADR
6. [ ] First **hook**: typecheck + tests after every edit

## Later (concepts waiting for their moment)

- Subagents (first: a reviewer), `/code-review`, CI with GitHub Actions
- Layer 2 (AI inside the app): Claude API, RAG over our sources, guardrails, evals
