# Product Vision

> Status: **Approved v0.4** (approved by the user on 2026-09-24). v0.4 replaced "the four lists" with two
> axes (Energy: Drains↔Recharges, Mood: Lifts↔Drags) + Longings, and added the target-user line.
> Anything marked `TODO` is an open question.

## The name

**Hardness** = *harness* (the AI harness this app is built with) + *hard* (keeping your mind well is hard work).
Logo: the Loch Ness monster wearing a harness. 🦕

## Problem

Improving your mental health is mostly about small, consistent actions and noticing patterns:
what drains you, what recharges you, what you keep postponing. All of that knowledge stays in your
head and gets lost, so nothing compounds.

## Vision (one sentence)

A private, mobile-first companion that helps me **know** what drains and recharges me, **start** the things
I've always wanted to do, and **improve 1% at a time** until a year of small steps adds up to real change.

## Target user

- Primary: me (single user, dogfooding).
- Later (TODO): other adults interested in self-improvement. Not a clinical population.
- **Designed for people who struggle to start and to keep up with things and habits.** Every extra tap,
  field or step is a reason to give up, so the app asks for the minimum and makes the rest optional.

## Core pillars

### 1. The lists (my personal inventory)

Things in my life are rated on **two independent axes**, each with two opposite ends:

| Axis | One end | Opposite end |
|---|---|---|
| **Energy** | **Drains** — eats my energy | **Recharges** — fills my batteries |
| **Mood** | **Lifts** — raises my mood | **Drags** — pulls my mood down |

One thing can sit on both axes at once: a challenging videogame can **lift** my mood *and* **drain** my
energy. So an item has up to two ratings (one per axis), each with its own intensity. The four lists
(Drains, Recharges, Lifts, Drags) are views of the same items.

Separate from those, **Longings** is a simple reminder list: things I've always wanted to do but never
started, or dropped. Longings have no ratings. (Turning a Longing into a practice is pillar 2.)

The lists are alive: I add, edit, reorder and archive items as I learn about myself. Archived items
stay visible as my history, so I can see who I used to be.

### 2. The 1% — continuous, tiny progress

Pick something from **Longings** and turn it into an ongoing practice (exercise, drawing, programming,
a new language — it doesn't matter which). The app tracks consistency, not intensity:
*a little bit, very often*. Over a year, the small steps add up — spaced, frequent practice beats cramming
(SRC-006…008, pending vetting). "1%" is a **metaphor, not maths**: skills grow fast early, then plateau;
the app never promises "37× better". What it shows is the accumulated *trail* of practice.
See [research note](../research/notes/compound-learning-little-often.md).

**It's about the journey, not about being the best.** The app is a heartwarming reminder of how I kept
showing up. If there's visible improvement (likely, but not required), it cheers me on. The goal is
working on my mind, not mastering the skill.

### 3. The journal (diary with photos & media)

Log progress with a photo/media, a short note, or a longer diary entry. A visible trail of evidence that
I *am* moving, which is exactly what's invisible when you feel stuck. Entries can show the photos/media
attached to them.

**Mantras**: while writing (or re-reading) the diary, I can turn a sentence into a **Mantra** — something
I want to always keep in mind. Mantras have **their own section** where I manage them (add, edit, delete),
and each one links back to the diary entry it came from, so I can revisit that moment.

### 4. Meditation

Guided meditation sessions (different kinds, each with its own timer), and a private history of the
sessions I've done. With many session types, I can organise them my way (e.g. hide ones I don't use,
favourite and reorder the ones I do). Meditation guidance must come from vetted sources, like every other advice.
TODO: `/research-topic` first (which practices, for whom, known adverse effects).

### 5. Daily mood check-in

At the end of the day, a quick check of how my mood was. Over time, the app crosses mood with my
activities (lists, practices, meditation, diary) to help me see what tends to go with good or bad days.
Mood is sensitive health data: local-only, never logged, and a low check-in always offers a path to help.
Insights say "tends to go with", never "causes" — it's one person's data, not a diagnosis.

### 6. Statistics & insights

Two layers, one place (a statistics page):

- **Statistics** — my own data shown back to me: mood over time, practice sessions, meditation history.
  Facts, no advice, so no citation needed. Kind framing only: no "missed days" in red, no comparisons.
- **Insights & recommendations** — patterns across lists, journal and mood (e.g. "low days tend to follow
  the drains I keep repeating", "the weeks I drew 3+ times, my mood tended to be higher"), and
  evidence-based suggestions **with a citation** from `docs/research/sources.md`.

## Non-goals (for now)

- Diagnosis, therapy, or clinical claims.
- Social features / sharing.
- Wearable or health-app integrations (ADR-0002).
- **Engagement-maximizing design.** No hooks, no dark patterns, no streaks that punish a missed day,
  no notification pressure, no "don't lose your progress!" guilt. A mental-health app must not exploit
  the psychology it claims to protect. Success is measured by the user's real-life progress,
  not by time spent in the app.

## Principles

1. **Mobile-first, one-thumb, < 10 seconds** to log anything.
2. **Private by default** (local-first; explicit consent before any data leaves the device).
3. **Evidence over vibes**: every recommendation cites a source.
4. **Kind, never guilt-tripping**: the app encourages, it doesn't scold.
5. **Reward the return, not the streak.** Coming back after a gap is the hardest and most valuable moment,
   so that's what we celebrate ("good to see you again, here's where you left off"), never
   "you broke your 14-day streak". Rewards are reflective (progress you can see, a kind word,
   your own journal evidence), not compulsive (points, badges, variable-reward slot machines).
   *Evidence*: missing a day doesn't break habit formation (SRC-001); self-compassion after a lapse beats
   self-criticism for recovery (SRC-002/003); extrinsic rewards can undermine intrinsic motivation (SRC-004);
   gamification in mental-health apps carries documented ethical/efficacy risks (SRC-005).
   The *specific* "celebrate the return" mechanic is a **design hypothesis** derived from that evidence, not a
   validated intervention — see [research note](../research/notes/rewarding-returns-vs-streaks.md).
6. **Grounded in practice, not vibes**: features that touch motivation, habit-building or learning must be
   informed by research on how people actually build skills and recover from setbacks (see
   [research policy](../research/README.md)).
7. **Safety**: always offer a path to professional or crisis help.

## Success looks like (v1)

> **v1** = the first *release*: the smallest version of the app I can install on my phone and use every day.
> It is a scope (a set of pillars), not a task or a session.
>
> | Release | Pillars |
> |---|---|
> | **v1** | 1 The lists · 2 The 1% · 3 The journal (diary + media) · 5 Daily mood check-in (collect data from day one) |
> | v1.x | Mantras (builds on the diary) |
> | Later | 4 Meditation (needs a research cycle first) · 6 Statistics & insights (needs weeks of data) |
>
> Decided with the user on 2026-09-24.

- I use it daily for 30 days without friction.
- I start at least one "Longing" and keep it going for a month.
- After 2+ weeks, it shows me at least one pattern I did not consciously know.

## Open questions

- ~~Web (PWA) or native (Expo/React Native)?~~ → PWA, decided in ADR-0002
- ~~How do low moments get logged?~~ → one tap on a Drains/Drags item: "this happened today"
  (spec 001). A richer "low moment" entry may come later with the mood check-in.
- ~~Daily mood check-in — one tap, or skip it entirely for v1?~~ → yes, end of day (pillar 5), in v1
- ~~Is meditation in v1, or a later pillar?~~ → later (see release table)
- TODO: Where does the "AI" live in the product? Rules-based patterns first, LLM suggestions later?
- ~~Which languages?~~ → multi-language from v1: **EN, ES, IT**
- ~~Which pillar do we build first?~~ → the lists; everything else builds on them

## Parking lot (design details — they belong in a spec's `design.md`, not here)

Captured so nothing is lost; each moves into the spec of its feature when we get there.

- Mantras: select text in a diary entry → a "Mantra" popup action adds it to the list.
- Mantras: edit / delete; what happens to a mantra if its source entry is deleted?
- Meditation: "hide this session", favourites, drag-and-drop ordering.
- Pillar 6 idea: learn which of my own Lifts/Recharges tend to help after a Drag/Drain, by recording what I
  did afterwards (keep it to one optional tap; say "tends to help", never "works").
