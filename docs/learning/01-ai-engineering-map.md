# 01 — The AI-Engineering Map

> Your cheat sheet. Each concept: **what it is**, **how it looks in this repo**, **why it matters**.

---

## 0. Two different kinds of "AI app". Keep them apart.

| Layer | Question | In this project |
|---|---|---|
| **AI to *build* the app** | How do agents write, test, and review my code? | Claude Code + specs + skills + hooks + subagents |
| **AI *inside* the app** | Does the product itself call an LLM? | Recommendations engine (later: Claude API + RAG over our sources) |

Most "AI developer" CV value today comes from mastering **layer 1** and being able to ship **layer 2** safely.
This project does both.

---

## 1. The fundamentals

**LLM (Large Language Model)**: predicts text. On its own it knows nothing about your repo and can't act.

**Context window**: everything the model can "see" in one conversation (your messages, files it read,
tool outputs). It's big but finite. When it fills up, old content gets summarized and detail is lost.
→ *Main rule of AI engineering: put the right information in context at the right time.*

**Prompt engineering vs context engineering**:
- *Prompt engineering* = wording one request well. (What you've been doing.)
- *Context engineering* = designing the **system** of files, docs, and tools so the agent always has what it
  needs: CLAUDE.md, specs, ADRs, skills. (What we're doing now.)

---

## 2. Agents and the agent loop

**Tool**: a function the model can ask to run (read file, edit file, run a shell command, search the web).

**Agent** = LLM + tools + a loop. It doesn't answer once. It keeps going until the goal is reached:

```
        ┌──────────────────────────────────────────┐
        ▼                                          │
  1. Gather context  (read files, specs, search)   │
  2. Plan / decide   (what's the next step?)       │
  3. Act             (edit code, run commands)     │
  4. Verify          (tests, typecheck, lint)  ────┘  ← failures feed back in
  5. Done? → report
```

**Harness**: the runtime *around* the model: which tools it has, permissions, memory files, hooks.
Claude Code **is a harness**. (Fun fact: your folder is called `hardness` 😉)

**Key insight**: an agent is only as good as its **verification step**. If there are no tests,
the loop has no way to notice it's wrong. That's the real reason SDD + tests matter in the AI era:
**acceptance criteria → tests → the agent can check its own work.**

---

## 3. Claude Code building blocks (and where they live)

| Concept | File/location | What it does | When to use it |
|---|---|---|---|
| **Memory** | `CLAUDE.md` | Loaded every session. Project rules and map | Always-true facts & rules. Keep it short |
| **Skill** | `.claude/skills/<name>/SKILL.md` | A packaged procedure. Only its `description` sits in context; the full instructions load **on demand** when relevant or when you type `/name` | Repeatable workflows: `/new-spec`, `/add-source`, `/implement-task` |
| **Subagent** | `.claude/agents/<name>.md` | A separate agent with **its own context window**, its own tools and prompt. It returns a summary to the main agent | Isolated jobs: code reviewer, test writer, research on medical sources. Keeps the main context clean |
| **Hook** | `.claude/settings.json` | A shell command the **harness** runs automatically on events (before/after a tool, at stop…) | Deterministic guarantees: "run lint+typecheck after every edit", "block edits to `.env`" |
| **MCP server** | `.mcp.json` | *Model Context Protocol*: a standard plug that gives the agent new tools (browser, DB, Figma, GitHub…) | Connect external systems |
| **Plan mode** | Shift+Tab in Claude Code | Agent can read & plan but not edit | Before any non-trivial change |
| **Permissions** | settings | What the agent may do without asking | Safety vs. speed tradeoff |

**Skills vs CLAUDE.md**: put something in CLAUDE.md if it applies to *every* task.
Put it in a skill if it's a procedure for *some* tasks. This keeps context lean ("progressive disclosure").

**Hooks vs instructions**: an instruction ("please run tests") is a *request*: the model can forget.
A hook is *code*: it always runs. Use hooks for anything that must never be skipped.

---

## 4. Workflow patterns (how agents are combined)

From Anthropic's *"Building Effective Agents"*, the vocabulary everyone uses:

| Pattern | Idea | Example here |
|---|---|---|
| **Prompt chaining** | Step A's output → step B's input | requirements → design → tasks |
| **Routing** | Classify, then send to a specialist | "is this a bug, a feature, or a content change?" |
| **Parallelization** | Several agents at once, results merged | 3 reviewers: a11y, security, perf |
| **Orchestrator–workers** | A lead agent splits the work and delegates to subagents | Main agent delegates "write tests" to a test subagent |
| **Evaluator–optimizer** | One agent generates, another critiques, loop | Writer drafts advice copy → reviewer checks it against sources |

**Rule of thumb**: use the simplest pattern that works. Most tasks = one agent + a good spec + tests.

**This table is a menu, not a checklist.** Patterns appear in two ways:
- *Implicitly*: the main agent picks them on the fly (e.g. it spawns an `Explore` subagent for a broad search).
- *Explicitly*: you configure them as files (skills that chain steps, subagents in `.claude/agents/`, hooks).

Add a piece only when something hurts (e.g. a reviewer subagent once the same kind of mistake keeps recurring).

---

## 5. Spec-Driven Development (SDD)

**What**: the spec, not the prompt, is the source of truth. Code is *generated from* and *checked against* it.

**Flow in this repo** (same shape as Kiro and GitHub Spec Kit):

```
vision.md → requirements.md (EARS) → design.md → tasks.md → implement 1 task → verify → next
              ▲ approve              ▲ approve    ▲ approve
```

**Why it beats "prompt the PO ticket"**:
- The agent gets unambiguous, testable criteria instead of guessing.
- You review a 1-page spec (cheap) instead of a 600-line diff (expensive).
- Specs are shared knowledge. A chat can be resumed, but only that one conversation gets its context back.
  Long chats also get summarized (compaction) and lose detail, and they're full of dead ends. A spec is seen by
  every session, subagent, CI run and human, it's versioned in git, and it holds only the approved version.
  → *Chat = the meeting. Spec = the minutes.* Resume a chat for short-term continuity; write files for decisions.

**EARS** (*Easy Approach to Requirements Syntax*): `WHEN <trigger> THE SYSTEM SHALL <response>`.
Each criterion gets an ID and is covered by **at least one test** that carries that ID:

```
requirements.md:  AC-1.2: IF the name is empty THEN THE SYSTEM SHALL disable the Save button.
test file:        it('AC-1.2: disables Save when name is empty', ...)
```
You (as PO) decide *what* the criteria are by approving them. The AC→test link is a *convention*
written in `design.md` (Testing strategy) and `tasks.md` (Verify). It can later be *enforced* by a hook/reviewer.

**Which document for what**:

| Doc | Scope | How many |
|---|---|---|
| `product/vision.md` | The whole app: why, for whom, pillars | One, rarely changes |
| `specs/NNN-feature/` | One feature (≈ an epic): requirements, design, tasks | One folder per feature |
| items in `tasks.md` | Small implementation steps (≈ subtasks / PRs) | Many per feature |
| `adr/NNNN-*.md` | One cross-cutting technical decision (≈ "why we chose X") | One file per decision |

- New feature → new spec folder. Change to an existing feature → edit its spec, then the code.
- Bug fix → no new spec; fix + regression test (maybe add a missing AC).
- **ADR** (*Architecture Decision Record*): one decision per file, so it stays small and linkable, and
  it's never re-argued. Changing your mind = a new ADR that *supersedes* the old one (the history of *why* survives).
  Specs say **what the app does**; ADRs say **why it's built this way**.

---

## 6. Verification & quality (the part that makes it "senior")

- **TDD with agents**: have the agent write failing tests from the ACs *first*, then implement.
- **Review**: `/code-review` or a reviewer subagent before every commit. You're the final reviewer.
- **CI**: GitHub Actions runs tests on every push. The agent's work must pass the same gate as a human's.
- **Evals** (layer 2): automated tests for *LLM output quality* (e.g. "does every recommendation cite a source?").

---

## 7. Glossary quick-ref

| Term | One-liner |
|---|---|
| Token | Chunk of text (~¾ word). Cost and context are measured in tokens |
| Tool use / function calling | Model requests a function call with structured args |
| Agentic loop | Gather → act → verify → repeat |
| Subagent | Child agent with isolated context |
| Skill | On-demand packaged instructions (`SKILL.md`) |
| Hook | Deterministic script triggered by harness events |
| MCP | Standard protocol for plugging tools/data into agents |
| RAG | Retrieve relevant docs, then generate an answer grounded on them |
| Grounding | Forcing the answer to rely on provided sources |
| Hallucination | Confident, wrong output. Countered by grounding + verification |
| Guardrails | Rules/checks limiting what the AI may output (e.g. no diagnoses) |
| Evals | Test suites for AI behavior |
| Headless mode | Running Claude Code non-interactively (`claude -p`), e.g. in CI |
| Worktree | Separate git checkout so parallel agents don't collide |
