# NNN — Feature name: Tasks

- **Status**: Draft
- **Design**: [design.md](design.md)

Rules:
- Each task is small (≈ one commit), independently verifiable, and references the ACs it satisfies.
- The agent implements **one task per loop**, runs verification, then ticks it off.

## Tasks

- [ ] **T1** — … _(AC-1.1)_
  - Verify: `npm test -- …`
- [ ] **T2** — …
  - Verify: …
