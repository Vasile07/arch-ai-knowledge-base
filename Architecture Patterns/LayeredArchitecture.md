# Layered Architecture

## Overview

**Layered Architecture** is one of the most widely used software architecture patterns, organizing an application into distinct layers, each with a specific responsibility. Each layer provides services to the layer above it while relying on the layer below it, promoting separation of concerns and maintainability.

The most common implementation consists of four layers:

- Presentation Layer
- Application (Service) Layer
- Domain (Business) Layer
- Data Access (Persistence) Layer

This architecture is particularly suitable for business applications with well-defined workflows and is often used as the internal structure of Modular Monoliths and Microservices.

---

## Core Principles

- Separation of concerns.
- Clear responsibility for each layer.
- Dependency flows downward through the layers.
- Business logic remains independent of presentation and persistence.
- Layers communicate only with adjacent layers.
- Each layer exposes well-defined interfaces.

---

## Architecture

A typical Layered Architecture consists of the following layers:

### Presentation Layer

Responsible for interacting with users or external clients.

Responsibilities include:

- User interfaces
- REST APIs
- GraphQL endpoints
- Input validation
- Request handling
- Response formatting

This layer should contain little or no business logic.

---

### Application Layer

Coordinates application workflows and business use cases.

Responsibilities include:

- Executing use cases
- Orchestrating business operations
- Transaction management
- Calling domain services
- Authorization checks
- Integration with external services

The Application Layer acts as a bridge between the Presentation Layer and the Domain Layer.

---

### Domain Layer

Contains the core business logic of the application.

Responsibilities include:

- Business rules
- Domain models
- Entities
- Value objects
- Domain services
- Business validation

This layer represents the heart of the application and should be independent of infrastructure concerns.

---

### Data Access Layer

Responsible for persisting and retrieving data.

Responsibilities include:

- Database access
- Repository implementations
- ORM configuration
- SQL queries
- External storage access

This layer should not contain business logic.

---

## Advantages

### Clear Separation of Responsibilities

Each layer has a well-defined purpose, making the architecture easier to understand and maintain.

### Maintainability

Changes within one layer often have minimal impact on other layers, provided interfaces remain stable.

### Reusability

Business logic can be reused by multiple presentation interfaces, such as web applications, mobile applications, or APIs.

### Testability

Individual layers can be tested independently using mocks or stubs.

### Familiarity

Layered Architecture is well understood by developers and supported by many frameworks.

### Simplicity

Its straightforward structure makes it suitable for a wide range of enterprise applications.

---

## Disadvantages

### Performance Overhead

Requests must pass through multiple layers, potentially adding unnecessary processing for simple operations.

### Risk of Anemic Domain Models

Business logic may become scattered across service layers instead of residing within the domain model.

### Tight Dependency Flow

Strict layer dependencies can make certain cross-cutting concerns more difficult to implement efficiently.

### Reduced Flexibility

Complex applications may require exceptions to strict layer boundaries, increasing architectural complexity.

### Potential for Large Service Layers

Without careful design, the Application Layer can become overloaded with business logic.

---

## Suitable When

Layered Architecture is a good choice when:

- Building traditional business applications.
- Requirements are well understood.
- Development teams prefer a familiar architectural style.
- Maintainability is a priority.
- Applications have relatively straightforward business workflows.
- A clear separation between UI, business logic, and persistence is desired.

---

## Avoid When

This pattern may be less suitable when:

- Applications require highly flexible dependency management.
- Complex domain logic benefits from Domain-Driven Design (DDD) or Hexagonal Architecture.
- Performance is critical and unnecessary abstraction should be minimized.
- Business workflows are heavily event-driven.
- Large distributed systems require service autonomy.

---

## SaaS Considerations

Layered Architecture provides a structured foundation for many cloud-native SaaS applications.

### Multi-tenancy

Tenant resolution is often performed in the Presentation or Application Layer, while the Domain Layer remains tenant-aware without depending on infrastructure.

### Authentication and Authorization

Authentication is typically handled in the Presentation Layer, while authorization decisions are enforced within the Application Layer.

### Billing

Billing functionality can be implemented as independent services within the Application Layer while keeping billing rules inside the Domain Layer.

### Deployment

Layered applications can be deployed as monolithic applications or used internally within individual microservices.

### Scalability

Although Layered Architecture itself does not improve scalability, it provides a maintainable structure that can later evolve into more advanced architectures.

---

## Quality Attributes

| Quality Attribute | Impact |
|-------------------|--------|
| Maintainability | High |
| Scalability | Medium |
| Performance | Medium |
| Availability | Medium |
| Security | High |
| Simplicity | High |
| Operational Cost | Low |

---

## Common Technologies

Layered Architecture is commonly implemented using:

- Spring Boot
- ASP.NET Core
- NestJS
- Django
- Laravel
- Express.js
- PostgreSQL
- MySQL
- SQL Server

---

## Typical Request Flow

A typical request follows these steps:

1. A client sends a request to the Presentation Layer.
2. The Presentation Layer validates the request.
3. The request is forwarded to the Application Layer.
4. The Application Layer coordinates the business use case.
5. The Domain Layer executes business rules.
6. The Data Access Layer retrieves or stores data.
7. The response propagates back through the layers to the client.

---

## Comparison with Hexagonal Architecture

| Aspect | Layered Architecture | Hexagonal Architecture |
|---------|----------------------|-------------------------|
| Dependency Direction | Top-down | Toward the domain |
| Infrastructure Coupling | Moderate | Low |
| Testability | High | Very High |
| Flexibility | Medium | High |
| Learning Curve | Low | Higher |
| Framework Dependence | Moderate | Low |
| Domain Isolation | Moderate | Very High |

---

## Best Practices

- Keep responsibilities clearly separated between layers.
- Avoid placing business logic in controllers or repositories.
- Keep the Domain Layer independent of frameworks.
- Use interfaces to reduce coupling between layers.
- Minimize direct dependencies across multiple layers.
- Apply dependency injection where appropriate.
- Prevent layers from bypassing established architectural boundaries.
- Keep controllers lightweight and focused on request handling.

---

## Common Challenges

- Business logic leaking into controllers.
- Large service classes with multiple responsibilities.
- Tight coupling between layers.
- Repeated data mapping between layers.
- Over-engineering simple applications.
- Maintaining clear boundaries as applications grow.

---

## Related Patterns

- Modular Monolith
- Hexagonal Architecture
- Microservices
- Event-Driven Architecture

---

## Related Quality Attributes

- Maintainability
- Security
- Simplicity
- Performance

---

## Summary

Layered Architecture structures an application into distinct layers, each responsible for a specific aspect of the system. Its simplicity, familiarity, and clear separation of concerns make it one of the most widely adopted architectural patterns for enterprise software. It is particularly effective for cloud-native SaaS applications with well-defined business processes and often serves as the internal architectural style of Modular Monoliths and individual Microservices. While it may not offer the flexibility of more advanced patterns such as Hexagonal Architecture, it provides a strong and maintainable foundation for many business applications.