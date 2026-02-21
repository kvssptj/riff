# Scorecard: Notification Center V1

**Version:** V1.0
**Date:** [YYYY-MM-DD]
**Author:** [Your Name]
**Last Updated:** [YYYY-MM-DD]
**Feature:** Notification Center — centralized in-app notification hub

---

> **Note:** This is a fictional example using a made-up product ("Acme Corp" / "Notification Center") to illustrate the Scorecard format. Replace all content with your real feature health data.

---

## 1. Health Rating

| Dimension | Rating | Notes |
|-----------|--------|-------|
| **Overall** | 🟡 At Risk | One blocking dependency not yet resolved |
| **Scope** | 🟢 On Track | R-01 through R-07 defined and sized |
| **Timeline** | 🟡 At Risk | Platform API dependency is 1 week behind schedule |
| **Quality** | 🟢 On Track | Acceptance criteria defined for all P0 requirements |
| **Dependencies** | 🔴 Blocked | Platform API endpoint needed for R-03 not delivered |

---

## 2. PM Assessment

The feature is well-defined and the team has clear direction. The primary risk is the Platform API dependency — it's 1 week behind, which compresses engineering time for R-03 and R-04. If the API doesn't land by [date], we will need to either push GA by 1 week or cut R-04 (inline actions) from V1. I'm monitoring daily and will escalate to [Platform PM] if we hit [date] with no delivery.

---

## 3. Scope Progress

**Overall:** 2 of 9 requirements complete (22%)

**By priority:**

| Priority | Complete | In Progress | Not Started | Total |
|----------|----------|-------------|-------------|-------|
| P0 (7 reqs) | 0 | 3 | 4 | 7 |
| P1 (3 reqs) | 1 | 1 | 1 | 3 |
| P2 (2 reqs) | 1 | 0 | 1 | 2 |

**P0 detail:**

| Req | Description | Status |
|-----|-------------|--------|
| R-01 | Bell icon + unread count | ✅ Done |
| R-02 | Slide-out panel shell | 🔄 In Progress |
| R-03 | Notification feed | ⏸ Blocked (API) |
| R-04 | Inline actions | ⏸ Blocked (API + R-03) |
| R-05 | Mark as read | 🔄 In Progress |
| R-06 | Filter by type | ⬜ Not Started |
| R-07 | Empty/loading/error states | ⬜ Not Started |

---

## 4. Scope Changes

| Date | Change | Impact | Approved By |
|------|--------|--------|-------------|
| [Date] | Removed per-source notification preferences from V1 | Scope reduced; V2 roadmap | PM |
| [Date] | Added keyboard navigation (R-09) as P1 | Scope increased; fits in capacity | PM + Eng Lead |

---

## 5. Decision Tracker

| Decision | Date | Impact | Source |
|----------|------|--------|--------|
| Panel (slide-out) over full page | [Date] | UX pattern locked | DM_[date]_panel-vs-page.md |
| Polling (30s) for V1 delivery | [Date] | No WebSocket infra needed | DM_[date]_polling-vs-realtime.md |
| 5 notification types with inline actions | [Date] | Scope boundary set | Product review [Date] |
| 30-day retention default | [Date] | Storage cost bounded | Eng + PM sync [Date] |

---

## 6. Risks & Blockers

**Active blockers:**

| Blocker | Owner | Due | Status |
|---------|-------|-----|--------|
| Platform API endpoint not delivered | Platform PM | [Date] | Escalated [Date] — awaiting response |

**Risks:**

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| API delay pushes GA | Med | High | Cut R-04 (inline actions) from V1 if API not landed by [date] |
| Design not final for R-02 | Low | Med | Design committed to handoff by [date] |
| R-04 inline actions complexity underestimated | Low | Med | Spike planned for [date] |
| Auth token scope for cross-feature actions unclear | Med | Med | Eng + Auth team sync scheduled [date] |

---

## 7. Key Metrics

| Metric | Target | Current | Source |
|--------|--------|---------|--------|
| Missed approval support tickets | -60% within 60 days of GA | Baseline: [N]/week | Support data |
| DAU who open notification center | 70% within 30 days | N/A (pre-launch) | Analytics |
| Inline action completion rate | 80% | N/A (pre-launch) | Analytics |
| Notification delivery latency | ≤30s | N/A (pre-launch) | Monitoring |

---

## 8. Open Questions (Top 5)

See `QL_notification-center.md` for full log.

| Q | Question | Priority | Owner |
|---|----------|----------|-------|
| Q-001 | What happens to notifications for deleted source records? | High | PM |
| Q-002 | Duplicate notifications for same thread — grouped or separate? | High | Eng Lead |
| Q-003 | Behavior when 500+ unread notifications | Med | PM + Eng |
| Q-004 | Does panel auto-close after inline action? | Med | Design |
| Q-005 | Error message when notification API unreachable | Low | Design + Eng |

---

## 9. Next Update Actions

| Action | Owner | Due |
|--------|-------|-----|
| Follow up on Platform API delivery | PM | [Date] |
| Confirm design handoff date for R-02 | PM | [Date] |
| Schedule Auth team sync for R-04 | Eng Lead | [Date] |
| Run inline actions complexity spike | Eng | [Date] |
| Update this scorecard | PM | Weekly |
