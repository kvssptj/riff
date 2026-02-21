---
name: decision-memo
description: Capture, evaluate, or retroactively document product decisions using the Decision Memo template. Produces atomic decision records that link to Intent Briefs and Question Logs. Use when a decision needs to be recorded, when evaluating options, or when documenting a past decision.
user-invocable: true
---

Capture a product decision using the Decision Memo template at `Docs/PRDdocs/decision_memo_template.md`. One decision, one memo.

## Modes

### Mode Detection

Check the start of the user's message for a `[bracket]` prefix. Valid modes: `[capture]`, `[evaluate]`, `[retro]`. Everything after the prefix is the task description.

### Default Behavior

When no mode prefix is given, behave as **`[capture]`** — document a decision that has been made.

### `[capture]` — Record a Decision (Default)

The decision has been made. Document it clearly.

**Required input:** The decision and its context (from the user's message, a transcript, or a Question Log entry).

**Output:** Complete Decision Memo with all 7 sections filled. Focus on sections 2 (Decision), 3 (Why This Not That), and 7 (Open Threads).

**Key behavior:**
- State the decision in one clear sentence in section 2
- Fill the options table with at least 2 alternatives that were considered
- Be honest about what this closes off (section 5)
- Link to the source (Question Log entry, meeting, or conversation)

### `[evaluate]` — Evaluate Options Before Deciding

The decision hasn't been made yet. Help the PM think through it.

**Required input:** The situation and at least 2 options to evaluate.

**Output:** Decision Memo with section 2 left as "[PENDING — options evaluated below]". Section 3 (Why This Not That) is the focus — detailed pro/con analysis for each option.

**Key behavior:**
- Don't make the decision for the PM — present the trade-offs
- Score each option if criteria are clear (table format)
- Highlight the most important differentiator between options
- End with a recommendation, clearly labeled as such

### `[retro]` — Retroactive Documentation

A decision was made in the past but never documented. Reconstruct it.

**Required input:** What was decided and any available context (old docs, transcripts, or the PM's memory).

**Output:** Complete Decision Memo. Mark assumptions explicitly in section 6. Flag anything that may no longer be accurate in section 7.

**Key behavior:**
- Mark sections where you're reconstructing from incomplete information: "[Reconstructed — verify with [person/team]]"
- Populate section 7 (Open Threads) with questions about whether the decision still holds
- Note the original decision date separately from the memo creation date

## Template

Use the Decision Memo template at `Docs/PRDdocs/decision_memo_template.md`. All 7 sections:

1. **Situation** — What's happening that requires a decision
2. **Decision** — One clear sentence stating the choice
3. **Why This, Not That** — Options table with reasoning
4. **What This Unlocks** — What becomes possible
5. **What This Closes Off** — What we're giving up
6. **Constraints & Assumptions** — Hard boundaries and beliefs
7. **Open Threads** — Follow-up questions that remain

## Linking to Other Artifacts

- **From Question Log:** When a question resolves into a significant decision, create a Decision Memo and link it in the Question Log's Resolution column
- **From Intent Brief:** Reference Decision Memos in section 5 (Solution Intent → Key Decisions Made)
- **From Scorecard:** Decision Memos appear in section 4 (Decision Tracker)

## Writing Standards

- One decision per memo. If you find yourself documenting two decisions, split into two memos.
- Section 3 must have at least 2 alternatives (including "do nothing" if applicable)
- Section 5 (Closes Off) must be honest — every decision has trade-offs
- Plain language, no buzzwords
- Ground claims in specific docs, capabilities, or data

## Naming Convention

Save as: `DM_[YYYY-MM-DD]_[short-description].md`

Example: `DM_2026-02-21_notification-delivery-channel.md`

## Quality Checklist

- [ ] Decision is one clear sentence
- [ ] At least 2 alternatives evaluated
- [ ] "Closes Off" section is honest and specific
- [ ] Constraints vs. assumptions clearly distinguished
- [ ] Open Threads captured for follow-up
- [ ] Linked to source artifact (Question Log, Intent Brief, or meeting)
- [ ] No banned language
