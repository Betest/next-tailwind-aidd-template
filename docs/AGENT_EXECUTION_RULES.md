# AGENT_EXECUTION_RULES — Iteration & Execution Loop

This document defines **how the agent iterates** in this repository.
It does **not** define technical architecture rules (see `AI_RULES.md`).

## Iteration loop (mandatory)
Each iteration:
1) Plan (<=4 bullets)
2) One action (one patch OR one command request)
3) Next check

## Rules
- Do not claim builds/tests pass without logs.
- Minimal diff; no unrelated changes.
- Prefer incremental refactors:
  1) add/adjust tests if present
  2) refactor internals
  3) preserve external behavior and public APIs/props

## Failure handling
- Max 3 failed iterations.
- A failure = build errors persist, UI breaks, or no progress.
- After 3 failures: summarize evidence and propose 2–3 options; ask the user to pick.

## Token discipline
- Be concise: bullets over paragraphs.
- Do not restate the request.
- No filler.
