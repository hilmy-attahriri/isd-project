# Phase 1: App Foundation and Staff Access - Discussion Log

> **Audit trail only.** Do not use as input to planning, research, or execution agents.
> Decisions are captured in CONTEXT.md — this log preserves the alternatives considered.

**Date:** 2026-06-09
**Phase:** 1-App Foundation and Staff Access
**Areas discussed:** Login and accounts, Role access, First-screen layout, Demo data

---

## Login and accounts

| Option | Description | Selected |
|--------|-------------|----------|
| Username login | Staff users sign in with a username and password. | |
| Email login | Staff users sign in with email and password. | ✓ |
| External auth | Use OAuth, SSO, or a third-party login provider. | |

**User's choice:** Email login with simple password rules, seeded staff accounts in `data.sql`.
**Notes:** Password minimum is 6 characters. Accounts are seeded instead of being created through a UI in Phase 1.

## Role access

| Option | Description | Selected |
|--------|-------------|----------|
| Admin only | One staff role handles everything. | |
| Admin + Librarian split | Admin manages staff/members; Librarian manages books/borrowing. | ✓ |
| Shared access | Both roles can do the same work. | |

**User's choice:** Admin manages staff and members; Librarian manages books and borrowing.
**Notes:** Role boundaries should be enforced, not just implied in the navigation.

## First-screen layout

| Option | Description | Selected |
|--------|-------------|----------|
| Dashboard home | Landing page shows summary cards and quick access. | ✓ |
| Direct CRUD landing | Land directly on books or members. | |
| Empty shell | Plain shell with no meaningful dashboard content. | |

**User's choice:** Dashboard-only landing page with quick metric cards.
**Notes:** The dashboard should be the default post-login view.

## Demo data

| Option | Description | Selected |
|--------|-------------|----------|
| Seed data | Include basic sample users and starter books in `data.sql`. | ✓ |
| Manual setup | Require the user to create all data after launch. | |
| No demo data | Start empty and let later phases populate records. | |

**User's choice:** Include basic sample users and starter books in `data.sql`.
**Notes:** This is for a smoother coursework demo and immediate verification after startup.

## the agent's Discretion

- Password reset, MFA, OAuth, and JWT were not requested and remain out of scope for this phase.

## Deferred Ideas

None - no out-of-scope ideas were introduced during this discussion.
