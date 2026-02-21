# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with this repository.

## Repository Overview

This is an **Agentic PM Framework** — a reusable product management system built for Claude Code. It provides a team of specialized AI agents and skills that help PMs produce better artifacts faster: Intent Briefs, Decision Memos, Question Logs, Scorecards, and User Stories.

**Primary Purpose:** Documentation and product management artifacts, not production code.

**To use this framework for your project:** Customize `@domain_pm` with your product's domain knowledge, then invoke agents and skills as described below.

## Agent Architecture

The system is organized around **5 PM artifacts**. Agents and skills map to artifact types — each produces or consumes one or more artifacts.

- **`@builder`** is the PM team lead. It handles strategy directly and spawns `@intent_writer`, `@design_image_analyzer`, and `@domain_pm` as teammates for focused deliverables.
- **`@domain_pm`** is the domain specialist. Customize it with your product's context. Use it for any domain-specific PM work.
- **`@intent_writer`** and **`@design_image_analyzer`** are specialists that can be invoked directly or spawned by `@builder`.
- **Skills** (`/user-story-writer`, `/backlog-groomer`, `/stakeholder-summarizer`, `/extract-transcript`, `/decision-memo`, `/question-log`, `/scorecard`) run inline — no subprocess needed.

## 5 PM Artifacts

All PM work produces one of 5 artifact types. Map your task to the right artifact first.

| Artifact | What It Is | Created By | Template |
|----------|-----------|------------|----------|
| **Decision Memo** | Atomic unit. One decision + reasoning. | `/decision-memo` | `decision_memo_template.md` |
| **Intent Brief** | PM writes intent (1-5), agent generates spec (6-9). Replaces PRD. | `@intent_writer` | `intent_brief_template.md` |
| **Context File** | Living domain background for agents. Not templated. | Manual / `@domain_pm` | N/A |
| **Question Log** | Tracks open questions through resolution. Replaces meeting notes. | `/question-log` | `question_log_template.md` |
| **Scorecard** | Living feature health tracker. Replaces periodic status updates. | `/scorecard` | `scorecard_template.md` |

**How artifacts connect:**
- Question Log questions → resolve into Decision Memos
- Decision Memos → referenced in Intent Brief section 5 (Key Decisions Made)
- Intent Brief scope → tracked in Scorecard section 3 (Scope Progress)
- Scorecard open questions → pulled from Question Log

**Naming conventions:**
- Decision Memos: `DM_[YYYY-MM-DD]_[short-description].md`
- Intent Briefs: `IB_[feature-name].md`
- Question Logs: `QL_[feature-area].md`
- Scorecards: `SC_[feature-name].md`

## Agents

### Team Lead

**`@builder`** (`.claude/agents/builder.md`)
- **Role:** PM team lead + strategist
- **Model:** Claude Opus
- **Handles directly:** Product strategy, competitive analysis, build-vs-buy decisions, metrics definition, roadmap planning, go-to-market strategy
- **Spawns teammates for:** Intent Briefs (`@intent_writer`), design analysis (`@design_image_analyzer`), domain-specific work (`@domain_pm`)

### Domain Agent

**`@domain_pm`** (`.claude/agents/domain_pm.md`)
- **Role:** Domain specialist — customize with your product's context
- **Model:** Claude Opus
- **Use for:** Any domain-specific PM work — Intent Briefs, stories, grooming, transcripts, design analysis
- **How to customize:** Edit the "Domain Expertise" section in `domain_pm.md` with your product's feature areas, constructs, and key docs

### Specialist Agents

| Agent | File | Use When |
|-------|------|----------|
| **`@design_image_analyzer`** | `.claude/agents/design_image_analyzer.md` | Analyzing Figma mockups, wireframes, or screenshots for design gaps. Output is `/question-log` compatible. |
| **`@intent_writer`** | `.claude/agents/intent_writer.md` | Writing Intent Briefs. Modes: `[intent]` (sections 1-5), `[spec]` (sections 6-9), `[full]`, `[review]`, `[exec]` |

## Skills

Invoke with `/skill-name`. Runs inline — no subprocess.

| Skill | Artifact | Use When |
|-------|----------|----------|
| `/decision-memo` | Decision Memo | Capturing, evaluating, or retroactively documenting a product decision |
| `/question-log` | Question Log | Tracking open questions from transcripts, reviews, or discussions |
| `/scorecard` | Scorecard | Creating or updating a feature health tracker |
| `/user-story-writer` | (feeds Intent Brief section 7) | Writing user stories with acceptance criteria and priority levels |
| `/backlog-groomer` | (feeds Scorecard section 3) | Prioritizing features using RICE/ICE/Kano frameworks |
| `/stakeholder-summarizer` | (one-off comms, not Scorecard) | Executive summaries, status updates, leadership briefs |
| `/extract-transcript` | (quick extraction) | Quick one-time question extraction from meeting transcripts |

## Routing Guide

| Task | Artifact | Use |
|------|----------|-----|
| "Plan feature X" | Intent Brief | `@intent_writer` (or `@domain_pm` for domain-specific features) |
| "We decided to do X" | Decision Memo | `/decision-memo [capture]` |
| "Should we do X or Y?" | Decision Memo | `/decision-memo [evaluate]` |
| "Track questions from this meeting" | Question Log | `/question-log [from-transcript]` |
| "Quick summary of this transcript" | — | `/extract-transcript` skill |
| "How is feature X doing?" | Scorecard | `/scorecard [create]` or `/scorecard [update]` |
| "Analyze this mockup" | (feeds Question Log) | `@design_image_analyzer` |
| "Domain-specific anything" | — | `@domain_pm` |
| "Write user stories for feature X" | (feeds Intent Brief) | `/user-story-writer` skill |
| "Prioritize these 10 features" | (feeds Scorecard) | `/backlog-groomer` skill |
| "Write a stakeholder update" | — | `/stakeholder-summarizer` skill |
| "Should we build or buy X?" | — | `@builder` (handles directly) |
| "Define success metrics for X" | — | `@builder` (handles directly) |
| "Multi-step: transcript → questions → decisions" | Multiple | `@builder` (chains artifacts in sequence) |

## Using Agents

**Agent invocation** — invoke agents directly:
```
@builder [your task/question]
@domain_pm [your task/question]
@intent_writer [your task/question]
@design_image_analyzer [your task/question]
```

**Skill invocation** — use slash commands inline:
```
/decision-memo [capture/evaluate/retro] [context]
/question-log [create/update/from-transcript] [input]
/scorecard [create/update/snapshot] [feature context]
/user-story-writer [paste requirements or Intent Brief]
/backlog-groomer [paste list of items]
/stakeholder-summarizer [paste context]
/extract-transcript [paste transcript]
```

**Multi-step work** — use `@builder` and it will chain agents and skills:
```
@builder Extract questions from this transcript, create a Question Log, and write Decision Memos for what was decided.
@builder Write an Intent Brief for the notification system, then create a Scorecard.
```

## Templates

All templates are in `Docs/PRDdocs/`:

| Template | File | Used By |
|----------|------|---------|
| **Intent Brief** | `intent_brief_template.md` | `@intent_writer` — 9-section template with PM Intent (1-5) / Agent Spec (6-9) split |
| **Decision Memo** | `decision_memo_template.md` | `/decision-memo` — 7-section template for atomic decisions |
| **Question Log** | `question_log_template.md` | `/question-log` — Question tracking with priority summary and feature grouping |
| **Scorecard** | `scorecard_template.md` | `/scorecard` — Health rating, scope progress, decision tracker, risks, metrics |
| **Legacy PRD** | `prd_template.md` | Preserved as reference. New features use Intent Brief instead. |

**Examples** (fictional Acme Corp / Notification Center):
- `Docs/PRDdocs/examples/EXAMPLE_intent_brief.md`
- `Docs/PRDdocs/examples/EXAMPLE_decision_memo.md`
- `Docs/PRDdocs/examples/EXAMPLE_context_file.md`
- `Docs/PRDdocs/examples/EXAMPLE_question_log.md`
- `Docs/PRDdocs/examples/EXAMPLE_scorecard.md`

## Writing Standards

### PM Documentation Template

All product documents follow this structure:

1. **Executive Summary** – 3-4 sentences explaining what the feature does and why it matters
2. **Problem Statement** – Current State, Business Impact, Desired Future State
3. **Target Personas / Audience** – 2-3 primary user types with goals and pain points
4. **Solution Framework / User Journey** – How the feature fits into user flow
5. **Detailed Use Cases or Stages** – Job-to-be-done, description, user value, key features
6. **Success Metrics** – 2-4 Primary KPIs, optional secondary metrics
7. **Dependencies / Open Questions** – Honest, specific callouts

**Section Numbering:** Use consistent numbering (1., 1.1, etc.) for traceability.

### Writing Tone and Style

**Do:**
- Use plain, simple language and short sentences
- Be direct and conversational
- Write like you speak (starting with "and" or "but" is fine)
- Use simple verbs: "shows," "fetches," "routes," "learns"
- Keep paragraphs ≤3 sentences

**Never use these phrases:**
- "let's dive in," "game-changing," "unleash potential"
- "leverage," "synergy," "streamline," "robust," "seamless"
- "revolutionary," "transformative"
- Marketing buzzwords or hype language

**Quality checklist:**
- ✅ Clear narrative from problem → solution → metrics
- ✅ Every claim grounded in user pain or data
- ✅ Consistent voice and terminology
- ✅ No speculative adjectives
- ✅ Critical Questions listed for open decisions

### Anti-Shallow Rules (Always Enforce)

1. **Ground every claim** – Reference specific docs, capabilities, or confirmed scope
2. **Require specificity** – At least one concrete example per section
3. **Mandate Critical Questions** – Each major section ends with Critical Questions or "No open questions"
4. **Map to product constructs** – Reference your domain's feature areas and coverage model
5. **Ban generic PM language** – Never use banned buzzwords
6. **Depth over breadth** – Prefer one well-developed use case over three shallow ones
7. **Traceability** – Consistent numbering, dependencies name teams/docs/features, version and date in header

## Common PM Tasks

**Planning a Feature (Intent Brief):**
1. Use `@intent_writer` (or `@domain_pm` for domain-specific features)
2. Default mode: `[intent]` — writes PM Intent (sections 1-5)
3. Then `[spec]` to generate Agent Spec (sections 6-9) from sections 1-5
4. Template: `Docs/PRDdocs/intent_brief_template.md`

**Documenting a Decision (Decision Memo):**
1. Use `/decision-memo` skill
2. Modes: `[capture]` (decision made), `[evaluate]` (weighing options), `[retro]` (documenting past decision)
3. Template: `Docs/PRDdocs/decision_memo_template.md`
4. Link in Intent Brief section 5 and Question Log resolution column

**Tracking Questions (Question Log):**
1. Use `/question-log` skill
2. From transcript: `/question-log [from-transcript]` — extracts and tracks questions
3. Quick extraction only: `/extract-transcript` — one-time summary, no tracking
4. Template: `Docs/PRDdocs/question_log_template.md`

**Tracking Feature Health (Scorecard):**
1. Use `/scorecard` skill
2. `[create]` for new features, `[update]` for existing, `[snapshot]` for shareable summary
3. Pulls from Intent Brief (scope), Decision Memos (decisions), Question Log (open questions)
4. Template: `Docs/PRDdocs/scorecard_template.md`

**Writing User Stories:**
1. Use `/user-story-writer` skill (or `@domain_pm` for domain-specific stories)
2. Reads from Intent Brief sections 6-7 when available
3. Format: "As a [persona], I want [goal] so that [value]"
4. Include acceptance criteria, priority (P0/P1/P2), and size (S/M/L)

**Backlog Grooming:**
1. Use `/backlog-groomer` skill for structured prioritization
2. Pulls from Intent Brief section 7 (stories) and feeds Scorecard section 3 (scope progress)
3. Default framework: RICE scoring with visible reasoning

**Analyzing Design Images:**
1. Use `@design_image_analyzer` agent (or `@domain_pm` for domain designs)
2. Output is `/question-log` compatible — questions can flow into a Question Log

**Stakeholder Communications:**
1. Use `/stakeholder-summarizer` skill for one-off exec summaries, status updates, briefs
2. For living health tracking, use `/scorecard` instead
3. Structure: Problem → Solution → Metrics. 1-2 pages max.

**Multi-Step Artifact Chains:**
1. Use `@builder` to chain artifacts: transcript → Question Log → Decision Memos → Intent Brief → Scorecard
2. Each step produces an artifact that feeds the next

## Important Notes

- **Agent teams:** `@builder` acts as team lead — spawns `@intent_writer`, `@design_image_analyzer`, and `@domain_pm` as teammates.
- **4 agents:** `@builder` (team lead), `@domain_pm` (domain specialist — customize), `@design_image_analyzer` (mockup analysis), `@intent_writer` (Intent Brief writing)
- **5 PM Artifacts:** Decision Memo, Intent Brief, Context File, Question Log, Scorecard. All templates in `Docs/PRDdocs/`.
- **Legacy PRD template** preserved at `prd_template.md` for reference. New features use Intent Brief template.
- **No code execution:** This is a documentation repository.
- **Philosophy:** See `Docs/agentic_pm.md` for the intellectual foundation of this framework.
