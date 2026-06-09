# Roadmap: Library Management System

## Overview

Build the Library Management System as a vertical MVP in six phases. The roadmap starts with a runnable, secured Spring Boot + Thymeleaf shell, then adds catalog and member records, then completes the core circulation loop through borrowing, returning, fine calculation, and final demo hardening. Each phase should leave the coursework project more demonstrable than the last.

## Phases

**Phase Numbering:**
- Integer phases (1, 2, 3): Planned milestone work
- Decimal phases (2.1, 2.2): Urgent insertions (marked with INSERTED)

Decimal phases appear between their surrounding integers in numeric order.

- [ ] **Phase 1: App Foundation and Staff Access** - Create the runnable Spring Boot MVC app with login, roles, navigation, and protected staff pages.
- [ ] **Phase 2: Book Catalog Management** - Add book CRUD, search/list screens, validation, and safe copy tracking.
- [ ] **Phase 3: Member Records Management** - Add member CRUD, search/list screens, and deletion/deactivation safeguards.
- [ ] **Phase 4: Borrowing Workflow** - Let staff create active loans for existing members and available books with due dates.
- [ ] **Phase 5: Returning and Fine Calculation** - Let staff return active loans, restore availability, and calculate/store overdue fines.
- [ ] **Phase 6: Circulation Review and Demo Hardening** - Polish dashboard, histories, validation feedback, and coursework demo verification.

## Phase Details

### Phase 1: App Foundation and Staff Access
**Goal**: A runnable Spring Boot + MySQL + Thymeleaf application exists with staff login, logout, protected pages, role-aware navigation, and a basic dashboard.
**Mode:** mvp
**Depends on**: Nothing (first phase)
**Requirements**: [AUTH-01, AUTH-02, AUTH-03, AUTH-04, UI-01]
**UI hint**: yes
**Success Criteria** (what must be TRUE):
  1. Staff user can log in and log out through Thymeleaf pages.
  2. Anonymous user is redirected to login when opening staff pages.
  3. Admin and Librarian users can reach the dashboard and circulation navigation.
  4. The application connects to MySQL and starts without manual code changes.
**Plans**: 3 plans

Plans:
- [ ] 01-01: Scaffold Spring Boot project, dependencies, configuration, and MySQL connectivity.
- [ ] 01-02: Implement staff authentication, seeded roles/users, login, logout, and route protection.
- [ ] 01-03: Build shared Thymeleaf layout, dashboard, navigation, and basic styling.

### Phase 2: Book Catalog Management
**Goal**: Staff can create, view, search, update, and safely delete book records while copy counts remain valid.
**Mode:** mvp
**Depends on**: Phase 1
**Requirements**: [BOOK-01, BOOK-02, BOOK-03, BOOK-04, BOOK-05, BOOK-06, UI-02]
**UI hint**: yes
**Success Criteria** (what must be TRUE):
  1. Staff user can create a book with required catalog and copy fields.
  2. Staff user can view, search, edit, and delete eligible books.
  3. Invalid book forms show validation messages.
  4. Available copies cannot become negative.
**Plans**: 3 plans

Plans:
- [ ] 02-01: Implement book entity, repository, service, validation, and service tests.
- [ ] 02-02: Implement book list, search, create, edit, and delete controllers.
- [ ] 02-03: Build Thymeleaf book pages with validation feedback and copy-count display.

### Phase 3: Member Records Management
**Goal**: Staff can manage member records used by circulation workflows.
**Mode:** mvp
**Depends on**: Phase 2
**Requirements**: [MEMB-01, MEMB-02, MEMB-03, MEMB-04, MEMB-05, UI-02]
**UI hint**: yes
**Success Criteria** (what must be TRUE):
  1. Staff user can create a member with identifying contact information.
  2. Staff user can view, search, and update members.
  3. Staff user can delete or deactivate only members without active borrowing transactions.
  4. Invalid member forms show validation messages.
**Plans**: 2 plans

Plans:
- [ ] 03-01: Implement member entity, repository, service, validation, and safeguards.
- [ ] 03-02: Build member list, search, create, edit, and delete/deactivate Thymeleaf workflows.

### Phase 4: Borrowing Workflow
**Goal**: Staff can create borrowing transactions for existing members and available books, with due dates and active loan tracking.
**Mode:** mvp
**Depends on**: Phase 3
**Requirements**: [BORR-01, BORR-02, BORR-03, BORR-04, BORR-05, FINE-01, FINE-02, UI-03]
**UI hint**: yes
**Success Criteria** (what must be TRUE):
  1. Staff user can borrow an available book to an existing member.
  2. System records borrow date, due date, member, book, and borrowed status.
  3. Borrowing decreases available copies exactly once.
  4. Borrowing is rejected when no copies are available or due date is invalid.
  5. Staff user can view active borrowing transactions with due dates.
**Plans**: 3 plans

Plans:
- [ ] 04-01: Implement loan model, repository, and circulation service for borrowing.
- [ ] 04-02: Add service tests for availability decrement, no-copy rejection, and due date validation.
- [ ] 04-03: Build borrowing form, active loans list, and transaction status displays.

### Phase 5: Returning and Fine Calculation
**Goal**: Staff can return active loans, prevent double returns, restore book availability, and calculate/store fines for overdue returns.
**Mode:** mvp
**Depends on**: Phase 4
**Requirements**: [RETN-01, RETN-02, RETN-03, RETN-04, RETN-05, FINE-03, FINE-04, FINE-05, UI-03]
**UI hint**: yes
**Success Criteria** (what must be TRUE):
  1. Staff user can process a return for an active loan.
  2. Returning marks the loan returned, records return date, and restores availability exactly once.
  3. The same loan cannot be returned twice.
  4. Fine calculation returns zero for early/on-time returns and positive amount for overdue returns.
  5. Staff user can view completed return history with fine values.
**Plans**: 3 plans

Plans:
- [ ] 05-01: Implement return processing and loan status transitions in circulation service.
- [ ] 05-02: Implement fine calculation service and tests for early, on-time, and overdue returns.
- [ ] 05-03: Build return workflow, return history pages, and fine display.

### Phase 6: Circulation Review and Demo Hardening
**Goal**: The complete coursework demo is coherent, validated, and ready to show end to end.
**Mode:** mvp
**Depends on**: Phase 5
**Requirements**: [UI-02, UI-03]
**UI hint**: yes
**Success Criteria** (what must be TRUE):
  1. Staff user can navigate dashboard, books, members, borrowing, and returns without broken links.
  2. Forms across v1 workflows show clear validation messages.
  3. Lists and detail pages clearly show status, due dates, and fine values.
  4. Manual demo can create a book, create a member, borrow, return, and show the resulting fine.
**Plans**: 2 plans

Plans:
- [ ] 06-01: Add dashboard polish, empty states, consistent validation feedback, and navigation cleanup.
- [ ] 06-02: Add final verification, sample data, and coursework demo checklist.

## Progress

**Execution Order:**
Phases execute in numeric order: 1 -> 2 -> 3 -> 4 -> 5 -> 6

| Phase | Plans Complete | Status | Completed |
|-------|----------------|--------|-----------|
| 1. App Foundation and Staff Access | 0/3 | Not started | - |
| 2. Book Catalog Management | 0/3 | Not started | - |
| 3. Member Records Management | 0/2 | Not started | - |
| 4. Borrowing Workflow | 0/3 | Not started | - |
| 5. Returning and Fine Calculation | 0/3 | Not started | - |
| 6. Circulation Review and Demo Hardening | 0/2 | Not started | - |

## Coverage

| Phase | Requirements |
|-------|--------------|
| Phase 1 | AUTH-01, AUTH-02, AUTH-03, AUTH-04, UI-01 |
| Phase 2 | BOOK-01, BOOK-02, BOOK-03, BOOK-04, BOOK-05, BOOK-06, UI-02 |
| Phase 3 | MEMB-01, MEMB-02, MEMB-03, MEMB-04, MEMB-05, UI-02 |
| Phase 4 | BORR-01, BORR-02, BORR-03, BORR-04, BORR-05, FINE-01, FINE-02, UI-03 |
| Phase 5 | RETN-01, RETN-02, RETN-03, RETN-04, RETN-05, FINE-03, FINE-04, FINE-05, UI-03 |
| Phase 6 | UI-02, UI-03 |

**Coverage check:** 33 v1 requirements mapped to phases. Shared UI requirements are reinforced in final hardening.
