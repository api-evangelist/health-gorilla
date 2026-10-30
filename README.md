# Health Gorilla

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

**Areas:** Health · Interoperability · FHIR · Clinical Data · Lab Ordering · TEFCA · QHIN · Health Information Exchange · Lab Results · Clinical Documents · SMART on FHIR · Patient Records

## Health Gorilla on APIs.io

Everything profiled for Health Gorilla is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/health-gorilla/](https://apis.io/providers/health-gorilla/)** — or go straight to one of the APIs or properties below.

### APIs (10)

- [Health Gorilla Binary API](https://apis.io/apis/health-gorilla/health-gorilla-binary-api/) — Raw clinical document content.
- [Health Gorilla Coverage API](https://apis.io/apis/health-gorilla/health-gorilla-coverage-api/) — Patient insurance coverage / eligibility.
- [Health Gorilla DiagnosticReport API](https://apis.io/apis/health-gorilla/health-gorilla-diagnosticreport-api/) — Structured lab and radiology results.
- [Health Gorilla Observation API](https://apis.io/apis/health-gorilla/health-gorilla-observation-api/) — Individual result observations.
- [Health Gorilla Patient API](https://apis.io/apis/health-gorilla/health-gorilla-patient-api/) — Patient demographics and patient-scoped record retrieval.
- [Health Gorilla Practitioner API](https://apis.io/apis/health-gorilla/health-gorilla-practitioner-api/) — Ordering and rendering providers.
- [Health Gorilla RequestGroup API](https://apis.io/apis/health-gorilla/health-gorilla-requestgroup-api/) — Parent diagnostic orders nesting individual ServiceRequest tests.
- [Health Gorilla ServiceRequest API](https://apis.io/apis/health-gorilla/health-gorilla-servicerequest-api/) — Diagnostic (lab and radiology) order requests.
- [Health Gorilla Capability Statement API](https://apis.io/apis/health-gorilla/health-gorilla-capability-statement-api/) — FHIR server capability discovery.
- [Health Gorilla Document Reference API](https://apis.io/apis/health-gorilla/health-gorilla-document-reference-api/) — Clinical document metadata.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### Arazzo workflows (4)

Multi-step workflows that chain operations into a business task.

- [Health Gorilla Coverage Retrieval](https://apis.io/arazzos/health-gorilla/health-gorilla-coverage-workflow/)
- [Health Gorilla FHIR Lab Order](https://apis.io/arazzos/health-gorilla/health-gorilla-lab-order-workflow/)
- [Health Gorilla Patient Everything](https://apis.io/arazzos/health-gorilla/health-gorilla-patient-everything-workflow/)
- [Health Gorilla Lab Results Retrieval](https://apis.io/arazzos/health-gorilla/health-gorilla-results-retrieval-workflow/)

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Health Gorilla Webhooks](https://apis.io/asyncapis/health-gorilla/health-gorilla-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [health-gorilla-docs](https://apis.io/servers/health-gorilla/health-gorilla-docs/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Health Gorilla Agentic Access](https://apis.io/agentic-access/health-gorilla/health-gorilla-agentic-access/)

#### JSON Schema (10)

The data models the API reads and writes.

- [Binary](https://apis.io/schemas/health-gorilla/health-gorilla-binary/)
- [Bundle](https://apis.io/schemas/health-gorilla/health-gorilla-bundle/)
- [CapabilityStatement](https://apis.io/schemas/health-gorilla/health-gorilla-capability-statement/)
- [Coverage](https://apis.io/schemas/health-gorilla/health-gorilla-coverage/)
- [DiagnosticReport](https://apis.io/schemas/health-gorilla/health-gorilla-diagnostic-report/)
- [DocumentReference](https://apis.io/schemas/health-gorilla/health-gorilla-document-reference/)
- [Patient](https://apis.io/schemas/health-gorilla/health-gorilla-patient/)
- [Practitioner](https://apis.io/schemas/health-gorilla/health-gorilla-practitioner/)
- [RequestGroup](https://apis.io/schemas/health-gorilla/health-gorilla-request-group/)
- [ServiceRequest](https://apis.io/schemas/health-gorilla/health-gorilla-service-request/)

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Health Gorilla Context](https://apis.io/jsonld/health-gorilla/health-gorilla-context/)

#### Collections (11)

Postman and Open Collection request collections.

- [Health Gorilla FHIR R4 API](https://apis.io/collections/health-gorilla/open-health-gorilla/)
- [Health Gorilla FHIR R4 Binary API](https://apis.io/collections/health-gorilla/open-health-gorilla-binary-api/)
- [Health Gorilla FHIR R4 Binary CapabilityStatement API](https://apis.io/collections/health-gorilla/open-health-gorilla-capabilitystatement-api/)
- [Health Gorilla FHIR R4 Binary Coverage API](https://apis.io/collections/health-gorilla/open-health-gorilla-coverage-api/)
- [Health Gorilla FHIR R4 Binary DiagnosticReport API](https://apis.io/collections/health-gorilla/open-health-gorilla-diagnosticreport-api/)
- [Health Gorilla FHIR R4 Binary DocumentReference API](https://apis.io/collections/health-gorilla/open-health-gorilla-documentreference-api/)
- [Health Gorilla FHIR R4 Binary Observation API](https://apis.io/collections/health-gorilla/open-health-gorilla-observation-api/)
- [Health Gorilla FHIR R4 Binary Patient API](https://apis.io/collections/health-gorilla/open-health-gorilla-patient-api/)
- [Health Gorilla FHIR R4 Binary Practitioner API](https://apis.io/collections/health-gorilla/open-health-gorilla-practitioner-api/)
- [Health Gorilla FHIR R4 Binary RequestGroup API](https://apis.io/collections/health-gorilla/open-health-gorilla-requestgroup-api/)
- [Health Gorilla FHIR R4 Binary ServiceRequest API](https://apis.io/collections/health-gorilla/open-health-gorilla-servicerequest-api/)

#### Overlays (10)

OpenAPI overlays, including conversational phrasing for each operation.

- [Health Gorilla Binary Api Overlay](https://apis.io/overlays/health-gorilla/health-gorilla-binary-api-overlay/)
- [Health Gorilla Capabilitystatement Api Overlay](https://apis.io/overlays/health-gorilla/health-gorilla-capabilitystatement-api-overlay/)
- [Health Gorilla Coverage Api Overlay](https://apis.io/overlays/health-gorilla/health-gorilla-coverage-api-overlay/)
- [Health Gorilla Diagnosticreport Api Overlay](https://apis.io/overlays/health-gorilla/health-gorilla-diagnosticreport-api-overlay/)
- [Health Gorilla Documentreference Api Overlay](https://apis.io/overlays/health-gorilla/health-gorilla-documentreference-api-overlay/)
- [Health Gorilla Observation Api Overlay](https://apis.io/overlays/health-gorilla/health-gorilla-observation-api-overlay/)
- [Health Gorilla Patient Api Overlay](https://apis.io/overlays/health-gorilla/health-gorilla-patient-api-overlay/)
- [Health Gorilla Practitioner Api Overlay](https://apis.io/overlays/health-gorilla/health-gorilla-practitioner-api-overlay/)
- [Health Gorilla Requestgroup Api Overlay](https://apis.io/overlays/health-gorilla/health-gorilla-requestgroup-api-overlay/)
- [Health Gorilla Servicerequest Api Overlay](https://apis.io/overlays/health-gorilla/health-gorilla-servicerequest-api-overlay/)

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [Health Gorilla API Rules](https://apis.io/rules/health-gorilla/health-gorilla-rules/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Health Gorilla Authentication](https://apis.io/security/health-gorilla/health-gorilla-authentication/)
- [Health Gorilla Domain Security](https://apis.io/security/health-gorilla/health-gorilla-domain-security/)
- [Health Gorilla Trust Center](https://apis.io/security/health-gorilla/health-gorilla-trust-center/)
- [Health Gorilla Vulnerability Disclosure](https://apis.io/security/health-gorilla/health-gorilla-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Health Gorilla Scopes](https://apis.io/scopes/health-gorilla/health-gorilla-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Health Gorilla Plans Pricing](https://apis.io/plans/health-gorilla/health-gorilla-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Health Gorilla Rate Limits](https://apis.io/rate-limits/health-gorilla/health-gorilla-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Health Gorilla Finops](https://apis.io/finops/health-gorilla/health-gorilla-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.healthgorilla.com)
- [Documentation](https://developer.healthgorilla.com)
- [Getting started](https://developer.healthgorilla.com/docs/developer-quickstart)
- [API reference](https://developer.healthgorilla.com/reference/api-reference)
- [Pricing](https://www.healthgorilla.com/home/contact)
- [Support](https://support.healthgorilla.com)
- [Changelog](https://developer.healthgorilla.com/changelog)
- [Blog](https://www.healthgorilla.com/home/resources/blogs)
- [Security](https://www.healthgorilla.com/home/security-txt)
- [Compliance](https://www.healthgorilla.com/home/company/health-data-security)
- [Terms of service](https://www.healthgorilla.com/home/terms-of-use)
- [Privacy policy](https://www.healthgorilla.com/home/privacy-policy)
- [GitHub](https://github.com/healthgorilla)
- [Status](https://status.healthgorilla.com)

## API Evangelist rating

**Kin Score 71.6** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 76.7 |
| Contract quality | 65.5 |
| Contract governance | 35.6 |
| Operational transparency | 84.2 |
| Developer ergonomics | 49.4 |
| Access clarity | 85.5 |

**Agent readiness 43.4** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | verified |
| Auth Clarity | served (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 52.3** — Health

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/health-gorilla/](https://apis.io/providers/health-gorilla/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Health Gorilla: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/health-gorilla/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
