# INDEX — AI-Driven Development (AIDD) — Next.js

This document defines **how AI agents and humans should navigate the documentation**
in this **Next.js (TypeScript)** repository.

It is the **entry point** for Cursor / Trae / Kilo and contributors.

---

## 1) Default Reading Order (AI Agents)

When solving a task, follow this order **strictly**:

1. **`RENDERING_RULES_V3.md`**
   → Default rendering + Next.js Server/Client rules (low token, mechanical)

2. **`AI_RULES.md`**
   → Hard constraints that must never be violated

3. **`CODING_STANDARDS.md`**
   → Code quality, refactor discipline, tests, safety

4. **`ENGINEERING_PRINCIPLES.md`**
   → Architecture, boundaries, ownership, public APIs

5. **`FRONTEND_AGENT_PLAYBOOK.md`**
   → Philosophy, trade-offs, long-term direction

Escalate **only if needed**:

- **`MECHANICAL_GUIDE_NEXTJS.md`**
  → Canonical procedural guide when ambiguity exists

---

## 2) Human-First Documents

Optimized for **human reading**, not default AI loading:

- `PERFORMANCE_GUIDE.md`
- `DESIGN_PATTERNS.md`
- `CONTRIBUTING_AI.md`
- `REPO_CONTEXT.md`

---

## 3) Prompt & Protocol Documents

| File | Responsibility |
|---|---|
| `docs/prompts/frontend_agent_prompt_*.md` | Agent role & behavior |
| `AGENT_EXECUTION_RULES.md` | Iteration loop, failure limits |
| `AGENT_PROTOCOL.md` | Response structure & discipline |
| `AGENT_PROTOCOL_MINI.md` | Token-efficient execution |
| `system-prompt.md` | System-level constraints |
| `user-prompt.md` | User input normalization |

---

## 4) Decision Heuristics (AI)

- Rendering / performance issue → **RENDERING_RULES_V3.md**
- Server vs Client boundary → `AI_RULES.md` + V3
- Data fetching / caching ambiguity → `AI_RULES.md`
- Forms / validation → `AI_RULES.md` + `CODING_STANDARDS.md`
- Deep React / Next behavior → **MECHANICAL_GUIDE_NEXTJS.md**

---

## 5) Single Source of Truth

- **Rendering rules** → `RENDERING_RULES_V3.md`
- **Hard constraints** → `AI_RULES.md`
- **Architecture** → `ENGINEERING_PRINCIPLES.md`

If documents conflict:

> `AI_RULES.md` > `RENDERING_RULES_V3.md` > others

---

**This index is authoritative for AIDD navigation.**
