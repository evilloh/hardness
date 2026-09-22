# Evidence Policy

The app gives wellbeing suggestions, so **every piece of advice must trace back to a credible source**.
This folder is the app's knowledge base. Later it will feed the recommendation engine (and possibly
an LLM, grounded on these sources only: that pattern is called **RAG**, Retrieval-Augmented Generation).

## Acceptable sources (in order of preference)

1. Clinical guidelines: NICE (UK), WHO, APA (American Psychological Association), NHS
2. Systematic reviews / meta-analyses (Cochrane, peer-reviewed journals)
3. Reputable institutional health sites (NIMH, Mayo Clinic, national health services)

**Not acceptable**: blogs, influencers, unsourced listicles, AI-generated summaries without the original source.

## How to add a source

Add an entry to [`sources.md`](sources.md) with an ID (`SRC-001`), then reference that ID from specs and
from the app's advice content.

## Safety

- Advice is phrased as a *suggestion*, never as a diagnosis or treatment.
- Crisis resources are always reachable from mood-related screens.
