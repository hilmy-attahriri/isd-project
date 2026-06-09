# Pitfalls Research

**Domain:** Library Management System coursework web app
**Researched:** 2026-06-09
**Confidence:** HIGH

## Critical Pitfalls

### Pitfall 1: Book Availability Drift

**What goes wrong:**
Available copy counts stop matching active borrow transactions.

**Why it happens:**
Developers update book counts manually in multiple places or forget to reverse counts on return.

**How to avoid:**
Only change availability inside `CirculationService` methods that create borrow transactions or process returns. Wrap those methods in database transactions.

**Warning signs:**
Controllers directly call `book.setAvailableCopies(...)`, or tests do not verify availability before and after borrow/return.

**Phase to address:**
Borrowing and returning workflow phases.

---

### Pitfall 2: Fine Calculation Is Not Deterministic

**What goes wrong:**
Fine values differ depending on when the page is viewed, or negative fines appear for early returns.

**Why it happens:**
Fine calculation is mixed into view logic or scattered across controllers.

**How to avoid:**
Create `FineService` with clear inputs: due date, return date, and daily rate. Store the calculated fine on return.

**Warning signs:**
Thymeleaf templates contain fine formulas, or the code uses current date when processing a completed return.

**Phase to address:**
Return and fine phase.

---

### Pitfall 3: Returning Without an Active Loan

**What goes wrong:**
Staff can return a book that was not borrowed, return the same loan twice, or create disconnected return records.

**Why it happens:**
The model treats borrow and return as unrelated CRUD records.

**How to avoid:**
Represent circulation as a loan with status. A return updates an active loan to returned and records return date and fine.

**Warning signs:**
Return form asks only for book ID/member ID and does not select an active loan.

**Phase to address:**
Circulation model and return workflow phases.

---

### Pitfall 4: Role Checks Are Only Visual

**What goes wrong:**
Buttons are hidden in the UI, but unauthorized users can still access URLs directly.

**Why it happens:**
Authorization is implemented only in Thymeleaf templates.

**How to avoid:**
Use Spring Security route/method authorization. Template visibility is only a UX aid.

**Warning signs:**
No security configuration protects `/books`, `/members`, or `/circulation` routes.

**Phase to address:**
Authentication and authorization phase.

---

### Pitfall 5: Date Handling Is Too Loose

**What goes wrong:**
Due dates can be before borrow dates, return dates can be before borrow dates, and fines become nonsensical.

**Why it happens:**
Forms accept dates without validation and services trust submitted values.

**How to avoid:**
Validate date ordering in services and form validation. Use `LocalDate` for library circulation dates.

**Warning signs:**
No tests cover early return, on-time return, overdue return, or invalid date ordering.

**Phase to address:**
Borrowing and returning workflow phases.

## Technical Debt Patterns

| Shortcut | Immediate Benefit | Long-term Cost | When Acceptable |
|----------|-------------------|----------------|-----------------|
| Hard-code fine rate in multiple controllers | Fast demo | Inconsistent fine values | Never; centralize in `FineService` or config. |
| Use one giant controller | Fewer files | Hard to test and maintain | Only for a tiny prototype, not final coursework. |
| Skip service tests | Faster initial build | Circulation bugs survive until demo | Never for borrow/return/fine rules. |
| Bind forms directly to entities | Less boilerplate | Accidental field changes and weak validation | Acceptable for very simple read-only forms only. |

## Integration Gotchas

| Integration | Common Mistake | Correct Approach |
|-------------|----------------|------------------|
| MySQL + JPA | Relying on automatic schema updates for final demo | Use controlled schema settings and stable sample data. |
| Thymeleaf forms | Losing validation errors after redirect | Use binding results on failed validation; redirect only after success. |
| Spring Security | Storing plaintext passwords | Use password encoding and seeded demo users. |

## Performance Traps

| Trap | Symptoms | Prevention | When It Breaks |
|------|----------|------------|----------------|
| No pagination on transactions | Slow loan list pages | Add pagination for loans/history | Hundreds to thousands of rows |
| No indexes on status/due date | Slow overdue lookup | Index status and due date | When loan history grows |
| N+1 entity loading | Many queries per list page | Use careful fetches or DTO queries | Larger book/member lists |

## Security Mistakes

| Mistake | Risk | Prevention |
|---------|------|------------|
| Staff routes unprotected | Anyone can modify circulation records | Require authenticated Admin/Librarian role. |
| Plaintext passwords | Credential compromise | Use Spring Security password encoding. |
| Trusting hidden form fields | Users can alter IDs or fine amounts | Recalculate and validate server-side. |
| Missing CSRF protection | Cross-site form submissions | Keep Spring Security CSRF protection enabled for forms. |

## UX Pitfalls

| Pitfall | User Impact | Better Approach |
|---------|-------------|-----------------|
| Borrow form lists unavailable books | Staff creates invalid transactions | Filter or clearly mark unavailable books. |
| Return workflow requires manual fine entry | Error-prone and inconsistent | Calculate fine automatically and display result. |
| No active-loan search | Staff cannot find what to return | Provide active loan list/search by member/book. |
| Dense forms without validation messages | Demo looks broken when invalid input happens | Show field-level validation feedback. |

## "Looks Done But Isn't" Checklist

- [ ] **Borrowing:** Verify available copies decrease and cannot go below zero.
- [ ] **Returning:** Verify the same loan cannot be returned twice.
- [ ] **Fine calculation:** Verify early, on-time, one-day overdue, and multi-day overdue returns.
- [ ] **Authorization:** Verify anonymous users cannot access staff pages.
- [ ] **Validation:** Verify invalid date ordering is rejected server-side.

## Recovery Strategies

| Pitfall | Recovery Cost | Recovery Steps |
|---------|---------------|----------------|
| Availability drift | MEDIUM | Recompute available copies from active loans; centralize updates in service. |
| Fine inconsistency | LOW | Move formula to `FineService`; update tests and templates. |
| Disconnected returns | HIGH | Refactor return records into loan status updates. |
| Weak route security | MEDIUM | Add Spring Security config and route tests/manual checks. |

## Pitfall-to-Phase Mapping

| Pitfall | Prevention Phase | Verification |
|---------|------------------|--------------|
| Availability drift | Borrowing workflow, returning workflow | Borrow/return tests assert copy counts. |
| Fine inconsistency | Return and fine calculation | Fine service tests cover date cases. |
| Disconnected returns | Circulation domain model | Return action requires active loan ID. |
| Visual-only security | Authentication and staff access | Anonymous access redirects to login; roles enforced. |
| Loose date handling | Borrowing and returning workflow | Invalid date tests and form validation. |

## Sources

- Project context from `.planning/PROJECT.md`.
- Official Spring Boot documentation for MVC, data access, and security concerns.
- Common circulation workflow failure modes from LMS domain modeling.

---
*Pitfalls research for: Library Management System*
*Researched: 2026-06-09*
