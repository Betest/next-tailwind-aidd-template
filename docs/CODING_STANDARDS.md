# CODING_STANDARDS — Engineering Quality Rules (Next.js)

These standards apply to all code changes, whether authored by humans or assisted by AI.

---

Non-goals:
- This document does not define rendering rules.
- This document does not override AI_RULES or Rendering Rules.


## 1) General Principles

- Clarity over cleverness.
- Minimal surface change: do not modify public APIs/contracts unless requested.
- Small units: functions/hooks/components should be small, focused, testable.
- Predictability: avoid hidden side-effects.

---

## 2) Next.js Conventions

- Prefer Server Components by default.
- Client Components must be minimal and justified.
- Data fetching belongs on server unless interactivity requires client fetching.
- Route handlers (`app/api/*`) must validate inputs and return explicit error shapes.

---

## 3) Error Handling

- Fail fast, be explicit, no silent failures.
- Preserve existing error semantics unless requested.

---

## 4) Testing Standards

- Tests required for new behavior, bug fixes, refactors that change logic.
- Prefer unit tests for pure logic (utils, reducers, schemas).
- Use integration tests when behavior spans layers.
- Tests must be deterministic.

---

## 5) Refactoring Discipline

1. Add/update tests (when present)
2. Refactor internals
3. Preserve behavior and public APIs

No rewrites disguised as refactors. No style-only refactors.

---

## 6) AI-Assisted Contributions

- Must follow these standards exactly.
- State assumptions explicitly.
- If unsure, ask one targeted question rather than guessing.

---

Final rule: another engineer must be able to understand and safely modify the solution quickly.
