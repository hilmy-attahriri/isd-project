# Feature Research

**Domain:** Library Management System coursework web app
**Researched:** 2026-06-09
**Confidence:** HIGH

## Feature Landscape

### Table Stakes (Users Expect These)

| Feature | Why Expected | Complexity | Notes |
|---------|--------------|------------|-------|
| Staff authentication | Staff-only systems need protected access. | MEDIUM | Admin and Librarian roles are enough for v1. |
| Book management | Library systems must track catalog records. | LOW | Include title, author, ISBN/code, category, total copies, available copies. |
| Member management | Borrowing requires identifying borrowers. | LOW | Members are records, not login users in v1. |
| Borrowing transaction | Core circulation workflow. | MEDIUM | Must reduce availability and record borrow date, due date, member, book, and status. |
| Returning transaction | Completes circulation and restores availability. | MEDIUM | Must record return date and calculate fine if overdue. |
| Due date tracking | Required to know when a loan is overdue. | LOW | Can be derived from borrow date plus loan period. |
| Fine calculation | Explicitly requested and common for overdue returns. | MEDIUM | Use a clear daily rate and avoid negative fines. |
| Search/list screens | Staff need to find books, members, and transactions quickly. | LOW | Basic keyword search is enough for coursework. |

### Differentiators (Competitive Advantage)

| Feature | Value Proposition | Complexity | Notes |
|---------|-------------------|------------|-------|
| Overdue dashboard | Helps librarians see what needs action. | LOW | Good v1.x enhancement after core transactions. |
| Role-specific navigation | Makes Admin/Librarian separation visible in demo. | LOW | Useful if assignment evaluates authorization. |
| Printable borrowing/return receipt | Strong demo feature. | MEDIUM | Can be a simple Thymeleaf receipt page. |
| Fine policy settings | Lets staff change fine rate and loan period. | MEDIUM | Defer unless coursework requires configurability. |

### Anti-Features (Commonly Requested, Often Problematic)

| Feature | Why Requested | Why Problematic | Alternative |
|---------|---------------|-----------------|-------------|
| Full member portal | Sounds complete and user-friendly. | Adds authentication, member UX, and extra authorization paths. | Keep members as records for v1. |
| Online fine payment | Completes the fine workflow. | Adds payment integration and security/compliance concerns. | Calculate and display fine only. |
| Barcode scanner integration | Real libraries often use scanners. | Hardware and browser integration distract from coursework goals. | Support manual book code/ISBN entry. |
| Multi-branch inventory | Common in public libraries. | Adds location, transfer, and branch permission complexity. | Single library inventory for v1. |

## Feature Dependencies

```text
Staff authentication
    -> protects -> Book management
    -> protects -> Member management
    -> protects -> Circulation workflows

Book management
    -> required by -> Borrowing transaction
    -> required by -> Returning transaction

Member management
    -> required by -> Borrowing transaction
    -> required by -> Returning transaction

Borrowing transaction
    -> creates -> Due date
    -> required by -> Returning transaction

Returning transaction
    -> uses -> Due date
    -> produces -> Fine calculation
```

### Dependency Notes

- **Borrowing requires books and members:** A transaction cannot be created without valid member and book records.
- **Returning requires an active loan:** Returns should target an existing borrowed transaction, not create a disconnected record.
- **Fine calculation requires due date and return date:** Fine rules should live in a service so they are testable.

## MVP Definition

### Launch With (v1)

- [ ] Staff login with Admin/Librarian roles - protects the system and satisfies the confirmed access model.
- [ ] Book CRUD - needed before any borrowing can happen.
- [ ] Member CRUD - needed before any borrowing can happen.
- [ ] Borrow book - core circulation behavior.
- [ ] Return book - core circulation behavior.
- [ ] Due date tracking - required for overdue detection.
- [ ] Fine calculation - explicitly requested and important for demo value.

### Add After Validation (v1.x)

- [ ] Overdue list/dashboard - useful once loan data exists.
- [ ] Borrowing history filters - useful after transactions accumulate.
- [ ] Fine paid/unpaid tracking - useful if coursework expands beyond calculation.

### Future Consideration (v2+)

- [ ] Member portal - defer until staff workflow is complete.
- [ ] Email notifications - defer because email setup adds infrastructure.
- [ ] Multi-branch inventory - defer because this is a university coursework system.
- [ ] Barcode scanner support - defer unless required by the assignment.

## Feature Prioritization Matrix

| Feature | User Value | Implementation Cost | Priority |
|---------|------------|---------------------|----------|
| Staff authentication | HIGH | MEDIUM | P1 |
| Book management | HIGH | LOW | P1 |
| Member management | HIGH | LOW | P1 |
| Borrowing transaction | HIGH | MEDIUM | P1 |
| Returning transaction | HIGH | MEDIUM | P1 |
| Due date tracking | HIGH | LOW | P1 |
| Fine calculation | HIGH | MEDIUM | P1 |
| Overdue dashboard | MEDIUM | LOW | P2 |
| Member portal | MEDIUM | HIGH | P3 |

## Competitor Feature Analysis

| Feature | Typical LMS | Coursework LMS | Our Approach |
|---------|-------------|----------------|--------------|
| Catalog management | Rich metadata and search | Basic book CRUD | Keep required fields simple and searchable. |
| Circulation | Borrow, return, renew, reserve | Borrow and return | Implement borrow/return first; defer renew/reserve. |
| Member accounts | Member login and profile | Staff-managed member records | Staff-only v1. |
| Fines | Configurable policies and payments | Calculated overdue amount | Calculate amount; defer payment. |

## Sources

- Project context from `.planning/PROJECT.md`.
- Common library circulation workflows: catalog, patron/member records, loan, return, overdue, fine.
- Official Spring Boot, Thymeleaf, and MySQL docs referenced in `STACK.md`.

---
*Feature research for: Library Management System*
*Researched: 2026-06-09*
