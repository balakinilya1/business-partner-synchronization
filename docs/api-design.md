# API / Interface Design

## 1. Design objective

The integration should hide implementation-specific differences between the SAP Business Partner model and the Salesforce Account model.

The mission uses SAP S/4HANA as the source and Salesforce as the target through Cloud Integration adapters. It does not specify complete public API contracts or exact resource URLs, so this document defines the **logical interface contract** rather than inventing endpoint details.

## 2. Source interface

**Logical operation:** Query Business Partner data from SAP S/4HANA.

**Direction:** Cloud Integration → SAP S/4HANA

**Expected response:** A collection of Business Partner/customer records.

**Transport/adapter:** SAP S/4HANA connectivity configured in Cloud Integration.

### Contract considerations

- The source must expose the fields required by the target Account mapping.
- Filtering at source level should be preferred where technically and functionally appropriate to reduce transferred volume.
- Pagination/large-result handling must be defined for production volumes.

## 3. Target interface

**Logical operation:** Create Account in Salesforce.

**Direction:** Cloud Integration → Salesforce

**Transport/adapter:** Salesforce adapter.

**Expected result:** Salesforce accepts the Account representation and returns a success/error response.

## 4. Canonical logical model

A production implementation should conceptually normalize the source record before mapping:

```text
BusinessPartner
 ├─ SourceKey
 ├─ OrganizationName
 ├─ Address
 │   ├─ Country
 │   ├─ City
 │   ├─ PostalCode
 │   └─ Street
 └─ ContactInformation
```

> The fields above are an architectural model, not a field-level mapping claimed by the mission. Exact SAP and Salesforce fields must be confirmed against the actual interfaces.

## 5. API design principles

- Keep source and target contracts independent.
- Use stable business identifiers.
- Validate mandatory target fields before outbound calls.
- Avoid exposing credentials through API parameters.
- Define timeout and retry policies explicitly.
- Prefer idempotent create/update behavior for master-data replication.

## 6. Open contract questions

- Which S/4HANA Business Partner service/API is used in the target implementation?
- Which Salesforce Account fields are mandatory?
- What is the source-to-target business key?
- Is the operation create-only or upsert?
- How are deletions/deactivations represented?
- What are the expected volume and page size?
