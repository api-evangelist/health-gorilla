---
name: Subscribe to Health Gorilla clinical events
description: >-
  Register a FHIR Subscription so Health Gorilla posts webhooks when clinical
  resources change, verify the HMAC-SHA512 signature on delivery, and reconcile
  with _lastUpdated so nothing is silently lost.
api: fhir/health-gorilla-r4-capabilitystatement.json
apis:
  - openapi/health-gorilla-diagnosticreport-api-openapi.yml
  - openapi/health-gorilla-documentreference-api-openapi.yml
operations:
  - searchDiagnosticReports
  - searchDocumentReferences
fhir_resources:
  - Subscription
generated: '2026-08-14'
method: generated
source: asyncapi/health-gorilla-webhooks.yml + fhir/health-gorilla-r4-capabilitystatement.json
---

# Subscribe to Health Gorilla clinical events

Health Gorilla has no separate webhook API. Events are FHIR **Subscription**
resources managed at `https://api.healthgorilla.com/fhir/R4/Subscription`, which
the live CapabilityStatement declares with create, read, patch, delete and
search interactions.

Webhooks are the preferred integration path; polling is the documented fallback
of last resort.

## 1. Stand up an endpoint that meets the requirements

Non-negotiable, or delivery fails silently:

- **HTTPS only.** `http://` endpoints are rejected.
- **TLS 1.2 or higher**, with a valid certificate. Self-signed or expired
  certificates count as a delivery failure.
- Respond **`200 OK` or `202 Accepted`**, quickly. Anything else — including a
  timeout — is a failure and triggers retries.
- Queue the payload and process it asynchronously. Do not do the work inside the
  request.

## 2. Create the subscription

```http
POST /fhir/R4/Subscription
Authorization: Bearer <access_token>
Content-Type: application/fhir+json
HG-Idempotency-Key: <uuid-v4>
```

```json
{
  "resourceType": "Subscription",
  "status": "active",
  "end": "2027-01-01T00:00:00Z",
  "reason": "Monitor diagnostic report updates",
  "criteria": "DiagnosticReport",
  "channel": {
    "type": "rest-hook",
    "endpoint": "https://yourapp.com/webhooks/hg",
    "payload": "application/fhir+json"
  }
}
```

Set `end` deliberately — a subscription without a sensible expiry outlives the
integration that created it.

## 3. Choose criteria

`criteria` is a FHIR search expression. Documented examples:

| Resource | Criteria |
|---|---|
| DocumentReference | `DocumentReference?status=current` |
| Encounter | `Encounter?status=finished` |
| AllergyIntolerance | `AllergyIntolerance?clinical-status=active` |
| Observation | `Observation?code=XXX` |
| Immunization | `Immunization?status=completed` |
| ADT messages | `Bundle?message.event=admin-notify` |
| Patient360 document import | `Patient.P360` |

Supported resources include DiagnosticReport, DocumentReference, Condition,
AllergyIntolerance, Immunization, MedicationRequest, MedicationStatement,
Observation, Encounter, CarePlan, Goal, Procedure and Coverage. Availability
varies by configuration — agree your criteria with the Health Gorilla
integration team rather than assuming.

## 4. Pick a payload type

- `application/fhir+json` — the full triggering resource.
- `application/hg-event+json` — a pointer only:
  `{"resource": "RequestGroup", "id": "RequestGroup/d6fjlvj9gjb9djlaww8q"}`.
  Re-fetch to get the data. Best when payloads must not cross your perimeter.
- `application/hg-ocr+json` — OCR output.
- No payload — you are told *something* changed; query with `_lastUpdated`.

## 5. Verify the signature

Health Gorilla can sign with **HMAC-SHA512**. Headers on delivery: `Date`,
`Digest`, `X-Hg-EventId`, `X-Hg-EventCreated`, `X-Hg-Signature`.

To verify:

1. Read `Date`, `X-Hg-EventId`, `Digest` and `X-Hg-Signature`.
2. Build the string to sign — three lines, in this order:
   `<Date>\n<X-Hg-EventId>\n<Digest>`
3. Compute HMAC-SHA512 with your configured signing secret.
4. Prefix with `sha512=`.
5. Compare against `X-Hg-Signature` using a constant-time comparison.

Reject anything that fails. These are clinical events.

If you protect your endpoint with OAuth instead, Health Gorilla supports a
client-credentials extension on the channel — but the credentials must be issued
by **your** organization, never the OAuth credentials Health Gorilla issued you
for API access.

## 6. Be idempotent on receive

The same event can arrive more than once. Deduplicate on `resource.id` plus
`meta.lastUpdated`, or store delivery hashes.

## 7. Know the retry and disable rules

Per-event backoff: roughly 5 seconds, 30 seconds, 2 minutes, then 10 minutes.
After the final attempt **the event is discarded and never redelivered**.
Separately, subscription-level redelivery retries every 15 minutes.

A subscription is **automatically disabled** when either holds:

- last successful delivery is 3+ days old **and** more than 10 failures, or
- no successful delivery ever **and** more than 20 failures.

Once disabled it must be re-enabled before notifications resume. Alert on
delivery failure — silence is what this failure mode looks like.

## 8. Respect the cap

30 active subscriptions by default; exceeding it returns `422 Unprocessable
Entity`. The limit can be raised on request. Delete subscriptions you no longer
use — `DELETE /fhir/R4/Subscription/{id}`.

## 9. Reconcile — always

Delivery is not guaranteed. Run a periodic sweep comparing what you received
against `GET /{ResourceType}?_lastUpdated=ge{last_sync}`. This is the only thing
that catches a subscription that was silently disabled.

## Related

- `asyncapi/health-gorilla-webhooks.yml` — the full webhook catalog
- `conventions/health-gorilla-conventions.yml`
- `errors/health-gorilla-problem-types.yml`
