# Library Management System

## What This Is

Library Management System is a university coursework project for managing core library circulation workflows. It is a Spring Boot, MySQL, and Thymeleaf web application used by staff users to manage books, members, borrowing transactions, returning transactions, due dates, and fine calculation.

The v1 product is a staff-facing system: admins and librarians log in and operate the application, while library members are managed as records rather than portal users.

## Core Value

Librarians can reliably track book borrowing and returning, including due dates and fines, through a simple web interface.

## Requirements

### Validated

(None yet - ship to validate)

### Active

- [ ] Staff users can log in as Admin or Librarian.
- [ ] Staff users can manage book records.
- [ ] Staff users can manage member records.
- [ ] Staff users can create borrowing transactions.
- [ ] Staff users can process returning transactions.
- [ ] The system tracks due dates for borrowed books.
- [ ] The system calculates fines for overdue returns.

### Out of Scope

- Member self-service portal - v1 treats members as records, not application users.
- Public library branch management - this is scoped as a university coursework system.
- Advanced reporting and analytics - circulation correctness is more important for v1.
- Online payment processing for fines - fine calculation is in scope, payment collection is not.

## Context

- This project is for university coursework, so the implementation should be understandable, demonstrable, and scoped tightly enough to complete.
- The chosen technology stack is Spring Boot for the backend, MySQL for persistence, and Thymeleaf for server-rendered views.
- The application should prioritize staff workflows over public-facing discovery features.
- The main domain entities are books, members, borrow transactions, return transactions, due dates, and fines.
- Authentication is required for staff roles, with Admin and Librarian as the v1 role model.

## Constraints

- **Tech stack**: Use Spring Boot, MySQL, and Thymeleaf - these are explicitly required for the coursework project.
- **Scope**: Focus v1 on circulation core - books, members, borrow, return, due dates, and fine calculation.
- **Audience**: Staff-facing system for Admin and Librarian users - members are records in v1.
- **Complexity**: Keep the system coursework-appropriate - avoid enterprise features that obscure the core domain.

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| Build as a staff-facing web app | The confirmed v1 access model is Admin + Librarian; members do not need accounts yet. | - Pending |
| Prioritize circulation core | Borrowing, returning, due dates, and fines are the project value. | - Pending |
| Use Spring Boot + MySQL + Thymeleaf | The user specified this technology stack for the coursework project. | - Pending |

## Evolution

This document evolves at phase transitions and milestone boundaries.

**After each phase transition** (via `$gsd-transition`):
1. Requirements invalidated? -> Move to Out of Scope with reason
2. Requirements validated? -> Move to Validated with phase reference
3. New requirements emerged? -> Add to Active
4. Decisions to log? -> Add to Key Decisions
5. "What This Is" still accurate? -> Update if drifted

**After each milestone** (via `$gsd-complete-milestone`):
1. Full review of all sections
2. Core Value check - still the right priority?
3. Audit Out of Scope - reasons still valid?
4. Update Context with current state

---
*Last updated: 2026-06-09 after initialization*
