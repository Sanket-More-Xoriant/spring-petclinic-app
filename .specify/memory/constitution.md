# Sanket-More-Xoriant/spring-petclinic-app Constitution

## Core Principles

### I. Domain Integrity and Business Rules
Every feature MUST adhere to the following core business rules:
- A Pet MUST always belong to exactly one Owner.
- A Visit MUST always be associated with exactly one Pet.
- A Pet MUST have a valid PetType at registration.
- An Owner MUST have a valid telephone number and address before registration is complete.
- Veterinarian specialty assignments are optional (zero or many per vet).
- Visit records MUST NOT be deleted once created; they can only be appended to.

### II. Modular Monolith Architecture
The application MUST be structured as a Modular Monolith. Server-side rendering (Thymeleaf) is tightly coupled to controller-returned model attributes. Validation relies on Jakarta Bean Validation annotations embedded directly in domain classes. A caching layer is applied at the service layer for veterinarian lookups.

### III. Data Persistence and Profiles
The application MUST support multiple database profiles (H2, MySQL, PostgreSQL) managed via Spring profiles. Database schema management MUST utilize Spring Data JPA/Hibernate DDL or versioned scripts. The default H2 in-memory profile is for development and testing and MUST NOT be used for production data volume or persistence behavior.

### IV. Test Coverage and Quality
Comprehensive unit and integration tests MUST be maintained. Tests MUST cover core domain logic, controller interactions, and repository operations. Specific integration tests MUST exist for database profile variations (e.g., `MySqlIntegrationTests`, `PostgresIntegrationTests`).

### V. Observability and Configuration
The application MUST expose health checks and metrics via Spring Boot Actuator and Micrometer. Internationalization (i18n) support MUST be configured via `WebConfiguration`, with mechanisms for locale resolution and language change interceptors.

## Out of Scope Governance

The following functionalities are explicitly out of scope for this project and MUST NOT be implemented:
- Billing/invoicing
- Payment processing
- Inventory/pharmacy management
- Insurance claims processing
- Multi-clinic/multi-location management

## Development Workflow and Practices

### Code Reviews
All Pull Requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to this constitution, including domain integrity, architectural principles, and test coverage.

### Dependency Management
The project MUST use Maven Wrapper or Gradle Wrapper scripts for consistent build environment setup. Dependencies MUST be managed through the build tool.

### Sensitive Data Handling
Owner records (name, address, telephone number fields) are considered sensitive zones. Access and handling of this data MUST be carefully considered and secured.

## Governance

This constitution supersedes all other practices for the Sanket-More-Xoriant/spring-petclinic-app repository. Amendments to this constitution require formal documentation, team approval, and a migration plan for affected code. All Pull Requests and code reviews MUST verify compliance with this constitution. Complexity MUST be justified.

**Version**: 1.0.0 | **Ratified**: 2026-09-10 | **Last Amended**: 2026-09-10