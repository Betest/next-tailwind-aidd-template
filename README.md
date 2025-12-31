# nextjs-aidd-template (App Router + Server Actions)

AI-Driven Development (AIDD) template for **Next.js + TypeScript + TailwindCSS**.

## Purpose
This repo is a reference implementation of an **AI-governed frontend codebase**:
- deterministic changes
- minimal diffs
- documented authority & escalation
- React 19 safe rendering rules
- Server Components first, Client leaves only

## Documentation Authority
Use `INDEX.md` to navigate.

Primary documents:
- `AI_RULES.md` — hard constraints
- `RENDERING_RULES_V3.md` — rendering/performance contract
- `CODING_STANDARDS.md` — code quality & refactor discipline
- `ENGINEERING_PRINCIPLES.md` — architecture & boundaries

Agent behavior:
- `AGENT_PROTOCOL.md`
- `AGENT_EXECUTION_RULES.md`
- `AGENT_PROTOCOL_MINI.md`

UI boundaries:
- `UI_CONSTRAINTS.md`

## Architecture (Feature-based)
- `src/app/(routes)` — Next routes (Server Components by default)
- `src/features/<feature>` — feature modules (public API via `index.ts`)
  - `actions/` — Server Actions (mutations)
  - `queries/` — server reads (data access per feature)
  - `schemas/` — Zod validation
  - `ui/` — UI components (server container + client leaf)

## Defaults
- Server Components first
- Mutations via Server Actions
- Validation at boundaries (Zod)
- Forms: React Hook Form + schema
- Icons: lucide-react only
- Styling: Tailwind only
