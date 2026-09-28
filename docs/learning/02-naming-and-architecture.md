# 02 — Naming, data modelling & architecture

Concepts from session 3 (2026-09-28), each with the moment in this project where it came up.

## Data modelling

- **Derived state.** Don't store what you can compute. Like React's "don't `useState` what you can derive
  from props". Here: a rating stores only its `value`; the `level` is computed (`levelOf`). Storing both
  would allow value 9 + level Low. (design.md DM-D1)
- **Make illegal states unrepresentable.** Shape the types so that invalid data can't be written at all.
  Like `{status:'loading'} | {status:'error', error}` instead of two booleans. Here: `Ratings` is a union
  keyed by axis, so "zero ratings" or "two Energy ratings" don't compile. (DM-D2)
  Limit: types don't check lengths or data read back from storage; that needs runtime validation.
- **Snapshot vs reference.** An order line stores `productId` *and* `priceAtPurchase`, because prices
  change. Here: an `Occurrence` stores `itemId` (what happened) *and* `effect` (as what it happened then). (DM-D7)

## Naming

- **Ubiquitous language** (from Domain-Driven Design). One word per concept, identical in specs, code and
  conversation. The glossary in each spec *is* the naming. Renaming a term = a new spec version
  (End → Effect, requirements v1.1).
- **Names slip in unchosen.** "Item" was an agent placeholder that got approved with everything else.
  When reviewing an agent's draft, ask: *which names did we actually choose?*

## Architecture

- **Screaming architecture** (Uncle Bob). The folder tree shows what the app *does* (`lists/`, `longings/`),
  not which framework it uses (`components/`, `hooks/`). (ADR-0003)
- **Light DDD.** Borrow what pays off (ubiquitous language, separate vocabulary areas per feature); skip
  what's ceremony for a one-person local app (aggregates, repositories, domain events).
- **ADRs: one decision each; supersede vs amend.** *Supersede* = replace a whole ADR. *Amend* = change one
  part, the rest stays in force. ADR-0002 bundled two decisions, so changing one forced an amendment.
- **Decisions don't update old text.** After every decision, search the repo for the old term
  (`src/domain` was still in `CLAUDE.md`). Same as grepping a prop name after renaming it.

## UI design without a designer

Fidelity ladder, cheapest first, each step approved before the next:
**ASCII wireframes** (structure, taps) → **visual tokens** (colours per effect/level, type, spacing;
colour never the only signal) → **clickable HTML mockup** on the phone → **real React code**.
The agent can't draw images; it can write HTML/SVG. Figma is possible via an MCP server, not set up.
