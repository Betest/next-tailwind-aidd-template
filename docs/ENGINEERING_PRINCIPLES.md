# ENGINEERING_PRINCIPLES — Next.js App Router + Server Actions

These principles define architecture, boundaries, and ownership rules.
They complement `AI_RULES.md` and `RENDERING_RULES_V3.md`.

---

## 1) Architectural Defaults

- Default to **Server Components**.
- Keep Client Components **small and leaf-level**.
- Use **Server Actions** for mutations when they reduce complexity and improve correctness.
- Prefer **cohesive feature boundaries** over shared “utils soup”.

---

## 2) Server vs Client Responsibilities

### Server (default)
Use the server for:
- data fetching
- authorization checks
- data shaping (DTO/view models)
- heavy rendering and composition
- mutations via Server Actions
- cache invalidation/revalidation

### Client (only when needed)
Use the client for:
- interactivity (handlers)
- local UI state (menus, dialogs, tabs)
- optimistic UI (when justified)
- client-only APIs (window, localStorage)

Golden rule:
> If it does not need the browser, keep it on the server.

---

## 3) Server Actions Principles

### When to use Server Actions
- mutations: create/update/delete
- workflows that require server-side validation
- when you want typed inputs + centralized auth + direct cache invalidation

### When NOT to use Server Actions
- public API consumption by third parties (use Route Handlers)
- complex integrations that require background jobs (use a job queue / worker)
- when the UI needs real-time progress streaming (consider SSE/WebSockets)

### Requirements
- Always validate inputs (schema validation).
- Always enforce authorization on the server.
- Return stable, typed results (avoid throwing raw errors to UI).
- Avoid passing large data payloads back to client unless necessary.

---

## 4) Route Handlers vs Server Actions

Use **Route Handlers** (`app/api/*`) when:
- you need a stable HTTP API boundary
- external clients will call it
- you want explicit caching headers and HTTP semantics

Use **Server Actions** when:
- the caller is your own Next.js UI
- you want colocated mutations and revalidation
- you want minimal network ceremony

---

## 5) Data Access Layer (DAL)

- Centralize data access in a DAL module (server-only).
- DAL functions must be:
  - deterministic
  - typed
  - safe (validation + auth at boundaries)
- Avoid mixing DAL calls directly inside large Client Components.

---

## 6) Caching & Revalidation Ownership

- Server is the authority for caching decisions.
- Mutations must explicitly revalidate or invalidate the correct scope:
  - `revalidatePath`
  - `revalidateTag`
- Prefer tags for domain-level caching when multiple pages depend on the same data.

---

## 7) Feature Boundaries & Public APIs

- Features must expose a public API via `index.ts`.
- Deep imports across feature internals are forbidden.
- Prefer placing server actions inside the feature that owns the domain change.

---

## 8) Error & Result Conventions

- Prefer typed results for Server Actions:
  - `{ ok: true, data }`
  - `{ ok: false, error: { code, message, fieldErrors? } }`
- Never leak internal error details to the client.
- UI handles errors consistently (toasts, inline messages).

---

## 9) Security Baselines

- Auth checks happen server-side (Server Components / Server Actions / Route Handlers).
- Never trust client inputs. Always validate.
- Avoid storing sensitive data in the client.

---

## 10) Practical “Stop Rules”

Stop and refactor when you see:
- large trees moved to `"use client"`
- duplicated fetching (server + client for same data without reason)
- server data stored in global client state
- inconsistent revalidation after mutations
