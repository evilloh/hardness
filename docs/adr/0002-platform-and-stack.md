# 0002 — Platform & tech stack

- **Status**: Accepted
- **Date**: 2026-09-22

## Context

The app is mobile-first, single-user at first, local-first for privacy. The developer is a senior React
engineer, and the project doubles as a CV showcase. Recruiters should be able to try it in seconds.
The main learning goal is the AI-native workflow, so we want as few *other* new technologies as possible.

## Options

### A. React PWA (Vite + TypeScript)
- ➕ Zero ramp-up, fastest to ship; a recruiter opens a URL and tries it
- ➕ Installable on the phone home screen, works offline, IndexedDB for local-first storage
- ➖ Limited native APIs (notifications on iOS only work when installed, no HealthKit)

### B. Expo (React Native + TypeScript)
- ➕ Truly native feel, reliable notifications, possible health integrations later
- ➕ Adds React Native to the CV
- ➖ Longer ramp-up; demoing needs Expo Go, store builds, or Expo's web target

### C. Next.js (web + server)
- ➕ Server features are easy (API routes for LLM calls)
- ➖ Server-first goes against local-first privacy. Overkill for v1.

## Decision

**Option A: a React + TypeScript SPA built with Vite, made installable/offline as a PWA** (via `vite-plugin-pwa`).

Architecture constraint that comes with it: **domain logic lives in framework-agnostic TypeScript**
(`src/domain/`: models, pattern detection, recommendation rules), with no imports from React or browser APIs.
The UI layer depends on the domain, never the other way around.

Out of scope for this ADR (each gets its own): storage library, state management, testing stack, hosting.

## Consequences

- ➕ The developer is productive from day 1; the demo is a URL.
- ➕ A later move to Expo means rewriting screens, not logic (thanks to the `src/domain/` boundary).
- ➖ Reminder notifications on iOS require the app to be installed to the home screen. Accepted for v1.
- ➖ No access to Apple Health / Google Fit. Exercise is logged manually.
- If reliable notifications or health data become must-haves, write a new ADR that supersedes this one.
