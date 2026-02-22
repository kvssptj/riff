---
name: product-discovery
description: JTBD interview guides, interview synthesis, opportunity solution trees, and assumption testing. Use when running customer discovery, synthesizing research transcripts, or mapping opportunities before writing a feature brief.
user-invocable: true
---

Run product discovery work using Jobs-to-be-Done methodology. Produces structured output that feeds Intent Briefs (sections 2 and 3) and Question Logs.

## Modes

### Mode Detection

Check the start of the user's message for a `[bracket]` prefix. Valid modes: `[interview]`, `[synthesize]`, `[opportunity-tree]`, `[assumption-test]`. Everything after the prefix is the task description or input.

### Default Behavior

When no mode prefix is given, infer:
- Input looks like interview notes or transcripts → `[synthesize]`
- Request for interview help, questions, or a guide → `[interview]`
- Request to map opportunities or build/update a tree → `[opportunity-tree]`
- Request to identify or test assumptions → `[assumption-test]`

---

### `[interview]` — Generate a JTBD Interview Guide

Produce a structured interview guide for a given problem area or persona.

**Required input:** Problem area, persona, or feature hypothesis being tested.

**Output:** A complete interview guide with opening, JTBD question sequences, probing prompts, and a note-taking template.

**Key behavior:**
- Start from the struggle, not the solution. Never ask "Would you use X?"
- Build a timeline reconstruction sequence — get the customer to retell the story chronologically
- Surface the four JTBD forces: push (frustration with current), pull (attraction to new), anxiety (fear of switching), habit (inertia of current)
- Include a closing section to capture verbatim, quote-worthy language

---

#### JTBD Interview Structure

**Opening (5 min) — Establish context, not solution**

"Walk me through the last time you [struggled with this problem]. Start from the beginning."

Never ask: "What do you think of [feature]?" or "Would you use X?"

**Timeline Reconstruction (10–15 min)**

- "When did you first realize you needed to do something about this?"
- "What were you doing when that came up?"
- "What did you try first?"
- "What made you decide to keep looking?"
- "When did you find [current solution]? What made you try it?"

**Current State Mapping (10 min)**

- "Walk me through exactly what you do today to handle this."
- "What parts of that process frustrate you?"
- "What would you lose if that disappeared tomorrow?"
- "What have you tried that didn't work? Why did you stop?"

**Struggle and Emotion (10 min)**

- "Tell me about a time this went badly. What happened?"
- "What's the cost when it goes wrong — time, money, stress?"
- "Who else is affected when this breaks?"
- "What do you wish you could do that you can't?"

**Progress and Outcome (5 min)**

- "When this works well, what does that look like?"
- "How would you know if you had actually solved this?"
- "What would you tell a colleague who has the same problem?"

**Closing**

- Capture verbatim quotes that express frustration or emotion
- Note persona role, company size, and context
- Record: what triggered the session, current solution, and how they'd define "good enough"

---

#### Note-Taking Template

```
# Interview: [Name] — [Role] — [Company size] — [Date]

## Context
- Role:
- Company size / segment:
- Current solution:
- Session triggered by:

## Timeline Reconstruction
[What triggered them? When did they first act?]

## Struggle Moments
[High-emotion quotes and friction points]

## Current Workarounds
[What they do today and what it costs them]

## Desired Outcome
[How they'd define success — in their words]

## Verbatim Quotes
> "[Quote 1]"
> "[Quote 2]"

## Patterns / Hypotheses
[What this suggests about the underlying job]
```

---

### `[synthesize]` — Synthesize Interviews into JTBD Themes

Parse multiple interview notes and produce structured insights: jobs, struggle patterns, segment differences, verbatim evidence, and a ranked opportunity list.

**Required input:** Interview notes (paste one or more; label by interviewee or date if multiple).

**Output:** Synthesis document with named jobs, patterns, segment differences, verbatim evidence, and a prioritized opportunity list.

**Key behavior:**
- Name each job in the format: "When [situation], I want to [motivation], so I can [outcome]"
- Surface struggle patterns only when they appear in 2+ interviews — single-respondent signals go in "Weak Signals"
- Separate findings by segment when input includes multiple personas
- Rank the opportunity list by: frequency × severity × (5 − current satisfaction score)
- End with open questions that warrant more research — feed these to `/question-log`

---

#### Synthesis Output Format

```
## Synthesis: [Feature area or problem space] — [Date range]

### Cohort
- [N] interviews, [segments represented]
- Date range: [start] to [end]

---

### Jobs Identified

**Job 1: [Job name]**
When: [Trigger situation]
Want to: [Motivation]
So I can: [Desired outcome]
Current approach: [What they do today]
Struggle: [Where it breaks down]
Evidence: [N/N interviewees] — [representative quote]

**Job 2: ...**

---

### Struggle Patterns

| Pattern | Frequency | Severity (1–5) | Current satisfaction (1–5) | Opportunity score |
|---------|-----------|----------------|---------------------------|-------------------|
| [Pattern] | [N/N] | [Score] | [Score] | [Freq × Sev × (5−Sat)] |

---

### Segment Differences
[Meaningful differences in job or struggle by persona, company size, or context]

---

### Verbatim Evidence
[3–5 quotes per major job — customer language, not paraphrased]

---

### Weak Signals
[Patterns mentioned by only 1 interviewee — worth tracking, not yet actionable]

---

### Open Questions
[What this research doesn't answer — feed these to `/question-log`]
```

---

### `[opportunity-tree]` — Build or Update an Opportunity Solution Tree

Structure research findings into a tree that maps from business outcome → customer opportunity → solution idea.

**Required input:** A business outcome (OKR or metric goal) + synthesis output or opportunity list.

**Output:** A structured opportunity solution tree ready to guide prioritization.

**Key behavior:**
- The root must be a measurable business outcome, not a feature ("Increase 30-day activation from 40% to 55%", not "Improve onboarding")
- Opportunities are customer problems, not solutions — "Customers can't find X" not "Add a search bar"
- Solution ideas attach to opportunities, not to the root
- Each opportunity gets: interview count, severity, and connection to the root outcome
- Flag orphaned ideas (solution ideas with no opportunity parent)

---

#### Opportunity Tree Format

```
## Opportunity Solution Tree

**Business Outcome:** [Measurable goal — metric + target + timeframe]

---

**Opportunity 1:** [Customer problem statement]
Evidence: [N interviews], severity [1–5], current satisfaction [1–5]
Reach: [Estimated % of affected users]
Solution ideas:
  - [Idea A]
  - [Idea B]
  - [Idea C]

**Opportunity 2:** [Customer problem statement]
Evidence: ...
Solution ideas:
  - ...

---

**Assumption Check**
[What must be true for the top-priority opportunity to be real?]
```

---

### `[assumption-test]` — Map Key Assumptions to Tests

Surface assumptions embedded in a feature idea or opportunity, and map each to the cheapest test that could disprove it.

**Required input:** Feature idea, opportunity statement, or Intent Brief section 5 (Solution Intent).

**Output:** Assumption map with test methods, cost, and blocker status.

**Key behavior:**
- Separate desirability assumptions (do customers want it?), feasibility assumptions (can it be built?), and viability assumptions (does it make business sense?)
- Name each assumption as a falsifiable statement: "Customers will pay $X more" not "Pricing is good"
- For each assumption: assign risk (High / Med / Low), suggest the cheapest test, flag blockers
- Cheapest test wins — a 5-customer conversation beats a 3-month build for desirability questions
- Flag blockers explicitly: must resolve before build starts

---

#### Assumption Map Format

```
## Assumption Map: [Feature or opportunity name]

| Assumption | Type | Risk | Test | Cost | Blocker? |
|------------|------|------|------|------|----------|
| [Customers will pay $X more for this] | Viability | High | 5 pricing conversations | Low | Yes |
| [Users discover the feature without prompting] | Desirability | Med | Unmoderated prototype test | Med | No |
| [Integration with [system] is feasible] | Feasibility | High | Eng spike (2 days) | Low | Yes |

**Blockers (must resolve before building):**
[List blocker assumptions]

**Safe to test in parallel:**
[List non-blocker assumptions]
```

---

## Artifact Relationships

| Artifact | Relationship |
|----------|-------------|
| **Intent Brief section 2 (Context)** | Synthesis output provides the research-grounded "why now" |
| **Intent Brief section 3 (Goals)** | Jobs and desired outcomes inform measurable goal targets |
| **Intent Brief section 4 (Scope)** | Opportunity tree informs what's in scope and what's explicitly deferred |
| **Question Log** | Open questions from synthesis → `/question-log` |
| **Decision Memo** | Assumption tests that confirm or kill a hypothesis → `/decision-memo [capture]` |
| **Scorecard section 7** | Research-identified risks feed Scorecard risks and open issues |

## Anti-Patterns

❌ **Asking customers what they want**
→ Ask about struggles and past behavior, not desired features. "Tell me about the last time X happened" beats "Would you use Y?"

❌ **Drawing conclusions from one interview**
→ A single vivid story is a hypothesis. A pattern needs at least 2 corroborating interviews. Surface single signals in Weak Signals.

❌ **Confusing job with solution**
→ "I want a better dashboard" is not a job. "When my team misses a deadline, I want to catch it early so I can course-correct before it escalates" is a job.

❌ **Opportunity trees rooted in features**
→ The root is a business outcome. Features are leaves. Never let a feature or a solution be the root.

❌ **Skipping assumption mapping before building**
→ Every feature has 3–5 embedded assumptions. The ones you don't name are the ones that kill the launch.

## Naming Convention

- Interview notes: `research/interviews/[YYYY-MM-DD]_[persona-or-name].md`
- Synthesis: `research/synthesis/[YYYY-MM-DD]_[feature-area]-synthesis.md`
- Opportunity tree: `research/opportunity-tree_[feature-area].md`

## Quality Checklist

- [ ] Jobs named in "When / Want to / So I can" format
- [ ] Struggle patterns backed by 2+ interviews
- [ ] Opportunity tree rooted in a measurable business outcome (metric + target + timeframe)
- [ ] Opportunities are customer problems, not solutions
- [ ] Assumption map separates desirability, feasibility, and viability
- [ ] Blockers identified and distinguished from parallel tests
- [ ] Open questions labeled for `/question-log`
- [ ] No banned language
