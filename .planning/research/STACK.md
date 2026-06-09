# Stack Research

**Domain:** Library Management System coursework web app
**Researched:** 2026-06-09
**Confidence:** HIGH

## Recommended Stack

### Core Technologies

| Technology | Version | Purpose | Why Recommended |
|------------|---------|---------|-----------------|
| Java | 21 LTS | Runtime and language | Stable LTS baseline for modern Spring Boot coursework and long enough support horizon. |
| Spring Boot | 4.0.6, or 3.5.x if coursework materials require Spring Boot 3 | Application framework | Official Spring docs list Spring Boot 4.0.6 as current stable. Spring Boot provides embedded server, auto-configuration, starters, security, data access, and production-ready defaults. |
| Spring Web MVC | Managed by Spring Boot | Server-rendered web controllers | Matches Thymeleaf and simple staff-facing page workflows. |
| Thymeleaf | 3.1.x | Server-rendered HTML templates | Official Thymeleaf documentation provides Spring integration for 3.1. Suitable for CRUD forms, validation errors, tables, and simple dashboards. |
| MySQL | 8.4 LTS | Relational database | Official MySQL docs identify 8.4 as the LTS reference line. A relational model fits books, members, loans, returns, roles, due dates, and fines. |

### Supporting Libraries

| Library | Version | Purpose | When to Use |
|---------|---------|---------|-------------|
| Spring Data JPA | Managed by Spring Boot | Repository and ORM layer | Use for entity persistence, relationship mapping, and standard CRUD queries. |
| Hibernate Validator / Jakarta Validation | Managed by Spring Boot | Form and entity validation | Use for required fields, ISBN formats, dates, and numeric fine inputs. |
| Spring Security | Managed by Spring Boot | Admin/Librarian authentication and authorization | Use for login, logout, password hashing, and role-based page access. |
| MySQL Connector/J | Managed by Spring Boot | JDBC driver | Required for MySQL connectivity. |
| Spring Boot DevTools | Managed by Spring Boot | Development reload support | Useful during coursework development; exclude from production packaging. |
| Bootstrap | 5.x | Basic responsive UI styling | Use for a clean coursework demo without building a custom design system. |

### Development Tools

| Tool | Purpose | Notes |
|------|---------|-------|
| Maven | Build and dependency management | Use Spring Initializr defaults for a conventional Spring Boot project. |
| Spring Initializr | Project scaffolding | Generate with Web, Thymeleaf, Data JPA, MySQL Driver, Validation, and Security. |
| MySQL Workbench or CLI | Database inspection | Useful for verifying schema and sample data during demo prep. |
| JUnit + Spring Boot Test | Automated verification | Cover services for loan rules, return processing, and fine calculation. |

## Installation

```bash
# Suggested Spring Initializr dependencies
spring-boot-starter-web
spring-boot-starter-thymeleaf
spring-boot-starter-data-jpa
spring-boot-starter-security
spring-boot-starter-validation
mysql-connector-j
spring-boot-devtools
spring-boot-starter-test
```

## Alternatives Considered

| Recommended | Alternative | When to Use Alternative |
|-------------|-------------|-------------------------|
| Thymeleaf server-rendered MVC | React/Vue frontend | Use only if the assignment explicitly requires SPA behavior; otherwise it adds avoidable complexity. |
| Spring Data JPA | Plain JDBC | Use JDBC if the course focuses on SQL fundamentals and forbids ORM. |
| MySQL 8.4 LTS | MySQL 8.0 | Use 8.0 only if the university environment has not moved to 8.4. |
| Bootstrap | Custom CSS-only UI | Use custom CSS if Bootstrap is disallowed or the assignment evaluates custom styling. |

## What NOT to Use

| Avoid | Why | Use Instead |
|-------|-----|-------------|
| Microservices | Too much infrastructure for coursework and a small circulation domain. | Single Spring Boot MVC application. |
| REST-only backend with no templates | Conflicts with the stated Thymeleaf stack. | MVC controllers returning Thymeleaf views. |
| Member portal in v1 | The confirmed access model is staff-only. | Staff records for members; defer member login. |
| Payment gateway for fines | Fine calculation is in scope, not payment collection. | Store calculated fine amount and optional paid/unpaid status later. |

## Stack Patterns by Variant

**If coursework requires current official versions:**
- Use Spring Boot 4.0.6, Java 21, and MySQL 8.4 LTS.
- Because those are current stable/LTS lines according to official docs checked on 2026-06-09.

**If coursework materials are based on Spring Boot 3:**
- Use Spring Boot 3.5.x and Java 17 or 21.
- Because many university tutorials lag behind current framework major versions, and Spring Boot 3 remains a stable teaching target.

## Version Compatibility

| Package A | Compatible With | Notes |
|-----------|-----------------|-------|
| Spring Boot 4.0.x | Java 21+ | Use the official Spring Boot requirements for the exact minor version during implementation. |
| Spring Boot starter-thymeleaf | Thymeleaf 3.1.x | Let Spring Boot manage the Thymeleaf version. |
| Spring Data JPA | Hibernate managed by Spring Boot | Let Spring Boot dependency management choose versions. |
| MySQL Connector/J | MySQL 8.4 LTS | Let Spring Boot manage connector version unless the university environment requires a specific driver. |

## Sources

- https://spring.io/projects/spring-boot/ - verified Spring Boot 4.0.6 current stable and Spring Boot purpose/features.
- https://docs.spring.io/spring-boot/reference/index.html - verified Spring Boot reference documentation and stable version list.
- https://www.thymeleaf.org/documentation - verified Thymeleaf 3.1 documentation and Spring integration material.
- https://dev.mysql.com/doc/refman/8.4/en/ - verified MySQL 8.4 Reference Manual.

---
*Stack research for: Library Management System*
*Researched: 2026-06-09*
