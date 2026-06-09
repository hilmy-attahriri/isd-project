# Library Management System

Library Management System is a university coursework project for managing core library circulation workflows with Spring Boot, MySQL, and Thymeleaf.

The repository currently contains an early Spring Boot backend starter with a book REST endpoint and JPA repository. The planning docs in `.planning/` define the intended v1 scope: staff-facing book, member, borrowing, returning, due date, and fine management.

## Overview

This project is designed for library staff, not public member accounts. Admin and librarian users should be able to:

- manage books
- manage member records
- create borrowing transactions
- process returns
- track due dates
- calculate overdue fines

## Current State

The code that is present now includes:

- Spring Boot 3.2.5 Maven project
- Java 17 target
- MySQL-backed JPA setup
- `Book` domain model placeholder
- `BookRepository` using Spring Data JPA
- REST controller at `/api/books` for listing and creating books
- MySQL connection settings in `application.properties`

Planned but not yet implemented in the current source tree:

- Thymeleaf pages
- login and role-based access
- complete book CRUD
- member CRUD
- borrow and return workflows
- due date handling
- fine calculation

## Tech Stack

- Java 17
- Spring Boot 3.2.5
- Spring Web MVC
- Spring Data JPA
- MySQL
- Maven

## Repository Layout

```text
.
├── app/
│   └── library-management-system/
│       ├── Book.java
│       ├── BookController.java
│       ├── BookRepository.java
│       ├── application.properties
│       ├── data.sql
│       ├── main.java
│       └── pom.xml
├── .planning/
├── docs/
├── specs/
└── tests/
```

## API

Current REST endpoints:

- `GET /api/books` - returns all books
- `POST /api/books` - creates a new book

## Configuration

The application is configured to connect to a local MySQL instance using:

- database: `db_library`
- host: `localhost`
- port: `3306`
- username: `root`
- password: `root`

JPA is configured with:

- `spring.jpa.hibernate.ddl-auto=update`
- SQL logging enabled
- SQL initialization enabled

## Prerequisites

- Java 17
- Maven 3.9+
- MySQL 8.x

## Run the Project

The Spring Boot project lives in `app/library-management-system`.

```bash
cd app/library-management-system
mvn spring-boot:run
```

If you want to build the JAR instead:

```bash
cd app/library-management-system
mvn clean package
java -jar target/library-management-system-0.0.1-SNAPSHOT.jar
```

## Database Setup

Create a local MySQL database named `db_library` before starting the app:

```sql
CREATE DATABASE db_library;
```

If your local MySQL credentials differ from `root` / `root`, update:

- `app/library-management-system/application.properties`

## Development Notes

- `data.sql` currently contains commented sample seed data only.
- The current Java files are minimal and do not yet represent the full planned domain model.
- The long-term project direction is captured in `.planning/PROJECT.md`, `.planning/REQUIREMENTS.md`, and `.planning/ROADMAP.md`.

## Planned v1 Scope

The intended coursework release is a staff-facing circulation system with:

- book management
- member management
- borrow transactions
- return transactions
- due date tracking
- overdue fine calculation

## Future Work

The planning docs describe the next major steps:

- add proper package structure under `src/main/java`
- implement Thymeleaf UI pages
- add authentication and authorization
- expand the domain model beyond books
- implement borrow and return services
- add automated tests for circulation rules

## License

No license file is currently provided in the repository.
