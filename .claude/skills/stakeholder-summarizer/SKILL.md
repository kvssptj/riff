---
name: stakeholder-summarizer
description: Create executive summaries, stakeholder updates, status reports, and leadership communications. Follows Problem-Solution-Metrics structure. 1-2 pages max, plain language, no buzzwords. Use when you need to brief leadership, write a sprint update, pitch an investment, or align partner teams.
user-invocable: true
---

Write a stakeholder communication from the provided context. Match the document type to the audience and purpose.

## Document Types

### 1. Executive Summary (1-pager)
For leadership or cross-functional stakeholders who need the big picture.

```
# [Feature/Project Name] — Executive Summary

**Date:** [Date]
**Author:** [Name]
**Status:** On Track / At Risk / Blocked

## What
[2-3 sentences: What we're building and who it's for]

## Why
[2-3 sentences: The problem and business case. Reference data.]

## Progress
[Bullet list of what's been done, what's in progress, what's next]

## Key Decisions Needed
[Specific asks — what you need from this audience]

## Risks
[Top 1-3 risks with mitigation plans]

## Timeline
[Key milestones with dates]
```

### 2. Sprint/Status Update
For teams and managers tracking week-to-week progress.

```
# [Team/Feature] — Status Update [Date]

## Summary
[1-2 sentences: Where we are vs. where we expected to be]

## Completed This Sprint
- [Item]: [Brief description]

## In Progress
- [Item]: [Current status and expected completion]

## Blocked
- [Item]: [What's blocking and who can unblock]

## Next Sprint
- [Planned work items]

## Metrics
[Key metrics movement if available]
```

### 3. Investment Pitch (Decision Brief)
For getting buy-in on a new initiative or resource allocation.

```
# [Proposal Name] — Decision Brief

## The Ask
[1 sentence: What you're requesting]

## The Problem
[2-3 sentences with data: Why this matters now]

## Proposed Solution
[2-3 sentences: What you want to build and how]

## Expected Impact
[Metric targets with sizing model]

## Alternatives Considered
[What else you evaluated and why this approach wins]

## Cost
[Engineering effort, timeline, trade-offs]

## Recommendation
[Your clear recommendation and next steps]
```

### 4. Cross-Functional Brief
For partner teams who need to understand your feature for their own planning.

```
# [Feature Name] — Partner Brief

## What's Changing
[What we're building and when it ships]

## What It Means for Your Team
[Specific impact — integrations, dependencies, timeline]

## What We Need from You
[Specific asks with deadlines]

## Key Dates
[Timeline with milestones relevant to the partner]

## Questions?
[Contact info and meeting invite]
```

## Writing Principles

- **Problem → Solution → Metrics** in every document
- Lead with the most important information
- 1-2 pages max
- Use headers, bullets, and tables — no walls of text
- Write for the audience: executives want impact, engineers want specifics, partners want "what does this mean for me"
- Honest about risks — don't hide bad news
- Reference specific numbers, not vague trends ("grew 12% week-over-week" not "engagement is improving")
- When you don't have data, say so: "We estimate [X] based on [assumption]"

## Never Use

leverage, synergy, streamline, robust, seamless, revolutionary, transformative, game-changing, "Excited to share...", "I'm pleased to report...", "Let's dive in..."

## Relationship to Scorecard

| | Stakeholder Summarizer | Scorecard |
|---|----------------------|-----------|
| **Type** | One-off communication | Living document, updated on cadence |
| **Audience** | Leadership, partners, stakeholders | PM + team (internal tracking) |
| **Created** | Fresh each time from current context | Incrementally updated |
| **Scope** | Can span multiple features | Single feature, deep |
| **Use when** | Briefing someone who doesn't track daily | Tracking feature health over time |

**When to use which:**
- Need to *tell* someone something → `/stakeholder-summarizer`
- Need to *track* something over time → `/scorecard`
- Need a point-in-time export from a Scorecard → `/scorecard [snapshot]`

**Pulling from Scorecards:**
When a Scorecard exists for the feature you're summarizing, use it as input. The Scorecard's health ratings, scope progress, and risk sections give you pre-analyzed data. Don't re-derive what the Scorecard already tracks.

## Quality Standards

- Every document has a clear "ask" or "so what"
- Risks are specific, not vague
- Progress is measurable — shipped items, completion percentages, metric movements
- No filler: if removing a sentence loses nothing, remove it
- Reader knows exactly what to do after reading this
