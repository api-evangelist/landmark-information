# Landmark Information Group (landmark-information)

Landmark Information Group is a United Kingdom property and land data business, part of Daily Mail and General Trust (DMGT), that sits in the middle of the UK residential and commercial property transaction rather than at the listing end of it. Founded in 1995 and headquartered in Exeter, it aggregates 700+ datasets from nearly 400 suppliers — Ordnance Survey mapping and AddressBase/UPRN addressing, environmental and flood and mining risk, historical maps, planning applications, and Barbour ABI project data — and sells them as conveyancing search reports (SearchFlow, Envirocheck, RiskView, SiteSolutions), estate agency compliance and material information products (LandmarkAgent, Metropix floor plans), case management software for property lawyers (Optimus, Intelliworks, Ochresoft, Vantage), and lender/surveyor valuation infrastructure (Secure Panel Network SPN and SPN+, Q-Guard).

The UK has no MLS and no RESO equivalent — residential listings are controlled by the Rightmove/Zoopla duopoly and reached through agency CRMs — so Landmark is not a listings company; it is the transaction-data and workflow layer beneath conveyancers, lenders, surveyors, and agents. Its API posture is unusually honest for this sector: Landmark runs a genuinely public, un-gated API documentation portal at landmarkcloudservices.com that publishes full OpenAPI 3.x contracts for its Compliance/Order, Conveyancing, Intelliworks, Document Vault, and Milestone Notification APIs, plus a public HTML technical pack for the Barbour ABI-powered Planning API. Reading the contracts is open to anyone; calling them is not. Every API is OAuth 2.0 client-credentials against Landmark's Auth0 tenant with a client ID and secret issued only after a commercial account is onboarded, and the Planning API requires a paid subscription or pay-as-you-go agreement plus a Landmark-issued API key. There is no RESO Web API certification, no RESO Data Dictionary posture, no OData `$metadata` document and no Universal Property Identifier anywhere in Landmark's surface — RESO is a North American MLS construct and is simply absent from the UK market. Landmark publishes no open data of its own; the open UK property layer belongs to HM Land Registry and Ordnance Survey, both of which are Landmark suppliers rather than Landmark products.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/landmark-information/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/landmark-information/refs/heads/main/apis.yml)

## Tags

- Real Estate
- United Kingdom
- PropTech
- Property Data
- Conveyancing
- Land Registry
- Geospatial
- Valuation
- Anti-Money Laundering
- Planning Data
- Mortgage

## Timestamps

- **Created:** 2026-07-26
- **Modified:** 2026-07-26

## APIs

### Landmark Order Experience API

Compliance ordering API used to place and retrieve Landmark compliance product orders — AML individual and company checks, UK and international AML with facial recognition, Persons with Significant Control, Landmark Ownership Check, Scottish Title Check, Source of Funds Check and Identity Verification Check. Five operations covering order creation, order retrieval, order status, document download, and an AML section override. Version 1.3.1 (2026-04-15), OpenAPI 3.0.3, harvested from the public Landmark Cloud Services documentation portal.

- **Human URL:** [https://www.landmarkcloudservices.com/?api=order-experience-api](https://www.landmarkcloudservices.com/?api=order-experience-api)
- **Base URL:** `https://api.landmarkcloudservices.com/connect`

#### Tags

- Compliance
- Anti-Money Laundering
- Identity Verification
- Orders

#### Properties

- [OpenAPI](openapi/landmark-information-order-experience-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://www.landmarkcloudservices.com/order-experience-api.html)
- [Authentication](authentication/landmark-information-openid-configuration.json)

### Landmark Conveyancing Experience API

Panel conveyancing API for quoting, instructing and managing conveyancing work through Landmark Optimus. Introducers create quotes, choose a conveyancer and instruct on a client's behalf; conveyancers accept or reject assigned cases and progress them against one shared case record. Twenty paths across Quotes and Cases including quote PDF generation, persons, instruct, accept/reject, status, handler, activities, tasks, notes and documents. Version 0.8.1, OpenAPI 3.0.3, with several endpoints explicitly marked Preview and not yet safe to build against. Uses OData-style `$filter` and `$orderby` query parameters, but is not an OData service and publishes no `$metadata` document.

- **Human URL:** [https://www.landmarkcloudservices.com/?api=conveyances-experience-api](https://www.landmarkcloudservices.com/?api=conveyances-experience-api)
- **Base URL:** `https://api.landmarkcloudservices.com/conveyances`

#### Tags

- Conveyancing
- Quotes
- Cases
- Panel Management

#### Properties

- [OpenAPI](openapi/landmark-information-conveyancing-experience-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://www.landmarkcloudservices.com/conveyances-experience-api.html)
- [Documentation](https://www.landmark.co.uk/products/optimus/)
- [Authentication](authentication/landmark-information-openid-configuration.json)

### Landmark Intelliworks APIs

Case creation and management API for the Intelliworks legal case management system, letting third-party systems create and update cases outside the Intelliworks UI for Sale, Purchase, New Build Purchase, General Property, Remortgage, Equity Release, Transfer of Equity, Wills, Lasting Power of Attorney and Probate workflows. Eight paths covering case create/update/list, task upsert, milestones, transaction requests, and document upload/list/download. Version 2.3.0, OpenAPI 3.0.1.

- **Human URL:** [https://www.landmarkcloudservices.com/?api=intelliworks-experienceapi-CreateCase-api](https://www.landmarkcloudservices.com/?api=intelliworks-experienceapi-CreateCase-api)
- **Base URL:** `https://api.landmarkcloudservices.com/`

#### Tags

- Case Management
- Conveyancing
- Documents
- Legal

#### Properties

- [OpenAPI](openapi/landmark-information-intelliworks-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://www.landmarkcloudservices.com/intelliworks-experienceapi-CreateCase-api.html)
- [Documentation](https://www.landmark.co.uk/legal-conveyancing/case-management/)
- [Authentication](authentication/landmark-information-openid-configuration.json)

### Landmark Document Vault API

API behind Contract Pack Vault — creates a secure, shareable container of transaction documents, adds and removes files (virus-scanned and analysed asynchronously, status `Pending` then `Available` or `Quarantined`), maintains property and reference details, manages the recipient organisation and its recipients, and reads the vault activity audit trail. Ten paths, version 1.0.1, OpenAPI 3.0.4. Sharing itself happens in the Contract Pack Vault web app, not the API. Billed per vault on first document added; documented rate limit 1,000 calls per minute per caller.

- **Human URL:** [https://www.landmarkcloudservices.com/?api=document-vault-experience](https://www.landmarkcloudservices.com/?api=document-vault-experience)
- **Base URL:** `https://api.landmarkcloudservices.com/document-vaults`

#### Tags

- Documents
- Conveyancing
- Contract Pack

#### Properties

- [OpenAPI](openapi/landmark-information-document-vault-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://www.landmarkcloudservices.com/document-vault-experience.html)
- [Documentation](https://www.landmark.co.uk/legal-conveyancing/contract-pack-vault/)
- [Authentication](authentication/landmark-information-openid-configuration.json)

### Landmark Milestone Notification Service API

Callback registration API for valuation transaction milestone notifications on the Landmark Secure Panel Network (SPN). Consumers register, update and delete callback URLs that Landmark then calls as valuation milestones occur, making this Landmark's webhook subscription surface. Two paths, version 1.0.0, OpenAPI 3.0.1. Documented rate limit 250 requests per customer per minute.

- **Human URL:** [https://www.landmarkcloudservices.com/?api=milestone-service-api](https://www.landmarkcloudservices.com/?api=milestone-service-api)
- **Base URL:** `https://api.landmarkcloudservices.com/valuation-spn/milestones/callbacks`

#### Tags

- Webhooks
- Valuation
- Milestones
- Lending

#### Properties

- [OpenAPI](openapi/landmark-information-milestone-notification-service-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://www.landmarkcloudservices.com/milestone-service-api.html)
- [Documentation](https://www.landmark.co.uk/products/spn/)
- [Authentication](authentication/landmark-information-openid-configuration.json)

### Landmark Planning API (powered by Barbour ABI)

RESTful planning-application data API combining Barbour ABI project information with Landmark geospatial data, covering UK and Republic of Ireland planning applications from 1 January 2017 (with historical project data back to 1997) across 19 documented attributes including UPRN, easting/northing, latitude/longitude and GeoJSON/WKT site boundaries. Documented operations are `GET login`, `GET logout`, `GET customers`, `GET lookups`, `GET locations` (preview search with a JSON query DSL and point-radius distance filtering) and `GET locations/{project_id}` (full details, which consumes a credit under pay-as-you-go). Documented in public HTML only — no OpenAPI, Postman collection, or other machine-readable contract is published. Authentication is a Landmark-issued `x-api-key` plus a Basic-auth login (base64 of username and SHA256-hashed password) that returns a bearer token valid until 30 days of disuse.

- **Human URL:** [https://www.landmark.co.uk/products/planning-api/planning-api-documentation/](https://www.landmark.co.uk/products/planning-api/planning-api-documentation/)
- **Base URL:** `https://api.barbour-abi.com/v4`

#### Tags

- Planning
- Geospatial
- Land Development
- Commercial Real Estate

#### Properties

- [Documentation](https://www.landmark.co.uk/products/planning-api/)
- [API Reference](https://www.landmark.co.uk/products/planning-api/planning-api-documentation/)

### Landmark Geodata Web Map Tile Service (WMTS)

On-demand raster mapping tile service delivered against the Open Geospatial Consortium Web Map Tile Service (OGC WMTS) standard, with 20 zoom levels spanning Ordnance Survey MasterMap through national-scale mapping, for use inside GIS platforms and web applications. Landmark documents the product and names the standard publicly but publishes no endpoint URL and no GetCapabilities document; access begins with a register-your-interest form at geodata.landmark.co.uk and a commercial agreement, so no base URL is recorded here.

- **Human URL:** [https://www.landmark.co.uk/products/web-map-tile-service-0/](https://www.landmark.co.uk/products/web-map-tile-service-0/)

#### Tags

- Geospatial
- Mapping
- WMTS
- OGC

#### Properties

- [Documentation](https://www.landmark.co.uk/products/web-map-tile-service-0/)
- [Sign Up](https://geodata.landmark.co.uk/register-your-interest-in-wmts)

## Common Properties

- [Website](https://www.landmark.co.uk/)
- [Documentation](https://www.landmarkcloudservices.com/)
- [Authentication](authentication/landmark-information-openid-configuration.json)
- [Sign Up](https://www.landmark.co.uk/our-group/contact/)
- [Blog](https://www.landmark.co.uk/news-insights/blog/)
- [Blog RSS](https://www.landmark.co.uk/feed/)
- [Privacy Policy](https://www.landmark.co.uk/privacy-policy/)
- [Terms of Service](https://www.landmark.co.uk/terms-conditions/)
- [GitHub Organization](https://github.com/Landmark-Information-Group)
- [LinkedIn](https://www.linkedin.com/company/landmark-information-group)
- [Careers](https://www.landmark.co.uk/careers/)
- [Partners](https://www.landmark.co.uk/partners-suppliers/)

## RESO Posture and Access

- **RESO posture:** No RESO reference found. No Web API certification, no Data Dictionary certification, no Universal Property Identifier, no OData `$metadata`. RESO is a North American MLS construct administered under NAR policy; the UK has no MLS, so it does not apply. The identifier Landmark actually uses throughout its contracts is the Ordnance Survey UPRN — a government identifier, not an industry-body one.
- **RESO certified:** No.
- **Access gate:** `partner-only`. Documentation is fully public and login-free; credentials are not. A developer must have a commercial account with Landmark before any client ID and secret (or Planning API key) is issued.
- **Open data:** No. Landmark publishes no open, unlicensed dataset. The open UK property layer — HM Land Registry Price Paid and Ordnance Survey open products — belongs to the public sector and is Landmark's supply, not Landmark's product.
- **Auth model:** OAuth 2.0 client credentials against Auth0 (`https://lmkmaster.eu.auth0.com/oauth/token`, audience `https://api.landmarkcloudservices.com`) returning a bearer JWT, plus an `Account-Id` header on the Document Vault API. The Planning API uses a separate `x-api-key` plus Basic-auth login token scheme against `api.barbour-abi.com`. No OAuth scopes are published; entitlement is enforced server-side per account.
- **Home market:** United Kingdom.

## Maintainers

- **Kin Lane** — kin@apievangelist.com
