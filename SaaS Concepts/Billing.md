# Billing

## Overview

**Billing** is the process of tracking customer usage, managing subscriptions, calculating charges, generating invoices, and processing payments within a SaaS application. It is a core business capability that enables software providers to monetize their services while supporting different pricing models and subscription plans.

In cloud-native SaaS applications, billing is typically implemented as an independent module or microservice that integrates with authentication, subscription management, payment providers, and usage monitoring systems.

A well-designed billing system should be secure, scalable, reliable, and flexible enough to support evolving business models.

---

## Core Principles

- Track customer subscriptions and usage accurately.
- Calculate charges based on pricing models.
- Generate invoices and payment records.
- Support automated recurring payments.
- Maintain accurate financial records.
- Integrate securely with external payment providers.
- Ensure billing operations are auditable and reliable.

---

## Billing Process

A typical SaaS billing workflow consists of the following steps:

1. A customer subscribes to a pricing plan.
2. The subscription is associated with a tenant.
3. Usage is tracked throughout the billing period.
4. Charges are calculated according to the selected pricing model.
5. An invoice is generated.
6. Payment is processed through a payment provider.
7. The subscription is renewed, updated, or cancelled.

---

## Pricing Models

### Subscription-Based Billing

Customers pay a recurring fee for access to the application.

Examples:

- Monthly subscription
- Annual subscription
- Enterprise contracts

#### Advantages

- Predictable revenue.
- Simple pricing structure.
- Easy financial forecasting.

#### Disadvantages

- Revenue may not reflect actual resource consumption.
- Less flexible for highly variable workloads.

---

### Usage-Based Billing

Charges are calculated according to actual resource consumption.

Examples include:

- API requests
- Storage used
- Compute time
- Number of active users
- Messages processed

#### Advantages

- Fair pricing.
- Scales with customer usage.
- Attractive for growing businesses.

#### Disadvantages

- Less predictable monthly costs.
- More complex implementation.

---

### Tiered Pricing

Customers select from predefined subscription plans offering different features or usage limits.

Example:

| Plan | Features |
|------|----------|
| Free | Basic functionality |
| Professional | Additional features and higher limits |
| Enterprise | Unlimited usage and advanced support |

This is one of the most common pricing strategies for SaaS applications.

---

### Per-User Pricing

Charges depend on the number of active users within a tenant.

Example:

- €10 per active user per month

This model is frequently used for collaboration platforms.

---

### Hybrid Pricing

Many SaaS platforms combine multiple pricing models.

Example:

- Monthly subscription
- Included usage quota
- Additional charges for exceeding limits

Hybrid pricing offers flexibility while maintaining predictable revenue.

---

## Subscription Management

Subscriptions typically include:

- Plan selection
- Billing cycle
- Renewal date
- Payment method
- Status (Active, Suspended, Cancelled)
- Usage limits
- Trial period

The billing system should support subscription upgrades, downgrades, renewals, and cancellations.

---

## Invoice Management

Invoices generally contain:

- Customer information
- Tenant information
- Billing period
- Subscription plan
- Usage details
- Taxes
- Discounts
- Total amount
- Payment status

Invoices should be stored for auditing and financial reporting purposes.

---

## Payment Processing

Payments are typically delegated to external payment providers.

Common providers include:

- Stripe
- PayPal
- Adyen
- Braintree
- Paddle

Typical payment flow:

1. Invoice generated.
2. Payment request sent.
3. Payment provider processes transaction.
4. Payment result returned.
5. Subscription updated accordingly.

Sensitive payment information should never be stored directly unless required and compliant with applicable standards.

---

## SaaS Considerations

Billing is closely integrated with several SaaS concepts.

### Multi-tenancy

Billing is generally managed at the tenant level.

Each tenant has:

- Subscription plan
- Billing history
- Payment methods
- Usage metrics
- Invoices

---

### Authentication

Only authorized users, such as tenant administrators or billing administrators, should manage subscription and payment information.

---

### Authorization

Billing operations should be restricted to users with appropriate permissions.

Examples include:

- View invoices
- Update payment method
- Change subscription plan
- Cancel subscription

---

### Usage Tracking

The application should continuously collect usage metrics required for billing.

Examples:

- API calls
- Active users
- Storage consumption
- Compute hours
- Generated reports

---

### Event-Driven Architecture

Billing systems commonly react to business events such as:

- UserCreated
- SubscriptionActivated
- PaymentSucceeded
- PaymentFailed
- UsageReported

This enables loose coupling between billing and other application components.

---

## Quality Attributes

| Quality Attribute | Impact |
|-------------------|--------|
| Reliability | Very High |
| Security | Very High |
| Availability | High |
| Scalability | High |
| Maintainability | High |
| Performance | High |
| Auditability | Very High |

---

## Common Technologies

Billing systems commonly integrate with:

- Stripe
- PayPal
- Paddle
- Adyen
- Braintree
- PostgreSQL
- Redis
- RabbitMQ
- Apache Kafka
- Docker
- Kubernetes

---

## Best Practices

- Separate billing logic from business functionality.
- Never store sensitive payment card information unless absolutely necessary.
- Use PCI DSS-compliant payment providers.
- Support idempotent payment processing.
- Track all billing events for auditing.
- Automate recurring billing processes.
- Support subscription upgrades and downgrades without service interruption.
- Monitor failed payments and retry when appropriate.
- Generate immutable invoices.
- Validate usage metrics before calculating charges.

---

## Common Challenges

- Supporting multiple pricing models.
- Handling failed payments.
- Managing subscription changes during billing periods.
- Calculating usage accurately.
- Processing refunds.
- Supporting multiple currencies.
- Managing taxes across different regions.
- Integrating with external payment providers.
- Maintaining financial audit trails.

---

## Relationship with Multi-tenancy

Billing is typically organized around tenants rather than individual users.

Each tenant usually has:

- One subscription
- One billing account
- One payment method (or multiple managed methods)
- Shared usage metrics
- Consolidated invoices

This aligns billing with the organizational structure of most SaaS applications.

---

## Related Concepts

- Multi-tenancy
- Authentication
- Authorization
- API Gateway
- Event-Driven Architecture

---

## Related Quality Attributes

- Reliability
- Security
- Availability
- Scalability
- Auditability

---

## Summary

Billing is a core business capability in cloud-native SaaS applications that manages subscriptions, tracks usage, calculates charges, generates invoices, and processes payments. A well-designed billing system supports multiple pricing models, integrates securely with external payment providers, and scales with customer growth while maintaining accuracy, reliability, and auditability. Because billing directly impacts both customer experience and business revenue, it should be designed as a secure, modular, and highly reliable component of the overall SaaS architecture.