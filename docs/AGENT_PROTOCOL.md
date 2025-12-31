# AGENT_PROTOCOL — AIDD Enforcement

This protocol defines **how the agent must reason, decide, and respond** in this repository.

---

## 1) Authority hierarchy

When solving any task, the agent must respect this order:

1. `AI_RULES.md`
2. `RENDERING_RULES_V3.md`
3. `CODING_STANDARDS.md`
4. `ENGINEERING_PRINCIPLES.md`
5. `FRONTEND_AGENT_PLAYBOOK.md`

If ambiguity exists, escalation to:
- `rendering_rules_react_type_script_mechanical_guide_v_2.md`

is allowed **only with explicit justification**.

---

## 2) Performance & rendering protocol

When a task involves:
- rerenders
- performance
- memoization
- hooks behavior
- context usage

The agent **must**:

1. State which **V3 rules apply**
2. Explain briefly how the change satisfies them
3. Avoid introducing new abstractions unless justified

---

## 3) Decision discipline

- Prefer the smallest correct change
- Avoid speculative refactors
- No rewrites unless explicitly requested

---

## 4) Escalation protocol

Escalate to v2 **only if**:

- V3 rules conflict
- V3 rules are insufficient
- React behavior is ambiguous

When escalating:

- Explicitly say **why V3 is insufficient**
- Quote the relevant v2 section

---

## 5) Violation handling

If a proposed solution violates any rule:

- The agent must flag the violation
- The agent must propose a compliant alternative

---

## 6) Output discipline

Responses must follow the system prompt structure:

Plan → Change → Next check

No filler. No chain-of-thought.

---

**This protocol is mandatory.**

