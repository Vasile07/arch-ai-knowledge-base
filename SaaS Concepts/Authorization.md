# Authorization

## Overview

**Authorization** is the process of determining what an authenticated user, application, or service is permitted to access or perform within a system. It answers the question:

> **"What are you allowed to do?"**

Authorization occurs **after successful authentication** and enforces access control policies based on the authenticated identity, assigned roles, permissions, or contextual information. In cloud-native SaaS applications, authorization is essential for protecting resources, enforcing tenant isolation, and ensuring users can only perform actions permitted by their role and organization.

Modern authorization systems often implement **Role-Based Access Control (RBAC)**, **Attribute-Based Access Control (ABAC)**, or combinations of multiple authorization models.

---

## Core Principles

- Authorization occurs after authentication.
- Access decisions are based on predefined policies.
- Users should have only the permissions they require.
- Authorization should be enforced consistently across the application.
- Access control should support tenant-aware security.
- Authorization logic should be centralized where possible.

---

## Authorization Process

A typical authorization workflow consists of the following steps:

1. A user successfully authenticates.
2. The application establishes the user's identity.
3. The requested resource and action are identified.
4. Authorization policies are evaluated.
5. Access is either granted or denied.
6. The request proceeds only if authorization succeeds.

---

## Authorization Models

### Role-Based Access Control (RBAC)

RBAC grants permissions based on predefined roles assigned to users.

Example roles:

- Administrator
- Manager
- Employee
- Customer
- Viewer

Each role defines a set of permissions.

#### Advantages

- Easy to implement.
- Simple to understand.
- Suitable for most business applications.
- Centralized permission management.

#### Disadvantages

- Large organizations may require many roles.
- Less flexible for complex access requirements.

---

### Attribute-Based Access Control (ABAC)

ABAC evaluates multiple attributes before granting access.

Examples include:

- User role
- Tenant
- Department
- Resource owner
- Time of day
- Device type
- Geographic location

Access is determined by evaluating policies rather than fixed roles.

#### Advantages

- Highly flexible.
- Fine-grained access control.
- Supports complex security requirements.

#### Disadvantages

- More difficult to implement.
- Policies may become difficult to manage.

---

### Policy-Based Access Control (PBAC)

PBAC evaluates access requests against centralized authorization policies.

Policies may include business rules such as:

- Managers may approve invoices below a certain amount.
- Financial reports may only be viewed during business hours.
- Customer data may only be accessed from trusted networks.

PBAC is commonly implemented using policy engines such as Open Policy Agent (OPA).

---

### Access Control Lists (ACLs)

ACLs associate permissions directly with individual resources.

Example:

```
Document A

Alice    Read, Write
Bob      Read
Carol    Read, Delete
```

ACLs provide fine-grained control but can become difficult to maintain at scale.

---

## Permissions

Permissions define the specific actions users may perform.

Examples include:

- Create
- Read
- Update
- Delete
- Approve
- Export
- Manage Users
- View Reports

Permissions are often grouped into roles for easier administration.

---

## SaaS Considerations

Authorization is one of the most important security mechanisms in cloud-native SaaS applications.

### Multi-tenancy

Authorization decisions should consider both:

- User permissions
- Tenant ownership

A user with administrator privileges should only manage resources belonging to their own tenant.

---

### Tenant Isolation

Authorization reinforces tenant isolation by ensuring users cannot access resources owned by another tenant, even if they possess valid credentials.

Every authorization decision should validate:

- User identity
- Tenant identity
- Resource ownership
- Requested operation

---

### Role Management

SaaS platforms commonly define roles such as:

- Tenant Administrator
- Organization Owner
- Manager
- Employee
- Billing Administrator
- Read-Only User

Enterprise customers may also require custom roles.

---

### Resource Ownership

Access may depend on ownership rather than role alone.

Examples include:

- A user may edit only documents they created.
- Managers may approve requests for their department.
- Customers may view only their own invoices.

---

### API Security

Every protected API endpoint should perform authorization before executing business logic.

Authorization should never rely solely on client-side validation.

---

### Microservices

In distributed systems, authorization may be:

- Centralized through an API Gateway or authorization service.
- Performed independently by each microservice.
- Shared using centralized policy engines.

The selected approach depends on security, scalability, and operational requirements.

---

## Authorization Strategies

### Centralized Authorization

A dedicated authorization service evaluates access requests for all applications.

#### Advantages

- Consistent policy enforcement.
- Easier auditing.
- Simplified management.

#### Disadvantages

- Additional network dependency.
- Potential performance bottleneck.

---

### Decentralized Authorization

Each service evaluates authorization independently.

#### Advantages

- Better resilience.
- Lower latency.
- Service autonomy.

#### Disadvantages

- Possible duplication of authorization logic.
- Harder to maintain consistent policies.

---

### Hybrid Authorization

Many cloud-native SaaS applications combine centralized policy management with local enforcement inside individual services.

This approach balances consistency with scalability.

---

## Quality Attributes

| Quality Attribute | Impact |
|-------------------|--------|
| Security | Very High |
| Maintainability | High |
| Scalability | High |
| Availability | High |
| Compliance | Very High |
| Performance | High |
| Flexibility | High |

---

## Common Technologies

Authorization is commonly implemented using:

- ASP.NET Authorization
- Spring Security
- Keycloak Authorization Services
- Auth0 Authorization
- Open Policy Agent (OPA)
- OAuth 2.0 Scopes
- JWT Claims
- Azure Role-Based Access Control (Azure RBAC)
- AWS IAM
- Casbin

---

## Best Practices

- Apply the Principle of Least Privilege.
- Separate authentication from authorization.
- Validate authorization on every protected request.
- Include tenant validation in every authorization decision.
- Use roles and permissions consistently.
- Keep authorization policies centralized when possible.
- Log authorization failures for auditing.
- Review user permissions regularly.
- Avoid hardcoding authorization logic throughout the application.
- Protect administrative operations with additional security controls.

---

## Common Challenges

- Managing large numbers of roles.
- Supporting fine-grained permissions.
- Preventing privilege escalation.
- Maintaining consistent authorization across microservices.
- Implementing tenant-aware access control.
- Auditing authorization decisions.
- Supporting dynamic business rules.
- Balancing security with usability.

---

## Relationship with Authentication

Authentication and authorization work together but solve different problems.

| Authentication | Authorization |
|----------------|---------------|
| Verifies identity. | Determines permissions. |
| Answers "Who are you?" | Answers "What are you allowed to do?" |
| Occurs first. | Occurs after authentication. |
| Creates a trusted identity. | Enforces access control. |

A user must first be authenticated before authorization policies can determine which resources they are allowed to access.

---

## Related Concepts

- Authentication
- Multi-tenancy
- Tenant Isolation
- API Gateway
- Security

---

## Related Quality Attributes

- Security
- Maintainability
- Scalability
- Availability
- Compliance

---

## Summary

Authorization is the process of determining whether an authenticated user, application, or service is permitted to perform a specific action on a particular resource. It is a critical component of cloud-native SaaS security, ensuring that access decisions consider user identity, roles, permissions, tenant ownership, and business policies. Modern SaaS applications commonly implement authorization using Role-Based Access Control (RBAC), Attribute-Based Access Control (ABAC), or policy-based approaches to provide secure, scalable, and flexible access control across distributed systems.