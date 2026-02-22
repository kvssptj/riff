---
name: competitive-analysis
description: Market landscape analysis, head-to-head competitor comparisons, and moat assessment. Use when evaluating market position, researching competitors before a feature or build/buy decision, or assessing how defensible your product is. Output feeds Intent Brief section 2 (Context) and Decision Memos.
user-invocable: true
---

Analyze the competitive landscape using structured frameworks. Output is scoped to what's useful for product decisions — not market research for its own sake.

## Modes

### Mode Detection

Check the start of the user's message for a `[bracket]` prefix. Valid modes: `[landscape]`, `[compare]`, `[moat]`. Everything after the prefix is the task description or input.

### Default Behavior

When no mode prefix is given, infer:
- Named competitors or products provided → `[compare]`
- Market category or problem space provided → `[landscape]`
- Question about defensibility, durability, or moat → `[moat]`

---

### `[landscape]` — Market Landscape Analysis

Map the competitive structure of a market category.

**Required input:** Market category or problem space (e.g., "B2B project management tools" or "AI-native writing assistants").

**Output:** Landscape analysis with Porter's Five Forces, positioning map, category dynamics, and identified white space.

**Key behavior:**
- Apply Porter's Five Forces concretely — name specific companies or dynamics for each force, not just "low/medium/high" labels
- Build a 2×2 positioning map with axes that actually differentiate competitors (not generic axes like "price vs. quality")
- Identify white space: where no current competitor is positioned, and whether that gap is intentional (no demand) or an opportunity
- End with a "Why now?" assessment: what market condition or technology shift makes this moment distinct

---

#### Porter's Five Forces

**Competitive Rivalry**
- Number of direct competitors, concentration, rate of feature copying and pricing pressure
- Specific recent example: "[Company X] launched [feature] in [period], directly targeting [segment]"

**Threat of New Entrants**
- Barriers: capital requirements, network effects, switching costs, regulatory hurdles
- Concrete assessment: "An AI-native entrant could replicate core functionality in 6–12 months; the moat is data, not features"

**Supplier Power**
- Key dependencies: AI model providers, infrastructure, data sources
- What happens if the primary supplier changes pricing or terms?

**Buyer Power**
- How easily can customers switch? What's the switching cost in time, data migration, retraining?
- Do large customers have leverage? Do credible alternatives exist?

**Threat of Substitutes**
- What do customers do instead? (Including doing nothing or building in-house)
- Is the substitute getting better faster than your product?

---

#### Positioning Map Format

```
## Positioning Map: [Category]

Axes: [X-axis label] (low → high) vs. [Y-axis label] (low → high)
Axis rationale: [Why these axes are the meaningful differentiators in this category]

Quadrant summary:
- Top-right [high/high]: [Companies] — [What this position means strategically]
- Top-left  [low/high]: [Companies] — [What this position means strategically]
- Bottom-right [high/low]: [Companies] — [What this position means strategically]
- Bottom-left  [low/low]: [Companies] — [What this position means strategically]

White space: [Unoccupied position and assessment of whether it's a real opportunity]
```

---

#### Landscape Output Format

```
## Competitive Landscape: [Category]
**Date:** [Today]

## Market Structure Summary
[3–4 sentences: number of competitors, category maturity, dominant dynamic]

## Porter's Five Forces
[Each force with specific companies and dynamics named]

## Positioning Map
[2×2 with labeled quadrants and company placements]

## Category Dynamics
[What's driving competition right now: pricing pressure, AI integration, consolidation, etc.]

## White Space
[Unoccupied positions — with assessment of whether they're real opportunities or gaps for a reason]

## Why Now
[What's changed that makes this moment distinct — technology shift, regulatory change, customer behavior]

## Implications for [Your Product]
[2–3 specific strategic takeaways — not generic observations]
```

---

### `[compare]` — Head-to-Head Comparison

Compare your product against specific named competitors on features, positioning, and strategy.

**Required input:** Your product context + 2–4 competitor names. Optionally: a specific feature area or decision you're trying to inform.

**Output:** Feature gap matrix, positioning comparison, and strategic assessment for each competitor.

**Key behavior:**
- Build a feature comparison table, but don't treat it as the conclusion — features can be copied. The strategic analysis (why each competitor made the choices they made) is what matters
- For each competitor: what's their actual business model, ICP, and what are they optimizing for? This explains their feature choices
- Distinguish: table stakes (everyone has it), differentiators (meaningful for some buyers), and white space (no one has it yet)
- Be honest about where competitors are stronger — that's more useful than listing only their weaknesses

---

#### Competitor Profile Format

```
## [Competitor Name]

**Positioning:** [One sentence — who they target and what value they claim]
**Business model:** [How they make money — pricing, segment, expansion motion]
**ICP:** [Who their ideal customer actually is]
**What they optimize for:** [Speed? Depth? Enterprise compliance? Low cost?]

**Feature comparison:**
| Capability | Us | [Competitor] | Notes |
|-----------|-----|-------------|-------|
| [Feature area] | ✓/∂/✗ | ✓/∂/✗ | [Table stakes or differentiator?] |
(✓ = full support, ∂ = partial, ✗ = not supported)

**Where they're stronger:** [Honest assessment]
**Where we're stronger:** [Honest assessment]
**Their strategic bet:** [What they believe will win the market]
**What must be true for their bet to pay off:** [The assumption underneath their strategy]
```

---

#### Table Stakes vs. Differentiators

After profiling each competitor, classify the feature landscape:

```
## Feature Classification

**Table stakes** (absence is a disqualifier for most buyers):
- [Feature]

**Differentiators** (meaningful for some buyers, not universal):
- [Feature] — differentiates for [segment] because [reason]

**White space** (no one has it, or only very early):
- [Feature] — [assessment of whether this is an opportunity or a gap for a reason]
```

---

### `[moat]` — Moat Analysis

Assess how defensible your product position is and what would erode it.

**Required input:** Your product and its current competitive position. Optionally: a specific moat type to focus on.

**Output:** Assessment across all five moat types, durability rating for each, biggest vulnerability, and the one moat most worth investing in.

**Key behavior:**
- Assess all five moat types — explicitly ruling one out is as useful as finding one
- Be honest about moat durability. "Our moat is great UX" is not a moat. Moats are structural, not executional.
- For each moat: name the specific mechanism and what a well-resourced competitor would need to do to neutralize it
- End with one clear recommendation on the most important moat to invest in

---

#### Moat Types

**Network Effects** — value compounds as more users join
- Direct: users benefit from other users directly (Slack, WhatsApp)
- Indirect: users on one side benefit from users on another side (marketplaces)
- Data: more usage → better model → more usage (AI products)
- Assessment: Does value compound with scale, or is it just additive?

**Switching Costs** — cost of leaving exceeds cost of staying
- Data migration complexity and timeline
- Workflow and process retraining cost
- Integration dependencies (API contracts, embedded in client systems)
- Assessment: How many hours/weeks would a full migration to a competitor actually take?

**Data Advantage** — unique data that improves the product and is hard to replicate
- Proprietary behavioral data, benchmarks, or training sets
- Assessment: Is the data advantage durable, or catchable within 12–24 months?

**Economies of Scale** — unit costs fall as you grow
- Infrastructure amortization, marginal cost per additional user
- Assessment: Does scale confer meaningful cost advantage at your current size?

**Brand / Distribution** — trust, familiarity, or channel access others can't replicate quickly
- Brand: does your name reduce friction in the buying process?
- Distribution: do you have a channel (PLG, sales, partnerships) others can't easily copy?

---

#### Moat Assessment Output

```
## Moat Analysis: [Product]
**Date:** [Today]

| Moat Type | Strength (1–5) | Durability | Primary Threat |
|-----------|----------------|------------|----------------|
| Network effects | [Score] | Strong/Moderate/Weak/None | [What would neutralize it] |
| Switching costs | [Score] | ... | ... |
| Data advantage | [Score] | ... | ... |
| Economies of scale | [Score] | ... | ... |
| Brand / distribution | [Score] | ... | ... |

## Strongest Current Moat
[Which moat and why — with specific evidence, not assertion]

## Biggest Vulnerability
[What a well-resourced competitor could do in 12–24 months to erode the position]

## Most Important Moat to Invest In
[Recommendation with rationale — why this one compounds most from here]
```

---

## Artifact Relationships

| Artifact | Relationship |
|----------|-------------|
| **Intent Brief section 2 (Context)** | Landscape and comparison output grounds "why now" and competitive positioning |
| **Decision Memo** | Competitive analysis informing a build/buy/partner decision → `/decision-memo [evaluate]` or `[capture]` |
| **@builder** | @builder handles competitive strategy — this skill provides the structured analysis it works from |

## Anti-Patterns

❌ **Positioning maps with generic axes**
→ "Price vs. quality" tells you nothing actionable. Axes should reflect actual strategic choices competitors are making.

❌ **Feature comparison as the conclusion**
→ Features can be copied in a sprint. The analysis that matters is why competitors made the choices they made and what they're betting on.

❌ **"We have no direct competitors"**
→ Every product competes with something — including doing nothing or building in-house. Name the substitutes.

❌ **Moat claims that are actually execution**
→ "Our moat is great UX" or "we move faster" aren't moats. Moats are structural advantages that compound over time. Name the mechanism.

❌ **Only listing competitor weaknesses**
→ An analysis that only surfaces competitor weaknesses is marketing, not strategy. Honest assessment of where you're behind is the most useful part.

## Naming Convention

Save as: `research/competitive/[YYYY-MM-DD]_[market-or-topic].md`

Example: `research/competitive/2026-02-22_b2b-project-management.md`

## Quality Checklist

- [ ] Porter's Five Forces: all five forces named with specific companies or dynamics
- [ ] Positioning map: axes are meaningful, not generic; white space identified
- [ ] Competitor profiles: ICP and business model stated, not just features listed
- [ ] Feature classification: table stakes vs. differentiators vs. white space distinguished
- [ ] Moat analysis: all five types assessed (including explicit ruling-out of inapplicable ones)
- [ ] Honest about where competitors are stronger
- [ ] Strategic takeaways are specific, not generic observations
- [ ] No banned language
