# Research note — "Reward the return, not the streak"

- **Date**: 2026-09-22
- **Status**: ⚠️ **Pending user vetting** (sources not yet approved)
- **Question**: When a user misses days, how should the app respond? Is avoiding streak mechanics and
  celebrating a user's return supported by evidence, or is it just our taste?
- **Why it matters**: it drives the core interaction design (principle 5 in the vision), so it must not be improvised.

## What the evidence supports

**1. Missing a day does not break habit formation.** In Lally et al. (2010), 96 people performed a daily
behaviour for 12 weeks; automaticity followed an asymptotic curve (median 66 days to plateau, range 18–254).
Missing a single opportunity had a negligible effect on the curve, and scores recovered.
→ *Design consequence*: a "broken streak" is a **UI fiction**, not a real loss of progress. Telling the user
they lost something is factually wrong as well as discouraging. **[SRC-001]**

**2. Self-compassion after a lapse predicts better recovery than self-criticism.** Across dietary-lapse and
physical-activity studies, self-compassionate responses relate to higher intentions and self-efficacy to
continue, less negative affect and rumination, more self-improvement motivation, and mastery-oriented goals.
→ *Design consequence*: the copy after a gap should normalise the lapse and lower the barrier to the next
action, not induce guilt. **[SRC-002] [SRC-003]**

**3. Extrinsic rewards can undermine intrinsic motivation.** The classic meta-analysis (128 studies)
found tangible, expected, contingent rewards reliably undermine intrinsic motivation for interesting tasks
("overjustification"). Motivation-crowding effects are reported specifically in gamified fitness apps.
→ *Design consequence*: points/badges for activities the user genuinely wants to do (their **Longings**)
risk making those activities feel like work. **[SRC-004]**

**4. Gamification in mental-health apps carries a documented engagement–efficacy–ethics tension.**
Reviews report that maximising engagement may not improve (and can undermine) clinical efficacy, and flag
risks: distress, pressure, dependence, demotivation after streak loss. Effects also decay over time
(one meta-analysis: RR 1.91 in the first 6 months → 1.37 after).
→ *Design consequence*: our non-goal on engagement mechanics is defensible, not merely ideological. **[SRC-005]**

## What the evidence does NOT say

- **No study tested the exact pattern "celebrate the return".** Points 1–4 justify *removing* streak pressure
  and *responding kindly* to a gap. The specific UX of a welcome-back reward is a **design hypothesis**
  derived from that evidence, not a validated intervention. Label it as such in the vision.
- **Streaks are not universally harmful.** Some users find them motivating, especially for genuinely
  uninteresting tasks, where the undermining effect is weakest. Our choice is a **values decision** for a
  mental-health context (do no harm, don't exploit), informed by evidence — not proof that streaks always fail.
- **Effect sizes and populations vary**; most lapse research is in diet/exercise, not mood journaling.

## Rejected techniques (effective but manipulative)

| Technique | Why rejected |
|---|---|
| Streak + loss aversion (Duolingo-style) | Turns a missed day into a punishment; contradicts finding 1, risks demotivation |
| Variable/intermittent rewards | Compulsion-forming; unethical in a mental-health context |
| Guilt/shame notifications ("don't let X down") | Self-criticism worsens lapse recovery (finding 2) |
| Points/badges on Longings | Overjustification risk on intrinsically motivated activities (finding 3) |

## Open follow-ups

- Behavioral activation research: how to size the "next smallest step" after a low period.
- Implementation intentions ("when X, I will Y"): a possible feature for turning a Longing into action.
- Self-determination theory (autonomy/competence/relatedness) as the framework for *what* to reward.
