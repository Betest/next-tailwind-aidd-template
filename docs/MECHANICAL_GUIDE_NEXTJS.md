# MECHANICAL_GUIDE_NEXTJS — App Router + Server Actions

Purpose: **low-level, mechanical rules** for Next.js App Router.  
No philosophy. No trade-offs. Just correct usage.

Escalation: `RENDERING_RULES_V3.md` → this guide → `rendering_rules_react_type_script_mechanical_guide_v_2.md` (only if needed)

---

## 1) Server vs Client Components

### Default
- Components are **Server Components** by default.

### A component MUST be a Client Component if it:
- uses React client hooks: `useState`, `useEffect`, `useReducer`, `useRef`
- uses event handlers: `onClick`, `onSubmit`, etc.
- uses browser-only APIs: `window`, `document`, `localStorage`
- depends on client-only UI libraries that require DOM

### Rules
- Add `"use client"` **only at the top of the module**.
- Do **not** add `"use client"` to a parent to “fix” a small interactive child.
- If only a small part is interactive, split it into a client leaf.

---

## 2) Canonical Server → Client Split

### Correct
```txt
ServerComponent
  └─ ClientLeaf (interactive)
```

### Incorrect
```txt
ClientComponent
  └─ Everything else (moved to client for convenience)
```

Rule:
> If only 5% needs interactivity, only 5% becomes client.

---

## 3) Data Fetching

### Server Components (preferred)
- Fetch on the server (Server Components or server-only query functions).
- Prefer feature-level query modules (`features/<feature>/queries/*`).

Allowed:
```ts
const data = await getFooQuery();
```

Forbidden by default:
- fetching the same server data in both server and client without a reason
- putting server responses into global client stores

---

## 4) Server Actions (Mutations)

### Declaration
- Must include:
```ts
'use server';
```

### Location (recommended)
- `src/features/<feature>/actions/*`

### Requirements
- Validate input (Zod schema or equivalent).
- Enforce authorization on the server.
- Return a typed result object (prefer over throwing raw errors).

Preferred result shape:
```ts
export type ActionError = {
  code: string;
  message: string;
  fieldErrors?: Record<string, string>;
};

export type ActionResult<T> =
  | { ok: true; data: T }
  | { ok: false; error: ActionError };
```

Forbidden:
- throwing raw errors to UI when a typed result is reasonable

---

## 5) Revalidation After Mutations

Mutations MUST explicitly revalidate:

- `revalidateTag()` for domain/shared data
- `revalidatePath()` for route-specific refresh

Rules:
- domain data → prefer `revalidateTag`
- route-specific UI → `revalidatePath`
- never rely on “implicit” revalidation

---

## 6) Forms

Rules:
- Forms must use **React Hook Form**.
- Schema validation is mandatory (e.g., Zod).
- Submission triggers a Server Action.

Forbidden:
- `useState` per field as the default approach
- manual ad-hoc validation in submit handlers

---

## 7) State Ownership

- Server state (remote async data):
  - server fetch (preferred) OR TanStack Query (client, only when needed)
- Global client state:
  - Zustand / RTK only for cross-cutting UI/client concerns
- Local state:
  - component or custom hook

Forbidden:
- storing server responses in global client stores

---

## 8) Custom Hooks (Mechanical)

Rules:
- Hooks should be deterministic and reusable.
- Hooks should not render JSX.
- Default: hooks should not fetch server data (unless explicitly client-side server state with TanStack Query).

---

## 9) `useEffect` Rules

Allowed:
- subscriptions
- timers
- external synchronization

Forbidden:
- computing derived UI state
- fetching server data that can live on the server

Dependencies:
- must be correct
- no blanket `eslint-disable` for exhaustive deps

---

## 10) Lists & Keys

Rules:
- Keys must be stable domain identifiers.
- Index as key allowed only for static lists that never reorder/insert/remove.

---

## 11) Errors

- Route-level errors: use `error.tsx`.
- Prefer typed error results for actions instead of leaking internal errors.

---

## 12) Final Mechanical Check

Before accepting a change, verify:

- unnecessary `"use client"`?
- duplicated fetching (server + client) without reason?
- missing `revalidateTag` / `revalidatePath` after mutation?
- server data stored in global client state?
- unstable props passed into memoized/large subtrees?
- `useEffect` computing derived UI state?

If any YES → refactor.

---

End of document.
