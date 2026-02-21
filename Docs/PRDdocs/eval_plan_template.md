# Eval Plan: [Feature / Agent Name]

**Version:** V1.0
**Date:** [YYYY-MM-DD]
**PM Owner:** [Name]
**Linked Intent Brief:** [IB_feature-name.md or "N/A"]
**Status:** Draft / Active / Closed

---

## 1. Overview

**What is being evaluated:**

[One paragraph. What is the feature or agent behavior under eval? Is this an agentic workflow (multi-step, tool-using) or an LLM output feature (single-turn generation)? What does success look like from a user perspective?]

**Eval goal:**

[What specific question does this eval answer? E.g., "Is the routing agent accurate enough to ship?" or "Does the summarization output meet tone and accuracy standards?"]

**PM owner:** [Name]
**Linked Intent Brief:** [IB_feature-name.md]
**Eval type:** Agentic workflow / LLM feature output / Both

---

## 2. Eval Scope

**Eval type:** Agentic (multi-step, tool-using) / LLM output (single-turn)

### In / Out

| Item | In Scope | Out of Scope | Notes |
|------|----------|--------------|-------|
| [Behavior or output type] | ✅ / — | — / ✅ | [Why] |

### Edge Cases

| Edge Case | Included | Rationale |
|-----------|----------|-----------|
| [Edge case] | Yes / No | [Why or why not] |

**Critical Questions:**
- [Open questions about scope — e.g., "Do we eval on adversarial inputs in V1?"]

---

## 3. Dimensions & Rubrics

**Scoring scale:** 1–5 (unless noted as pass/fail)

| # | Dimension | Description | Rubric (1 = fail, 5 = excellent) | Weight | Eval Method |
|---|-----------|-------------|-----------------------------------|--------|-------------|
| D-01 | [Dimension name] | [What it measures] | 1: [fail state] / 3: [acceptable] / 5: [excellent] | [%] | [Method] |

**For agentic evals — standard dimensions (customize thresholds):**
- Task Completion Rate: Did the agent complete the intended task end-to-end?
- Tool Selection Accuracy: Did the agent call the right tools in the right order?
- Multi-Step Reasoning Coherence: Are intermediate steps logical and consistent?
- Memory / Context Retrieval Efficiency: Did the agent retrieve and use relevant context correctly?

**For LLM feature evals — standard dimensions (customize thresholds):**
- Output Accuracy: Is the content factually correct relative to inputs?
- Relevance: Does the output address the user's actual intent?
- Tone & Safety: Is the output on-brand and free of harmful content?
- Latency: Does the output arrive within the acceptable time threshold?

**Critical Questions:**
- [Open questions about dimensions or rubric calibration]

---

## 4. Eval Methods

| Dimension | Method | Cadence | Notes |
|-----------|--------|---------|-------|
| [D-01] | Human eval / LLM-as-judge / Regression / Golden dataset / Red-team | [Per release / Weekly / Continuous] | [Any calibration notes] |

**Method descriptions:**
- **Human eval:** Human raters score outputs against the rubric. Use for high-stakes or nuanced dimensions.
- **LLM-as-judge:** A separate LLM scores outputs against the rubric. Use for volume; validate against human ratings first.
- **Regression suite:** Automated test suite run against known-good inputs. Use for task completion and tool accuracy.
- **Golden dataset:** Fixed set of labeled examples. Score is % correct. Use for accuracy dimensions.
- **Red-team:** Adversarial inputs designed to break the behavior. Use for safety and edge case coverage.

**Critical Questions:**
- [Open questions about method selection or calibration]

---

## 5. Ship Criteria

All P0 dimensions must be Green before shipping.

| # | Dimension | Priority | Green (ship) | Yellow (iterate) | Red (no-ship) | Current Status |
|---|-----------|----------|-------------|-----------------|---------------|----------------|
| D-01 | [Dimension name] | P0 / P1 | [Threshold, e.g., ≥4.0] | [e.g., 3.0–3.9] | [e.g., <3.0] | Not yet run |

**Ship decision rule:**
- All P0 dimensions Green → **Ship**
- Any P0 dimension Yellow → **Iterate with plan** (define specific improvement and re-eval date)
- Any P0 dimension Red → **No-ship** (document with `/decision-memo [capture]`)

**Document the ship/no-ship decision in:** `DM_[YYYY-MM-DD]_[feature-name]-ship-decision.md`

**Critical Questions:**
- [Open questions about thresholds or what "good enough" means for this feature]

---

## 6. Open Questions

Questions unresolved at eval plan creation. Feed to Question Log.

| # | Question | Priority | Owner | Status |
|---|----------|----------|-------|--------|
| EQ-001 | [Question] | High / Med / Low | [Name] | Open |

---

*Eval Plan template. Derived from Intent Brief sections 3 (Goals) and 6 (Requirements). Results feed Scorecard section 6b (Eval Results). Ship/no-ship decision → `/decision-memo [capture]`.*
*Naming convention: `EP_[feature-name]_[YYYY-MM-DD].md`*
