# Compound learning: a little, often

- **Status**: Draft — sources SRC-006…010 are `pending` user vetting
- **Date**: 2026-09-24
- **Feeds**: vision pillar 2 (*The 1%*), future spec for practices/Longings

## The question

Is "a few minutes, frequently" really better than "two full days" for learning a skill or hobby?
Does progress *compound* over a year the way the "1% better every day" slogan says?
→ This decides how the app frames the 1% pillar, what it measures, and what it promises.

## Findings (plain language)

### 1. Spreading practice out beats cramming — well supported

- A meta-analysis of 63 studies found people who practised in **spaced** sessions performed better than
  those who practised in one **massed** block (mean weighted effect ≈ 0.46). The size of the benefit
  depended on the **type of task** and the **gap between sessions** (SRC-006).
- The largest review of spacing in memory tasks (317 experiments) found spacing helps retention, and that
  **the longer you want to remember something, the longer the ideal gap between sessions** (SRC-007).
- A 2025 meta-analysis of **real classrooms** (22 studies, N > 3000) found the same direction: spacing practice
  across separate days beat massed practice (d = 0.54), with larger benefits for longer retention (SRC-008).

→ Two independent lines (lab + classroom, verbal + motor) agree. This supports *"a little, often"*.

### 2. Some learning happens *between* sessions — supported (for motor skills)

- In a finger-tapping skill study, a **night of sleep** after practice produced measurable gains without any
  extra practice; the same time awake did not (SRC-009). Rest is part of learning, not a gap in it.

→ Reinforces our stance: a day off is not "lost progress" (see also SRC-001).

### 3. Practice matters, but it is not the whole story — supported, and important for honest copy

- A meta-analysis of deliberate practice found that the amount of practice explained a meaningful but
  **modest** share of differences in performance (e.g. ~26% in games, ~21% in music, ~18% in sports,
  much less in education and professions) (SRC-010).

→ The app must not promise "practise X minutes and you'll master it". Practice helps everyone improve;
it does not guarantee a specific level.

### 4. The "1% a day = 37× better in a year" maths is **not** what learning looks like

- `1.01^365 ≈ 37.8` is compound-interest arithmetic, popularised in self-help books, not a finding about skills.
- Research on learning curves (the "power law of practice", Newell & Rosenbloom 1981, and the later debate
  that individual curves may be exponential) describes the opposite shape: **fast gains early, then
  diminishing returns and plateaus**. *(Seen in secondary sources — see "To verify".)*

→ What *does* accumulate is **practice itself and what you retain**, not an exponentially growing skill.
The honest version of the slogan: *small, frequent sessions add up, and after a year the difference is
visible — even though week-to-week it often feels like nothing is happening.*

## What this means for Hardness (design implications — hypotheses, not validated)

1. **Keep "1%" as a metaphor, never as a number.** No copy, chart or projection claiming "37× better".
2. **Default to small, frequent sessions** when a Longing becomes a practice (minutes, not hours).
   How small exactly is *not* in this evidence — it's a product decision.
3. **Make the accumulation visible**: total sessions, then-vs-now photos/notes from the journal.
   That's the real "compound" the user can see. Show a *trail*, not a *projected curve*.
4. **Plateaus are normal** — say so kindly when progress feels flat, instead of pushing more effort.
5. **Rest is part of learning** — consistent with "reward the return, not the streak".

## Rejected ideas

| Idea | Why rejected |
|---|---|
| Show a compounding "you'll be 37× better" projection | Not supported by learning-curve research; sets up disappointment |
| Daily minimum-minutes target with a streak counter | Streak pressure — violates our no-engagement-hooks rule (see [rewarding-returns-vs-streaks](rewarding-returns-vs-streaks.md)) |
| "Practise more to master it" nudges | Overstates what practice alone explains (SRC-010) |

## Limits & what the evidence does NOT say

- Most spacing studies measure **memory or simple motor tasks over days/weeks**, not hobbies over a year.
  Extending it to "drawing for 10 minutes a day for a year" is a reasonable **extrapolation**, not a tested result.
- No source here tells us the ideal session length or frequency for a hobby.
- Donovan & Radosevich (SRC-006) and Cepeda (SRC-007) were read via abstracts/summaries, not full text.
- The sleep result (SRC-009) is for motor sequence learning; later work debates how general it is.

## To verify at the primary source

- Newell & Rosenbloom (1981), "Mechanisms of skill acquisition and the law of practice" — only seen second-hand.
- Heathcote, Brown & Mewhort (2000), "The power law repealed" — only seen second-hand.
