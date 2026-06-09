# Requirements: Library Management System

**Defined:** 2026-06-09
**Core Value:** Librarians can reliably track book borrowing and returning, including due dates and fines, through a simple web interface.

## v1 Requirements

Requirements for the initial coursework release. Each requirement maps to roadmap phases.

### Authentication

- [ ] **AUTH-01**: Staff user can log in with username/email and password.
- [ ] **AUTH-02**: Staff user can log out from any authenticated page.
- [ ] **AUTH-03**: Anonymous user is redirected to login when accessing staff pages.
- [ ] **AUTH-04**: Admin and Librarian roles can access circulation workflows.

### Books

- [ ] **BOOK-01**: Staff user can create a book record with title, author, ISBN/code, category, total copies, and available copies.
- [ ] **BOOK-02**: Staff user can view a list of book records.
- [ ] **BOOK-03**: Staff user can search or filter book records by keyword.
- [ ] **BOOK-04**: Staff user can update a book record.
- [ ] **BOOK-05**: Staff user can delete a book record when it is not tied to an active borrowing transaction.
- [ ] **BOOK-06**: System prevents available copies from becoming negative.

### Members

- [ ] **MEMB-01**: Staff user can create a member record with identifying contact information.
- [ ] **MEMB-02**: Staff user can view a list of member records.
- [ ] **MEMB-03**: Staff user can search or filter member records by keyword.
- [ ] **MEMB-04**: Staff user can update a member record.
- [ ] **MEMB-05**: Staff user can delete or deactivate a member record when it is not tied to an active borrowing transaction.

### Borrowing

- [ ] **BORR-01**: Staff user can create a borrowing transaction for an existing member and available book.
- [ ] **BORR-02**: System records borrow date, due date, member, book, and transaction status.
- [ ] **BORR-03**: System decreases available copies when a borrowing transaction is created.
- [ ] **BORR-04**: System rejects borrowing when the selected book has no available copies.
- [ ] **BORR-05**: Staff user can view active borrowing transactions.

### Returning

- [ ] **RETN-01**: Staff user can process a return for an active borrowing transaction.
- [ ] **RETN-02**: System records return date and marks the borrowing transaction as returned.
- [ ] **RETN-03**: System increases available copies when a return is processed.
- [ ] **RETN-04**: System prevents the same borrowing transaction from being returned more than once.
- [ ] **RETN-05**: Staff user can view completed return history.

### Due Dates and Fines

- [ ] **FINE-01**: System assigns a due date to each borrowing transaction.
- [ ] **FINE-02**: System validates that due date is not before borrow date.
- [ ] **FINE-03**: System calculates zero fine for early or on-time returns.
- [ ] **FINE-04**: System calculates overdue fine from days overdue multiplied by a configured daily fine rate.
- [ ] **FINE-05**: System stores the calculated fine amount on the returned transaction.

### User Interface

- [ ] **UI-01**: Staff user can navigate between dashboard, books, members, borrowing, and returns pages.
- [ ] **UI-02**: Forms show validation messages when submitted data is invalid.
- [ ] **UI-03**: Lists and detail pages show transaction status, due date, and fine values clearly.

## v2 Requirements

Deferred to future release. Tracked but not in current roadmap.

### Member Portal

- **PORT-01**: Member can log in to view current loans.
- **PORT-02**: Member can search available books from a public/member-facing page.

### Notifications

- **NOTF-01**: System can notify members about overdue books.
- **NOTF-02**: System can notify staff about due-soon or overdue items.

### Reporting

- **REPT-01**: Staff user can view monthly borrowing statistics.
- **REPT-02**: Staff user can export borrowing and fine reports.

### Inventory Enhancements

- **INVN-01**: System can support barcode scanner input.
- **INVN-02**: System can support multiple library branches.

## Out of Scope

Explicitly excluded. Documented to prevent scope creep.

| Feature | Reason |
|---------|--------|
| Member self-service portal | v1 is staff-facing; members are records, not login users. |
| Online fine payment | Fine calculation is required, but payment processing adds unnecessary integration and security complexity. |
| Multi-branch inventory | This is a university coursework system focused on one library inventory. |
| Barcode scanner integration | Hardware/browser integration distracts from the core Spring Boot/MySQL/Thymeleaf coursework goals. |
| Email/SMS notifications | Useful later, but not needed to validate circulation workflows. |
| Advanced analytics | Basic circulation correctness is more important for v1. |

## Traceability

Which phases cover which requirements. Updated during roadmap creation.

| Requirement | Phase | Status |
|-------------|-------|--------|
| AUTH-01 | TBD | Pending |
| AUTH-02 | TBD | Pending |
| AUTH-03 | TBD | Pending |
| AUTH-04 | TBD | Pending |
| BOOK-01 | TBD | Pending |
| BOOK-02 | TBD | Pending |
| BOOK-03 | TBD | Pending |
| BOOK-04 | TBD | Pending |
| BOOK-05 | TBD | Pending |
| BOOK-06 | TBD | Pending |
| MEMB-01 | TBD | Pending |
| MEMB-02 | TBD | Pending |
| MEMB-03 | TBD | Pending |
| MEMB-04 | TBD | Pending |
| MEMB-05 | TBD | Pending |
| BORR-01 | TBD | Pending |
| BORR-02 | TBD | Pending |
| BORR-03 | TBD | Pending |
| BORR-04 | TBD | Pending |
| BORR-05 | TBD | Pending |
| RETN-01 | TBD | Pending |
| RETN-02 | TBD | Pending |
| RETN-03 | TBD | Pending |
| RETN-04 | TBD | Pending |
| RETN-05 | TBD | Pending |
| FINE-01 | TBD | Pending |
| FINE-02 | TBD | Pending |
| FINE-03 | TBD | Pending |
| FINE-04 | TBD | Pending |
| FINE-05 | TBD | Pending |
| UI-01 | TBD | Pending |
| UI-02 | TBD | Pending |
| UI-03 | TBD | Pending |

**Coverage:**
- v1 requirements: 33 total
- Mapped to phases: 0
- Unmapped: 33

## User Stories & Acceptance Criteria

### User Stories

- As a librarian, I can log in and manage circulation data so that only staff can change library records.
- As a librarian, I can manage books and members so that borrowing transactions use accurate records.
- As a librarian, I can borrow a book to a member so that the system tracks who has the book and when it is due.
- As a librarian, I can process a return so that book availability and transaction history stay correct.
- As a librarian, I can see overdue fines so that the library can communicate charges consistently.

### Acceptance Criteria

- Staff-only pages require authentication.
- Borrowing is only allowed when the book has available copies.
- Returning an active loan restores book availability exactly once.
- Fine calculation returns zero for early/on-time returns and positive amount for overdue returns.
- Validation errors are visible on forms.

## Definition of Done

- Spring Boot application builds and runs locally.
- MySQL persistence is configured.
- Thymeleaf pages cover the v1 staff workflows.
- Service-level tests cover borrow, return, and fine rules.
- Manual demo can create a book, create a member, borrow a book, return it, and show the resulting fine.

---
*Requirements defined: 2026-06-09*
*Last updated: 2026-06-09 after initial definition*
