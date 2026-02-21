# Eval Plan: AI Notification Routing Agent

**Version:** V1.0
**Date:** 2026-02-21
**PM Owner:** [PM Name]
**Linked Intent Brief:** IB_notification-center.md
**Status:** Draft

---

> **Note:** This is a fictional example using a made-up product ("Acme Corp" / "Notification Center") to illustrate the Eval Plan format. Replace all content with your real eval context.

---

## 1. Overview

**What is being evaluated:**

The AI notification routing agent classifies incoming platform events into one of four notification types — Needs Action, FYI, System, Alert — and resolves the correct recipient list. It runs as a multi-step agentic workflow: read the event payload, classify the type, retrieve the recipient policy for that event, and write the notification record. This is an agentic workflow — multiple tool calls, stateful, triggered on every platform event.

**Eval goal:**

Is the routing agent accurate and safe enough to handle 100% of production notification events at GA? Specifically: does it classify types correctly, route to the right users, and fail gracefully on malformed or edge-case inputs?

**PM owner:** [PM Name]
**Linked Intent Brief:** IB_notification-center.md
**Eval type:** Agentic workflow (multi-step, tool-using)

---

## 2. Eval Scope

**Eval type:** Agentic (multi-step, tool-using)

### In / Out

| Item | In Scope | Out of Scope | Notes |
|------|----------|--------------|-------|
| Notification type classification (4 types) | ✅ | — | Core agentic task |
| Recipient list resolution | ✅ | — | Agent retrieves policy per event type |
| Malformed / incomplete event payloads | ✅ | — | Must fail with logged error, not silently |
| Notification content generation | — | ✅ | Content is templated, not AI-generated in V1 |
| Email routing | — | ✅ | Separate system, outside agent scope |
| Per-source notification preferences | — | ✅ | V2 — not in agent scope for V1 |

### Edge Cases

| Edge Case | Included | Rationale |
|-----------|----------|-----------|
| Event with no matching recipient policy | Yes | Agent must surface an error, not drop the notification silently |
| Notification for a deleted source record | Yes | Top support ticket driver — agent must handle this explicitly |
| Duplicate events from the same source | Yes | Deduplication is in agent scope |
| Ambiguous type (e.g., approval that also qualifies as System alert) | Yes | Multi-label cases test classification confidence threshold |
| Non-English notification content | No | V1 is English-only; V2 scope |

**Critical Questions:**
- Do we test against production event distribution or synthetic samples for the golden dataset? (See EQ-001)
- What volume of labeled examples do we have available for the golden dataset before the first eval run?

---

## 3. Dimensions & Rubrics

**Scoring scale:** 1–5, except D-04 (Edge Case Handling) which is pass/fail.

| # | Dimension | Description | Rubric | Weight | Eval Method |
|---|-----------|-------------|--------|--------|-------------|
| D-01 | **Task Completion Rate** | Did the agent complete the full routing workflow without error? | 1: Agent errors or crashes on >10% of inputs; 3: Completes with recoverable errors on 3–10%; 5: Completes cleanly on ≥98% of inputs | 30% | Regression suite |
| D-02 | **Classification Accuracy** | Did the agent assign the correct notification type (Needs Action / FYI / System / Alert)? | 1: <70% correct; 3: 80–89% correct; 5: ≥95% correct | 30% | Golden dataset |
| D-03 | **Recipient Accuracy** | Did the agent route to the right recipient list? | 1: >10% of outputs have wrong recipients; 3: 3–10% wrong; 5: <2% wrong | 20% | Human eval (sampled) |
| D-04 | **Edge Case Handling** | Does the agent fail gracefully on all 5 in-scope edge cases? | Pass: All 5 cases handled without silent failure or wrong routing; Fail: Any case causes a silent drop or incorrect routing | Pass/Fail | Regression suite |
| D-05 | **Multi-Step Reasoning Coherence** | Are the agent's intermediate steps — classify → retrieve policy → write record — logically consistent? | 1: Steps contradict each other; 3: Minor inconsistencies but outcome is correct; 5: Steps are fully coherent and traceable | 20% | LLM-as-judge |

**Note:** D-04 is a hard gate — a Fail on any edge case is a no-ship regardless of other scores.

**Critical Questions:**
- Is 95% classification accuracy achievable with the labeled data available before GA? Requires Eng input before finalizing threshold.
- Should D-05 coherence be scored per-trace or averaged over a batch?

---

## 4. Eval Methods

| Dimension | Method | Cadence | Notes |
|-----------|--------|---------|-------|
| D-01 Task Completion | Regression suite | Every release | 200 synthetic event payloads covering all 4 notification types and all recipient policy types |
| D-02 Classification Accuracy | Golden dataset | Every release | 500 labeled examples (125 per type); sourced from 2 weeks of production events, labeled by 2 raters |
| D-03 Recipient Accuracy | Human eval (sampled) | Every release | 50 randomly sampled outputs per run; 2 human raters; inter-rater agreement required ≥85% before averaging |
| D-04 Edge Case Handling | Regression suite | Every release | 5 fixed edge cases defined in section 2; all 5 must pass |
| D-05 Multi-Step Coherence | LLM-as-judge | Every release | Claude Opus 4 as judge; rubric prompt provided to judge; validated against 20 human-rated traces before first run |

**Critical Questions:**
- Who owns the golden dataset labeling? Needs 500 labeled examples by [date] for V1 eval run. (See EQ-002)
- Has the LLM-as-judge been validated against human raters? Need ≥80% agreement before relying on it for ship decisions. (See EQ-003)

---

## 5. Ship Criteria

All P0 dimensions must be Green before shipping.

| # | Dimension | Priority | Green (ship) | Yellow (iterate) | Red (no-ship) | Current Status |
|---|-----------|----------|-------------|-----------------|---------------|----------------|
| D-01 | Task Completion Rate | P0 | ≥4.5 avg | 3.5–4.4 | <3.5 | Not yet run |
| D-02 | Classification Accuracy | P0 | ≥95% correct | 85–94% correct | <85% correct | Not yet run |
| D-03 | Recipient Accuracy | P0 | <2% wrong recipients | 2–10% wrong | >10% wrong | Not yet run |
| D-04 | Edge Case Handling | P0 | All 5 pass | — | Any fail | Not yet run |
| D-05 | Multi-Step Coherence | P1 | ≥4.0 avg | 3.0–3.9 | <3.0 | Not yet run |

**Ship decision rule:**
- D-01, D-02, D-03, D-04 all Green → **Ship**
- Any P0 dimension Yellow → **Iterate** — PM defines the specific fix and a re-eval date within 2 weeks
- Any P0 dimension Red → **No-ship** — document in `/decision-memo [capture]` and escalate

**Document the ship/no-ship decision in:** `DM_[date]_notification-routing-agent-ship-decision.md`

**Critical Questions:**
- If D-02 (Classification Accuracy) returns at 90% (Yellow), what is the iteration plan? PM and Eng Lead must align on this before the first eval run so Yellow doesn't stall the decision.
- Who has final sign-off on the ship decision — PM alone, or PM + Eng Lead?

---

## 6. Open Questions

| # | Question | Priority | Owner | Status |
|---|----------|----------|-------|--------|
| EQ-001 | Do we test against production event distribution or synthetic samples for the golden dataset? | High | PM + Eng | Open |
| EQ-002 | Who labels the golden dataset? What deadline do we need to hit 500 labeled examples before V1 eval? | High | PM | Open |
| EQ-003 | LLM-as-judge validation: does Opus judge agree with human raters ≥80% of the time on coherence scoring? | High | Eng | Open |
| EQ-004 | If D-02 returns Yellow (85–94%), what is the specific improvement path and re-eval timeline? | Med | PM + Eng | Open |
| EQ-005 | Should the edge case test set expand to 10 cases before GA? Current 5 cover V1 scope but not all known failure modes. | Low | PM + QA | Open |
