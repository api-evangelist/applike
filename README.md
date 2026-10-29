# AppLike Group

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

AppLike Group is a Hamburg, Germany-based company builder in the mobile app economy, founded in 2015 by Jonas Thiemann and Carlo Szelinsky and backed by Bertelsmann. The group operates four independent businesses that cover the mobile app value chain: adjoe (rewarded user acquisition, the Playtime engagement ad format, the Arcade loyalty layer and a programmatic ads platform), justtrack (mobile attribution, user-acquisition automation, cohort and monetization analytics), JustDice (app-discovery products for mobile gamers) and Sunday (mobile game development and publishing). Two of the four brands publish public developer surfaces: justtrack ships OpenAPI 3.1 contracts for its Management and AppEvent APIs plus documented Reporting, Revenue Events and Raw Data Export interfaces, and adjoe publishes SSP reporting APIs and a server-to-server rewarded-payout callback alongside Android, iOS, Unity, Flutter, React Native and Cordova SDKs.

**Areas:** Mobile Attribution · User Acquisition · AdTech · Mobile Advertising · App Monetization · rewarded-advertising · Mobile SDK · Mobile Analytics · Marketing Attribution · Mobile Games · Event Tracking · Company

## AppLike Group on APIs.io

Everything profiled for AppLike Group is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/applike/](https://apis.io/providers/applike/)** — or go straight to one of the APIs or properties below.

### APIs (11)

- [justtrack Reporting API](https://apis.io/apis/applike/justtrack-reporting-api/) — Reporting API exposing the metrics behind the justtrack dashboard — acquisition tables, cohort analysis and event drill-down — as POST endpoints under…
- [justtrack Revenue Events API](https://apis.io/apis/applike/justtrack-revenue-events-api/) — Server-to-server revenue postback sink. Monetization partners and customers send real-time revenue events as GET requests with query parameters to…
- [adjoe SSP Revenue API](https://apis.io/apis/applike/adjoe-ssp-revenue-api/) — Publisher-facing reporting API returning daily aggregated Playtime revenue, eCPM, offerwall shows, SDK bootups, first impressions, coin sums and view…
- [adjoe User Ad Data Report API](https://apis.io/apis/applike/adjoe-user-ad-data-report-api/) — Per-user ad data report download for Playtime publishers. A single GET /v3/ssp-api/user-ad-data-report/sdk/{sdkHash} endpoint returns a text/csv report for…
- [AppLike Group App Partner Connection API](https://apis.io/apis/applike/applike-app-partner-connection-api/) — With the App Partner Connection API, you can: - View details about an app partner connection - Create a partner connection for an app (This is the API…
- [AppLike Group Apps API](https://apis.io/apis/applike/applike-apps-api/) — With the App API, you can: - View your list of apps - Create an app
- [AppLike Group Bids API](https://apis.io/apis/applike/applike-bids-api/) — Bidding operates as a distributed transaction. The sequential flow is as follows: 1. you upload a bid 2. we store it in justtrack -> status: pending 3. we…
- [AppLike Group Campaigns API](https://apis.io/apis/applike/applike-campaigns-api/) — The Campaigns API from AppLike Group — 2 operation(s) for campaigns.
- [AppLike Group Partner Configurations API](https://apis.io/apis/applike/applike-partner-configurations-api/) — In justtrack, you integrate your app with the advertising partners that run your campaigns. Depending on the integrated partner, we exchange data for at…
- [AppLike Group Partners API](https://apis.io/apis/applike/applike-partners-api/) — The Partners API from AppLike Group — 1 operation(s) for partners.
- [AppLike Group App Events API](https://apis.io/apis/applike/applike-app-events-api/) — The App Events API from AppLike Group — 1 operation(s) for app events.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Applike Webhooks](https://apis.io/asyncapis/applike/applike-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [applike](https://apis.io/servers/applike/applike/)

#### Collections (7)

Postman and Open Collection request collections.

- [Management App Partner Connection API](https://apis.io/collections/applike/open-applike-app-partner-connection-api/)
- [AppEvent Appevents API](https://apis.io/collections/applike/open-applike-appevents-api/)
- [Management Apps API](https://apis.io/collections/applike/open-applike-apps-api/)
- [Management Bids API](https://apis.io/collections/applike/open-applike-bids-api/)
- [Management Campaigns API](https://apis.io/collections/applike/open-applike-campaigns-api/)
- [Management Partner Configurations API](https://apis.io/collections/applike/open-applike-partner-configurations-api/)
- [Management Partners API](https://apis.io/collections/applike/open-applike-partners-api/)

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Applike Justtrack App Events Overlay](https://apis.io/overlays/applike/applike-justtrack-app-events-overlay/)
- [Applike Justtrack Management Overlay](https://apis.io/overlays/applike/applike-justtrack-management-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Applike Authentication](https://apis.io/security/applike/applike-authentication/)
- [Applike Domain Security](https://apis.io/security/applike/applike-domain-security/)
- [Applike Trust Center](https://apis.io/security/applike/applike-trust-center/)

#### Rate limits (1)

Published request limits.

- [Applike Rate Limits](https://apis.io/rate-limits/applike/applike-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://applike-group.com/)
- [Documentation](https://docs.justtrack.io/)
- [Getting started](https://docs.justtrack.io/sdk/setup/)
- [API reference](https://docs.justtrack.io/api/overview/)
- [Pricing](https://justtrack.io/pricing/)
- [Support](https://justtrack.io/contact/)
- [Changelog](https://docs.justtrack.io/sdk/more/changelog/)
- [Blog](https://adjoe.io/blog/)
- [Terms of service](https://justtrack.io/terms-of-service/)
- [Privacy policy](https://justtrack.io/privacy-notice/)
- [GitHub](https://github.com/justtrackio)
- [Status](https://status.justtrack.io/)

## API Evangelist rating

**Kin Score 59.9** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 57.8 |
| Contract governance | 18.2 |
| Operational transparency | 71.1 |
| Developer ergonomics | 66.1 |
| Access clarity | 53.9 |

**Agent readiness 60.4** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | verified |
| Auth Clarity | served (partial credit) |
| Idempotency | documented (partial credit) |
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
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 29.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/applike/](https://apis.io/providers/applike/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for AppLike Group: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/applike/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
