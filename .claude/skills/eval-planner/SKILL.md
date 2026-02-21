---
name: eval-planner
description: Write eval plans, define rubrics and quality dimensions, and drive ship/no-ship decisions for AI and agentic features. Covers both agentic workflow evals (task completion, tool accuracy, reasoning coherence) and LLM feature evals (accuracy, relevance, tone, latency). Use when you need to evaluate an AI feature before shipping.
user-invocable: true
---

Write an Eval Plan using the template at `Docs/PRDdocs/eval_plan_template.md`. An Eval Plan defines quality dimensions, scoring rubrics, eval methods, and ship criteria for an AI-native feature or agentic workflow.

## Modes

### Mode Detection

Check the start of the user's message for a `[bracket]` prefix. Valid modes: `[create]`, `[rubric]`, `[update]`. Everything after the prefix is the task description.

### Default Behavior

When no mode prefix is given, behave as **`[create]`** — write a complete Eval Plan.

### `[create]` — Write a Complete Eval Plan (Default)

A new eval is needed. Write all 6 sections.

**Required input:** Paste an Intent Brief, or describe the feature/agent behavior being evaluated. The more specific the input, the better the rubric.

**Output:** Complete Eval Plan with all 6 sections filled. Dimensions and rubrics tailored to whether this is an agentic workflow or an LLM feature output.

**Key behavior:**
- Read Intent Brief sections 3 (Goals) and 6 (Requirements) to derive dimensions. If no Intent Brief is provided, derive from the description.
- Determine eval type: agentic workflow or LLM feature output (or both)
  - **Agentic:** default dimensions are task completion rate, tool selection accuracy, multi-step reasoning coherence, memory/context retrieval efficiency
  - **LLM feature:** default dimensions are output accuracy, relevance, tone & safety, latency
- Mark P0 dimensions explicitly — these gate the ship decision
- Fill ship criteria (section 5) with specific numeric thresholds, not vague language
- Close with open questions (section 6) that should feed the Question Log

### `[rubric]` — Dimensions and Rubric Only

You need eval dimensions and scoring rubrics, not a full plan.

**Required input:** Feature or agent description, plus any constraints on scope or method.

**Output:** Section 3 (Dimensions & Rubrics) and Section 5 (Ship Criteria) only — a dimensions table with rubric levels (1–5), weights, and suggested eval method per dimension.

**Key behavior:**
- Produce a clean, table-first output — no narrative filler
- Include at least one dimension that is pass/fail (e.g., safety, edge case handling)
- Weight columns must sum to 100%
- Suggest eval method per dimension: human eval, LLM-as-judge, regression, golden dataset, or red-team

### `[update]` — Record Results and Surface Ship/No-Ship Flag

Eval results are in. Update the plan and determine status.

**Required input:** Existing Eval Plan (paste or reference) + new eval scores per dimension.

**Output:** Updated Eval Plan with current scores filled into Section 5 (Ship Criteria, "Current Status" column) + a clear ship/no-ship recommendation at the top.

**Key behavior:**
- Compare each dimension's score to its threshold
- Flag the overall recommendation at the top of the output: **SHIP / ITERATE / NO-SHIP**
- If any P0 dimension is Yellow: state the specific improvement needed and suggest a re-eval date
- If any P0 dimension is Red: prompt the user to document with `/decision-memo [capture]`
- Provide the Scorecard section 6b row to paste in

## Template

Use the Eval Plan template at `Docs/PRDdocs/eval_plan_template.md`. All 6 sections:

1. **Overview** — Feature/agent behavior being evaluated, eval goal, PM owner, linked Intent Brief
2. **Eval Scope** — Agentic vs. LLM output; in/out table; edge cases included/excluded
3. **Dimensions & Rubrics** — Quality dimensions with scoring rubric (1–5 or pass/fail) and weights
4. **Eval Methods** — Methods per dimension: human eval, LLM-as-judge, regression suite, golden dataset, red-team — with cadence
5. **Ship Criteria** — Per-dimension thresholds: Green (ship), Yellow (iterate), Red (no-ship)
6. **Open Questions** — Unresolved eval design questions (feeds Question Log)

## Linking to Other Artifacts

- **From Intent Brief:** Read sections 3 (Goals) and 6 (Requirements) to derive dimensions
- **To Scorecard:** Eval results go into Scorecard section 6b (Eval Results); update the Eval Coverage row in section 1 (Health Rating)
- **To Decision Memo:** Ship/no-ship decisions → `/decision-memo [capture]`
- **To Question Log:** Open questions from section 6 → `/question-log`

## Writing Standards

- Rubric levels must be specific and distinguishable — avoid vague descriptors like "good" or "acceptable"
- Each dimension needs a weight — weights must sum to 100%
- Ship criteria must use numbers, not qualitative phrases (e.g., "≥4.0" not "mostly correct")
- P0 vs. P1 dimensions must be explicit — P0 gates shipping
- No buzzwords. Plain language.

## Naming Convention

Save as: `EP_[feature-name]_[YYYY-MM-DD].md`

Example: `EP_notification-routing-agent_2026-02-21.md`

## Quality Checklist

- [ ] Eval type identified (agentic / LLM feature / both)
- [ ] At least 3 dimensions defined with explicit weights summing to 100%
- [ ] P0 dimensions clearly marked
- [ ] Ship thresholds are numbers, not qualitative phrases
- [ ] At least 2 distinct eval methods specified
- [ ] Open questions captured for Question Log
- [ ] Naming convention followed
