# Architecture Decision Records (ADRs)

An ADR is a short document recording **one** significant decision: the context, the options, what we
chose and the consequences. ADRs are never edited after acceptance. If a decision changes, write a new ADR
that *supersedes* the old one.

Why it matters with AI: agents have no memory between sessions. ADRs stop the agent (and future you)
from re-arguing settled decisions or quietly undoing them.

Filename: `NNNN-kebab-title.md`. Statuses: `Proposed` → `Accepted` | `Rejected` → (`Superseded by NNNN`).

Rules:
- **One decision per ADR.** If two choices could change independently, they get two ADRs.
  (Lesson from 0002, which bundled platform + domain boundary: changing one forced an amendment.)
- **Append-only**: ADRs are never deleted, and an accepted decision is never rewritten. Rejected ADRs stay too
  ("we considered X and said no, because Y").
- **All `Accepted` ADRs are in force at the same time.** They usually cover different topics.
- **A newer ADR replaces an older one only explicitly**: the new one says `Supersedes: NNNN`, the old one's
  status becomes `Superseded by MMMM`. Newer date alone means nothing.
- **To change only part of an ADR, amend it**: the new one says `Amends: NNNN (which part)`, the old one's
  status gets `(… amended by MMMM)`. The rest of the old ADR stays in force. After 2–3 amendments, write one
  clean ADR that supersedes it, so readers don't have to piece it together.
- **ADR-worthy** = hard to reverse, affects many parts, or future-you will ask "why?". Feature behavior
  belongs in a spec, not an ADR.

| # | Title | Status |
|---|---|---|
| [0001](0001-record-architecture-decisions.md) | Record architecture decisions | Accepted |
| [0002](0002-platform-and-stack.md) | Platform & tech stack (React PWA) | Accepted (domain location amended by 0003) |
| [0003](0003-code-architecture.md) | Code architecture: feature-first folders, light DDD | Accepted |
