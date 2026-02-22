---
name: roadmapping-strategy
description: Build or validate a product roadmap using OKR alignment, Now-Next-Later framing, and 70-20-10 portfolio thinking. Use when planning a quarter or half, auditing a proposed roadmap against OKRs, or writing a stakeholder-ready roadmap narrative. Not a backlog prioritization tool — use /backlog-groomer to score individual items first.
user-invocable: true
---

Build or evaluate a product roadmap. A roadmap is a set of bets with a strategic rationale — not a feature list with dates.

## Modes

### Mode Detection

Check the start of the user's message for a `[bracket]` prefix. Valid modes: `[build]`, `[align]`, `[present]`. Everything after the prefix is the task description or input.

### Default Behavior

When no mode prefix is given, infer:
- Input includes OKRs + features/items to plan → `[build]`
- Input includes a proposed roadmap to evaluate → `[align]`
- Request for a narrative or stakeholder communication → `[present]`

---

### `[build]` — Build a Roadmap

Create a roadmap for a planning period from OKRs, capacity, and a prioritized feature list.

**Required input:** Planning period + OKRs or goals + feature/initiative list. Capacity (team size or velocity) is optional but strongly recommended.

**Output:** A complete Now-Next-Later roadmap with OKR mapping, portfolio balance check, and an explicit "what we're not doing" section.

**Key behavior:**
- Start with OKRs — every item in Now must map to at least one OKR. Items without an OKR connection get flagged, not silently included.
- Be explicit about capacity. If the PM provides team size or velocity, show what actually fits in "Now." If not, flag that capacity is assumed and "Now" may be aspirational.
- Apply 70-20-10: 70% core/committed, 20% expansion, 10% exploratory bets. Show the balance. Deviations are fine — but state the reason.
- The "what we're not doing" section is required. A roadmap without explicit trade-offs is a wish list.

---

#### OKR Alignment Check

Before placing any item on the roadmap:

```
For each initiative:
→ Which OKR does this move? (Name it explicitly)
→ How directly? Primary driver / contributes / indirect
→ Is there evidence it moves the metric, or is it assumed?

Items with no OKR connection → flag as "Unaligned — needs rationale to include"
Items with weak connection → flag as "Low alignment — confirm before committing capacity"
```

---

#### 70-20-10 Portfolio

| Bucket | Target % | What goes here |
|--------|----------|----------------|
| **Core** | ~70% | Committed items that directly drive current OKRs. High confidence, near-term impact. |
| **Expansion** | ~20% | Adjacent bets that extend the product or open new segments. Medium confidence. |
| **Exploratory** | ~10% | Long-horizon bets, new capabilities, or experiments. Designed to learn, not ship features. |

The 70-20-10 is a check, not a constraint. If current OKRs require a heavier core allocation (e.g., reliability work), state the deviation and the reason.

---

#### Now-Next-Later

- **Now:** In active development this planning period. Specific, sized, assigned (or assignable). Nothing gets here that isn't fully scoped and resourced. If it can't be fully scoped by week 2, it's not Now.
- **Next:** Committed for the period after Now. Direction is set; details can shift. Items in Next should be sequenced deliberately — each should either unlock something in Now or depend on it.
- **Later:** Directional intent, not commitment. Items here are bets, not promises. They can be reprioritized when the period comes. If an item is actually cut, say it's cut — "Later" is not a polite holding bin.

---

#### Roadmap Output Format

```
## Roadmap: [Product or Team] — [Quarter / Period]
**Date:** [Today]
**OKRs this roadmap serves:** [List]
**Capacity:** [Team size / sprints / person-weeks available, or "Assumed — not provided"]

---

## Portfolio Balance
Core (70%): [N weeks] | Expansion (20%): [N weeks] | Exploratory (10%): [N weeks]
[Note any deviation from 70-20-10 and the reason]

---

## Now — [Period, e.g., Q2 2026]
| Initiative | OKR | Bucket | Size | Owner | Notes |
|-----------|-----|--------|------|-------|-------|
| [Item] | [OKR] | Core | [M] | [Team] | [Constraint or dependency] |

## Next — [Following period]
| Initiative | OKR | Bucket | Est. size | Dependency |
|-----------|-----|--------|-----------|-----------|
| [Item] | [OKR] | Expansion | [L] | Depends on [Now item] completing |

## Later — Directional
| Initiative | OKR hypothesis | Bucket | Status |
|-----------|----------------|--------|--------|
| [Item] | [What we're betting on] | Exploratory | Active bet |
| [Item] | [No OKR yet — watching signal] | — | Deferred |

---

## What We're Not Doing (and Why)
| Item | Why it's off the roadmap |
|------|--------------------------|
| [Item] | [Specific reason: low RICE, no OKR connection, insufficient capacity, deferred to H2] |

---

## Open Questions
[Decisions that would change the roadmap if resolved differently — feed to `/question-log`]

## Assumptions
[What must be true for this roadmap to hold — flag the highest-risk ones]
```

---

### `[align]` — Audit a Roadmap Against OKRs

Review a proposed roadmap and surface alignment gaps, over-indexing, and missing OKR coverage.

**Required input:** Proposed roadmap (paste content) + current OKRs.

**Output:** Alignment audit with a coverage map (which OKRs are over/under-served), a list of unaligned items, portfolio balance check, and specific recommendations.

**Key behavior:**
- Over-indexing on one OKR is as much a problem as gaps — it usually means another OKR is being neglected
- Surface implicit assumptions: items that look aligned but depend on unvalidated hypotheses
- Flag capacity risk: if Now has more than the period can realistically hold, say so with specifics
- Don't just flag problems — give a specific recommendation for each gap

---

#### Alignment Audit Output Format

```
## Roadmap Alignment Audit: [Product or Team]
**Date:** [Today]

## OKR Coverage Map
| OKR | Items serving it | Coverage |
|-----|-----------------|----------|
| [OKR 1] | [Items] | Over-indexed / Appropriate / Under-indexed / No coverage |
| [OKR 2] | [Items] | ... |

## Findings

### Unaligned Items
| Item | Current placement | Recommendation |
|------|------------------|----------------|
| [Item] | Now | Remove or find OKR connection before committing capacity |

### OKR Gaps (OKRs with no roadmap coverage)
| OKR | Gap | Recommended action |
|-----|-----|-------------------|
| [OKR] | Nothing in Now or Next moves this metric | Add coverage or document why this OKR is deprioritized this period |

### Portfolio Balance
Estimated: Core [X%] / Expansion [Y%] / Exploratory [Z%]
Target: 70 / 20 / 10
Assessment: [In balance / Over-indexed on core / Under-investing in bets / reason for deviation]

### Capacity Risk
[If Now appears over-capacity: flag which items are at risk and what the sequencing dependency is]

## Recommendations
1. [Most important change + specific rationale]
2. ...
```

---

### `[present]` — Roadmap Narrative

Write a stakeholder-ready roadmap narrative — the strategic logic of what's being built and why, not a status update.

**Required input:** Current roadmap (from `[build]` output or PM description).

**Output:** A 1–2 page narrative explaining the OKR context, themes, trade-offs made, and what stakeholders should watch for.

**Key behavior:**
- Lead with context, not features — start with where the product is going and why this period matters
- Explain trade-offs explicitly: "We chose X over Y because..." — this is what stakeholders need to understand, not a feature list
- Be honest about what's committed (Now) vs. directional (Next/Later)
- 1–2 pages max; plain language; no buzzwords

---

#### Narrative Output Format

```
## [Product] Roadmap — [Period]
**Last updated:** [Date]

## Where We're Headed
[2–3 sentences: the OKR context and what this period needs to accomplish]

## What We're Building and Why

**Theme 1: [Theme name]**
[2–3 sentences: what's in this theme, which OKR it serves, why it's prioritized now]
Key initiatives: [List]

**Theme 2: [Theme name]**
...

## Trade-offs We Made
[What we chose not to do, and the specific reason — this is the most important section for stakeholder alignment]

## What's Directional, Not Committed
[Honest statement about Next/Later — we're pointing in this direction, but details will shift]

## What Would Change This Plan
[Top 2–3 assumptions or risks that would cause reprioritization — signals stakeholders should watch for]
```

---

## Relationship to Other Tools

| Tool | When to use instead |
|------|---------------------|
| `/backlog-groomer` | Scoring individual items with RICE/ICE/Kano. Use before `[build]` to have ranked items ready. |
| `/stakeholder-summarizer` | One-off status update or brief. Use when the audience needs current status, not strategic rationale. |
| `@builder` | Strategic context for the roadmap: competitive dynamics, market timing, build-vs-buy calls. Use `@builder` first, then `[build]` with that context. |
| `/decision-memo` | When a roadmap trade-off is significant enough to document formally — use `/decision-memo [capture]` for items cut with material impact. |

## Anti-Patterns

❌ **Roadmap as a feature list with dates**
→ A list of features with ship dates is a schedule. A roadmap explains the strategic logic of what's being built and why, including what isn't.

❌ **Now without capacity math**
→ "Now" must be scoped to what can actually ship in the period. Without explicit capacity, "Now" is aspirational and the roadmap loses credibility with engineering.

❌ **Every item maps to every OKR**
→ If all items serve all OKRs, the OKR mapping is decorative. Force each item to a primary OKR.

❌ **No "what we're not doing" section**
→ A roadmap without explicit trade-offs is a wish list. What you're not building is as important as what you are.

❌ **Later as a polite holding bin**
→ "Later" is directional intent, not a place to put ideas you don't want to say no to. If something is cut, say it's cut and why.

## Naming Convention

Save as: `strategy/roadmap_[YYYY-MM-DD]_[period].md`

Example: `strategy/roadmap_2026-02-22_Q2-2026.md`

## Quality Checklist

- [ ] Every "Now" item maps to a named OKR
- [ ] Capacity is explicit — "Now" is scoped to what actually fits
- [ ] 70-20-10 balance assessed; deviations explained
- [ ] "What we're not doing" section is present and specific
- [ ] Open questions fed to `/question-log`
- [ ] Assumptions named; highest-risk ones flagged
- [ ] No banned language
