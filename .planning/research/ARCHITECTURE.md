# Architecture Research

**Domain:** Library Management System coursework web app
**Researched:** 2026-06-09
**Confidence:** HIGH

## Standard Architecture

### System Overview

```text
Browser
  |
  v
Spring MVC Controllers
  |
  v
Application Services
  |
  v
Spring Data JPA Repositories
  |
  v
MySQL Database

Thymeleaf Templates render pages returned by MVC controllers.
Spring Security protects routes and controls Admin/Librarian access.
```

### Component Responsibilities

| Component | Responsibility | Typical Implementation |
|-----------|----------------|------------------------|
| Controllers | Handle HTTP requests, bind forms, choose views. | `@Controller` classes under `web` or feature packages. |
| Services | Own business rules and transactions. | `@Service` classes such as `BorrowingService` and `FineService`. |
| Repositories | Persist and query entities. | Spring Data JPA interfaces. |
| Entities | Represent database model. | JPA `@Entity` classes for Book, Member, Loan, User, Role. |
| Templates | Render staff UI pages. | Thymeleaf files under `src/main/resources/templates`. |
| Security configuration | Login, logout, role restrictions. | Spring Security configuration class plus user persistence. |

## Recommended Project Structure

```text
src/main/java/.../library/
├── LibraryManagementApplication.java
├── config/
│   └── SecurityConfig.java
├── book/
│   ├── Book.java
│   ├── BookRepository.java
│   ├── BookService.java
│   └── BookController.java
├── member/
│   ├── Member.java
│   ├── MemberRepository.java
│   ├── MemberService.java
│   └── MemberController.java
├── circulation/
│   ├── Loan.java
│   ├── LoanRepository.java
│   ├── CirculationService.java
│   ├── FineService.java
│   └── CirculationController.java
├── user/
│   ├── User.java
│   ├── Role.java
│   ├── UserRepository.java
│   └── UserService.java
└── common/
    └── exception/

src/main/resources/
├── templates/
│   ├── layout/
│   ├── auth/
│   ├── books/
│   ├── members/
│   └── circulation/
├── static/
│   ├── css/
│   └── js/
└── application.properties
```

### Structure Rationale

- **Feature packages:** Keep entity, repository, service, controller, and forms near the domain they serve.
- **circulation:** Borrowing, returning, due dates, and fines are tightly related and should share one service boundary.
- **user/config:** Security concerns should stay separate from circulation logic.
- **templates grouped by feature:** Makes Thymeleaf screens easy to find and demonstrate.

## Architectural Patterns

### Pattern 1: Service Owns Transaction Rules

**What:** Controllers delegate borrowing and returning to service methods.
**When to use:** Always for circulation actions.
**Trade-offs:** Adds a class layer, but keeps business rules testable.

```java
@Transactional
public Loan borrowBook(Long bookId, Long memberId, LocalDate dueDate) {
    // validate availability, create active loan, decrement available copies
}
```

### Pattern 2: Fine Calculation as a Dedicated Service

**What:** Fine calculation lives in a small service with deterministic inputs.
**When to use:** Fine rules are explicit requirements and need tests.
**Trade-offs:** Slightly more structure, much easier to validate.

```java
public BigDecimal calculateFine(LocalDate dueDate, LocalDate returnDate) {
    // if returnDate is after dueDate, days overdue * daily rate
}
```

### Pattern 3: Form DTOs for Web Input

**What:** Use form objects for create/update pages instead of binding directly to entities.
**When to use:** Forms with validation, IDs, dates, or role-limited fields.
**Trade-offs:** More classes, but avoids accidental entity mutation from web input.

## Data Flow

### Borrow Flow

```text
Librarian opens borrow form
  -> Controller validates selected book/member
  -> CirculationService checks book availability
  -> Loan is created with BORROWED status and due date
  -> Book available copy count decreases
  -> Thymeleaf displays confirmation/list
```

### Return Flow

```text
Librarian selects active loan
  -> Controller submits return date
  -> CirculationService loads loan
  -> FineService calculates overdue fine
  -> Loan is marked RETURNED with return date and fine amount
  -> Book available copy count increases
  -> Thymeleaf displays return result
```

### Key Data Flows

1. **Book availability:** Book total/available copies update when borrow and return transactions complete.
2. **Loan status:** Active loans are queryable for return workflows; returned loans remain historical records.
3. **Fine calculation:** Return date and due date determine fine; the calculated fine is stored on the loan record for auditability.

## Scaling Considerations

| Scale | Architecture Adjustments |
|-------|--------------------------|
| Coursework/demo | Single Spring Boot app and MySQL database are sufficient. |
| Department library | Add indexes for ISBN/code, member ID, loan status, and due date. |
| Large institution | Consider audit logging, notification jobs, reporting tables, and deployment separation. |

### Scaling Priorities

1. **First bottleneck:** Slow transaction lists. Add pagination and indexes.
2. **Second bottleneck:** Reporting queries. Keep reports separate from core circulation actions.

## Anti-Patterns

### Anti-Pattern 1: Controller-Heavy Business Logic

**What people do:** Put borrow/return/fine logic directly in controller methods.
**Why it's wrong:** Hard to test and easy to duplicate.
**Do this instead:** Put rules in `CirculationService` and `FineService`.

### Anti-Pattern 2: Separate Return Entity Without Loan Link

**What people do:** Create return transactions that are not tied to the original loan.
**Why it's wrong:** Makes status, due date, and fine calculation inconsistent.
**Do this instead:** Treat return processing as an update to an active loan, optionally with return metadata.

### Anti-Pattern 3: Deriving Availability Only From Counts Without Transaction Validation

**What people do:** Manually edit available copies and ignore active loans.
**Why it's wrong:** Counts drift from actual circulation state.
**Do this instead:** Update availability only inside borrow/return service transactions.

## Integration Points

### External Services

| Service | Integration Pattern | Notes |
|---------|---------------------|-------|
| MySQL | JDBC DataSource managed by Spring Boot | Configure URL, username, password, and dialect through properties. |
| Browser UI | Thymeleaf MVC | Render forms and tables server-side. |

### Internal Boundaries

| Boundary | Communication | Notes |
|----------|---------------|-------|
| Book ↔ Circulation | Service/repository calls | Circulation updates availability transactionally. |
| Member ↔ Circulation | Service/repository calls | Borrowing validates member exists and is eligible. |
| Security ↔ Web | Route authorization | Admin/Librarian role checks should protect staff pages. |

## Sources

- https://docs.spring.io/spring-boot/reference/index.html - Spring Boot reference documentation and web/data/security capabilities.
- https://www.thymeleaf.org/documentation - Thymeleaf Spring integration.
- Project context from `.planning/PROJECT.md`.

---
*Architecture research for: Library Management System*
*Researched: 2026-06-09*
