# RENDERING_RULES_V3 — Next.js + React + TypeScript (AIDD-Optimized)

Purpose: default rendering contract for AIDD in **Next.js App Router**.
Scope: fast, mechanical rules with minimal tokens.
Escalation: if ambiguity exists, consult `rendering_rules_react_type_script_mechanical_guide_v_2.md`.

---

## 0) Core Definitions

- Stable value: primitive or stable reference across renders.
- Unstable value: inline `{}` / `[]` / `() => {}` created during render.
- Server Component: runs on server; no hooks, no event handlers.
- Client Component: `"use client"`; can use hooks and handlers.
- Server state: remote async data.
- Client state: UI / interaction state.

---

## 1) Golden Defaults

- Default to **Server Components**.
- Keep client components **small and localized**.
- Props are OK. Avoid prop drilling and unstable identities.
- Memoization is opt-in, never default.

---

## 2) Server → Client Boundary Rule (High Impact)

Rule: Do not “promote” large trees to `"use client"` to fix a small interactive need.

Fix:
- split: a small client leaf for interactivity
- keep data fetching + heavy rendering in server

---

## 3) Identity Rules (High Impact)

Rule: Inline objects/arrays/functions passed to children are forbidden
if the child is memoized or part of a large tree.

Fix: hoist constant, `useMemo`, `useCallback`, or refactor API.

---

## 4) Effects

Rule: `useEffect` is for external synchronization only.

- forbidden: computing derived UI state in effects
- allowed: IO, subscriptions, timers
- deps must be correct; no blanket eslint disables

---

## 5) Context

Rule: Broad contexts must contain stable values only.

- volatile data → local state or dedicated subtree
- split contexts by volatility

---

## 6) Lists & Keys

Rule: keys must be stable and semantic.

- forbidden: index as key when reorder/insert/remove is possible
- allowed: unique domain identifier

---

## 7) State Ownership

Rule: each state has a single owner.

- server fetch (server) OR TanStack Query (client)
- global client UI state → Zustand/RTK (cross-cutting only)
- never store server responses in global stores

---

## 8) Forms

Rule: React Hook Form + schema validation required.

- forbidden: `useState` per field by default

---

## 9) Memoization

Rule: `React.memo` allowed only if ALL apply:

- component is pure
- parent rerenders frequently
- render is expensive or list is large
- props are stable

Memo must include a 1-line justification comment.

---

## 10) Mechanical Check (Fast)

Before accepting a change:

- large client boundary introduced unnecessarily?
- unstable identities passed down?
- volatile context values?
- index used as key?
- `useEffect` computing UI state?
- `React.memo` without justification?

If any YES, refactor.

---

Default AIDD contract. Escalate to v2 only when necessary.
