# AI_RULES — Primary Constraints (Next.js)

These rules are **non-negotiable**.
If a solution violates any rule below, it is **invalid**, even if it works.

---

## 1) Primary Rendering Authority

- `RENDERING_RULES_V3.md` is the **default and primary rendering contract**.
- Escalation to `rendering_rules_react_type_script_mechanical_guide_v_2.md`
  is allowed **only when ambiguity exists**.
- UI constraints (icons, styling, UI libs) are enforced by `UI_CONSTRAINTS.md`
  and must be respected at all times.

---

## 2) Next.js Server / Client Boundaries (Hard)

- Default to **Server Components**.
- Use **Client Components** only when required:
  - event handlers (`onClick`, etc.)
  - `useState`, `useEffect`, `useReducer`, `useRef`
  - browser-only APIs (window, localStorage)
  - interactive UI libraries that require DOM
- Do not move large trees to client just to “make it work”.
- If a component is client, minimize its surface area and keep heavy data work in server.

---

## 3) Data Fetching & Caching (Hard)

- Prefer **server-side fetching** (Server Components / route handlers).
- Do not fetch server data inside global client stores.
- For client-side server state (only when needed), use **TanStack Query**.
- Avoid duplicate fetching:
  - server fetch → pass data down
  - client fetch only when truly interactive/refreshing is required

---

## 4) State Ownership (Hard)

- **Server state** (remote async data) → TanStack Query (client) or server fetch (server)
- **Global client state** (cross-cutting UI) → Zustand or Redux Toolkit only
- **Local state** → component or hook
- Server responses are **forbidden** in global client stores.

---

## 5) React / Concurrency Safety

- No side-effects during render.
- No assumptions about render count.
- All effects must be idempotent.

---

## 6) Identity Stability

- Inline `{}` / `[]` / `() => {}` passed to memoized children are forbidden.
- Volatile values in broad context providers are forbidden.

---

## 7) Forms

- Forms **must** use React Hook Form.
- Schema validation is mandatory (e.g., Zod).
- Field-level `useState` is forbidden unless explicitly justified.

---

## 8) TypeScript

- `any` is forbidden.
- Unsafe casts are forbidden.
- Prefer inference, narrowing, discriminated unions.

---

## 9) Feature Boundaries

- Deep imports from feature internals are forbidden.
- Features communicate only through public APIs (`index.ts`).

---



## 10) Conflict Resolution

If documents conflict, the order of authority is:

1. `AI_RULES.md`
2. `RENDERING_RULES_V3.md`
3. `CODING_STANDARDS.md`
4. `ENGINEERING_PRINCIPLES.md`

---

**Violations must be reported explicitly.**
