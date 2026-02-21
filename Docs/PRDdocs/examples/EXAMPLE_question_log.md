# Question Log: Notification Center

**Version:** V1.0
**Date:** [YYYY-MM-DD]
**Author:** [Your Name]
**Status:** Active
**Feature:** Notification Center V1

---

> **Note:** This is a fictional example using a made-up product ("Acme Corp" / "Notification Center") to illustrate the Question Log format. Replace all content with your real questions and resolutions.

---

## Priority Summary

| Priority | Open | In Discussion | Resolved |
|----------|------|---------------|----------|
| High | 2 | 1 | 1 |
| Med | 2 | 0 | 0 |
| Low | 1 | 0 | 1 |
| **Total** | **5** | **1** | **2** |

---

## Notification Feed

| ID | Question | Context | Source | Priority | Status | Owner | Resolution |
|----|----------|---------|--------|----------|--------|-------|------------|
| Q-001 | What happens to a notification when its source record is deleted? | If a task is deleted after a notification is created, the notification card becomes orphaned. Clicking "View" would 404. | Design review, [Date] | High | Open | PM | — |
| Q-002 | How do we handle duplicate notifications? | If a user is @mentioned twice in the same comment thread, do they get 2 notifications or 1 grouped notification? | Eng sync, [Date] | High | In Discussion | Eng Lead | Exploring grouping by thread ID |
| Q-003 | What is the behavior when a user has 500+ unread notifications? | The feed could become very long for power users who don't check frequently. Does pagination kick in? Infinite scroll? | PM concern, [Date] | Med | Open | PM + Eng | — |
| Q-004 | Should the panel auto-close after an inline action completes? | After clicking "Approve" and seeing the success toast, does the panel stay open or close automatically? | Design question, [Date] | Med | Open | Design | — |
| Q-005 | What error message shows if the notification API is unreachable? | Users should understand the panel isn't broken — it's a connectivity issue. | Eng review, [Date] | Low | Open | Design + Eng | — |

---

## Delivery & Infrastructure

| ID | Question | Context | Source | Priority | Status | Owner | Resolution |
|----|----------|---------|--------|----------|--------|-------|------------|
| Q-006 | Polling (30s) vs. WebSocket real-time — which for V1? | Real-time would be better UX but requires new infrastructure. Polling is simpler but has latency. | Architecture discussion, [Date] | High | Resolved | Arch | **Polling (30s) chosen for V1.** WebSocket deferred to V2. See DM_[date]_polling-vs-realtime.md |
| Q-007 | Can the V2 WebSocket implementation reuse the same API contract as the polling endpoint? | If the API contract changes between V1 and V2, we'll have migration work. | [Date] PM + Eng sync | Low | Resolved | Eng Lead | **Yes — same REST API.** WebSocket would be an alternate transport layer only. Confirmed [Date]. |

---

## Naming Convention

Save this file as: `QL_[feature-area].md`

Example: `QL_notification-center.md`, `QL_approval-workflow.md`

Update this file whenever:
- New questions are raised in meetings, reviews, or async discussions
- Existing questions are resolved (fill the Resolution column — don't delete the row)
- A significant decision is made (note "→ See DM_[filename]" in the Resolution column)
