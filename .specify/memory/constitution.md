# spring-petclinic-app Constitution

## Core Principles

### I. Modular Monolith Architecture
Every feature must be developed within the established modular monolith structure. Components should be logically grouped and adhere to the layered architecture (Controller, Repository, Domain, Configuration). Dependencies between modules must be explicit and managed to maintain loose coupling where possible, while acknowledging the inherent tight coupling of server-side rendering with controller-returned model attributes.

### II. Data Integrity and Business Rules Enforcement
All business rules, as defined in the concept file, MUST be strictly enforced. This includes:
- "A Pet must always belong to exactly one Owner."
- "A Visit must always be associated with exactly one Pet."
- "A Pet must have a valid PetType at registration."
- "An Owner must have a valid telephone number and address before registration is complete."
- "Veterinarian specialty assignments are optional (zero or many per vet)."
- "Visit records must not be deleted once created, only appended to."
Validation will primarily leverage Jakarta Bean Validation annotations embedded within domain classes.

### III. Test-First Development (NON-NEGOTIABLE)
Test-Driven Development (TDD) is mandatory for all new features and bug fixes. The Red-Green-Refactor cycle MUST be strictly enforced. Unit tests should cover individual components, while integration tests will focus on interactions between layers and with external dependencies (databases, caching).

### IV. Database Profile Management
The application supports multiple database profiles (H2, MySQL, PostgreSQL). Development and testing MUST utilize the appropriate profile. The default H2 in-memory profile is for rapid development and testing only and is NOT representative of production data persistence behavior. Versioned database scripts or Spring Data JPA/Hibernate DDL management MUST be used for schema evolution.

### V. Observability and Caching
The application MUST expose health checks and metrics via Spring Boot Actuator and Micrometer. A caching layer is applied at the service layer for veterinarian lookups, which is managed by `CacheConfiguration.java`. This caching mechanism MUST be documented and its behavior understood by developers.

## Scope and Constraints

### In Scope
- Owner registration and management.
- Pet registration and record-keeping.
- Veterinarian directory and specialty management.
- Visit scheduling and visit history tracking.
- Basic clinic administration via web UI.

### Out of Scope
- Billing/invoicing.
- Payment processing.
- Inventory/pharmacy management.
- Insurance claims processing.
- Multi-clinic/multi-location management.

### Sensitive Data Handling
Owner records, specifically name, address, and telephone number fields, are considered sensitive. Access and handling of this data MUST comply with relevant privacy regulations.

### Technology Stack
- Java
- Spring Boot
- Spring Data JPA
- Thymeleaf (for server-side rendering)
- H2, MySQL, PostgreSQL (database profiles)
- Maven Wrapper / Gradle Wrapper
- GitHub Actions CI

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to this constitution, code quality, test coverage, and adherence to established architectural patterns.

### Testing Gates
Successful execution of all unit and integration tests is a mandatory quality gate for merging code. Specific integration tests are defined for database profiles (e.g., `MySqlIntegrationTests`, `PostgresIntegrationTests`).

### Dependency Management
Dependencies MUST be managed via Maven Wrapper or Gradle Wrapper. New dependencies MUST be carefully evaluated for necessity and potential impact on the project's architecture and maintainability.

## Governance
This constitution supersedes all other development practices for the `spring-petclinic-app` repository. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments must include a migration plan to ensure existing code and practices are updated accordingly. All pull requests and code reviews must verify compliance with this constitution. Complexity must always be justified.

**Version**: 1.0.0 | **Ratified**: 2026-09-10 | **Last Amended**: 2026-09-10