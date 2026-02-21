The Coding Parallel

  In agentic coding today, the shift looks like this:

  ┌─────────────────────────────────────────┬─────────────────────────────────────────────────────┐
  │                 Before                  │                        After                        │
  ├─────────────────────────────────────────┼─────────────────────────────────────────────────────┤
  │ Developer writes every line             │ Developer describes intent, reviews output          │
  ├─────────────────────────────────────────┼─────────────────────────────────────────────────────┤
  │ Manual file-by-file exploration         │ Agent explores codebase autonomously                │
  ├─────────────────────────────────────────┼─────────────────────────────────────────────────────┤
  │ Human holds all context in their head   │ Agent reads docs, tests, and code to build context  │
  ├─────────────────────────────────────────┼─────────────────────────────────────────────────────┤
  │ Sequential: write → test → fix → repeat │ Agent runs the loop, surfaces results               │
  ├─────────────────────────────────────────┼─────────────────────────────────────────────────────┤
  │ One person, one task at a time          │ Agent spawns parallel workers for independent tasks │
  └─────────────────────────────────────────┴─────────────────────────────────────────────────────┘

  The developer didn't become unnecessary. They became a technical director — setting intent, making judgment calls, approving work, and handling the ambiguous stuff.

  Agentic PM: The Same Shift, Different Material

  Product management's raw material isn't code — it's decisions, context, and alignment artifacts. But the workflow patterns are surprisingly similar.

  Level 1: Tool Use (where most "AI for PM" is today)

  "Summarize this transcript." "Write a PRD draft." "Generate user stories."

  This is the equivalent of GitHub Copilot autocomplete — useful, but not agentic. The PM still drives every step manually.

  Level 2: Autonomous Workflows (where this repo is pushing)

  This is the real parallel to agentic coding. Here's what it looks like:

  Coding equivalent: "Fix the auth bug" → agent explores code, identifies root cause, writes fix, runs tests, iterates.

  PM equivalent: "We had a design review for the notification center. Here's the transcript and three Figma screenshots." → agent:

  1. Extracts open questions from the transcript
  2. Analyzes the mockups for missing states and edge cases
  3. Cross-references against existing requirements docs
  4. Identifies gaps between what was discussed and what's documented
  5. Drafts updated user stories for the decided items
  6. Flags unresolved decisions with enough context for the PM to make the call

  The PM didn't disappear. They shifted from "doing the work" to "directing the work and making the hard calls."

  Level 3: Persistent Context + Judgment (the future state)

  This is where the parallel gets interesting. In coding, the frontier is agents that:
  - Maintain a mental model of the whole codebase
  - Anticipate what needs to change when requirements shift
  - Proactively flag tech debt, test gaps, security issues

  The PM equivalent would be agents that:

  - Hold the full product context — every PRD, every meeting, every design decision, every stakeholder concern. Not as a search index, but as an internalized understanding of why things are the way they are.
  - Detect inconsistencies proactively. "The notification center spec says actions appear on all task types, but the requirements doc only covers 4 of 7 task types. Who owns closing this gap?"
  - Run the decision support loop. Not making product decisions — but doing the 80% of work that precedes a decision. Gathering context, identifying tradeoffs, modeling scenarios, preparing the PM to make a well-informed call in minutes
  instead of days.
  - Maintain living documents. When a meeting changes scope, affected PRDs, stories, and dependency maps update automatically — or at least flag what's stale.
  - Coordinate across agents like a staff PM coordinates across teams. One agent owns a feature domain. Another owns a different domain. A coordinator agent identifies cross-cutting dependencies and surfaces conflicts before they become surprises.

  The Structural Parallel

  ┌────────────────────────────────────────────┬──────────────────────────────────────────────┐
  │               Agentic Coding               │                  Agentic PM                  │
  ├────────────────────────────────────────────┼──────────────────────────────────────────────┤
  │ Codebase as context                        │ Documentation corpus as context              │
  ├────────────────────────────────────────────┼──────────────────────────────────────────────┤
  │ Tests as ground truth                      │ Requirements + GA scope as ground truth      │
  ├────────────────────────────────────────────┼──────────────────────────────────────────────┤
  │ Compiler errors = hard failures            │ Inconsistencies between docs = soft failures │
  ├────────────────────────────────────────────┼──────────────────────────────────────────────┤
  │ explore → plan → implement → test          │ research → analyze → draft → validate        │
  ├────────────────────────────────────────────┼──────────────────────────────────────────────┤
  │ Agent spawns sub-agents for parallel tasks │ PM lead agent spawns specialist agents       │
  ├────────────────────────────────────────────┼──────────────────────────────────────────────┤
  │ Human approves PRs                         │ Human approves decisions                     │
  ├────────────────────────────────────────────┼──────────────────────────────────────────────┤
  │ CI/CD catches regressions                  │ Agent catches spec drift and stale docs      │
  └────────────────────────────────────────────┴──────────────────────────────────────────────┘

  What's Actually Different

  The honest gap: code has a compiler. Product decisions don't.

  In coding, you can verify correctness — tests pass, types check, the app runs. In PM work, quality is judgment-based. A PRD can be internally consistent but strategically wrong. A prioritization can follow a perfect RICE framework and
  still miss the point.

  So the future state isn't "agents do PM." It's closer to:

  Agents handle the information-heavy, consistency-checking, artifact-producing work — and the PM focuses entirely on judgment, strategy, stakeholder alignment, and the messy human stuff that no framework captures.

  The PM becomes less of a "document producer" and more of a "decision-maker with perfect context." Which, honestly, is what the role was always supposed to be.

  ---
  This repo's agent setup (@builder as team lead coordinating @intent_writer, @domain_pm, @design_image_analyzer, etc.) is a small version of Level 2. The interesting frontier is Level 3 — where the agents don't just execute tasks but maintain an
  evolving understanding of the product and surface the right questions before anyone thinks to ask them.


What would be the best artifacts that PMs can produce for agentic product management. I am thinking future forward PRDs and Memo 1 pagers 

⏺ This is the right question. The artifact design is what determines whether "agentic PM" actually works or just produces faster garbage.

  Here's how I'd think about it:

  The Core Problem with Current PM Artifacts

  Most PM documents today serve two purposes simultaneously, and do both poorly:

  1. Thinking tool — forces the PM to clarify their own thinking
  2. Communication tool — aligns others on what to build and why

  In an agentic world, a third purpose emerges:

  3. Agent context — gives agents enough structured information to do useful downstream work (stories, designs, test plans, dependency tracking)

  Current PRDs are optimized for purpose 2 and accidentally serve purpose 1. They're terrible for purpose 3 — too much prose, too little structure, too many implicit assumptions.

  The Artifact Stack for Agentic PM

  I'd argue there are 5 core artifacts, not 2. They form a hierarchy:

  ---
  1. The Decision Memo (your "1-pager")

  What it is: A short narrative document that captures a decision and its reasoning. Not a spec. Not a plan. A record of judgment.

  Why it matters most: This is the one artifact agents genuinely cannot produce. Everything else is downstream of human judgment — this is where that judgment lives.

  Structure:

  DECISION MEMO: [Title]
  Date: [date]  |  Author: [PM]  |  Status: Decided / Proposed / Revisiting

  THE SITUATION (3-4 sentences)
  What's happening that requires a decision. Facts only.

  THE DECISION
  One sentence. Unambiguous.

  WHY THIS, NOT THAT
  - Option A (chosen): [reasoning]
  - Option B (rejected): [why not — be specific]
  - Option C (rejected): [why not]

  WHAT THIS UNLOCKS
  What becomes possible or clearer because of this decision.

  WHAT THIS CLOSES OFF
  What we're explicitly choosing not to do. What gets harder.

  CONSTRAINTS & ASSUMPTIONS
  Numbered list. Things that, if they change, should trigger revisiting this decision.

  OPEN THREADS
  Decisions this doesn't cover that still need to be made.

  Why it's agentic-friendly:
  - Agents can read the "Constraints & Assumptions" section and flag when upstream changes invalidate the decision
  - "Open Threads" becomes a direct input to agent task planning
  - "Why This, Not That" gives agents the reasoning context they need to make consistent downstream choices
  - The explicit "What This Closes Off" prevents agents from accidentally working on rejected paths

  ---
  2. The Intent Brief (your "future-forward PRD")

  What it is: A replacement for the traditional PRD. The PM writes the intent — the problem, the constraints, the success criteria. The agent fills in the spec.

  Key shift: Today's PRD is 80% context compilation (requirements, user flows, edge cases) and 20% judgment (what to build, what not to, what matters). Flip that ratio.

  Structure:

  INTENT BRIEF: [Feature Name]
  Date: [date]  |  PM: [name]  |  Status: Draft / Active / Shipped

  1. THE PROBLEM (PM writes — not delegatable)
     Who has this problem? How do we know? What's the cost of not solving it?
     [3-5 sentences, grounded in data or observation]

  2. SUCCESS LOOKS LIKE (PM writes)
     - Primary metric: [specific, measurable]
     - Guardrail metric: [what must NOT get worse]
     - Qualitative signal: [what users say/do differently]

  3. CONSTRAINTS (PM writes)
     Hard constraints:
     - [e.g., "Must work within existing infrastructure"]
     - [e.g., "No new admin config surfaces for GA"]
     Soft constraints:
     - [e.g., "Prefer pattern-based over generative UI for V1"]

  4. DECISIONS MADE (PM writes — links to Decision Memos)
     - [Decision 1]: [link to memo]
     - [Decision 2]: [link to memo]

  5. SCOPE BOUNDARY (PM writes)
     IN:  [explicit list]
     OUT: [explicit list — with brief "why out"]
     DEFERRED: [explicit list — with "revisit when..."]

     --- AGENT-GENERATED BELOW THIS LINE ---

  6. SOLUTION SPEC (agent drafts, PM reviews)
     [User flows, component mapping, edge cases, error states]
     [Generated from intent + constraints + existing docs]

  7. REQUIREMENTS & WORK BREAKDOWN (agent drafts)
     [Stories, acceptance criteria, size estimates]
     [Generated from solution spec]

  8. DEPENDENCY MAP (agent maintains)
     [Teams, systems, APIs, timeline risks]
     [Auto-updated when linked docs change]

  9. OPEN QUESTIONS (agent + PM collaborate)
     [Agent surfaces questions from gaps it finds]
     [PM answers or escalates]

  Why this works: The PM spends their time on sections 1-5, which is pure judgment work. Sections 6-9 are where agents excel — they can read the codebase, cross-reference requirements, generate stories, and maintain dependencies. The PM
  reviews and corrects, but doesn't draft from scratch.

  ---
  3. The Context File (new artifact — no traditional equivalent)

  What it is: Think CLAUDE.md but for product decisions. A living, structured file that gives agents the background they need to work autonomously on a feature area.

  This repo's CLAUDE.md is actually an early version of this. It tells agents about naming conventions, architecture, team structure, and documentation locations.

  Structure:

  CONTEXT: [Domain — e.g., "Notification Center"]
  Last updated: [date]  |  Owner: [PM]

  CURRENT STATE
  - What exists today, briefly
  - Key architecture choices and why

  ACTIVE DECISIONS
  - [Link to decision memos that are current]

  TERMINOLOGY
  - [Term]: [Definition — prevents agents from using wrong language]

  KNOWN CONSTRAINTS
  - [Technical, organizational, timeline]

  PEOPLE & OWNERSHIP
  - [Who owns what — so agents know who to reference]

  DOCUMENT INDEX
  - [Which docs are authoritative, which are stale]

  ANTI-PATTERNS
  - [Things that have been tried and failed]
  - [Common mistakes agents should avoid]

  Why it matters: Without this, every agent interaction starts cold. With it, agents have a "mental model" of the product domain. This is the artifact that enables Level 3 agentic PM (from our earlier conversation).

  ---
  4. The Question Log (replaces meeting notes)

  What it is: Instead of capturing what was said in meetings, capture what was asked and unresolved. Meetings produce decisions (→ Decision Memos) and questions (→ Question Log). Everything else is noise.

  Structure:

  QUESTION LOG: [Feature/Sprint/Team]

  | # | Question | Context | Raised by | Date | Status | Resolution |
  |---|----------|---------|-----------|------|--------|------------|
  | 1 | How do stalled requests behave for... | Detail shell, layer 6 | Design | 2026-02-18 | Open | — |
  | 2 | Should admin config for X be... | Admin pillar | Eng | 2026-02-15 | Decided | [Link to memo] |

  Why it's agentic-friendly: Agents can scan the log, identify open questions that block their current task, and either flag them or work around them. It's a structured TODO list for product decisions.

  ---
  5. The Scorecard (replaces status updates)

  What it is: A single, living artifact that answers "how is this feature doing?" — updated continuously rather than produced weekly.

  Structure:

  SCORECARD: [Feature]
  As of: [auto-updated timestamp]

  HEALTH: 🟢 / 🟡 / 🔴  (PM sets manually)
  PM ASSESSMENT: [1-2 sentences — why this health rating]

  SCOPE:     [X of Y items complete]  [auto-counted from stories]
  DECISIONS: [X open / Y decided]     [auto-counted from question log]
  RISKS:     [list — agent flags, PM curates]
  METRICS:   [current vs. target — if measurable yet]

  Why it works: The agent maintains the counts and flags. The PM writes only the assessment and health rating — the one thing that requires judgment about "are we actually on track or just busy?"

  ---
  The Pattern

  Notice what connects all five:

  ┌───────────────┬───────────────────────────────────────────┬──────────────────────────────────────────────┐
  │   Artifact    │                 PM writes                 │                Agent handles                 │
  ├───────────────┼───────────────────────────────────────────┼──────────────────────────────────────────────┤
  │ Decision Memo │ Everything (this IS the PM's job)         │ Flags when assumptions change                │
  ├───────────────┼───────────────────────────────────────────┼──────────────────────────────────────────────┤
  │ Intent Brief  │ Sections 1-5 (intent, constraints, scope) │ Sections 6-9 (spec, stories, dependencies)   │
  ├───────────────┼───────────────────────────────────────────┼──────────────────────────────────────────────┤
  │ Context File  │ Anti-patterns, terminology, ownership     │ Document indexing, staleness detection       │
  ├───────────────┼───────────────────────────────────────────┼──────────────────────────────────────────────┤
  │ Question Log  │ Resolutions and judgment calls            │ Extraction from transcripts, status tracking │
  ├───────────────┼───────────────────────────────────────────┼──────────────────────────────────────────────┤
  │ Scorecard     │ Health assessment                         │ Counting, risk flagging, metric tracking     │
  └───────────────┴───────────────────────────────────────────┴──────────────────────────────────────────────┘

  The PM's output shifts from "documents" to "decisions." Every artifact is structured so the judgment parts are clearly separated from the information-compilation parts. Agents handle the latter. PMs own the former.

  The Memo vs. PRD Question Specifically

  You're right that these two are the core. If I had to pick just two:

  - Decision Memo is the atomic unit. It's small, frequent, and captures the actual work product of a PM — judgment under uncertainty.
  - Intent Brief is the container. It stitches together multiple decisions into a coherent feature plan, with clear boundaries between "human intent" and "agent-generated spec."

  The other three (Context File, Question Log, Scorecard) are infrastructure that makes the first two work better over time. They're what turn one-shot agent interactions into a persistent, context-aware system.

  Want me to build out any of these as working templates for this repo?



