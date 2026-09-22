# 0001 — Record architecture decisions

- **Status**: Accepted
- **Date**: 2026-09-22

## Context

This project is built with AI agents that start every session with no memory. Decisions that
only live in chat history get lost, and they get re-argued or silently reversed.

## Decision

We record every significant technical decision as an ADR in `docs/adr/`, using the format
Context / Options / Decision / Consequences.

## Consequences

- The agent must check `docs/adr/` before proposing architectural changes.
- Changing a decision means writing a new ADR, not editing an old one.
