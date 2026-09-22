# Evidence Policy

The app gives wellbeing suggestions, so **every piece of advice must trace back to a credible source**.
This folder is the app's knowledge base. Later it will feed the recommendation engine (and possibly
an LLM, grounded on these sources only: that pattern is called **RAG**, Retrieval-Augmented Generation).

## Acceptable sources (in order of preference)

1. Clinical guidelines: NICE (UK), WHO, APA (American Psychological Association), NHS
2. Systematic reviews / meta-analyses (Cochrane, peer-reviewed journals)
3. Reputable institutional health sites (NIMH, Mayo Clinic, national health services)
4. Established theories with a research base: self-determination theory, behavioral activation,
   implementation intentions, deliberate practice, self-compassion research

**Not acceptable as a citation**: blogs, influencers, unsourced listicles, AI-generated summaries
without the original source.

### Practitioner content (pointers, not citations)

Clinician-created content — e.g. **Dr. Alok Kanojia (Dr. K, HealthyGamerGG)**, a psychiatrist who talks about
motivation, gaming, and building a life you want — is excellent for *finding the right question* and for tone.
It is **not** a citation: a video is not peer review, and it's often a simplification.

Workflow: watch/read → identify the concept named → find the guideline or study behind it → cite **that**.

## Topics this project cares about

Habit formation and consistency · restarting after a lapse (self-compassion vs. self-criticism) ·
intrinsic vs. extrinsic motivation · learning a new skill (deliberate practice, realistic goal-setting) ·
behavioral activation for low mood · exercise and mental health · journaling/expressive writing ·
identifying energy drains and boundaries.

## Ethical design constraint

The product rejects engagement-maximizing mechanics (see `CLAUDE.md`). When research describes a
persuasive technique that would hook the user (variable rewards, loss aversion, streak pressure),
record it in the notes as **rejected**, with the reason. Studying dark patterns is fine; shipping them isn't.

## How research is done

Use the `/research-topic` skill. Notes go in `docs/research/notes/`, sources in `sources.md`.

## How to add a source

Add an entry to [`sources.md`](sources.md) with an ID (`SRC-001`), then reference that ID from specs and
from the app's advice content. **Every source is vetted by the user before it informs the product.**

## Safety

- Advice is phrased as a *suggestion*, never as a diagnosis or treatment.
- Crisis resources are always reachable from mood-related screens.
