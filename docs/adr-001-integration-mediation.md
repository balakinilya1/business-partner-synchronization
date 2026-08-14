# ADR-001: Use SAP Integration Suite as the Mediation Layer

## Status

Accepted

## Context

SAP S/4HANA and Salesforce expose different data models, connectivity mechanisms and authentication requirements. Direct application-to-application coupling would place transformation and connectivity responsibilities in the source or target systems.

## Decision

Use SAP Integration Suite / SAP Cloud Integration as the mediation and orchestration layer.

The integration runtime is responsible for:
- scheduled execution;
- source retrieval;
- result evaluation;
- record splitting;
- transformation;
- filtering;
- target delivery;
- credential references;
- operational monitoring.

## Consequences

### Positive

- Decouples SAP S/4HANA from Salesforce.
- Centralizes transformation logic.
- Centralizes connectivity configuration.
- Allows security material to be managed outside the flow logic.
- Provides a consistent runtime for monitoring and operations.

### Negative

- Adds another runtime component.
- Integration failures can become a dependency for CRM synchronization.
- The integration platform itself requires governance, monitoring and lifecycle management.

## Alternatives considered

### Direct SAP → Salesforce integration

Rejected for this case because it increases coupling between the two applications and does not provide a dedicated mediation boundary.

### CRM polling SAP directly

Rejected because the integration responsibility would move into the CRM side and reduce reuse of the enterprise integration platform.

### Event-driven integration

Not selected for the mission implementation because the source scenario is explicitly scheduled. It remains a future option when business latency requirements justify it.
