# Research Summary

**Domain:** Library Management System coursework web app
**Researched:** 2026-06-09
**Confidence:** HIGH

## Key Findings

**Stack:** Use a single Spring Boot MVC application with Thymeleaf templates, Spring Data JPA, Spring Security, and MySQL. Official docs currently list Spring Boot 4.0.6 as stable and MySQL 8.4 as the LTS reference line, but Spring Boot 3.5.x remains a practical fallback if coursework materials are based on Spring Boot 3.

**Table Stakes:** Staff login, book CRUD, member CRUD, borrowing, returning, due dates, fine calculation, and basic search/list pages. These directly support the confirmed coursework scope.

**Watch Out For:** Keep circulation rules in services. Prevent book availability drift, require returns to target active loans, calculate fines deterministically, validate date ordering, and enforce access through Spring Security rather than only hiding buttons.

## Recommended v1 Scope

1. Staff authentication with Admin and Librarian roles.
2. Book management with total and available copy tracking.
3. Member management as staff-managed records.
4. Borrowing workflow that creates active loans and due dates.
5. Returning workflow that closes active loans and restores availability.
6. Fine calculation based on due date, return date, and daily rate.
7. Basic staff UI with Thymeleaf forms, lists, and validation messages.

## Recommended Deferred Scope

- Member portal.
- Online payment processing.
- Multi-branch inventory.
- Barcode scanner integration.
- Email notifications.
- Advanced analytics/reporting.

## Architecture Guidance

- Use feature-oriented packages for `book`, `member`, `circulation`, and `user`.
- Put borrow/return/fine rules in services, not controllers or templates.
- Model return as an update to an active loan, not as an unrelated transaction.
- Store calculated fine on the returned loan for auditability.
- Use tests for service rules because circulation bugs are easy to miss in UI-only demos.

## Source Links

- Spring Boot project page: https://spring.io/projects/spring-boot/
- Spring Boot reference: https://docs.spring.io/spring-boot/reference/index.html
- Thymeleaf documentation: https://www.thymeleaf.org/documentation
- MySQL 8.4 Reference Manual: https://dev.mysql.com/doc/refman/8.4/en/

---
*Research summary for: Library Management System*
*Researched: 2026-06-09*
