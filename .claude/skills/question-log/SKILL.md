---
name: question-log
description: Create or update a Question Log from transcripts, reviews, or ad-hoc questions. Tracks questions from Open through Resolution to Decision Memo. Can consume meeting transcripts as input. Use when you need to track open questions across meetings, reviews, or async discussions.
user-invocable: true
---

Create or update a Question Log using the template at `Docs/PRDdocs/question_log_template.md`. Question Logs are living documents — they track questions from raised to resolved.

## Modes

### Mode Detection

Check the start of the user's message for a `[bracket]` prefix. Valid modes: `[create]`, `[update]`, `[from-transcript]`. Everything after the prefix is the task description.

### Default Behavior

When no mode prefix is given, infer the mode:
- If the input looks like a transcript (speaker names, timestamps, dialogue) → behave as `[from-transcript]`
- If the input references an existing Question Log → behave as `[update]`
- Otherwise → behave as `[create]`

### `[create]` — New Question Log

Build a Question Log for a feature area from scratch.

**Required input:** Feature area and questions (from PRD review, design review, planning session, or PM's list).

**Output:** Complete Question Log with priority summary, questions grouped by feature area, all statuses set to "Open."

**Key behavior:**
- Group questions by feature area or component
- Assign sequential IDs (Q-001, Q-002, ...)
- Set priority based on: High = blocks development, Med = affects scope or design, Low = nice to clarify
- Set source based on how the question arose

### `[update]` — Update Existing Log

Add new questions or resolve existing ones.

**Required input:** Current Question Log content + updates (new questions, resolutions, status changes).

**Output:** Updated Question Log. New questions get the next sequential ID. Resolved questions get Resolution column filled.

**Key behavior:**
- Don't re-number existing questions — IDs are stable
- When resolving a question, fill the Resolution column
- If a resolution is a significant decision, note "→ Decision Memo" in the Status column and prompt the PM to create one using `/decision-memo`
- Update the priority summary table
- Keep resolved questions in the log (don't delete them — they're the record)

### `[from-transcript]` — Extract from Transcript

Parse a meeting transcript and extract all open questions, decisions, and action items into Question Log format.

**Required input:** Meeting transcript (with or without speaker labels/timestamps).

**Output:** Question Log entries extracted from the transcript. Include the meeting date/name as the Source for all entries.

**Key behavior:**
- Extract questions that were explicitly asked AND implied questions (e.g., "We need to figure out how to handle X" → question about handling X)
- Mark questions that were answered in the meeting as "Resolved" with the answer in the Resolution column
- Mark questions left open as "Open"
- If a decision was made in the meeting, mark as "Resolved" and note "Consider `/decision-memo` for formal documentation" in the Resolution column
- Group by feature area discussed in the transcript
- Assign priorities based on urgency expressed in the discussion

## Relationship to /extract-transcript

`/extract-transcript` is a quick extraction tool — it pulls questions from a transcript and outputs a flat list grouped by feature area.

`/question-log [from-transcript]` does the same extraction but produces a living Question Log artifact with:
- Sequential IDs for tracking
- Status tracking (Open → Resolved)
- Links to Decision Memos
- Priority summary
- Can be updated with future transcripts

**Rule of thumb:** Use `/extract-transcript` for a quick one-time summary. Use `/question-log [from-transcript]` when you want to track those questions over time.

## Question Lifecycle

```
Open → In Discussion → Resolved
                          ↓
                    (if significant)
                          ↓
                    → Decision Memo
```

When a question is resolved:
1. Fill the Resolution column
2. If the decision is significant (affects scope, architecture, or timeline), create a Decision Memo with `/decision-memo [capture]`
3. If the resolution changes scope, flag that the Intent Brief needs updating

## Linking to Other Artifacts

- **To Decision Memo:** When a question resolves into a significant decision, link the Decision Memo in the Resolution column
- **To Intent Brief:** Open questions feed into Intent Brief section 9. Resolved questions may affect sections 3-5.
- **To Scorecard:** Top open questions appear in Scorecard section 7

## Grouping Convention

Group questions by your product's feature areas or workstreams. Use the same taxonomy your team uses in tickets, docs, and sprint planning — whatever makes it easiest for your team to triage by area.

Flag questions that affect your release milestone (e.g., GA date, sprint commitment) — these should be prioritized High and resolved before the cutoff.

## Naming Convention

Save as: `QL_[feature-area].md` (living document, one per feature area or meeting series)

Example: `QL_notification-center.md`, `QL_sprint-planning.md`

## Quality Checklist

- [ ] Every question has a sequential ID
- [ ] Questions are grouped by feature area
- [ ] Priorities assigned: High (blocks dev), Med (affects scope), Low (nice to know)
- [ ] Source is specific (meeting name + date, review name, person)
- [ ] Resolved questions have Resolution column filled
- [ ] Significant decisions flagged for Decision Memo creation
- [ ] Priority summary table is accurate
- [ ] No banned language
