---
name: backlog-groomer
description: Prioritize and groom product backlogs using RICE, ICE, Kano, and Opportunity Scoring frameworks. Evaluates items against GA scope, identifies dependencies, and produces sprint-ready prioritized backlogs. Use when you have a list of features, requests, or stories to prioritize.
user-invocable: true
---

Prioritize the provided backlog items. Apply a scoring framework, identify dependencies, and produce a clean sprint-ready backlog.

## Prioritization Frameworks

### RICE (Default)

| Factor | Definition | Scale |
|--------|-----------|-------|
| **Reach** | How many users/accounts affected per quarter | Actual number estimate |
| **Impact** | Effect on individual user when they encounter it | 3 = massive, 2 = high, 1 = medium, 0.5 = low, 0.25 = minimal |
| **Confidence** | How sure you are about reach and impact estimates | 100% = high, 80% = medium, 50% = low |
| **Effort** | Person-months of engineering + design work | Actual estimate |

**RICE Score = (Reach × Impact × Confidence) / Effort**

### ICE (Quick Scoring)

**ICE Score = Impact × Confidence × Ease** (each 1-10)

### Kano (Feature Classification)

- **Must-Have:** Expected. Absence causes dissatisfaction.
- **Performance:** More is better. Linear satisfaction.
- **Delighter:** Unexpected. Presence creates delight.
- **Indifferent:** Users don't care either way.

### Opportunity Scoring

**Opportunity = Importance + max(Importance − Satisfaction, 0)** (each 1-10)

## Grooming Process

1. **Inventory** — List all items. Flag duplicates, items missing info, items to merge.
2. **Classify** — Map to feature area/epic. Tag Kano category. Mark GA scope alignment (in-scope / stretch / post-GA).
3. **Score** — Apply RICE or ICE. Show reasoning for each score. Note confidence level.
4. **Dependencies** — Identify blocking relationships. Flag external dependencies.
5. **Sprint Allocation** — Group into sprints by score + dependencies + capacity. Leave ~20% buffer for bugs.

## Output Format

### Prioritized Backlog Table

| Rank | Item | RICE Score | Priority | Sprint | Dependencies | Notes |
|------|------|-----------|----------|--------|-------------|-------|
| 1 | [Item] | [Score] | P0 | Sprint N | [Deps] | [Notes] |

### Scoring Detail (top items)

For each top-10 item:
- **Reach:** [Estimate] — [Reasoning]
- **Impact:** [Score] — [Reasoning]
- **Confidence:** [%] — [What you're sure about, what you're not]
- **Effort:** [Estimate] — [Reasoning]
- **RICE Score:** [Calculation]

### Recommendations

- **Do now (this sprint):** [Items]
- **Do next (next sprint):** [Items]
- **Defer:** [Items + why]
- **Cut:** [Items + why]

## Project Context

Align grooming to your project's release constraints:

- **Release milestone:** Identify your GA or release date. Flag items that threaten it.
- **Scope alignment:** Mark items as in-scope / stretch / post-release relative to your confirmed scope.
- **Domain constructs:** Map items to your product's feature areas (defined in your `@domain_pm` context). Use the same taxonomy your team uses.
- **Dependencies:** Reference your actual platform and integration dependencies. Note what's internal vs. external.

## Artifact Integration

### Pulling from Intent Briefs
- **Section 7 (User Stories)** is your primary input when grooming an Intent Brief's backlog
- **Section 6 (Requirements)** provides the P0/P1/P2 classification — respect it as a starting point, but re-score if evidence warrants
- **Section 8 (Dependencies)** tells you about blocking relationships to factor into sprint allocation

### Feeding Scorecards
- Your prioritized backlog output feeds into Scorecard section 3 (Scope Progress)
- When you recommend cutting or deferring items, note the impact on the Scorecard's scope tracking
- Flag items that affect GA scope — these should trigger a Scorecard health rating update

### Referencing Decision Memos
- If a backlog item depends on an unresolved decision, flag it as blocked and reference the relevant Question Log entry
- If a past Decision Memo affects priority (e.g., a "Closes Off" that removes an option), factor it into scoring

### Artifact-Aware Recommendations
In addition to the standard Do Now / Do Next / Defer / Cut recommendations, add:
- **Decisions Needed:** Items that can't be scored until a decision is made (link to Question Log)
- **Scorecard Impact:** How the prioritized backlog changes the feature's health rating

## Quality Standards

- Every score has visible reasoning — not just a number
- Dependencies are explicit, not implied
- Recommendations are opinionated ("Do this, not that") with rationale
- Show trade-offs: "If we do X, we can't do Y this sprint"
- Distinguish between facts, estimates, and assumptions
- Plain language, no buzzwords
