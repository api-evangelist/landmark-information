---
name: Quote and instruct panel conveyancing
description: Create a conveyancing quote as an introducer, complete it with people and property details, instruct a panel conveyancer, and then work the resulting case through the Landmark Conveyancing Experience API.
api: openapi/landmark-information-conveyancing-experience-api-openapi.yml
operations:
  - conveyances-experience-quote-create
  - conveyances-experience-quote-person-create
  - conveyances-experience-quote-address-update
  - conveyances-experience-quote-product-details-update
  - conveyances-experience-quote-pdf-download
  - conveyances-experience-quote-instruct
  - conveyances-experience-case-list
  - conveyances-experience-case-read
  - conveyances-experience-case-accept
  - conveyances-experience-case-reject
  - conveyances-experience-case-status-update
  - conveyances-experience-case-handler-add
  - conveyances-experience-case-task-list
  - conveyances-experience-case-task-complete
  - conveyances-experience-case-note-create
---

# Quote and instruct panel conveyancing

Two roles share one API and one case record. As an **introducer** you quote, choose a conveyancer
and instruct on the client's behalf. As a **conveyancer** you pick up assigned cases and progress
them. You only ever see cases your account is party to.

**Base URL** `https://api.landmarkcloudservices.com/conveyances` (UAT: `https://uat-api.landmarkcloudservices.com/conveyances`)

Auth is the same Auth0 client-credentials flow as every Landmark API; there is no `Account-Id`
header on this one — the credentials identify the account.

**Version 0.8.1.** `conveyances-experience-case-document-create` and
`conveyances-experience-case-document-read` are marked **Preview** by Landmark: do not build
against them.

## Introducer flow

1. `conveyances-experience-quote-create` (`POST /quotes`) → **201** with the `quoteId`.
2. Complete the quote:
   - `conveyances-experience-quote-person-create` (`POST /quotes/{quoteId}/persons`) for each party;
     each returns a `personReference` you use to update or remove them
     (`conveyances-experience-quote-person-update`, `conveyances-experience-quote-person-delete`).
   - `conveyances-experience-quote-address-update` (`PUT /quotes/{quoteId}/property-address`).
   - `conveyances-experience-quote-product-details-update` (`PUT /quotes/{quoteId}/product-details`).
3. `conveyances-experience-quote-pdf-download` (`GET /quotes/{quoteId}/pdf`) to hand the client a
   quote document. Returns the file itself, not JSON.
4. `conveyances-experience-quote-instruct` (`POST /quotes/{quoteId}/instruct`) → **201**.
   **This is the point of no return** — the quote becomes a live case and a conveyancer is engaged
   on your client's behalf. Require explicit human confirmation before calling it.

## Conveyancer flow

1. `conveyances-experience-case-list` (`GET /cases`) — supports `$top`, `$skip`, `$filter` and
   `$orderby`. This is OData-flavoured query syntax, not an OData service: there is no `$metadata`
   document, so do not point an OData client at it.
2. `conveyances-experience-case-read` (`GET /cases/{caseId}`).
3. `conveyances-experience-case-accept` or `conveyances-experience-case-reject`
   (`POST /cases/{caseId}/accept` | `/reject`). Rejection takes a reason in the body.
4. `conveyances-experience-case-handler-add` (`PUT /cases/{caseId}/handler`) to name the fee earner.
   This is the one operation that can return **409** — the case is not in a state that accepts a
   handler.
5. Progress the case: `conveyances-experience-case-status-update` (`POST /cases/{caseId}/status`),
   `conveyances-experience-case-task-list` then `conveyances-experience-case-task-complete`
   (`PUT /cases/{caseId}/tasks/{taskId}/complete`), and
   `conveyances-experience-case-note-create` (`POST /cases/{caseId}/notes`) to keep the introducer
   informed. `conveyances-experience-case-activity-list` is the shared audit trail.

## Rules

- **No idempotency key.** `POST /quotes` and `POST /quotes/{quoteId}/instruct` are both unsafe to
  blind-retry. Store the id you got back before any retry logic runs.
- **Errors**: `application/problem+json` with `status`, `code`, `title`, `messages[]`. `40001` is
  validation with per-property messages; `40302` means your account is not a party to that case;
  `40900` means the case is not in a valid status for the operation you attempted.
- **Trace**: every response carries `traceresponse`; quote it to support.
- Support contact for this API is listed as TBC in Landmark's own documentation.
