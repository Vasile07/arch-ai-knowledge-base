# Multi-tenancy

## Overview

**Multi-tenancy** is a software architecture approach in which a single application instance serves multiple customers, known as **tenants**. Each tenant shares the same application while their data, configurations, and user access remain logically isolated from those of other tenants.

Multi-tenancy is one of the defining characteristics of Software-as-a-Service (SaaS) applications, enabling efficient resource utilization, simplified maintenance, and lower operational costs compared to deploying separate application instances for each customer.

A well-designed multi-tenant architecture balances resource sharing with security, scalability, performance, and tenant isolation.

---

## Core Principles

- A single application serves multiple tenants.
- Tenants share application infrastructure.
- Each tenant's data is isolated.
- Tenant context is maintained throughout each request.
- Resources are shared efficiently while preserving security.
- The application should scale as the number of tenants grows.

---

## Key Concepts

### Tenant

A tenant is an individual customer or organization using the SaaS application.

Each tenant typically has:

- Users
- Data
- Roles and permissions
- Configuration settings
- Subscription plan
- Usage limits

---

### Tenant Context

Every request processed by the application should include a tenant identifier that determines:

- Which data can be accessed
- Which configuration applies
- Which features are available
- Which authorization rules should be enforced

The tenant context is commonly derived from:

- JWT claims
- API keys
- Subdomains
- Custom domains
- Request headers

---

### Shared Infrastructure

Multiple tenants typically share:

- Application servers
- APIs
- Compute resources
- Caching infrastructure
- Monitoring systems
- Networking resources

Sharing infrastructure reduces operational costs while maximizing resource utilization.

---

## Multi-tenancy Models

### Shared Database, Shared Schema

All tenants share the same database and the same tables.

Each record contains a tenant identifier.

Example:

```
Customers
-------------------------
Id
TenantId
Name
Email
```

#### Advantages

- Lowest infrastructure cost
- Simplest deployment
- Easy scaling
- Efficient resource utilization

#### Disadvantages

- Strong application-level isolation required
- Higher risk of accidental data leakage
- More complex query filtering

---

### Shared Database, Separate Schemas

All tenants share the same database but each tenant has its own database schema.

#### Advantages

- Better logical isolation
- Easier tenant backup and migration
- Reduced risk of cross-tenant queries

#### Disadvantages

- More administrative overhead
- Database complexity increases as tenants grow

---

### Separate Database per Tenant

Each tenant has its own database.

#### Advantages

- Strong data isolation
- Simplified backup and restore
- Easier regulatory compliance
- Independent database scaling

#### Disadvantages

- Higher operational costs
- More infrastructure to manage
- More complex provisioning

---

### Separate Application per Tenant

Each tenant has an independent deployment.

#### Advantages

- Complete isolation
- Independent customization
- Independent scaling
- Maximum security

#### Disadvantages

- Highest infrastructure cost
- Complex deployment management
- Limited resource sharing

This approach is sometimes used for enterprise customers with strict compliance or security requirements.

---

## Advantages

### Efficient Resource Utilization

Infrastructure is shared among tenants, reducing unused capacity.

### Lower Operational Costs

Hosting a single application is generally less expensive than maintaining separate deployments for each customer.

### Simplified Maintenance

Application updates, bug fixes, and new features can be deployed once for all tenants.

### Faster Feature Delivery

All tenants benefit from new functionality immediately after deployment.

### Easier Monitoring

Operations teams manage one application instead of many independent deployments.

---

## Disadvantages

### Tenant Isolation Complexity

Strong safeguards are required to prevent unauthorized access between tenants.

### Noisy Neighbor Problem

Resource-intensive tenants can negatively impact the performance experienced by others if resource limits are not enforced.

### Increased Security Requirements

Any isolation failure may expose data belonging to multiple tenants.

### More Complex Testing

Testing must verify that tenant boundaries are consistently enforced throughout the application.

---

## SaaS Considerations

Multi-tenancy influences nearly every architectural decision within a SaaS application.

### Authentication

Users must be authenticated and associated with the correct tenant before accessing application resources.

### Authorization

Authorization policies should consider both user permissions and tenant ownership.

### Data Storage

The selected database strategy should balance scalability, isolation, operational complexity, and compliance requirements.

### Billing

Usage, subscriptions, and invoices are typically managed on a per-tenant basis.

### Configuration

Each tenant may have:

- Feature flags
- Branding
- Localization settings
- Business rules
- Subscription limits

### Monitoring

Metrics should include tenant-specific information to identify performance issues and usage patterns.

---

## Design Considerations

When designing a multi-tenant application, architects should evaluate:

- Expected number of tenants
- Tenant size variability
- Compliance requirements
- Performance expectations
- Security requirements
- Disaster recovery strategy
- Cost constraints
- Future scalability

---

## Quality Attributes

| Quality Attribute | Impact |
|-------------------|--------|
| Scalability | Very High |
| Maintainability | High |
| Availability | High |
| Security | Very High |
| Performance | High |
| Cost Optimization | Very High |
| Complexity | Medium to High |

---

## Common Technologies

Multi-tenant SaaS applications commonly use:

- PostgreSQL
- SQL Server
- Azure SQL Database
- MongoDB
- Redis
- Docker
- Kubernetes
- Identity Providers (Azure AD, Auth0, Keycloak)
- API Gateways

---

## Best Practices

- Include the tenant identifier in every business request.
- Enforce tenant isolation at multiple layers of the application.
- Never rely solely on client-provided tenant identifiers.
- Apply authorization after tenant resolution.
- Encrypt sensitive tenant data.
- Implement tenant-aware logging and monitoring.
- Use automated provisioning for onboarding new tenants.
- Design databases with future growth in mind.
- Consider hybrid tenancy models for enterprise customers.

---

## Common Challenges

- Preventing cross-tenant data access.
- Managing tenant onboarding and offboarding.
- Scaling infrastructure for thousands of tenants.
- Supporting tenant-specific customizations.
- Migrating tenants between database models.
- Monitoring tenant-specific performance.
- Handling noisy neighbor scenarios.
- Meeting compliance and data residency requirements.

---

## Related Concepts

- Tenant Isolation
- Authentication
- Authorization
- Billing
- API Gateway

---

## Related Quality Attributes

- Scalability
- Security
- Availability
- Cost Optimization
- Maintainability

---

## Summary

Multi-tenancy is a foundational concept of cloud-native SaaS architecture, enabling multiple customers to securely share a single application while maintaining logical separation of their data and configurations. By efficiently sharing infrastructure, multi-tenant systems reduce operational costs, simplify maintenance, and improve scalability. Selecting an appropriate multi-tenancy model requires balancing security, performance, compliance, operational complexity, and cost based on the application's requirements and the needs of its tenants.