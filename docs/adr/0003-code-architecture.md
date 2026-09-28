# 0003 — Code architecture: feature-first folders, light DDD

- **Status**: Accepted (by the user, 2026-09-28)
- **Date**: 2026-09-28
- **Amends**: [0002](0002-platform-and-stack.md), only *where* domain code lives (`src/domain/`). Its rule
  "domain logic is framework-agnostic, UI depends on domain" stays in force.

## Context

Spec 001's design is about to name folders and types, and the naming discussion (End → Effect) showed we
need one agreed vocabulary. ADR-0002 put all domain logic in one top-level `src/domain/`. That is a
*layer-first* layout: the tree says "domain / ui", not "lists / journal / practices".

The app will grow by pillars (lists, practices, journal, mood, insights), each with its own words.
It is built by one developer plus an AI agent, which needs to find everything about one feature in one place
and must not blur vocabularies.

## Options

### A. Layer-first (ADR-0002 as written)
`src/domain/lists/`, `src/ui/lists/`, `src/data/lists/`…
- ➕ Already written down; the purity boundary is one folder, easy to lint
- ➖ One feature is spread over three trees; the top level says nothing about the app

### B. Feature-first ("screaming architecture") with a light DDD vocabulary
`src/lists/domain/`, `src/lists/ui/`…
- ➕ The tree shouts what the app does; one feature = one folder (for humans and for the agent's context)
- ➕ Maps naturally to vision pillars and to the specs' glossaries
- ➖ The purity rule must be checked in every `*/domain/` folder, not one

### C. Full DDD / hexagonal (aggregates, repositories, ports & adapters, domain events)
- ➕ Scales to large teams and complex business rules
- ➖ Ceremony for a single-user, local-first app; lots of new concepts that don't earn their keep yet

## Decision

**Option B.**

```
src/
  app/          shell: routing, providers, PWA setup, language switch
  lists/        spec 001: Item, Effect, Rating, Occurrence, the four lists
    domain/     pure TS: types + rules (levelOf, sortList…). No React, browser or storage imports
    ui/         React: screens and components
    data/       storage access (library decided in its own ADR)
    index.ts    the feature's public API
  longings/     spec 001: Longing
  shared/       only what ≥2 features really use (Id, Timestamp, UI kit, i18n)
```

Rules:

1. **Top-level folders are named after domain concepts** from the specs' glossaries, never after tech
   (`components/`, `hooks/`, `services/` are not allowed at the top level).
2. **Dependency direction**: `ui → domain`, `data → domain`. `domain` imports nothing from `ui`, `data`,
   React or browser APIs (ADR-0002's rule, now per feature).
3. **Features talk only through `index.ts`.** No reaching into another feature's internals.
4. **Light DDD, not full DDD**: we adopt the **ubiquitous language** (each spec's glossary *is* the naming;
   code names match it; renaming a term = a new spec version). Features act as separate vocabulary areas.
   We do **not** adopt aggregates, repository/port patterns or domain events unless a future ADR says so.
5. **Folders follow vocabulary, not specs.** One spec can touch several features (001 → `lists` and
   `longings`), and one feature will be touched by many specs.
6. `shared/` starts empty and grows only when a second feature needs something ("rule of two").

## Consequences

- ➕ Opening `src/` tells you what Hardness does; one feature's code is in one place.
- ➕ The glossary → code link is explicit, so the agent has one source for names.
- ➖ Until a lint rule exists, rules 2–3 rely on convention and review. The rule (e.g. `no-restricted-imports`
  or `eslint-plugin-boundaries`) is added when the project is scaffolded (tooling/testing ADR).
- ➖ Risk of `shared/` becoming a junk drawer; rule 6 is the guard.
- ADR-0002's status line points here ("domain location amended by 0003"); its text is not rewritten.
