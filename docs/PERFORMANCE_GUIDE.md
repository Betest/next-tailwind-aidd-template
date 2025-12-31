# Performance Guide (Next.js + React)

## Defaults
- Prefer clarity first (KISS). Optimize only when it matters.
- Default to Server Components. Keep Client Components small.

## Client boundary
- Avoid promoting large trees to `"use client"`.
- Split: server parent + small interactive client leaf.

## Stable props
Prefer:
- primitives
- stable objects via useMemo (only if needed)
- stable callbacks via useCallback (only if identity matters)

Avoid:
- inline `{}` / `[]` / handlers passed to memoized/large subtrees

## Component boundaries
- Split by volatility: fast-changing state stays low.
- Keep state close to where it is used.

## Context
- Keep provider values stable.
- Split contexts by volatility.

## Effects
- useEffect only for external sync.
- Correct deps; no blanket disables.

## Memoization
- Never memoize by habit.
- Memo only with evidence (expensive render + stable props).

## Next.js App Router Considerations

- Prefer Server Components for performance and caching.
- Avoid promoting components to `"use client"` for minor interactivity.
- Client Components should be leaf-level whenever possible.
- RSC boundaries are performance boundaries.
