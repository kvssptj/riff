# Riff

In agentic coding, the developer stopped writing every line of code. They became a technical director — describing intent, reviewing output, making judgment calls. The code still gets written. The developer's job fundamentally changed.

The same shift is happening in product management. This framework is a working implementation of what that looks like.

---

## What This Is

Most "AI for PM" is prompt-and-paste. Ask Claude to summarize a transcript. Ask it to draft a PRD. Copy the output, edit it manually, move on. The PM still drives every step.

This is different. It's an architecture for **agentic PM work** — where a team of specialized agents coordinates autonomously to handle the information-dense, consistency-checking, artifact-producing work, while the PM focuses on what only a human can do: judgment, strategy, and the decisions that no framework captures.

The core structural insight: PM work follows the same pattern as agentic coding. A team lead (`@builder`) coordinates specialists (`@intent_writer`, `@domain_pm`, `@design_image_analyzer`), each producing artifacts that feed the next. The PM stays in the loop at decision points — not to produce documents, but to make calls. Agents draft. PMs decide.

---

## The Three Levels of Agentic PM

Most "AI for PM" work today is Level 1. This framework targets Level 2, with infrastructure for Level 3.

**Level 1 — Tool Use** (where most teams are today)

"Summarize this transcript." "Write a PRD draft." "Generate user stories."

This is the equivalent of autocomplete — useful, but not agentic. The PM still drives every step manually.

**Level 2 — Autonomous Workflows** (where this framework operates)

PM says: "We had a design review for the notification center. Here's the transcript and three Figma screenshots."

Agent:
1. Extracts open questions from the transcript
2. Analyzes the mockups for missing states and edge cases
3. Cross-references against existing requirements docs
4. Identifies gaps between what was discussed and what's documented
5. Drafts updated user stories for the decided items
6. Flags unresolved decisions with enough context for the PM to make the call

The PM shifted from "doing the work" to "directing the work and making the hard calls."

**Level 3 — Persistent Context + Judgment** (the frontier this framework enables)

Agents that maintain an evolving understanding of the product and surface the right questions before anyone thinks to ask them. The Context File and artifact-linking system in this framework are the foundation for Level 3.

---

## The 5-Artifact System

All PM work produces one of 5 artifact types:

| Artifact | What It Is | PM writes | Agent handles |
|----------|-----------|-----------|---------------|
| **Decision Memo** | One decision + reasoning. Atomic unit of PM judgment. | Everything (this is the PM's job) | Flags when assumptions change |
| **Intent Brief** | PM writes intent (sections 1-5), agent generates spec (6-9). | Sections 1-5: problem, goals, constraints, scope | Sections 6-9: spec, stories, dependencies |
| **Context File** | Living domain background that agents read to stay grounded. | Anti-patterns, terminology, ownership | Document indexing, staleness detection |
| **Question Log** | Tracks open questions from raised to resolved. | Resolutions and judgment calls | Extraction from transcripts, status tracking |
| **Scorecard** | Living feature health tracker updated on cadence. | Health assessment | Counting, risk flagging, metric tracking |

**The hierarchy:**
- **Decision Memo** is the atomic unit — small, frequent, captures actual PM judgment
- **Intent Brief** is the container — stitches decisions into a coherent feature plan
- **Context File + Question Log + Scorecard** are infrastructure — they make the first two work better over time and turn one-shot interactions into a persistent, context-aware system

**How they connect:**

```
Question Log → resolves into → Decision Memos
Decision Memos → referenced in → Intent Brief (section 5)
Intent Brief scope → tracked in → Scorecard (section 3)
Scorecard open questions → pulled from → Question Log
```

---

## Agent Architecture

```
@builder (team lead)
├── @intent_writer       — Write Intent Briefs (PM Intent + Agent Spec)
├── @domain_pm           — Domain specialist (you customize this)
└── @design_image_analyzer — Extract questions from Figma mockups
```

**`@builder`** handles strategy directly (competitive analysis, build-vs-buy, roadmap, metrics) and spawns teammates for focused deliverables.

**`@domain_pm`** is a template agent. You fill it in with your product's domain knowledge — feature areas, constructs, key docs — and it becomes a grounded specialist for your product.

**Skills** run inline without subprocesses: `/decision-memo`, `/question-log`, `/scorecard`, `/user-story-writer`, `/backlog-groomer`, `/stakeholder-summarizer`, `/extract-transcript`.

---

## Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/[your-username]/agentic-pm-framework.git
cd agentic-pm-framework
```

Open the folder in Claude Code.

### 2. Customize `@domain_pm`

Edit `.claude/agents/domain_pm.md`. Fill in the "Domain Expertise" section with your product's:
- Feature areas or pillars
- Coverage model (what "fully supported" looks like)
- Key reference documents
- User personas

This is the only file that's truly project-specific. Everything else works out of the box.

### 3. Run your first skill

Try a quick win:

```
/decision-memo [evaluate] Should we build our own search or use a third-party library?
```

Or start an Intent Brief:

```
@intent_writer Write an Intent Brief for [your feature].
```

Or chain a full artifact pipeline:

```
@builder Here is a transcript from our design review. Extract questions, create a Question Log, and draft Decision Memos for what we decided.
```

---

## Directory Structure

```
agentic-pm-framework/
├── README.md
├── CLAUDE.md                          # Agent + skill routing guide
├── .claude/
│   ├── agents/
│   │   ├── builder.md                 # PM team lead
│   │   ├── domain_pm.md               # Domain specialist — customize this
│   │   ├── intent_writer.md           # Intent Brief specialist
│   │   └── design_image_analyzer.md   # Design mockup analysis
│   └── skills/
│       ├── backlog-groomer/SKILL.md   # RICE/ICE/Kano prioritization
│       ├── decision-memo/SKILL.md     # Decision documentation
│       ├── humanized-writing/SKILL.md # Writing style enforcement
│       ├── product-mece/SKILL.md      # MECE framework for product thinking
│       ├── question-log/SKILL.md      # Question tracking
│       ├── scorecard/SKILL.md         # Feature health tracking
│       ├── stakeholder-summarizer/SKILL.md  # Exec summaries + status updates
│       └── user-story-writer/SKILL.md # Sprint-ready user stories
└── Docs/
    ├── agentic_pm.md                  # Philosophy + intellectual foundation
    ├── Sprint_Planning_Template.md    # Sprint planning document
    └── PRDdocs/
        ├── intent_brief_template.md   # 9-section Intent Brief template
        ├── decision_memo_template.md  # 7-section Decision Memo template
        ├── question_log_template.md   # Question Log template
        ├── scorecard_template.md      # Scorecard template
        ├── prd_template.md            # Legacy PRD (reference only)
        └── examples/                  # Fictional Acme Corp examples
            ├── EXAMPLE_intent_brief.md
            ├── EXAMPLE_decision_memo.md
            ├── EXAMPLE_context_file.md
            ├── EXAMPLE_question_log.md
            └── EXAMPLE_scorecard.md
```

---

## Key Concepts

**Intent Brief vs. PRD:** A traditional PRD is 80% context compilation (requirements, user flows, edge cases) and 20% judgment. The Intent Brief flips that ratio. The PM writes sections 1-5 (what, why, goals, scope, solution intent — pure judgment). The agent generates sections 6-9 (requirements, stories, dependencies, open questions — information-dense drafting). The PM stays in the judgment seat.

**Decision Memo as atomic unit:** Every significant product decision gets its own 7-section memo: Situation, Decision, Why This Not That, What This Unlocks, What This Closes Off, Constraints, Open Threads. Small format, big discipline. Decisions referenced in Intent Briefs, tracked in Scorecards, linked from Question Logs.

**Context File:** The agent equivalent of onboarding docs. Your `@domain_pm` reads this to understand your product before producing any artifact. Without it, agents start cold every session. With it, they ground every claim in your real product context — this is what enables Level 3 agentic PM.

**Anti-shallow rules:** Every agent and skill enforces: ground every claim, at least one concrete example per section, no banned buzzwords (leverage, synergy, streamline, robust, seamless, revolutionary), depth over breadth, traceability with consistent numbering.

---

## Philosophy

### The Coding Parallel

In agentic coding, the shift looks like this:

| Before | After |
|--------|-------|
| Developer writes every line | Developer describes intent, reviews output |
| Manual file-by-file exploration | Agent explores codebase autonomously |
| Human holds all context in their head | Agent reads docs, tests, and code to build context |
| Sequential: write → test → fix → repeat | Agent runs the loop, surfaces results |
| One person, one task at a time | Agent spawns parallel workers for independent tasks |

The developer didn't become unnecessary. They became a technical director — setting intent, making judgment calls, approving work, and handling the ambiguous stuff.

### The Structural Parallel

PM work follows the same pattern:

| Agentic Coding | Agentic PM |
|----------------|------------|
| Codebase as context | Documentation corpus as context |
| Tests as ground truth | Requirements + confirmed scope as ground truth |
| Compiler errors = hard failures | Inconsistencies between docs = soft failures |
| explore → plan → implement → test | research → analyze → draft → validate |
| Agent spawns sub-agents for parallel tasks | PM lead agent spawns specialist agents |
| Human approves PRs | Human approves decisions |
| CI/CD catches regressions | Agent catches spec drift and stale docs |

### What's Actually Different

The honest gap: code has a compiler. Product decisions don't.

In coding, you can verify correctness — tests pass, types check, the app runs. In PM work, quality is judgment-based. A PRD can be internally consistent but strategically wrong. A prioritization can follow a perfect framework and still miss the point.

So the future state isn't "agents do PM." It's closer to: agents handle the information-heavy, consistency-checking, artifact-producing work — and the PM focuses entirely on judgment, strategy, stakeholder alignment, and the messy human stuff that no framework captures.

The PM becomes less of a "document producer" and more of a "decision-maker with perfect context." Which, honestly, is what the role was always supposed to be.

Read the full argument in `Docs/agentic_pm.md`.

---

## Contributing

PRs welcome. The most valuable contributions:
- New skill definitions for common PM workflows
- Improvements to the Intent Brief or Decision Memo templates
- Better examples (keep them fictional — no real company data)
- Improvements to `@domain_pm` to make customization easier
