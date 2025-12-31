# nextjs-tailwind-aidd-template

> **AI-Driven Development (AIDD) Template** for **Next.js (App Router) + TypeScript + TailwindCSS**.

This repository is not a typical Next.js starter.
It is a **reference implementation of an AIDD-governed frontend codebase**, explicitly designed to work with AI agents (Cursor / Trae / Kilo) while preserving **determinism, correctness, and architectural discipline**.

---

## 🎯 Purpose

This template exists to:

* Serve as a **baseline AIDD project** for modern Next.js applications
* Enforce **deterministic, low-risk changes** by AI agents
* Encode **engineering rules as contracts**, not suggestions
* Reduce token usage while increasing output correctness
* Align humans and AI around a single, shared set of standards

This repository **assumes AI will actively modify the codebase**.

---

## 🧠 What makes this different from a normal Next.js template

Unlike typical Next.js starters, this project includes:

* A **documentation hierarchy optimized for AI reasoning**
* Explicit **authority and escalation rules** for decisions
* Clear separation between:

  * hard technical constraints
  * rendering and Server/Client boundaries
  * execution discipline
  * contribution standards
* A **mechanical rendering contract** aligned with App Router and React 19
* First-class support for **Server Components and Server Actions**

This template prioritizes **predictability over convenience**.

---

## 📚 Documentation Map (AIDD)

The repository is governed by the following documents:

### 🔹 Primary Authority (AI-first)

1. **`RENDERING_RULES_V3.md`**
   Default rendering, performance, and Server/Client boundary contract (low-token, mechanical)

2. **`AI_RULES.md`**
   Hard, non-negotiable technical constraints

3. **`CODING_STANDARDS.md`**
   Code quality, refactor discipline, and safety rules

4. **`ENGINEERING_PRINCIPLES.md`**
   Architecture, boundaries, ownership, and public APIs

5. **`FRONTEND_AGENT_PLAYBOOK.md`**
   Trade-offs, long-term direction, and agent reasoning guidelines

### 🔹 Escalation & Execution

* **`MECHANICAL_GUIDE_NEXTJS.md`** — procedural fallback for ambiguous cases
* **`AGENT_EXECUTION_RULES.md`** — iteration loop, failure limits, execution discipline
* **`AGENT_PROTOCOL.md`** — response structure and output discipline
* **`AGENT_PROTOCOL_MINI.md`** — token-efficient execution rules

### 🔹 Human-First References

* `PERFORMANCE_GUIDE.md`
* `DESIGN_PATTERNS.md`
* `CONTRIBUTING_AI.md`
* `REPO_CONTEXT.md`

> See **`INDEX.md`** for the authoritative navigation order.

---

## 🏗️ Architecture (Feature-based)

The recommended structure is **feature-based**:

* `src/app/(routes)` — Next.js routes (Server Components by default)
* `src/features/<feature>` — feature modules (public API via `index.ts`)

  * `actions/` — Server Actions (mutations)
  * `queries/` — server reads and data access
  * `schemas/` — Zod validation schemas
  * `ui/` — UI components (server containers + client leaves)

---

## 🧱 Tech Stack

* **Next.js App Router**
* **React 19–compatible rendering model**
* **TypeScript** (strict)
* **TailwindCSS** (utility-first, no CSS-in-JS)
* **lucide-react** for all icons
* **Forms:** React Hook Form + schema validation
* **Mutations:** Server Actions
* **Client server-state (when required):** TanStack Query

No UI kits, design systems, or state libraries are included by default.

---

## 🤖 AI Usage Model

This repository is designed for AI-assisted workflows using tools such as:

* Cursor
* Trae
* Kilo
* Chat-based agents

AI agents **must**:

* Follow `INDEX.md` for document loading order
* Obey `RENDERING_RULES_V3.md` and `AI_RULES.md`
* Apply **minimal diffs only**
* Avoid speculative or stylistic rewrites
* Stop after **3 failed iterations** and escalate

Any output violating these rules is considered **non-compliant**.

---

## 🚦 Contribution Model

All contributions (human or AI-assisted) must follow:

* `CONTRIBUTING_AI.md`
* `CODING_STANDARDS.md`
* `AGENT_EXECUTION_RULES.md`

This ensures:

* Predictable reviews
* Low-risk refactors
* Stable long-term evolution under AI-driven workflows

---

## 🧪 Intended Use Cases

* Bootstrap an **AIDD-ready Next.js project**
* Serve as a **golden reference** for AI-assisted refactors
* Internal templates for teams adopting AI coding workflows
* Teaching and experimentation with **AI-governed codebases**

---

## ⚠️ Non-Goals

This template does **not**:

* Provide a full UI kit or design system
* Optimize for rapid prototyping over correctness
* Hide complexity behind generators or abstractions

Correctness and discipline are preferred over speed.

---

## ✅ Status

This repository represents:

> **AIDD_BASELINE v1.0 (Next.js)**

It is safe to clone, extend, and evolve under AI-driven development workflows.

---

## 📌 Final Note

If you remove the documents, this becomes a normal Next.js template.

If you keep them, this becomes an **AI-governed engineering system**.

Choose intentionally.
