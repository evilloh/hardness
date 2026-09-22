---
name: new-spec
description: Start a new feature spec following this project's Spec-Driven Development flow. Use when the user wants to add, plan, or specify a new feature, or types /new-spec.
---

# New spec

You are creating a feature spec for the Hardness app. **Do not write any production code in this skill.**

## Steps

1. **Understand**: read `docs/product/vision.md`, `docs/specs/README.md`, and existing specs to avoid overlap.
2. **Interview**: ask the user 3–6 focused questions about the feature (who, what, why, edge cases,
   what's out of scope). Wait for the answers.
3. **Scaffold**: pick the next number `NNN` and create `docs/specs/NNN-kebab-name/` by copying
   `docs/specs/_template/`.
4. **Write `requirements.md` only**: user stories and EARS acceptance criteria. Fill in the
   safety & privacy checklist honestly.
5. **Register**: add the spec to the index table in `docs/specs/README.md` with status `Draft`.
6. **Stop and ask for review.** `design.md` and `tasks.md` are written only after the user approves
   the requirements (one phase at a time, one approval per phase).

## Quality bar for acceptance criteria

- Each one is testable by a human or an automated test.
- No implementation details ("use Zustand") in requirements. Those belong in `design.md`.
- Advice-related criteria reference a source ID from `docs/research/sources.md` (or flag it as TODO).
