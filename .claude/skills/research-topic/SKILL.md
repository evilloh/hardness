---
name: research-topic
description: Research an evidence-based psychology/behavioral topic (habit formation, motivation, learning a skill, staying consistent, recovering from a lapse, mood) before designing a feature or writing advice copy. Use when a spec touches motivation/wellbeing/learning, when advice text is needed, or when the user types /research-topic.
---

# Research a topic

Goal: turn a question ("how do people actually keep up a new hobby?") into **citable, vetted notes**
the app can build on. Never improvise psychology.

## Steps

1. **Frame the question** precisely, and say how it maps to a feature decision.
   Bad: "motivation". Good: "what does research say about restarting a practice after a lapse,
   and how should an app respond to a missed day?"
2. **Search** with WebSearch/WebFetch. Prefer, in order:
   1. Clinical guidelines (NICE, WHO, APA, NHS)
   2. Systematic reviews / meta-analyses (Cochrane, peer-reviewed)
   3. Named theories with a research base (self-determination theory, behavioral activation,
      implementation intentions, deliberate practice, self-compassion research)
   4. Reputable practitioner content (e.g. Dr. Alok Kanojia / HealthyGamerGG, clinician-authored
      institutional sites) — **as a pointer only**: find and cite the underlying research or guideline.
3. **Cross-check**: at least 2 independent sources for any claim that becomes user-facing advice.
   Flag disagreement rather than picking the convenient answer.
4. **Write it up** in `docs/research/notes/<topic>.md`: the question, the findings (plain language),
   what it means for our design, and the limits/caveats.
5. **Register sources** in `docs/research/sources.md` with IDs (`SRC-NNN`).
6. **Report to the user for vetting.** The user approves every source before it informs the product.
   Say plainly what is well-supported, what is contested, and what you could not verify.

## Rules

- Never present a YouTube video, blog or podcast as the citation. It can point you to the evidence.
- Never invent statistics, study names, or paraphrase beyond what the source says.
- Respect the product rule: **no engagement hooks**. If research suggests an addictive mechanic
  (variable rewards, loss aversion, streak pressure), note it explicitly as **rejected** and why.
- Advice copy is a *suggestion*, never a diagnosis or treatment.
