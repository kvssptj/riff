---
name: user-story-writer
description: Write user stories with acceptance criteria, priority levels, and size estimates. Maps stories to your product's domain constructs (feature areas, coverage model, implementation tiers). Use when breaking down a PRD, feature brief, or list of requirements into sprint-ready stories.
user-invocable: true
---

Write user stories from the provided requirements, PRD, or feature description. Produce stories that engineering can pick up and build without ambiguity.

## Story Format

```
### [ID] [Story Title]

**Priority:** P0 (must ship) / P1 (should ship) / P2 (stretch)
**Size:** S / M / L
**Persona:** [Who]

**Story:**
As a [specific persona], I want [capability] so that [measurable benefit].

**Acceptance Criteria:**
- [ ] [Criterion 1 — observable, testable]
- [ ] [Criterion 2 — observable, testable]
- [ ] [Criterion 3 — observable, testable]

**Edge Cases:**
- [What happens when boundary condition]
- [What happens when unusual input]

**Dependencies:**
- [Blocked by / blocks]

**Notes:**
- [Implementation hints, design references, or constraints]
```

## Priority Definitions

- **P0 — Must Ship:** Core functionality. Feature is broken or unusable without this. Ships in GA.
- **P1 — Should Ship:** Important but the feature works at a basic level without it. Strong candidate for GA.
- **P2 — Stretch:** Nice to have. Can ship post-GA.

## Size Definitions

- **S (Small):** 1-2 days. Single component or endpoint. Clear implementation path.
- **M (Medium):** 3-5 days. Multiple components or integration points. Some design decisions.
- **L (Large):** 1-2 weeks. Consider breaking down further. Cross-cutting concerns or new patterns.

## Acceptance Criteria Standards

- Written as observable behaviors, not implementation details
- Each criterion is independently testable
- Cover the happy path, at least one error path, and boundary conditions
- Use "Given [context], When [action], Then [result]" format when helpful

## Map to Product Constructs

Stories should map to your product's specific constructs. Before writing stories, identify:

- **Feature areas or domains** — which area of the product does this story belong to?
- **Coverage model** — what states or layers define a complete implementation? (e.g., list view, detail view, empty state, error state, actions, post-action)
- **User personas** — who specifically takes this action? Be precise (e.g., "admin", "end user", "approver").
- **Technical tiers** — if your product has multiple rendering targets or implementation paths, note which tier applies.

Fill in your own domain's constructs in the `@domain_pm` agent and reference them here when writing stories.

## Organization

Group stories by epic or feature area, then priority (P0 first). Stories that unblock others go first.

Include a summary table at the end:

| Priority | Count | Total Size |
|----------|-------|------------|
| P0 | [N] | [S/M/L breakdown] |
| P1 | [N] | [S/M/L breakdown] |
| P2 | [N] | [S/M/L breakdown] |

## Working with Intent Briefs

When the input is an Intent Brief (or sections from one):

### Reading from Intent Briefs
- **Section 6 (Requirements)** is your primary input — each P0/P1/P2 requirement becomes one or more stories
- **Section 7 (User Stories)** may already have draft stories — refine and expand them, don't duplicate
- **Section 3 (Goals)** tells you the "so that [value]" for each story
- **Section 5 (Solution Intent)** provides the user flows that stories should trace through

### Referencing Decision Memos
- If the Intent Brief's section 5 links to Decision Memos, read them for context on design choices
- When a story depends on a decision, note the Decision Memo in the story's Dependencies field
- If a story raises a new question, flag it for the Question Log

### Output Destination
- Stories generated from an Intent Brief should be formatted to slot into section 7 of that brief
- Use the same sequential ID scheme (S-01, S-02, ...) used in the Intent Brief template

## Quality Standards

- No story without acceptance criteria
- Every "so that [benefit]" is specific — never vague
- Stories map to a specific product construct (feature area, domain model, implementation tier)
- Plain language, no buzzwords
