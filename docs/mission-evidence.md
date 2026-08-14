# Mission Evidence vs Portfolio Design

This document prevents accidental overclaiming in the portfolio.

## Directly supported by the supplied mission material

- Use case: synchronize customer/account data between SAP S/4HANA and a third-party CRM.
- CRM example: Salesforce.
- SAP Integration Suite / SAP Cloud Integration is the integration platform.
- SAP S/4HANA Business Partner data is queried.
- Processing includes receiving results, checking whether results exist, splitting accounts, transforming to Salesforce format and filtering.
- Salesforce Account creation is the target operation.
- The integration is scheduled with a recurring Timer Start.
- S/4HANA and Salesforce receiver configuration is performed.
- Security Material is configured in SAP Integration Suite.
- Salesforce OAuth2 Client Credentials are created with Token Service URL, Client ID and Client Secret.
- The flow references S/4HANA credential information and Salesforce authentication material.
- The integration is saved and deployed.

These points are visible in the attached mission screenshots. 

## Added as architecture work for this portfolio

The following are deliberately recommendations/design artifacts rather than claims about what the mission implemented:

- detailed business requirements and NFRs;
- production SLA/KPI targets;
- exact field-level mapping;
- canonical data model;
- idempotency/upsert strategy;
- bounded retry policy;
- dead-letter/reprocessing model;
- enterprise alerting;
- multi-environment DEV/TEST/PROD promotion;
- CI/CD;
- event-driven future architecture;
- volume/performance strategy;
- API contract details not shown by the mission.

## Why this distinction matters

The portfolio should demonstrate architecture thinking without implying production implementation where only a learning mission was completed. The strongest presentation is:

> **Implemented in the SAP mission:** the integration scenario and technical configuration.
>
> **Designed for the portfolio:** the enterprise-level requirements, controls, operational model and evolution path around that scenario.
