---
name: Pull a complete Health Gorilla patient record
description: >-
  Locate a patient, read the Patient resource, then pull the full longitudinal
  record with $everything — handling the asynchronous federated retrieval path
  and the documents that come back as DocumentReference plus Binary.
api: openapi/health-gorilla-patient-api-openapi.yml
apis:
  - openapi/health-gorilla-patient-api-openapi.yml
  - openapi/health-gorilla-documentreference-api-openapi.yml
  - openapi/health-gorilla-binary-api-openapi.yml
operations:
  - searchPatients
  - readPatient
  - patientEverything
  - searchDocumentReferences
  - readDocumentReference
  - readBinary
generated: '2026-08-14'
method: generated
source: openapi/*.yml + conventions/ + arazzo/health-gorilla-patient-everything-workflow.yml
---

# Pull a complete Health Gorilla patient record

Two different things are called "the record" here, and confusing them is the
most common mistake:

1. **What Health Gorilla already holds** for the patient — available immediately
   via `$everything`.
2. **What exists out on the national networks** (TEFCA/QHIN, CommonWell,
   Carequality) — retrieved by Patient360, which is **asynchronous** and requires
   patient authorization.

This skill covers (1) and tells you where (2) begins.

## 1. Authenticate

`Authorization: Bearer <access_token>`, `Accept: application/fhir+json`.
Base URL `https://api.healthgorilla.com/fhir/R4`.

## 2. Find the patient — `searchPatients`

`GET /Patient?identifier={mrn}` — or name plus `birthdate` plus `gender`.

Resolve to exactly **one** match. If `Bundle.total` is greater than 1, narrow the
query or stop and ask a human. Never merge candidate records yourself; Health
Gorilla has a `$merge` operation for that and it is a clinical decision.

## 3. Read the demographics — `readPatient`

`GET /Patient/{id}` — confirm you have the right person before pulling their
chart. Check name, birth date, and identifiers against what you searched for.

## 4. Pull the record — `patientEverything`

`GET /Patient/{id}/$everything`

Returns a `Bundle` containing the patient's resources — conditions, medications,
allergies, immunizations, encounters, observations, procedures, care plans,
documents. This is one call instead of traversing twenty resource types.

**Page it.** `$everything` is explicitly paginated: follow
`Bundle.link[relation=next]` and use the `_cursor` URL as-is until no `next`
link is present. Set `_count` to keep pages manageable.

Alternative: `Patient/$export-ccda` returns the whole history as a single C-CDA
document instead of a FHIR Bundle — better when you are handing the record to a
system that speaks CDA.

## 5. Fetch document content — `searchDocumentReferences` → `readBinary`

`$everything` gives you `DocumentReference` **metadata**, not the file.

1. `GET /DocumentReference?patient=Patient/{id}` (or take them from the Bundle)
2. `GET /DocumentReference/{id}` — read `content.attachment.url`
3. `GET /Binary/{id}` — the raw bytes

Set `Accept` to match the attachment's `contentType`. Documents are commonly
C-CDA XML or PDF. `$ocr` and `$pdf` operations exist on DocumentReference for
scanned and rendered content respectively.

## 6. If the record is not there yet: Patient360

If `$everything` returns less than expected, the records may exist on the
national networks but not yet be retrieved into this tenant. That is the
Patient360 path, and it is different in three ways that matter:

- It is **asynchronous** — retrieval returns `202 Accepted` and you poll for
  completed / partial / failed status. Do not hold a synchronous request open.
- It requires **patient authorization**, and your organization is responsible for
  obtaining it, keeping it valid at retrieval time, and honoring revocation.
- It is scope-gated on `patient360` (and `rls` for the Record Locator Service),
  assigned at client registration.

Do not attempt these operations without reading
`https://developer.healthgorilla.com/docs/patient360-overview` first — they
initiate real queries against other organizations' systems under TEFCA
governance.

## Consent and provenance

- `Consent` resources record the patient authorization governing access.
- `Provenance` records where each aggregated record came from — read-only, and
  the right answer to "which source said this?"
- Aggregated records are deduplicated and categorised by source; a value
  appearing twice from two sources is normal.

## Errors

`OperationOutcome` on every failure.

- `401` — refresh the token.
- `403 forbidden` — missing scope. Not retryable without Health Gorilla.
- `404` — no such patient in this tenant.
- `202` on a retrieval operation is **success**, not a pending error. Poll.
- `500`, `503` — back off and retry.

Log `X-HG-Request-Id`.

## Related

- `arazzo/health-gorilla-patient-everything-workflow.yml`
- `data-model/health-gorilla-data-model.yml`
- `conventions/health-gorilla-conventions.yml`
