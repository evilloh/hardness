# 001 — The lists: Design

- **Status**: Draft
- **Requirements**: [requirements.md](requirements.md)

## Overview

2–3 sentences: the approach.

## UI / screens

Mobile-first flows. ASCII sketches are fine.

## Components

| Component | Responsibility | Props / state |
|---|---|---|

## Data model

Framework-agnostic types in `src/lists/domain/` and `src/longings/domain/` (no React, no storage imports;
see [ADR-0003](../../adr/0003-code-architecture.md)). `Id` and `Timestamp` go to `src/shared/`, since both
features use them. Storage is decided in
"State & persistence"; this model doesn't depend on it.

```ts
type Id = string;             // crypto.randomUUID()
type Timestamp = string;      // ISO 8601 with the device's local offset, e.g. "2026-09-28T09:14:00+02:00"

// ── Axes, effects, levels ────────────────────────────────────────────
type EnergyEffect = 'drains' | 'recharges';
type MoodEffect   = 'lifts'  | 'drags';
type Effect = EnergyEffect | MoodEffect;           // = the four lists

type Level = 'low' | 'mid' | 'high';
type Value = 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10;

// A rating stores only effect + value. The level is DERIVED from the value (see levelOf below).
interface Rating<E extends Effect = Effect> {
  effect: E;
  value: Value;
}

// "1 or 2 ratings, at most one per axis" (AC-1.1) is enforced by the type itself:
// ratings are keyed by axis, and at least one key must be present.
type Ratings =
  | { energy: Rating<EnergyEffect>; mood?: Rating<MoodEffect> }
  | { energy?: Rating<EnergyEffect>; mood: Rating<MoodEffect> };

// ── Records ───────────────────────────────────────────────────────
interface Item {
  id: Id;
  title: string;              // trimmed, 1–60 chars (AC-1.6)
  description?: string;
  ratings: Ratings;
  createdAt: Timestamp;       // "newest" sort (AC-3.5)
  archivedAt?: Timestamp;     // present = archived (AC-4.1)
}

interface Longing {           // deliberately NOT an Item without ratings (AC-5.3)
  id: Id;
  title: string;              // trimmed, 1–60 chars, same rule as items (DM-Q3)
  description?: string;       // no length limit, for items and Longings (DM-Q3)
  createdAt: Timestamp;
  archivedAt?: Timestamp;
}

interface Occurrence {        // separate record, not an array inside Item
  id: Id;
  itemId: Id;                 // WHAT happened
  effect: 'drains' | 'drags'; // AS WHAT it happened: the list it was tapped in (DM-D7)
  at: Timestamp;              // AC-6.1
}

// ── Ordering & settings ───────────────────────────────────────────
type ListKey = Effect | 'longings';

// Manual order is per list (AC-3.4): an item in Drains AND Lifts has two independent positions.
type ManualOrder = Record<ListKey, Id[]>;

type SortMode = 'manual' | 'newest' | 'az' | 'value';   // 'value' not offered for longings (AC-5.2)

interface Settings {
  language: 'en' | 'es' | 'it';   // default 'en' (AC-7.2, AC-7.3)
}
```

Pure domain functions (unit-tested, no I/O):

| Function | Rule | ACs |
|---|---|---|
| `levelOf(value)` | 1–4 → low, 5–7 → mid, 8–10 → high | AC-2.4, AC-3.3 |
| `defaultValue(level)` | low → 3, mid → 6, high → 8 | AC-1.5, AC-2.3 |
| `axisOf(effect)` | drains/recharges → energy, lifts/drags → mood | AC-1.1, AC-3.2 |
| `validateTitle(raw)` | trim; error if empty or > 60 chars | AC-1.6 |
| `listItems(items, effect)` | active items with a rating on that effect | AC-3.1, AC-3.2 |
| `sortList(items, order, mode, effect)` | returns a sorted copy; never mutates `ManualOrder` | AC-3.5 |
| `canRecordOccurrence(item)` | true if the item has a `drains` or `drags` rating | AC-6.1 |

### Design decisions (not dictated by the ACs — please review)

- **DM-D1 — Level is derived, not stored.** The level ranges cover 1–10 with no gaps, so the value alone
  determines the level. Storing both would allow them to disagree (e.g. value 9 + level low). AC-2.3 and
  AC-2.4 then come for free: changing the level = setting the value to `defaultValue(level)`.
- **DM-D2 — Ratings keyed by axis + union type.** An item with zero ratings, or with two Energy ratings,
  cannot be represented. (Changing a rating's effect *within* an axis, e.g. Drains → Recharges, is just a new
  `effect`; moving it to the other axis is remove + add.)
- **DM-D3 — Occurrences are their own records**, linked by `itemId`. Pillar 6 will query them across items
  by date; an array inside `Item` would make that harder and make every item heavier.
- **DM-D4 — Timestamps keep the local offset.** "Happened today" means the user's day. A plain UTC string
  (`toISOString()`) would place a 00:30 occurrence in Rome on the previous day.
- **DM-D5 — Manual order is a separate map of id arrays**, one per list. Reordering rewrites one array.
  One rule, no special cases: **ids missing from a list's array go on top** (newest first). New items and
  restored items are simply not in the array yet (archiving removes the id), so both land on top (DM-Q1).
  Unknown ids are ignored.
- **DM-D6 — Nothing extra.** No `updatedAt`, tags, colours, user id or sync fields: no AC needs them.
  One exception, DM-D7.
- **DM-D7 — Occurrences remember their effect.** An item's effect can change over time (Gym: Drains →
  Recharges); the occurrence stores the effect it had *when it happened*, like an order line stores the
  price at purchase. Otherwise old occurrences become ambiguous and that history can't be fixed later.
  The effect is the list the user tapped in, which also settles items that are both Drains *and* Drags.
  The type allows only `drains | drags` for now; pillar 6 can widen it without migrating stored data.

### Open questions for the user

- ~~**DM-Q1**: new / restored item position?~~ → **top** for both, via the single rule in DM-D5. The
  user prefers slim code over enforcing this if it ever needs special logic.
- ~~**DM-Q2**: remember the last sort mode per list?~~ → **no**. Lists open in manual order.
- ~~**DM-Q3**: title/description limits for Longings?~~ → titles **60 chars** (same as items);
  descriptions **no limit**.
- ~~**DM-Q4**: a Drains item with occurrences becomes Recharges only?~~ → its occurrences are **kept**
  (each one remembers it happened as a Drain, DM-D7); the "happened today" button disappears, because in
  this spec occurrences exist only on Drains/Drags (requirements Q1).

## State & persistence

Where data lives, how it's stored, migrations.

## Edge cases & errors

- …

## Testing strategy

Which acceptance criteria (AC-x.y) are covered by which tests (unit / component / e2e).

## Alternatives considered

- …
