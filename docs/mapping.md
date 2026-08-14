# Data Mapping

## 1. Mapping approach

The mission explicitly includes a transformation step from SAP data into Salesforce format, but the supplied mission material does not contain a field-by-field mapping table.

Therefore, the mapping below is a **portfolio mapping template** that identifies the business concepts to be mapped without pretending that exact technical fields were demonstrated.

## 2. Conceptual mapping

| Business concept | SAP S/4HANA source | Salesforce target | Transformation | Status |
|---|---|---|---|---|
| Business Partner identifier | Business Partner ID | Account external/source ID | Direct | Validate exact target field |
| Organization name | BP organization name | Account name | Direct / trim | Validate |
| Country | BP address country | Account billing country | Code/value mapping if required | Validate |
| City | BP address city | Account billing city | Direct | Validate |
| Postal code | BP address postal code | Account billing postal code | Direct | Validate |
| Street | BP address street | Account billing street | Direct | Validate |
| Contact information | BP contact data | Relevant Account/contact fields | Business-specific mapping | TBD |
| Account eligibility | Source attributes | N/A | Filter condition | TBD |

## 3. Transformation rules

**Portfolio design:**

1. Normalize empty strings/null values according to target requirements.
2. Convert source codes to target codes where the value sets differ.
3. Apply mandatory-field validation before the Salesforce call.
4. Preserve the stable source identifier for traceability.
5. Do not silently truncate values; route validation failures to error handling.

## 4. Filtering

The mission includes a **Filter Data** step before Salesforce Account creation. The exact filter predicate is not shown in the supplied source.

For a production implementation, the filter should be documented as a business rule, for example:

```text
EligibleForCRM = true
AND
RequiredAccountDataIsPresent = true
```

The actual predicate must be agreed with the business and implemented against real source fields.

## 5. Mapping ownership

- Business owner: defines business meaning and eligibility.
- SAP functional owner: confirms source semantics.
- CRM owner: confirms Salesforce target fields.
- Integration architect: defines transformation strategy and traceability.
- Integration developer: implements and tests the mapping.

## 6. Mapping test cases

- Complete valid BP
- Missing mandatory target attribute
- Unsupported country/code
- Empty optional attribute
- Special characters / Unicode
- Duplicate source identifier
- Multiple BP records in one response
