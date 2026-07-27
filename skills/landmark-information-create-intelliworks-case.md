---
name: Create and progress an Intelliworks case from another system
description: Create, update and read cases in the Intelliworks legal case management system from an external application, upsert tasks and milestones, and move documents in and out.
api: openapi/landmark-information-intelliworks-api-openapi.yml
operations:
  - createCase
  - updateIwCase
  - getCaseIw
  - getTransactionRequestStatus
  - upsertTask
  - getMilestone
  - upsertMilestone
  - uploadDocument
  - getCompletedDocuments
  - downloadDocument
---

# Create and progress an Intelliworks case from another system

Everything done through this API is visible in the Intelliworks UI, and vice versa. The point is
to stop conveyancers re-keying data that already exists in the originating system.

**Base URL** `https://api.landmarkcloudservices.com/` (UAT: `https://uat-api.landmarkcloudservices.com/`)

## Before you start

You need two identifiers that are **not discoverable through the API**:

- **`branchId`** — a UUID per office/site of the customer firm, issued by Ochresoft. Request them
  from Ochresoft before you integrate.
- **`workflowId`** — the case type. Documented values: `220-Sale`, `210-Purchase`,
  `216-New Build Purchase`, `10200-General Property`, `300-Remortgage`, `360-Equity Release (360)`,
  `700-Transfer of Equity`, `415-Wills`, `500-Lasting Power of Attorney`, `601-Probate`.

## Steps

1. **Create the case** — `createCase` (`POST /case`) with the workflow-specific body: clients, a
   summary, the case type, and for conveyancing the property and price agreed. Returns **202
   Accepted** with a transaction id — *the case does not exist yet*.
2. **Confirm it landed** — `getTransactionRequestStatus`
   (`GET /transaction-requests/{transactionRequestId}`). Poll until the request resolves. Every
   write on this API is asynchronous and returns 202; this is how you find out whether it worked.
3. **Update** — `updateIwCase` (`POST /updateCase`) takes the same workflow-specific body as create,
   plus the parent `transactionId` from the original create response.
4. **Read back** — `getCaseIw` (`GET /cases`) by `branchId` plus at least one of `caseId` (the
   Intelliworks reference) or `externalCaseId` (your reference). Supplying neither is a 400.
5. **Tasks** — `upsertTask` (`POST /upsertTask`). Create-or-update semantics, 202 Accepted.
6. **Milestones** — `getMilestone` (`GET /milestones`) returns the actual completion date of one
   milestone; supply `branchId`, `milestoneId` and one of `caseId`/`externalCaseId`, plus
   `workflowId` where the workflow requires it. `upsertMilestone` (`POST /milestones`) writes one.
   **Milestone ids are workflow-specific** and enumerated in Landmark's published documentation —
   look them up per workflow, never reuse an id across workflows.
7. **Documents** — `uploadDocument` (`POST /documents`, 202),
   `getCompletedDocuments` (`GET /documents`), `downloadDocument` (`GET /documents/{id}/download`,
   returns the file).

## Rules

- **202 does not mean success.** Treat every write as a request, and reconcile through
  `getTransactionRequestStatus` or by reading the case back. Do not report a case as created on the
  strength of the 202 alone.
- **No idempotency key.** Retrying a `POST /case` after a timeout can create a duplicate case in a
  live legal matter. Carry your own `externalCaseId`, and on any uncertain retry call `getCaseIw`
  with it first.
- **Errors**: `application/problem+json` with `status`/`code`/`title`/`messages[]`. This API also
  declares **406** and **415** — send `application/json` (or `multipart/form-data` for uploads) and
  accept JSON. `40000` is an invalid content type. `40401` is not found.
- Support: support@ochresoft.com, +44 (0)3300 366 700.
