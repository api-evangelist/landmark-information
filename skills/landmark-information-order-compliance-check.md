---
name: Order a Landmark compliance check and collect the result
description: Place an AML, ownership, title, source-of-funds or identity-verification order through the Landmark Order Experience API, track it to completion, and download the result document.
api: openapi/landmark-information-order-experience-api-openapi.yml
operations:
  - order-experience-create-order
  - order-experience-get-order-status
  - order-experience-get-order
  - order-experience-download-order-documents
  - order-experience-override-order-result-aml-section
---

# Order a Landmark compliance check and collect the result

Use this when a property transaction needs a regulated check on a person or company —
AML individual or company, UK or international AML with facial recognition, Persons with
Significant Control, Landmark Ownership Check, Scottish Title Check, Source of Funds Check,
or Identity Verification Check.

**Base URL** `https://api.landmarkcloudservices.com/connect` (UAT: `https://uat-api.landmarkcloudservices.com/connect`)

## Before you start

1. You need an onboarded Landmark account. Client ID and secret are issued by a Landmark
   commercial contact, separately for UAT and production. There is no self-service signup.
2. Get a token: POST `client_id`, `client_secret`, `grant_type=client_credentials` and
   `audience=https://api.landmarkcloudservices.com` to `https://lmkmaster.eu.auth0.com/oauth/token`.
   Use the UAT tenant `https://lmkmaster-uat.eu.auth0.com/oauth/token` with the UAT audience while
   building. Cache the token until close to `expires_in`; do not fetch one per call.
3. Send `Authorization: Bearer <access_token>` on every request.
4. **Production orders are billable and create real regulated records.** Build against UAT.

## Steps

1. **Place the order** — `order-experience-create-order` (`POST /orders`).
   The request body is product-specific; pick the product schema for the check you need and supply
   the person or company details it requires. Note two documented rules: `dateOfBirth` must not be
   within the last 16 years, and `transactionAddress` is not required for every product.
   Include a `callback.url` in the body if you want to be told when the order finishes instead of
   polling — Landmark POSTs an `orderStatusResponse` to it (see
   `asyncapi/landmark-information-webhooks.yml`).
   Returns **202 Accepted** with the `orderId`. The order is not complete at this point.

2. **Track it** — `order-experience-get-order-status` (`GET /orders/{orderId}/status`).
   Poll this until `status` leaves the in-progress states. `statusDescription` carries the detail.
   `Cancelled` is a valid terminal value. Skip this step entirely if you registered a callback.

3. **Read the result** — `order-experience-get-order` (`GET /orders/{orderId}`).
   Returns the full result payload, including `overallStatus` on the AML products and the
   `pepsAndSanctions`, `addressAndMortality` and `idVerification` sections, plus a `documents`
   array carrying `documentId`, `filename` and `createdDate`.

4. **Download the document** — `order-experience-download-order-documents`
   (`GET /orders/{orderId}/documents/{documentId}`). Returns the file itself.
   **Handle 410 Gone**: result documents expire and this operation is the only one in the API
   that returns 410 (`code` 41000). Fetch and store the document when you first see it.

5. **Override an AML section** (only if your account is entitled and a human has reviewed the
   result) — `order-experience-override-order-result-aml-section`
   (`PUT /orders/{orderId}/results/override-aml-section`). Returns 204. This is a compliance
   decision with regulatory weight; never let an agent perform it unattended.

## Rules

- **No idempotency key.** Re-POSTing `/orders` places a second billable order. Record the `orderId`
  against your case before retrying anything, and never blind-retry a 5xx on order creation.
- **Errors** are `application/problem+json` with `status`, `code`, `title` and optional `messages[]`.
  `40001` is validation — read `messages[]`, each entry names the offending property.
  `40100` means the token is missing, expired or has the wrong audience.
  `40300`/`40301` mean the account is not entitled to that product — a commercial issue, not a
  token issue, so do not retry.
  `42900` is rate limiting. Full catalogue: `errors/landmark-information-problem-types.yml`.
- **Trace**: quote the `traceresponse` header when raising support. A malformed `traceparent`
  request header is rejected with `40002`.
