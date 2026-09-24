# 001 — The lists: Requirements

- **Status**: Approved (by the user, 2026-09-24)
- **Owner**: @me
- **Related**: [vision v0.4, pillar 1](../../product/vision.md), [ADR-0002 — React PWA](../../adr/0002-platform-and-stack.md)

## Context

Pillar 1 of the vision: my personal inventory. Things in my life are rated on two independent axes:
**Energy** (Drains ↔ Recharges) and **Mood** (Lifts ↔ Drags). One thing can sit on both axes (a hard
videogame can lift my mood and drain my energy). Separately, **Longings** is a plain reminder list of things
I've always wanted to do.

Everything else in the app builds on these lists: practices (pillar 2), mood crossing (pillar 5),
insights (pillar 6). The app is for people who struggle to start and keep up with things, so **every extra
tap is a cost**. Ask for the minimum, make the rest optional.

## Glossary

| Term | Meaning |
|---|---|
| **Item** | A thing in my life that I rate: a title, an optional description, and 1–2 ratings |
| **Axis** | Energy or Mood |
| **End** | One side of an axis: Drains / Recharges (Energy), Lifts / Drags (Mood) |
| **Rating** | An end + a level + a value. An item has at most one rating per axis |
| **Level** | Low / Mid / High: how strongly the item pulls towards that end |
| **Value** | A number 1–10 that fine-tunes the level (for sorting) |
| **List** | A view showing every active item with a rating on one end (Drains, Recharges, Lifts, Drags) |
| **Occurrence** | A record that a Drains/Drags item "happened today" |
| **Longing** | A reminder: a title and an optional description, no ratings |

Level ↔ value mapping: **Low = 1–4 (default 3)**, **Mid = 5–7 (default 6)**, **High = 8–10 (default 8)**.

## User stories

- **US-1**: As a user, I want to add an item in a couple of taps, so that capturing it never feels like work.
- **US-2**: As a user, I want to edit an item and fine-tune its ratings, so that it reflects what I learn about myself.
- **US-3**: As a user, I want to see each list and order it my way, so that I can find what matters.
- **US-4**: As a user, I want to archive items instead of losing them, so that I can look back at my past self.
- **US-5**: As a user, I want a simple Longings list, so that I remember what I've always wanted to do.
- **US-6**: As a user, I want to record with one tap that a Drain or Drag happened today, so that I can
  later see how often it hits me.
- **US-7**: As a user, I want the app in my language (EN, ES or IT).
- **US-8**: As a user, I want my lists to stay private on my device, so that I can be honest in them.

## Acceptance criteria (EARS notation)

### US-1 — Add an item

- **AC-1.1**: WHEN the user saves a new item THE SYSTEM SHALL require a non-empty title and exactly one or
  two ratings, at most one per axis.
- **AC-1.2**: WHEN the user starts adding an item from a list (e.g. Drains) THE SYSTEM SHALL preselect that
  list's end, so the user only types the title and picks a level.
- **AC-1.3**: THE SYSTEM SHALL ask for the level immediately in the add flow (no hidden default level).
- **AC-1.4**: THE SYSTEM SHALL let the user add an optional description and an optional second rating
  (on the other axis) while adding, without making either one required.
- **AC-1.5**: WHEN a rating is created THE SYSTEM SHALL set its value to the level's default (3 / 6 / 8).
- **AC-1.6**: IF the title is empty or longer than 60 characters THEN THE SYSTEM SHALL not save and
  SHALL say kindly what's wrong.
- **AC-1.7**: THE SYSTEM SHALL make it possible to add an item from an open list in: type title → pick
  level → save (no other required step).

### US-2 — Edit an item

- **AC-2.1**: WHEN the user edits an item THE SYSTEM SHALL let them change the title, description, and
  each rating's end, level and value, and add or remove a second rating.
- **AC-2.2**: THE SYSTEM SHALL show and edit the value only in the item's edit view (not in the add flow
  or the lists).
- **AC-2.3**: WHEN the user changes a rating's level THE SYSTEM SHALL reset its value to the new level's default.
- **AC-2.4**: WHEN the user changes a rating's value to a number outside the current level's range
  THE SYSTEM SHALL move the level to the one that contains that value.
- **AC-2.5**: IF the user tries to remove an item's only rating THEN THE SYSTEM SHALL prevent it and
  suggest archiving the item instead.

### US-3 — See and order the lists

- **AC-3.1**: THE SYSTEM SHALL show four lists (Drains, Recharges, Lifts, Drags), each containing every
  active item that has a rating on that end.
- **AC-3.2**: WHEN an item has ratings on both axes THE SYSTEM SHALL show it in both corresponding lists,
  and editing it in one SHALL update it in both.
- **AC-3.3**: THE SYSTEM SHALL show each item's rating(s) so that the end and level are recognisable at a
  glance in the list. (How — colours, split pill — is decided in `design.md`.)
- **AC-3.4**: THE SYSTEM SHALL let the user reorder items manually within a list, and SHALL remember that
  order per list.
- **AC-3.5**: THE SYSTEM SHALL let the user sort a list by: manual order, newest, A–Z, and value
  (highest first). Sorting SHALL NOT overwrite the saved manual order.
- **AC-3.6**: WHEN a list is empty THE SYSTEM SHALL show one short sentence explaining what the list is for
  and a way to add the first item. The sentence SHALL describe the list, not give advice.

### US-4 — Archive

- **AC-4.1**: WHEN the user archives an item THE SYSTEM SHALL remove it from all lists and keep it,
  with its ratings, occurrences and archive date, in an Archive view.
- **AC-4.2**: WHEN the user restores an archived item THE SYSTEM SHALL put it back in its lists.
- **AC-4.3**: THE SYSTEM SHALL let the user permanently delete an archived item after an explicit
  confirmation, removing all its data (it's their sensitive data).
- **AC-4.4**: THE SYSTEM SHALL frame the archive as history ("things I've moved past"), never as failure.

### US-5 — Longings

- **AC-5.1**: THE SYSTEM SHALL let the user add a Longing with a required title and an optional
  description, and nothing else required.
- **AC-5.2**: THE SYSTEM SHALL let the user edit, reorder, sort (manual / newest / A–Z), archive, restore
  and permanently delete Longings, with the same rules as items (AC-3.4, AC-3.5, AC-4.x).
- **AC-5.3**: Longings SHALL NOT have ratings or values and SHALL NOT appear in the four lists.

### US-6 — "This happened today" (occurrences)

- **AC-6.1**: WHEN the user taps "happened today" on an item in Drains or Drags THE SYSTEM SHALL record an
  occurrence with the current date and time, in one tap, with no confirmation dialog.
- **AC-6.2**: WHEN an occurrence has just been recorded THE SYSTEM SHALL offer an undo for a few seconds.
- **AC-6.3**: THE SYSTEM SHALL show an item's occurrences as a plain dated history in its detail view.
- **AC-6.4**: THE SYSTEM SHALL NOT show counts, streaks, trends or judgement about occurrences in this
  feature (e.g. no "3 times this week!"). Patterns belong to pillar 6, with kind framing.
- **AC-6.5**: THE SYSTEM SHALL offer a discreet, always-reachable path to help resources from the
  Drains and Drags lists and from the occurrence flow, without pop-ups or interrupting the user.
- **AC-6.6**: The help resources (helplines per language/country) SHALL come from a vetted source list.
  **TODO**: research and vet the resources for EN / ES / IT before release.
- **AC-6.7**: WHEN the user records an occurrence THE SYSTEM SHALL show, without blocking or requiring a tap,
  a few of the user's **own** active Recharges and Lifts items as gentle reminders
  (e.g. "Something from your Recharges?"). IF the user has none THEN THE SYSTEM SHALL show nothing extra.
- **AC-6.8**: These reminders SHALL be phrased as suggestions, never instructions ("you should…"), and
  SHALL be visually distinct from the help resources of AC-6.5: they complement professional help,
  they never replace it.

### US-7 — Languages

- **AC-7.1**: THE SYSTEM SHALL provide all interface text in English, Spanish and Italian.
- **AC-7.2**: WHEN the app starts for the first time THE SYSTEM SHALL use English.
- **AC-7.3**: THE SYSTEM SHALL let the user switch the interface language (EN / ES / IT) inside the app,
  and SHALL remember the choice.
- **AC-7.4**: THE SYSTEM SHALL NOT translate the user's own content (titles, descriptions).

### US-8 — Privacy & availability

- **AC-8.1**: THE SYSTEM SHALL store all items, Longings and occurrences only on the device.
- **AC-8.2**: THE SYSTEM SHALL NOT send this data anywhere nor write it to any log or analytics.
- **AC-8.3**: THE SYSTEM SHALL work fully offline for everything in this spec.
- **AC-8.4**: WHEN the app is first installed THE SYSTEM SHALL start with empty lists.
- **AC-8.5**: THE production build SHALL NOT contain any development sample data (mock items used during
  development stay in dev-only builds).

## Safety, privacy & ethics check

- [x] Does this touch mood/trigger data? → **Yes**: ratings and occurrences say what drains me and pulls my
      mood down. Local-only, never logged (AC-8.1, AC-8.2), permanent delete available (AC-4.3).
- [x] Does it show advice? → **No app advice**. Empty-state text describes the list (AC-3.6). After an
      occurrence the app only reflects the user's **own** Recharges/Lifts back to them (AC-6.7/6.8), so no
      citation is needed. Dev mock data never reaches production (AC-8.5).
      Note: "when low, do something from your own list of good activities" resembles behavioural activation;
      if we ever present it as a technique, run `/research-topic` first.
- [x] Does it touch low moments? → **Yes**: occurrences on Drains/Drags. Discreet help path (AC-6.5),
      resources vetted (AC-6.6, TODO).
- [x] **No engagement hooks**: no counts/streaks on occurrences (AC-6.4), archive framed as growth (AC-4.4),
      no notifications in this feature. It asks for the minimum (AC-1.7).
- [x] Does it touch motivation / habits / learning? → **No**, this is an inventory. (Practices are pillar 2.)
      Note: the two-axis model resembles known two-dimensional models of affect; it's a product choice
      here, not a psychological claim, so no citation needed unless we ever present it as one.

## Out of scope

- Turning a Longing into a practice (the 1% spec).
- Counts, charts or patterns about items and occurrences (pillar 6).
- The daily mood check-in and a richer "low moment" entry (pillar 5).
- Recording an occurrence on a past day.
- Learning which of my own Lifts/Recharges tend to help after a Drag/Drain (needs recording what I did
  afterwards; belongs to pillar 6, see the vision's parking lot).
- Backup, sync, export, sharing, notifications.
- Visual design (colours per end/level, the split pill for two ratings): that's `design.md`.

## Open questions

- ~~Q1: "happened today" also for Lifts and Recharges?~~ → not in this spec (Drains and Drags only).
  Revisit with pillar 6: learning "what helps" will need it.
- ~~Q2: maximum title length?~~ → 60 characters (AC-1.6).
- ~~Q3: change the language inside the app?~~ → yes; English by default (AC-7.2, AC-7.3).
- **Q4**: Which help resources, per language/country? Needs a research + vetting cycle (AC-6.6).
