---
name: Place a Health Gorilla lab order
description: >-
  Confirm server capabilities, locate the patient, then submit a diagnostic
  (laboratory or radiology) order as a RequestGroup containing one ServiceRequest
  per test, using OAuth 2.0 and an idempotency key.
api: openapi/health-gorilla-requestgroup-api-openapi.yml
apis:
  - openapi/health-gorilla-capabilitystatement-api-openapi.yml
  - openapi/health-gorilla-patient-api-openapi.yml
  - openapi/health-gorilla-servicerequest-api-openapi.yml
  - openapi/health-gorilla-requestgroup-api-openapi.yml
operations:
  - getCapabilityStatement
  - searchPatients
  - createServiceRequest
  - createRequestGroup
  - readRequestGroup
generated: '2026-08-14'
method: generated
source: openapi/*.yml + conventions/ + errors/ + arazzo/health-gorilla-lab-order-workflow.yml
---

# Place a Health Gorilla lab order

Health Gorilla models a diagnostic order as a **RequestGroup** (the requisition)
that nests one **ServiceRequest** per ordered test. Never create a bare
ServiceRequest and expect it to reach a lab — it must be grouped.

## Before you start

- Base URL: `https://api.healthgorilla.com/fhir/R4` (sandbox:
  `https://sandbox.healthgorilla.com/fhir/R4`).
- Always build against the sandbox first. It is a closed system that returns
  randomly generated, non-clinical mock results.
- TLS 1.2 or higher is mandatory. Plain HTTP is rejected.

## 1. Authenticate

Get an OAuth 2.0 bearer token from `https://www.healthgorilla.com/oauth/token`.
Send it on every request:

```
Authorization: Bearer <access_token>
Content-Type: application/fhir+json
Accept: application/fhir+json
```

Ordering requires a scope assigned at client registration — the docs use
`place_orders` as the worked example. You cannot self-assign it; if a POST comes
back `403 Forbidden` with issue code `forbidden`, the token is missing the scope
and Health Gorilla must add it to your client. Do not retry; it will not succeed.

## 2. Confirm the server supports what you are about to send — `getCapabilityStatement`

`GET /metadata` returns the live CapabilityStatement. Check that `RequestGroup`
and `ServiceRequest` both declare the `create` interaction before ordering. This
is cheap, unauthenticated, and it is the only reliable way to know what this
server actually accepts today.

## 3. Find the patient — `searchPatients`

`GET /Patient?identifier=...` or `GET /Patient?name=...&birthdate=...&gender=...`

- The response is a FHIR `Bundle` of type `searchset`.
- **Resolve to exactly one patient before ordering.** If the Bundle has
  `total` greater than 1, do not guess — narrow the search with more
  demographics, or stop and ask.
- If `total` is 0, the patient does not exist in this tenant. Create them with
  `createPatient` first.
- Keep `Patient.id` — you will reference it as `Patient/{id}`.

## 4. Create each ordered test — `createServiceRequest`

`POST /ServiceRequest` once per test, with:

- `subject.reference` set to `Patient/{id}`
- `requester` referencing the ordering Practitioner or PractitionerRole
- `code` carrying the lab's compendium code for the test

Send a fresh `HG-Idempotency-Key` (UUID v4) on **every** POST. Keep the returned
`ServiceRequest.id` for each test.

## 5. Group the tests into a requisition — `createRequestGroup`

`POST /RequestGroup` with an `action[]` entry per ServiceRequest, each
`action.resource.reference` pointing at `ServiceRequest/{id}`, plus the patient
as `subject` and the ordering provider as `author`.

Use a new `HG-Idempotency-Key` for this POST too.

## 6. Confirm the order — `readRequestGroup`

`GET /RequestGroup/{id}` and check `status`. Store the id; results arrive
against it later (see the results-retrieval skill).

## Idempotency — read this before you retry anything

Every POST in this flow creates a real clinical order. A blind retry can
double-order a patient's blood draw.

- Send `HG-Idempotency-Key: <uuid-v4>` on every POST.
- Replaying the **same key with the same payload** inside the window (typically
  up to one hour) returns the original response. This is the safe retry.
- Replaying the **same key with a different payload** returns `409 Conflict`
  with an empty body. Generate a new UUID when the payload changes.
- `202 Accepted` on a replay means the original request is still processing.
  Poll rather than resend.

## Errors

All failures return a FHIR `OperationOutcome` in `application/fhir+json`.
Read `issue[].code` and `issue[].diagnostics`, not just the status.

| Status | Issue code | What to do |
|---|---|---|
| 400 | `structure`, `invalid` | Malformed body. Fix and resend with a new key. |
| 401 | — | Token expired or invalid. Refresh, then retry. |
| 403 | `forbidden` | Missing scope. Stop — this needs Health Gorilla, not a retry. |
| 409 | `duplicate` | The resource already exists. Search by identifier instead of creating. |
| 409 | — (empty body) | Idempotency key reused with a different payload. New UUID. |
| 422 | `required` | A required field is missing; `issue[].location` names it. |
| 422 | `not-found` | A reference does not resolve. Verify the Patient/Practitioner id. |
| 500, 503 | `processing` | Retry with backoff and the **same** idempotency key. |

Log `X-HG-Request-Id` from every response. Health Gorilla support needs it, and
it is the only handle on a specific transaction.

## Related

- `arazzo/health-gorilla-lab-order-workflow.yml` — the executable version of this flow
- `conventions/health-gorilla-conventions.yml`
- `errors/health-gorilla-problem-types.yml`
- `sandbox/health-gorilla-sandbox.yml`
