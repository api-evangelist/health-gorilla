---
name: Check Health Gorilla patient coverage
description: >-
  Locate a patient, search their insurance Coverage resources, and read one for
  full plan detail before placing an order or determining eligibility.
api: openapi/health-gorilla-coverage-api-openapi.yml
apis:
  - openapi/health-gorilla-patient-api-openapi.yml
  - openapi/health-gorilla-coverage-api-openapi.yml
operations:
  - searchPatients
  - searchCoverage
  - readCoverage
generated: '2026-08-14'
method: generated
source: openapi/*.yml + conventions/ + arazzo/health-gorilla-coverage-workflow.yml
---

# Check Health Gorilla patient coverage

Coverage is the FHIR resource carrying a patient's insurance. Check it **before**
submitting a diagnostic order — the payer determines whether an ABN is needed on
the requisition.

## 1. Authenticate

`Authorization: Bearer <access_token>`, `Accept: application/fhir+json`.
Base URL `https://api.healthgorilla.com/fhir/R4`.

## 2. Find the patient — `searchPatients`

`GET /Patient?identifier={mrn}` — resolve to exactly one `Patient.id`.

## 3. List coverages — `searchCoverage`

`GET /Coverage?patient=Patient/{id}`

Returns a `Bundle` of type `searchset`. A patient can have several coverages
(primary, secondary, tertiary), so do not take the first entry and stop.

Note: Coverage declares only **one** search parameter in the live
CapabilityStatement, so filtering server-side is limited. Filter the returned
Bundle client-side on `status` and `period`.

## 4. Read one coverage — `readCoverage`

`GET /Coverage/{id}`

Fields that matter:

- `status` — only `active` coverage is usable. Check it.
- `order` — 1 is primary, 2 secondary, and so on.
- `payor` — reference to the paying Organization.
- `subscriberId` / `subscriber` — the member id and who holds the policy, which
  is not always the patient.
- `beneficiary` — must be the patient you searched for.
- `period` — verify today falls inside `period.start` and `period.end`. Expired
  coverage that is still `active` is a real and common data condition.
- `class` — plan and group identifiers.

## 5. Use it on the order

Reference the chosen Coverage from the diagnostic order so the lab bills
correctly. If the patient is self-pay or coverage is inactive, expect the ABN
path — `RequestGroup/$abn` generates the Advance Beneficiary Notice.

## What this is not

Health Gorilla's Coverage resource reports the coverage **on record**. It is not
a real-time X12 270/271 eligibility check against the payer. Do not tell a user
"you are covered" on the strength of this call alone — report what the record
says and where it came from.

## Errors

`OperationOutcome` on failure.

- `401` — refresh the token.
- `403 forbidden` — token lacks read scope for Coverage.
- `404` — no such Coverage in this tenant.
- Empty Bundle (`total: 0`) is not an error. It means no coverage is on file —
  report that plainly rather than treating it as a failure.

Log `X-HG-Request-Id`.

## Related

- `arazzo/health-gorilla-coverage-workflow.yml`
- `skills/health-gorilla-place-lab-order.md`
- `conventions/health-gorilla-conventions.yml`
