# Landmark Information Group

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

Landmark Information Group is a United Kingdom property and land data business, part of Daily Mail and General Trust (DMGT), that sits in the middle of the UK residential and commercial property transaction rather than at the listing end of it. Founded in 1995 and headquartered in Exeter, it aggregates 700+ datasets from nearly 400 suppliers — Ordnance Survey mapping and AddressBase/UPRN addressing, environmental and flood and mining risk, historical maps, planning applications, and Barbour ABI project data — and sells them as conveyancing search reports (SearchFlow, Envirocheck, RiskView, SiteSolutions), estate agency compliance and material information products (LandmarkAgent, Metropix floor plans), case management software for property lawyers (Optimus, Intelliworks, Ochresoft, Vantage), and lender/surveyor valuation infrastructure (Secure Panel Network SPN and SPN+, Q-Guard). The UK has no MLS and no RESO equivalent — residential listings are controlled by the Rightmove/Zoopla duopoly and reached through agency CRMs — so Landmark is not a listings company; it is the transaction-data and workflow layer beneath conveyancers, lenders, surveyors, and agents. Its API posture is unusually honest for this sector: Landmark runs a genuinely public, un-gated API documentation portal at landmarkcloudservices.com that publishes full OpenAPI 3.x contracts for its Compliance/Order, Conveyancing, Intelliworks, Document Vault, and Milestone Notification APIs, plus a public HTML technical pack for the Barbour ABI-powered Planning API. Reading the contracts is open to anyone; calling them is not. Every API is OAuth 2.0 client-credentials against Landmark's Auth0 tenant with a client ID and secret issued only after a commercial account is onboarded ("your Landmark contact will confirm what's available to you"), and the Planning API requires a paid subscription or pay-as-you-go agreement plus an API key issued by Landmark. There is no RESO Web API certification, no RESO Data Dictionary posture, no OData $metadata document and no Universal Property Identifier anywhere in Landmark's surface — RESO is a North American MLS construct and is simply absent from the UK market. Landmark publishes no open data of its own; the open UK property layer belongs to HM Land Registry and Ordnance Survey, both of which are Landmark suppliers rather than Landmark products.

**Areas:** Real Estate · United Kingdom · PropTech · Property Data · Conveyancing · Land Registry · Geospatial · Valuation · AML · Planning Data · Mortgage

## Landmark Information Group on APIs.io

Everything profiled for Landmark Information Group is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/landmark-information/](https://apis.io/providers/landmark-information/)** — or go straight to one of the APIs or properties below.

### APIs (10)

- [Landmark Planning API (powered by Barbour ABI)](https://apis.io/apis/landmark-information/landmark-planning-api/) — RESTful planning-application data API combining Barbour ABI project information with Landmark geospatial data, covering UK and Republic of Ireland planning…
- [Landmark Geodata Web Map Tile Service (WMTS)](https://apis.io/apis/landmark-information/landmark-geodata-web-map-tile-service/) — On-demand raster mapping tile service delivered against the Open Geospatial Consortium Web Map Tile Service (OGC WMTS) standard, with 20 zoom levels…
- [Landmark Information Group Activities API](https://apis.io/apis/landmark-information/landmark-information-activities-api/) — Read a vault's audit history.
- [Landmark Information Group Cases API](https://apis.io/apis/landmark-information/landmark-information-cases-api/) — Once you instruct a quote it becomes a case. If you're the conveyancer, these are the cases assigned to you: you work them through to completion and post…
- [Landmark Information Group Document Vaults API](https://apis.io/apis/landmark-information/landmark-information-document-vaults-api/) — Create a vault and manage its details and recipients.
- [Landmark Information Group Documents API](https://apis.io/apis/landmark-information/landmark-information-documents-api/) — Add and remove the files held in a vault.
- [Landmark Information Group Milestones API](https://apis.io/apis/landmark-information/landmark-information-milestones-api/) — Operations to manage callback configurations for transaction milestone notifications
- [Landmark Information Group Order Experience API](https://apis.io/apis/landmark-information/landmark-information-order-experience-api-api/) — Operations to create and receive order results.
- [Landmark Information Group Quotes API](https://apis.io/apis/landmark-information/landmark-information-quotes-api/) — Quotes are where a job begins. You build a quote for your client's transaction, get back the panel conveyancers available to you with their pricing, and…
- [Landmark Information Group Transaction Requests API](https://apis.io/apis/landmark-information/landmark-information-transaction-requests-api/) — APIs for tracking asynchronous request status

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### Arazzo workflows (4)

Multi-step workflows that chain operations into a business task.

- [Assemble a Contract Pack Vault](https://apis.io/arazzos/landmark-information/landmark-information-assemble-contract-pack/)
- [Order a Landmark compliance check and collect the result](https://apis.io/arazzos/landmark-information/landmark-information-order-compliance-check/)
- [Quote to conveyancing instruction](https://apis.io/arazzos/landmark-information/landmark-information-quote-to-instruction/)
- [Subscribe to valuation milestone notifications](https://apis.io/arazzos/landmark-information/landmark-information-subscribe-valuation-milestones/)

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Landmark Information Webhooks](https://apis.io/asyncapis/landmark-information/landmark-information-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [landmark-information](https://apis.io/servers/landmark-information/landmark-information/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Landmark Information Agentic Access](https://apis.io/agentic-access/landmark-information/landmark-information-agentic-access/)

#### Collections (5)

Postman and Open Collection request collections.

- [Landmark Conveyancing Experience API](https://apis.io/collections/landmark-information/open-landmark-information-conveyancing-experience-api/)
- [Document Vault API](https://apis.io/collections/landmark-information/open-landmark-information-document-vault-api/)
- [Intelliworks APIs](https://apis.io/collections/landmark-information/open-landmark-information-intelliworks-api/)
- [Milestone Notification Service API](https://apis.io/collections/landmark-information/open-landmark-information-milestone-notification-service-api/)
- [Order Experience API](https://apis.io/collections/landmark-information/open-landmark-information-order-experience-api/)

#### Overlays (5)

OpenAPI overlays, including conversational phrasing for each operation.

- [Landmark Information Conveyancing Experience Api Overlay](https://apis.io/overlays/landmark-information/landmark-information-conveyancing-experience-api-overlay/)
- [Landmark Information Document Vault Api Overlay](https://apis.io/overlays/landmark-information/landmark-information-document-vault-api-overlay/)
- [Landmark Information Intelliworks Api Overlay](https://apis.io/overlays/landmark-information/landmark-information-intelliworks-api-overlay/)
- [Landmark Information Milestone Notification Service Api Overlay](https://apis.io/overlays/landmark-information/landmark-information-milestone-notification-service-api-overlay/)
- [Landmark Information Order Experience Api Overlay](https://apis.io/overlays/landmark-information/landmark-information-order-experience-api-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Landmark Information Authentication](https://apis.io/security/landmark-information/landmark-information-authentication/)
- [Landmark Information Domain Security](https://apis.io/security/landmark-information/landmark-information-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Landmark Information Scopes](https://apis.io/scopes/landmark-information/landmark-information-scopes/)

#### Rate limits (1)

Published request limits.

- [Landmark Information Rate Limits](https://apis.io/rate-limits/landmark-information/landmark-information-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.landmark.co.uk/)
- [Documentation](https://www.landmarkcloudservices.com/)
- [Getting started](https://www.landmarkcloudservices.com/conveyances-experience-api.html#section/Getting-started)
- [API reference](https://www.landmarkcloudservices.com/)
- [Sign up](https://www.landmark.co.uk/our-group/contact/)
- [Support](https://www.landmark.co.uk/our-group/contact/)
- [Blog](https://www.landmark.co.uk/news-insights/blog/)
- [Terms of service](https://www.landmark.co.uk/terms-conditions/)
- [Privacy policy](https://www.landmark.co.uk/privacy-policy/)
- [GitHub](https://github.com/Landmark-Information-Group)

## API Evangelist rating

**Kin Score 52.4** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 62.5 |
| Contract quality | 60.1 |
| Contract governance | 4.5 |
| Operational transparency | 47.4 |
| Developer ergonomics | 66.1 |
| Access clarity | 34.2 |

**Agent readiness 47.0** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | — |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 34.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/landmark-information/](https://apis.io/providers/landmark-information/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Landmark Information Group: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/landmark-information/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
