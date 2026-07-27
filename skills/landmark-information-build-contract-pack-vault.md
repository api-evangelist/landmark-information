---
name: Build and share a Contract Pack Vault
description: Assemble a secure, shareable container of transaction documents from a case management system using the Landmark Document Vault API, then hand it to the web app for review and sharing.
api: openapi/landmark-information-document-vault-api-openapi.yml
operations:
  - document-vault-vaults-create
  - document-vault-documents-create
  - document-vault-vaults-read
  - document-vault-reference-update
  - document-vault-property-update
  - document-vault-recipient-organisation-update
  - document-vault-recipients-create
  - document-vault-recipients-delete
  - document-vault-documents-delete
  - document-vault-activities-list
---

# Build and share a Contract Pack Vault

The API builds and maintains the vault. Reviewing the AI analysis and actually sharing it with the
buyer's conveyancer happen in the Contract Pack Vault web app — there is no share operation in the
API.

**Base URL** `https://api.landmarkcloudservices.com/document-vaults` (UAT: `https://uat-api.landmarkcloudservices.com/document-vaults`)

## Before you start

- Auth0 client credentials, audience `https://api.landmarkcloudservices.com`.
- **This API also requires `Account-Id: <your account id>` on every request** — issued with your
  credentials. It is the only Landmark API with an account header.
- **Billing**: a charge applies per vault when the *first document* is added. Creating an empty
  vault is free; adding a document is not. UAT is not charged.

## Steps

1. **Create the vault** — `document-vault-vaults-create` (`POST /`) with the property address and
   whatever detail you have. Returns the vault `id`. Optionally set `reference` (your case
   reference) — it must be unique within your account, and a clash returns **409** (`40900`).
2. **Add documents one per call** — `document-vault-documents-create`
   (`POST /{documentVaultId}/documents`), `multipart/form-data`.
   Limits: one document per call, up to 60 per vault, 25 MB per file, PDF/DOC/DOCX/JPEG/PNG only.
   Exceeding the size returns **413**.
   The document comes back `Pending` while it is virus-scanned and analysed, then becomes
   `Available` or `Quarantined` if it failed the scan. **Do not treat a 200 as "document is in the
   pack"** — re-read the vault until the status settles.
3. **Keep details current** — `document-vault-reference-update` (`PUT /{documentVaultId}/reference`),
   `document-vault-property-update` (`PATCH /{documentVaultId}/property`),
   `document-vault-recipient-organisation-update`
   (`PATCH /{documentVaultId}/recipient-organisation`).
4. **Set up recipients** — `document-vault-recipients-create`
   (`POST /{documentVaultId}/recipient-organisation/recipients`), individual or team.
   **Adding a recipient is not sharing.** Sharing happens in the web app, and the recipient only
   gets access after verifying their email.
5. **Check progress** — `document-vault-vaults-read` (`GET /{documentVaultId}`) for state, or
   `document-vault-activities-list` (`GET /{documentVaultId}/activities`) for the full audit trail.
6. **Hand over to the web app** — deep-link from your case management system using the vault id:
   `https://connect.landmark.co.uk/case/{documentVaultId}` (UAT:
   `https://uat-connect.landmark.co.uk/case/{documentVaultId}`).

## Rules

- **No idempotency key.** Re-POSTing a create is a second billable vault. Use your unique
  `reference` as the guard: create, and treat a 409 on reference as "already exists", then look it
  up rather than creating again.
- The AI checklist (document typing, missing pages, signature presence, address/name/date
  cross-checks) is **not returned by the API** — it is only visible in the web app. Do not promise
  a caller programmatic access to it.
- **Rate limit** 1,000 calls per minute per caller; over it returns **429** with code `42900` and
  no `Retry-After` header, so back off on your own schedule.
- **Errors**: `application/problem+json`, `status`/`code`/`title`/`messages[]`. `40400` is not
  found on this API (the other Landmark APIs use `40401`). Quote `lgsTraceResponse` to support at
  support@ochresoft.com.
