# Agent Protocol

Each iteration:
1) Plan (<=4 bullets)
2) One action (one patch OR one command request)
3) Next check

Rules:
- Do not claim builds/tests pass without logs.
- Minimal diff; no unrelated changes.
- Stop after 3 failed iterations; propose options.

Documentation authority:
- Follow `INDEX.md` to decide which documents to consult.
- Rendering and performance decisions must follow `RENDERING_RULES_V3.md`.
- Escalate to `rendering_rules_react_type_script_mechanical_guide_v_2.md`
  only if V3 is insufficient or ambiguous.

Violations:
- If a solution violates `AI_RULES.md`, it must be flagged explicitly
  and a compliant alternative must be proposed.
