---
name: Subscribe to Landmark valuation milestone notifications
description: Register, update and remove callback endpoints on the Landmark Secure Panel Network so Landmark pushes valuation transaction milestones to your system, and handle the nine notification types correctly.
api: openapi/landmark-information-milestone-notification-service-api-openapi.yml
operations:
  - spn-milestone-register-callback
  - spn-milestone-update-callback
  - spn-milestone-delete-callback
---

# Subscribe to Landmark valuation milestone notifications

This is Landmark's webhook subscription surface for the Secure Panel Network. You register a URL;
Landmark POSTs valuation milestones to it as they happen.

**Base URL** `https://api.landmarkcloudservices.com/valuation-spn/milestones/callbacks`
(UAT: `https://uat-api.landmarkcloudservices.com/valuation-spn/milestones/callbacks`)

## Register

`spn-milestone-register-callback` (`POST /callbacks`) → **201** with the `callbackId`.

The body is one of three shapes, chosen by how you want Landmark to authenticate *to you*:

- **Basic** — username and password on the callback request.
- **ClientIdSecret** — a client id and secret presented on the callback request.
- **OAuth2** — Landmark fetches a token from your `token_generation_url` using a `client_id` and
  `client_secret` (optionally `audience` and `scope`) and presents it as
  `Authorization: Bearer` on the callback. Prefer this one.

`spn-milestone-update-callback` (`PUT /callbacks/{callbackId}`) and
`spn-milestone-delete-callback` (`DELETE /callbacks/{callbackId}`) both return **204**.
Registering a duplicate returns **409** (`40900`).

## Receiving notifications

Landmark POSTs a `lgsTransactionRequestMilestoneSPN` body. **Answer 204 No Content.** Non-2xx
responses (400/401/403/429/500) are recognised failures.

Every payload carries the envelope — `transactionId`, `transactionRequestId`,
`transactionRequestMilestoneId`, `transactionRequestType` (`Order`, `Inspection`,
`PanelConveyancing` or `InspectionRequest`), `datePredicted`, `dateAchieved` and an optional
`additionalInformation` string — plus one of nine typed variants:

| id | milestoneName | extra fields |
|----|---------------|--------------|
| 1 | Valuation Instructed | surveyorBranchId |
| 2 | Instruction Panelled | surveyorBranchId, reason |
| 3 | Valuation Held | reason |
| 4 | Contact Tried | reason |
| 5 | Valuation Cancelled | reason |
| 6 | Valuation Booked | appointmentDate, timeWindowStart, timeWindowEnd |
| 7 | Valuation Complete | — |
| 8 | Document Available | documentId, tags |
| 9 | Valuation Rejected | surveyorBranchId, reason |

Switch on `milestoneId`, not on `milestoneName` — the name is a fixed string pattern in the schema
but the id is the stable discriminator. The payload schema sets `additionalProperties: true`, so
tolerate unknown fields rather than rejecting.

## Rules

- **Rate limit** 250 requests per customer per minute, 429 with code `42900`.
- **No idempotency key and no delivery-id header.** Deduplicate on
  `transactionRequestMilestoneId`, and make your handler idempotent — a retried delivery must not
  double-advance your workflow.
- Milestones cannot be triggered synthetically. To test, register a UAT callback and exercise the
  underlying valuation workflow.
- **Errors**: `application/problem+json`; **413** is declared on registration, so keep the callback
  configuration body small.
- Support: lvsinfo@landmark.co.uk, +44 (0)3300 366 110.
