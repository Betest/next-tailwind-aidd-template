# FRONTEND_AGENT_PLAYBOOK — Next.js (AIDD)

This playbook defines how the agent should make trade-offs in this repository.

---

This playbook assumes all constraints in `AI_RULES.md` are already enforced.


## 1) Default Approach (Always)

1. Start server-first (Server Components + server fetch).
2. Add small client leaves only for interactivity.
3. Use Server Actions for mutations when appropriate.
4. Revalidate deterministically.

---

## 2) Decision Checklist: Should this be a Client Component?

Make it a Client Component only if at least one is true:
- needs event handlers
- uses React client hooks (`useState`, `useEffect`, etc.)
- uses browser APIs
- needs client-side animation/stateful UI widgets

If only a small part needs client behavior:
- split into a client leaf
- keep the rest server

---

## 3) Decision Checklist: Server Action vs Route Handler

Use Server Action if:
- only your UI calls it
- you need typed inputs and server validation
- you want colocated revalidation

Use Route Handler if:
- external clients call it
- you need explicit HTTP semantics
- you need non-Next consumers

---

## 4) Patterns (Preferred)

- Server container + client leaf pattern
- Typed `ActionResult` for all mutations
- Zod validation at boundaries
- Tag-based caching for shared domain data
- Custom hooks for client-only UI logic (not data fetching by default)

---

## 5) Anti-Patterns (Flag Immediately)

- “Just add `use client` at the top” for convenience
- Fetching the same data on server and client without reason
- Keeping server responses in Zustand/RTK
- Using `useEffect` to compute derived UI state
- Memo spam (`useMemo`/`useCallback` everywhere)

---

## 6) Output Discipline (Agent)

When proposing a change:
- Mention which `AI_RULES` and `RENDERING_RULES_V3` rules apply.
- Keep diffs minimal.
- If uncertainty exists, ask **one** targeted question.

---

## 7) Mutation Flow (Canonical)

1. Client form (React Hook Form + schema)
2. Server Action validates + authorizes
3. Mutation occurs
4. Revalidate scope (path/tag)
5. Return typed result
6. UI shows success/error deterministically
