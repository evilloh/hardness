# Product Vision

> Status: **Draft v0.2** — reviewed with the user. Anything marked `TODO` is an open question.

## The name

**Hardness** = *harness* (the AI harness this app is built with) + *hard* (keeping your mind well is hard work).
Logo: the Loch Ness monster wearing a harness. 🦕

## Problem

Improving your mental health is mostly about small, consistent actions and noticing patterns:
what drains you, what recharges you, what you keep postponing. All of that knowledge stays in your
head and gets lost, so nothing compounds.

## Vision (one sentence)

A private, mobile-first companion that helps me **know** what drains and restores me, **start** the things
I've always wanted to do, and **improve 1% at a time** until a year of small steps adds up to real change.

## Target user

- Primary: me (single user, dogfooding).
- Later (TODO): other adults interested in self-improvement. Not a clinical population.

## Core pillars

### 1. The four lists (my personal inventory)

| List | Question it answers |
|---|---|
| **Drains** | What drags me down / eats my energy? |
| **Restores** | What recharges my batteries? |
| **Lifts** | What makes me happy / raises my mood? |
| **Longings** | What have I always wanted to do but never started, or dropped? |

The lists are alive: I add, edit and reorder items as I learn about myself.

### 2. The 1% — continuous, tiny progress

Pick something from **Longings** and turn it into an ongoing practice (exercise, drawing, programming,
a new language — it doesn't matter which). The app tracks consistency, not intensity:
*a little bit, very often*. Over a year, the small steps compound.

### 3. The journal (photos, notes, diary)

Log progress with a photo, a short note, or a longer diary entry. A visible trail of evidence that
I *am* moving, which is exactly what's invisible when you feel stuck.

### 4. Insights & recommendations

Spot patterns across the lists and the journal (e.g. "low days cluster after the drains I keep repeating",
"the weeks I drew 3+ times, my mood was higher"), and suggest evidence-based actions
**with a citation** from `docs/research/sources.md`.

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

- I use it daily for 30 days without friction.
- I start at least one "Longing" and keep it going for a month.
- After 2+ weeks, it shows me at least one pattern I did not consciously know.

## Open questions

- ~~Web (PWA) or native (Expo/React Native)?~~ → PWA, decided in ADR-0002
- TODO: How do low moments get logged? A dedicated entry (intensity + trigger, linked to a **Drain**),
  or just a journal entry with a mood value?
- TODO: Daily mood check-in — one tap, or skip it entirely for v1?
- TODO: Where does the "AI" live in the product? Rules-based patterns first, LLM suggestions later?
- TODO: Which languages? (EN / ES / IT?)
- TODO: Which pillar do we build first? (Suggestion: the four lists — everything else builds on them.)
