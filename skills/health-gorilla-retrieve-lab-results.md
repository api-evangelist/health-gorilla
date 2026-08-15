---
name: Retrieve Health Gorilla lab results
description: >-
  Locate a patient, pull their laboratory DiagnosticReports, read one report, and
  fetch the discrete Observation values behind it — paging correctly with the
  FHIR cursor.
api: openapi/health-gorilla-diagnosticreport-api-openapi.yml
apis:
  - openapi/health-gorilla-patient-api-openapi.yml
  - openapi/health-gorilla-diagnosticreport-api-openapi.yml
  - openapi/health-gorilla-observation-api-openapi.yml
operations:
  - searchPatients
  - searchDiagnosticReports
  - readDiagnosticReport
  - searchObservations
generated: '2026-08-14'
method: generated
source: openapi/*.yml + conventions/ + arazzo/health-gorilla-results-retrieval-workflow.yml
---

# Retrieve Health Gorilla lab results

A result set is a **DiagnosticReport** whose discrete values are separate
**Observation** resources. Reading the report alone gives you the envelope, not
the numbers.

## 1. Authenticate

`Authorization: Bearer <access_token>`, `Accept: application/fhir+json`.
Base URL `https://api.healthgorilla.com/fhir/R4`.

## 2. Find the patient — `searchPatients`

`GET /Patient?identifier={mrn}` — resolve to exactly one `Patient.id` before
going further. A multi-match here silently returns the wrong person's labs.

## 3. List the reports — `searchDiagnosticReports`

`GET /DiagnosticReport?patient=Patient/{id}&category=LAB`

Useful filters, all declared in the live CapabilityStatement (twelve search
parameters on this resource):

- `category` — `LAB`, `RAD`, and as of release v2629 a clinical-test category
- `date` — FHIR date prefixes (`ge2026-01-01`, `lt2026-06-30`)
- `status` — `final`, `preliminary`, `amended`
- `_lastUpdated` — everything changed since your last sync
- `_count` — page size

## 4. Page correctly

The response is a `Bundle` of type `searchset`.

- Follow `link` where `relation` is `next`; use its URL as-is.
- The cursor is opaque. **Do not construct or edit `_cursor`.**
- Prefer `_cursor` over `_offset`. Offset paging drifts if data changes mid-walk
  and Health Gorilla explicitly discourages it for large sets.
- No `next` link means you are on the last page. That is the only termination
  signal — do not rely on counting against `Bundle.total`.
- Keep `_count` moderate. `_count=1000` is called out as excessive.

## 5. Read one report — `readDiagnosticReport`

`GET /DiagnosticReport/{id}`

Note `DiagnosticReport.result[]` — each entry references an Observation. Also
available: `$pdf` for the rendered report and `$hl7` for the source HL7 message
(both declared in the CapabilityStatement).

## 6. Get the values — `searchObservations`

`GET /Observation?patient=Patient/{id}` and match against the ids in
`DiagnosticReport.result[]`, or use `_include` to pull them alongside the report
in one call.

Each Observation carries `code` (LOINC), `valueQuantity` or `valueString`,
`referenceRange`, and `interpretation`. Report the units from
`valueQuantity.unit` — never assume them.

## Incremental sync

For an ongoing feed, do not re-walk the whole history. Either:

1. Subscribe to `DiagnosticReport` events (see `asyncapi/health-gorilla-webhooks.yml`)
   and treat webhooks as the primary path; or
2. Poll with `_lastUpdated` since your last successful sync.

Health Gorilla states webhook delivery is not guaranteed, so run a `_lastUpdated`
reconciliation pass even when you subscribe.

## Errors

`OperationOutcome` in `application/fhir+json` on every failure.

- `401` — refresh the token and retry.
- `403 forbidden` — the token lacks read scope for this resource. Not retryable.
- `404` — the report id does not exist in this tenant.
- `500`, `503` — retry with exponential backoff.

Log `X-HG-Request-Id` on every response.

## Related

- `arazzo/health-gorilla-results-retrieval-workflow.yml`
- `conventions/health-gorilla-conventions.yml`
- `asyncapi/health-gorilla-webhooks.yml`
