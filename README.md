# Health Gorilla (health-gorilla)

Health Gorilla operates a national health-data interoperability network and a FHIR-first API suite for healthcare developers. Its HL7 FHIR R4 REST API provides access to patient records, person-authorized record retrieval across national exchange networks (QHIN / TEFCA), diagnostic (lab and radiology) ordering and results, clinical documents, and coverage/eligibility data under OAuth 2.0.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/health-gorilla/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/health-gorilla/refs/heads/main/apis.yml)

## Tags

- Health
- Interoperability
- FHIR
- Clinical Data
- Lab Ordering

## Timestamps

- **Created:** 2026-06-21
- **Modified:** 2026-06-21

## APIs

### Patients (FHIR)

FHIR R4 Patient resources - read, search, create, update, and the patient-scoped $everything operation for retrieving a complete patient record as a FHIR Bundle.

- **Human URL:** [https://developer.healthgorilla.com/reference/r4-overview](https://developer.healthgorilla.com/reference/r4-overview)
- **Base URL:** `https://api.healthgorilla.com/fhir/R4`

#### Tags

- Patients
- FHIR
- Demographics

#### Properties

- [Documentation](https://developer.healthgorilla.com/reference/r4-overview)
- [API Reference](https://developer.healthgorilla.com/reference/fhir-api-reference)
- [OpenAPI](openapi/health-gorilla-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/health-gorilla.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/health-gorilla.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Record Query/Retrieval

Person-authorized federated FHIR query and record retrieval across national exchange networks. Initiate a retrieval, poll its status, and pull results as FHIR Bundles of DocumentReference and Binary resources.

- **Human URL:** [https://developer.healthgorilla.com/docs/federated-fhir](https://developer.healthgorilla.com/docs/federated-fhir)
- **Base URL:** `https://api.healthgorilla.com/fhir/R4`

#### Tags

- Query
- Record Retrieval
- TEFCA
- QHIN

#### Properties

- [Documentation](https://developer.healthgorilla.com/docs/federated-fhir)
- [API Reference](https://developer.healthgorilla.com/docs/api-endpoints-overview)
- [OpenAPI](openapi/health-gorilla-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/health-gorilla.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/health-gorilla.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Lab Ordering

Submit laboratory and radiology orders to participating diagnostic partners using a RequestGroup parent order that nests individual ServiceRequest tests, then track order status.

- **Human URL:** [https://developer.healthgorilla.com/docs/diagnostic-network](https://developer.healthgorilla.com/docs/diagnostic-network)
- **Base URL:** `https://api.healthgorilla.com/fhir/R4`

#### Tags

- Lab Ordering
- Diagnostics
- ServiceRequest
- RequestGroup

#### Properties

- [Documentation](https://developer.healthgorilla.com/docs/diagnostic-network)
- [API Reference](https://developer.healthgorilla.com/reference/servicerequest-1)
- [OpenAPI](openapi/health-gorilla-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/health-gorilla.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/health-gorilla.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Diagnostic Reports

Retrieve structured lab and radiology results as FHIR R4 DiagnosticReport resources with their associated Observation resources.

- **Human URL:** [https://developer.healthgorilla.com/reference/fhir-api-reference](https://developer.healthgorilla.com/reference/fhir-api-reference)
- **Base URL:** `https://api.healthgorilla.com/fhir/R4`

#### Tags

- Diagnostic Reports
- Results
- Observations

#### Properties

- [Documentation](https://developer.healthgorilla.com/reference/fhir-api-reference)
- [API Reference](https://developer.healthgorilla.com/reference/r4-overview)
- [OpenAPI](openapi/health-gorilla-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/health-gorilla.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/health-gorilla.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Documents

Access clinical documents via FHIR R4 DocumentReference resources and download the underlying content as Binary resources (CCDA, PDF, and other formats).

- **Human URL:** [https://developer.healthgorilla.com/reference/fhir-api-reference](https://developer.healthgorilla.com/reference/fhir-api-reference)
- **Base URL:** `https://api.healthgorilla.com/fhir/R4`

#### Tags

- Documents
- DocumentReference
- Binary

#### Properties

- [Documentation](https://developer.healthgorilla.com/reference/fhir-api-reference)
- [API Reference](https://developer.healthgorilla.com/docs/api-endpoints-overview)
- [OpenAPI](openapi/health-gorilla-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/health-gorilla.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/health-gorilla.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Eligibility

Coverage and identity data via FHIR R4 Coverage resources plus the OAuth 2.0 identity / IAS token flow used to authorize person-level queries.

- **Human URL:** [https://developer.healthgorilla.com/reference/fhir-r4-careplan](https://developer.healthgorilla.com/reference/fhir-r4-careplan)
- **Base URL:** `https://api.healthgorilla.com/fhir/R4`

#### Tags

- Eligibility
- Coverage
- Identity

#### Properties

- [Documentation](https://developer.healthgorilla.com/reference/r4-overview)
- [Authentication](https://developer.healthgorilla.com/reference/oauth-20-authentication)
- [OpenAPI](openapi/health-gorilla-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/health-gorilla.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/health-gorilla.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [GitHub Organization](https://github.com/healthgorilla)
- [LinkedIn](https://www.linkedin.com/company/health-gorilla)
- [Website](https://www.healthgorilla.com)
- [Documentation](https://developer.healthgorilla.com)
- [Plans](plans/health-gorilla-plans-pricing.yml)
- [Rate Limits](rate-limits/health-gorilla-rate-limits.yml)
- [Fin Ops](finops/health-gorilla-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
