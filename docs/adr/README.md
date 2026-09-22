# Architecture Decision Records (ADRs)

An ADR is a short document recording **one** significant decision: the context, the options, what we
chose and the consequences. ADRs are never edited after acceptance. If a decision changes, write a new ADR
that *supersedes* the old one.

Why it matters with AI: agents have no memory between sessions. ADRs stop the agent (and future you)
from re-arguing settled decisions or quietly undoing them.

Filename: `NNNN-kebab-title.md`. Statuses: `Proposed` → `Accepted` | `Rejected` → (`Superseded by NNNN`).

Rules:
- **Append-only**: ADRs are never deleted, and an accepted decision is never rewritten. Rejected ADRs stay too
  ("we considered X and said no, because Y").
- **All `Accepted` ADRs are in force at the same time.** They usually cover different topics.
- **A newer ADR replaces an older one only explicitly**: the new one says `Supersedes: NNNN`, the old one's
  status becomes `Superseded by MMMM`. Newer date alone means nothing.
- **ADR-worthy** = hard to reverse, affects many parts, or future-you will ask "why?". Feature behavior
  belongs in a spec, not an ADR.

| # | Title | Status |
|---|---|---|
| [0001](0001-record-architecture-decisions.md) | Record architecture decisions | Accepted |
| [0002](0002-platform-and-stack.md) | Platform & tech stack (React PWA) | Accepted |
