# Decision Memo: Default Notification Delivery — Polling vs. Real-Time

**Version:** V1.0
**Date:** [YYYY-MM-DD]
**Author:** [Your Name]
**Status:** Accepted
**Feature:** Notification Center V1

---

> **Note:** This is a fictional example using a made-up product ("Acme Corp" / "Notification Center") to illustrate the Decision Memo format. Replace all content with your real decision context.

---

## 1. Situation

The Notification Center needs to fetch new notifications for users. Two delivery approaches are technically viable: polling (client checks the server on a fixed interval) and real-time via WebSocket. The choice affects infrastructure cost, implementation complexity, delivery latency, and battery consumption on mobile (future). This decision must be made before engineering begins the notification feed (R-03).

## 2. Decision

**V1 will use polling at a 30-second interval. WebSocket real-time delivery is deferred to V2.**

## 3. Why This, Not That

| Option | Pros | Cons | Decision |
|--------|------|------|----------|
| **Polling (30s interval)** — Chosen | Simple to implement; works with existing REST API; no new infrastructure; predictable cost | 30s latency on new notifications; slightly higher server load than idle WebSocket | ✅ Chosen |
| **WebSocket real-time** | Sub-second delivery; better UX for time-sensitive alerts | Requires new WebSocket infrastructure; adds auth complexity; increases scope by ~3 weeks | ❌ Rejected for V1 |
| **Polling (5s interval)** | Near-real-time feel; no new infra | 6x the server load; unacceptable for 50K+ concurrent users at current infrastructure capacity | ❌ Rejected |

**Most important differentiator:** Real-time adds 3 weeks of infrastructure work that puts the GA date at risk. 30-second polling covers 95% of use cases — the only user-impacting scenario is approvals, which users typically handle in batches, not in real-time.

**Recommendation:** Ship polling in V1. Revisit real-time after GA once we have data on actual notification volume and user behavior.

## 4. What This Unlocks

- Engineering can start the notification feed (R-03) immediately using the existing REST API.
- No new infrastructure provisioning required for GA.
- GA date remains achievable.
- Post-GA, if data shows users need faster delivery, we have a clear upgrade path to WebSocket without changing the client contract (same API, different delivery mechanism).

## 5. What This Closes Off

- Sub-second notification delivery is not possible in V1.
- Users with time-critical workflows (e.g., emergency approvals) will have up to 30 seconds of latency.
- **Mitigation:** Users with extreme time-sensitivity will still receive email notifications immediately. In-app polling is supplemental, not the primary alert channel.

## 6. Constraints & Assumptions

1. Current infrastructure cannot support WebSocket connections for 50K+ concurrent users without significant provisioning work.
2. 30-second latency is acceptable for the primary use cases in scope (approvals, task assignments, @mentions).
3. Email notifications continue to fire in real-time, providing a fallback for time-sensitive alerts.
4. V2 WebSocket work can reuse the same API contract — this assumption must be validated with Eng before V2 scoping.

## 7. Open Threads

- [ ] Validate assumption #4 with Eng: Can WebSocket V2 reuse the same API contract? Owner: [Eng Lead], Due: [Date]
- [ ] Define what happens if polling fails (e.g., network timeout) — does the badge go stale or show an error? Owner: [PM], Due: [Date]
- [ ] Confirm email notification system continues firing in real-time (no change in scope). Owner: [Email team PM], Due: [Date]
