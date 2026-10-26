# Health Gorilla (health-gorilla)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
