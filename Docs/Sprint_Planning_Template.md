# Sprint Planning Document

**Version:** 1.0
**Date:** February 18, 2026
**Sprint Duration:** 2 weeks
**Sprint Goal:** [To be filled during planning]

---

## Executive Summary

Sprint planning establishes what the team will deliver in the next iteration and how they'll accomplish it. This document captures sprint goals, committed work items, capacity planning, and dependencies to align the team and stakeholders on sprint scope and success criteria.

---

## 1. Sprint Overview

### 1.1 Sprint Information

| Attribute | Details |
|-----------|---------|
| Sprint Number | [e.g., Sprint 15] |
| Start Date | [e.g., February 19, 2026] |
| End Date | [e.g., March 4, 2026] |
| Sprint Goal | [One sentence describing what the sprint achieves] |
| Team | [Team name or composition] |

### 1.2 Sprint Goal

**Primary Objective:**
[2-3 sentences describing the main outcome this sprint delivers. Connect to product goals or GA milestones.]

**Why This Sprint Matters:**
[1-2 sentences explaining business impact or user value.]

**Success Criteria:**
- [ ] Criterion 1 (measurable)
- [ ] Criterion 2 (measurable)
- [ ] Criterion 3 (measurable)

---

## 2. Team Capacity

### 2.1 Availability

| Team Member | Role | Available Days | Capacity (%) | Notes |
|-------------|------|----------------|--------------|-------|
| [Name] | [Engineer/Designer/PM] | 10 | 100% | |
| [Name] | [Engineer/Designer/PM] | 8 | 80% | PTO on [dates] |
| [Name] | [Engineer/Designer/PM] | 10 | 100% | |

**Total Team Capacity:** [X] story points or [Y] developer days

### 2.2 Capacity Deductions

- **Meetings & ceremonies:** [X] hours/week (standups, retro, planning)
- **On-call/support:** [X] hours
- **Tech debt/maintenance:** [X]% allocated
- **Other commitments:** [List any known interruptions]

**Adjusted Sprint Capacity:** [X] story points or [Y] developer days

---

## 3. Committed Work

### 3.1 Priority Ranking

Stories are prioritized using [RICE/ICE/MoSCoW] framework:

| Rank | Story ID | Title | Priority | Story Points | Assignee |
|------|----------|-------|----------|--------------|----------|
| 1 | [TICKET-123] | [Story title] | Must Have | 5 | [Name] |
| 2 | [TICKET-124] | [Story title] | Must Have | 8 | [Name] |
| 3 | [TICKET-125] | [Story title] | Should Have | 3 | [Name] |
| 4 | [TICKET-126] | [Story title] | Should Have | 5 | [Name] |

**Total Committed:** [X] story points

### 3.2 Sprint Backlog Detail

#### Story 1: [Title]
**ID:** [TICKET-XXX]
**Priority:** Must Have
**Story Points:** [X]

**User Story:**
As a [persona], I want [capability] so that [value].

**Acceptance Criteria:**
- [ ] Given [context], when [action], then [outcome]
- [ ] Given [context], when [action], then [outcome]
- [ ] Given [context], when [action], then [outcome]

**Technical Approach:**
[1-2 sentences on implementation approach]

**Dependencies:**
[List any blockers or dependencies]

**Definition of Done:**
- [ ] Code complete and reviewed
- [ ] Unit tests written and passing
- [ ] Integration tests passing
- [ ] Documentation updated
- [ ] Deployed to staging environment
- [ ] QA sign-off
- [ ] PM/Design acceptance

---

#### Story 2: [Title]
[Repeat structure for each committed story]

---

### 3.3 Stretch Goals

If the team completes committed work early:

| Story ID | Title | Story Points | Why Stretch |
|----------|-------|--------------|-------------|
| [TICKET-XXX] | [Story title] | 3 | Lower priority but valuable |
| [TICKET-XXX] | [Story title] | 5 | Depends on external team |

**Note:** Stretch goals are not commitments. Only pull if committed work is done.

---

## 4. Dependencies and Risks

### 4.1 External Dependencies

| Dependency | Owner | Status | Impact if Delayed | Mitigation |
|------------|-------|--------|-------------------|------------|
| [Design mockups for Feature X] | [Designer name] | In Progress | Blocks Story 1 | Request draft by Wed |
| [API endpoint from Platform team] | [Team name] | Not Started | Blocks Story 3 | Use mock data initially |

### 4.2 Technical Risks

| Risk | Probability | Impact | Mitigation Strategy |
|------|-------------|--------|---------------------|
| [e.g., Performance issues with new widget system] | Medium | High | Spike in first 3 days, fallback to simpler approach |
| [e.g., Integration complexity with external service] | Low | Medium | Pair programming, early integration testing |

### 4.3 Known Blockers

- **Blocker 1:** [Description] → **Resolution:** [Action plan]
- **Blocker 2:** [Description] → **Resolution:** [Action plan]

---

## 5. Technical Scope

### 5.1 In Scope

**Features:**
- [Feature/capability 1]
- [Feature/capability 2]
- [Feature/capability 3]

**Components Affected:**
- [Component 1] - [Brief description of changes]
- [Component 2] - [Brief description of changes]

### 5.2 Explicitly Out of Scope

- [Feature X] - Moved to next sprint due to [reason]
- [Feature Y] - Not part of GA scope
- [Feature Z] - Requires design review first

---

## 6. Quality and Testing Strategy

### 6.1 Testing Approach

| Test Type | Coverage Target | Owner | Notes |
|-----------|-----------------|-------|-------|
| Unit Tests | 80% for new code | Engineers | Run on every commit |
| Integration Tests | Critical paths covered | QE + Engineers | Run nightly |
| E2E Tests | Happy path + 2 edge cases per story | QE | Run before deployment |
| Manual Testing | Full acceptance criteria | QE | Sign-off required |

### 6.2 Quality Gates

- [ ] All tests passing in CI/CD pipeline
- [ ] Code review approved by 2+ engineers
- [ ] No P0/P1 bugs introduced
- [ ] Performance benchmarks met (if applicable)
- [ ] Security review completed (if touching auth/data access)
- [ ] Accessibility standards met (WCAG 2.1 AA)

---

## 7. Sprint Ceremonies

### 7.1 Daily Standup

**Time:** [Daily at X:XX AM/PM]
**Duration:** 15 minutes
**Format:**
- What did you complete yesterday?
- What will you work on today?
- Any blockers?

### 7.2 Mid-Sprint Check-in

**Time:** [Day 5, X:XX AM/PM]
**Purpose:** Assess progress, adjust scope if needed, surface blockers early

### 7.3 Sprint Review/Demo

**Time:** [Last day, X:XX AM/PM]
**Duration:** 1 hour
**Attendees:** Team + stakeholders
**Agenda:**
- Demo completed work
- Review sprint goal achievement
- Gather stakeholder feedback

### 7.4 Sprint Retrospective

**Time:** [Last day, after review]
**Duration:** 45 minutes
**Format:** [What went well / What didn't / Action items]

---

## 8. Communication Plan

### 8.1 Stakeholder Updates

| Stakeholder | Update Frequency | Format | Key Info |
|-------------|------------------|--------|----------|
| [Leadership] | Weekly | Email summary | Sprint progress, risks, blockers |
| [Product Team] | Daily | Slack updates | Completed stories, upcoming work |
| [Partner Teams] | As needed | Sync meetings | Dependencies, integration points |

### 8.2 Status Indicators

- 🟢 **On Track** - Sprint goal achievable, no major blockers
- 🟡 **At Risk** - Minor delays or blockers, may need scope adjustment
- 🔴 **Blocked** - Critical blockers, sprint goal in jeopardy

**Current Status:** [🟢/🟡/🔴]

---

## 9. Success Metrics

### 9.1 Sprint Metrics

| Metric | Target | Actual | Notes |
|--------|--------|--------|-------|
| Velocity (story points completed) | [X] | [To be filled at end] | |
| Sprint goal achieved | Yes/No | [To be filled at end] | |
| Stories completed vs committed | 100% | [To be filled at end] | |
| Carry-over stories | 0 | [To be filled at end] | |
| Bugs introduced | < 3 P1/P0 | [To be filled at end] | |

### 9.2 Product Metrics (if applicable)

- [Metric 1]: [Target] → [Actual]
- [Metric 2]: [Target] → [Actual]

---

## 10. Open Questions and Decisions

### 10.1 Open Questions

| Question | Owner | Due Date | Status |
|----------|-------|----------|--------|
| [Question about technical approach] | [Name] | [Date] | Open/Answered |
| [Question about requirements] | [Name] | [Date] | Open/Answered |

### 10.2 Key Decisions Made

| Decision | Rationale | Date | Decision Maker |
|----------|-----------|------|----------------|
| [Decision 1] | [Why we chose this] | [Date] | [Name/Team] |
| [Decision 2] | [Why we chose this] | [Date] | [Name/Team] |

---

## 11. Post-Sprint Actions

### 11.1 Next Sprint Preview

**Likely priorities for next sprint:**
- [Feature/area 1]
- [Feature/area 2]
- [Tech debt or maintenance work]

**Preparatory work needed:**
- [ ] [Design/technical spike]
- [ ] [Dependency from another team]
- [ ] [Requirements clarification]

### 11.2 Continuous Improvement

**From last retrospective:**
- Action 1: [What we committed to improve] → Status: [Done/In Progress/Blocked]
- Action 2: [What we committed to improve] → Status: [Done/In Progress/Blocked]

---

## Appendix

### A. Reference Documents

- Product Roadmap: [Link or location]
- Technical Architecture: [Link or location]
- Definition of Done: [Link or location]
- Team Working Agreement: [Link or location]

### B. Sprint Planning Meeting Notes

[Add any additional context, discussions, or decisions from the planning meeting]

### C. Burndown Chart

[Placeholder for burndown tracking - update daily]

**Day 1:** [X] points remaining
**Day 2:** [X] points remaining
...
**Day 10:** [X] points remaining

---

**Document Owner:** [Product Manager name]
**Last Updated:** [Date]
**Next Review:** [End of sprint]
