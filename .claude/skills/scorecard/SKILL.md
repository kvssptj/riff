---
name: scorecard
description: Create, update, or snapshot feature health scorecards. Living tracker that pulls from Intent Briefs, Decision Memos, and Question Logs. Differentiates from stakeholder-summarizer — scorecards are living documents updated on cadence, not one-off comms. Use when you need to track feature health over time.
user-invocable: true
---

Create or update a feature Scorecard using the template at `Docs/PRDdocs/scorecard_template.md`. Scorecards are living documents — they get updated, not replaced.

## Modes

### Mode Detection

Check the start of the user's message for a `[bracket]` prefix. Valid modes: `[create]`, `[update]`, `[snapshot]`. Everything after the prefix is the task description.

### Default Behavior

When no mode prefix is given, behave as **`[create]`** — produce a new scorecard.

### `[create]` — New Scorecard

Build a scorecard for a feature from scratch.

**Required input:** Feature name and current context (Intent Brief, recent status, or PM description).

**Output:** Complete 8-section scorecard. All sections populated. Health ratings with justification.

**Key behavior:**
- Set initial health ratings based on available information
- Pull scope items from the Intent Brief's section 6 (Requirements) if available
- Populate Decision Tracker from any existing Decision Memos
- Pull open questions from the Question Log if one exists
- Set a review cadence recommendation (weekly for pre-GA, biweekly for stable features)

### `[update]` — Update Existing Scorecard

Update a scorecard with new information.

**Required input:** Current scorecard content + what changed (status update, new decisions, resolved questions, scope changes).

**Output:** Updated scorecard with changes highlighted. Include a "Changes This Update" callout at the top.

**Key behavior:**
- Update health ratings and explain any rating changes
- Move completed items in scope progress
- Add new decisions to the Decision Tracker
- Update risk status — resolve mitigated risks, add new ones
- Move resolved questions out of section 7
- Add items to "Next Update Actions" (section 8)
- Increment the version number and update "Last Updated" date

### `[snapshot]` — Point-in-Time Summary

Export the current scorecard state as a shareable summary. This is where Scorecard and stakeholder-summarizer overlap — use `[snapshot]` when you want a summary derived from the living scorecard data.

**Output:** 1-page summary with: Health rating, PM assessment, scope % complete, top 3 risks, top 3 open questions, next actions.

**Key behavior:**
- This is a read-only export — it doesn't modify the scorecard
- Format for sharing (clean headers, no internal tracking fields)
- Include the "as of [date]" timestamp

## Relationship to Stakeholder Summarizer

| | Scorecard | Stakeholder Summarizer |
|---|-----------|----------------------|
| **Type** | Living document, updated on cadence | One-off communication |
| **Audience** | PM + team (internal tracking) | Leadership, partners, stakeholders |
| **Updates** | Incremental (add/modify sections) | Fresh each time |
| **Scope** | Single feature, deep | Can span multiple features |
| **Use when** | Tracking health over time | Briefing someone who doesn't track daily |

**Rule of thumb:** If you need to *track* something, use a Scorecard. If you need to *tell* someone something, use the stakeholder-summarizer.

## Pulling from Other Artifacts

| Scorecard Section | Source Artifact | What to Pull |
|-------------------|----------------|-------------|
| 3. Scope Progress | Intent Brief section 6-7 | Requirements and stories |
| 4. Decision Tracker | Decision Memos | Decision + date + impact |
| 5. Risks & Blockers | Intent Brief section 8, Question Log | Dependencies, unresolved high-priority questions |
| 6. Key Metrics | Intent Brief section 3 | Goal metrics and targets |
| 7. Open Questions | Question Log | Top unresolved questions by priority |

## Project Context

Align the scorecard to your project's release milestone:

- **Release date:** Flag anything that threatens your GA or release date in section 5 (Risks).
- **Scope model:** Map scope items in section 3 to your domain's feature areas and coverage model (defined in `@domain_pm`).
- **Dependencies:** Reference your actual platform, infrastructure, and integration dependencies in risks.

## Naming Convention

Save as: `SC_[feature-name].md` (living document, one per feature)

Example: `SC_notification-center.md`

## Quality Checklist

- [ ] Health ratings have justification (not just a color)
- [ ] Scope progress uses real numbers, not estimates
- [ ] Decision Tracker links to Decision Memos
- [ ] Risks have owners and mitigation plans
- [ ] Open Questions reference Question Log entries
- [ ] PM Assessment is honest — flags real concerns
- [ ] No banned language
