# Context File: Notification Center

**Last Updated:** [YYYY-MM-DD]
**Maintainer:** [Your Name]
**Purpose:** Living domain background for agents working on Notification Center features.

---

> **Note:** This is a fictional example using a made-up product ("Acme Corp" / "Notification Center") to illustrate the Context File format. Replace all content with your real domain context.

---

## What This Is

The Notification Center is a centralized in-app notification hub for the Acme platform. It is in active development (V1 targeting [release date]).

**Scope:** V1 covers web only. The mobile app and email notification system are out of scope for this workstream.

**Team:** PM ([Your Name]), Eng Lead ([Name]), Design ([Name]), QA ([Name]).

---

## Current State

Before the Notification Center, notifications were scattered:
- Email digests (sent by the email service team, separate system)
- Badge counts on individual feature pages (each team managed their own)
- No unified in-app feed

V1 introduces a unified slide-out panel accessible from the global navigation bar.

---

## Key Concepts

**Notification types (V1 scope):**
- **Needs Action:** Approval requests, task assignments — shown with action buttons (Approve / Reject / Dismiss)
- **@Mentions:** Someone mentioned the user in a comment — shown with "View" link
- **Status Changes:** A record the user owns changed state — shown with "View" link
- **FYI:** Informational, no action required — shown with "Mark read" only
- **System:** Platform alerts (maintenance, outages) — shown with "Dismiss"

**Delivery model (V1):** 30-second polling interval. Real-time WebSocket delivery is V2. See `DM_[date]_polling-vs-realtime.md`.

**Retention:** 30 days by default. Older notifications are archived (not deleted) — accessible via export on request.

**Unread count:** Shown as a badge on the bell icon. Capped at "99+" display. Computed server-side.

---

## Confirmed Decisions

| Decision | Date | Source |
|----------|------|--------|
| Panel (slide-out) over full page | [Date] | DM_[date]_panel-vs-page.md |
| Polling (30s) over real-time WebSocket for V1 | [Date] | DM_[date]_polling-vs-realtime.md |
| 5 notification types with inline actions for V1 | [Date] | Product review [Date] |
| 30-day retention, export on request | [Date] | Eng + PM sync [Date] |

---

## Active Open Questions

See `QL_notification-center.md` for the full Question Log. Top open items:

- Q-001: What happens to notifications for deleted source records?
- Q-004: Behavior when 500+ unread notifications exist?
- Q-005: Does the panel auto-close after an inline action?

---

## Anti-Patterns (What Not to Do)

- **Don't add notification types beyond the V1 list without a scope conversation.** Scope is already tight.
- **Don't assume real-time delivery.** V1 is 30-second polling. Don't design UX that depends on sub-5-second freshness.
- **Don't conflate in-app notifications with email notifications.** They are separate systems with separate teams. Changes to email behavior are out of scope.
- **Don't design for mobile.** Web only for V1. Flag any mobile-specific patterns for V2.

---

## Document Index

| Document | Type | Status | Notes |
|----------|------|--------|-------|
| `IB_notification-center.md` | Intent Brief | Active | Primary spec |
| `DM_[date]_panel-vs-page.md` | Decision Memo | Decided | Panel chosen |
| `DM_[date]_polling-vs-realtime.md` | Decision Memo | Decided | Polling for V1 |
| `QL_notification-center.md` | Question Log | Active | 5 open questions |
| `SC_notification-center.md` | Scorecard | Active | Health: 🟡 At Risk (dependency) |

---

## People & Ownership

| Area | Owner | Notes |
|------|-------|-------|
| PM | [Your Name] | |
| Eng Lead | [Name] | |
| Design | [Name] | |
| Platform API (dependency) | [Name] | External team |
| Email notifications (dependency) | [Name] | Separate PM, separate team |
