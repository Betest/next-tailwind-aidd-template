# CONTRIBUTING_AI — AI & Human Contribution Guidelines (Next.js)

These rules apply to both human contributors and LLM-assisted contributions.
They are enforceable, pragmatic, and optimized for AIDD.

---

## 1) Non-Negotiable Principles

- KISS first.
- DRY (rule of three).
- Clean Code: clear names, small components, explicit types.
- Minimal diff; no unrelated changes.
- No behavior changes unless requested.

---

## 2) Stack Constraints (Hard Rules)

### Allowed
- Next.js (App Router)
- React (hooks + functional components only)
- TypeScript (strict)
- TailwindCSS
- `lucide-react` for all icons/logos

### Forbidden (unless explicitly requested)
- UI frameworks/design systems
- additional icon libraries
- CSS-in-JS/theming libs
- additional state/query libraries

---

## 3) PR Checklist (Mandatory)

- SRP: each component/hook does one thing.
- No premature abstractions.
- Composition over complex hierarchies.
- Types are explicit and readable.
- Tailwind only; icons from lucide-react.
- Do not claim builds/tests pass without logs/output.

---

## 4) Hooks & Effects

- `useEffect` only for external synchronization.
- No derived UI state in effects.

---

## 5) Performance & Re-Renders

- Default to Server Components.
- Avoid unnecessary `"use client"` boundaries.
- Avoid unstable props in memoized/large trees.
- Memoization only with evidence; no memo spam.

---

## 6) Agent Discipline

Each iteration:
1) Plan (<=4 bullets)
2) One action (one patch OR one command request)
3) Next check

Max 3 failed iterations; then propose options.

---

Final rule: the best solution is the one another developer can understand quickly without prior context.
