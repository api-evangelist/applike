---
name: applike-pull-adjoe-publisher-revenue
description: >-
  Pull daily aggregated Playtime revenue from the adjoe SSP Revenue API and download the per-user ad data report,
  respecting the published rate limit and the report-pending state.
api: adjoe SSP Revenue API, adjoe User Ad Data Report API
base_url: https://prod.adjoe.zone
grounding: documentation
operations:
  - GET /v2/ssp-api/aggregation/daily
  - GET /v2/ssp-api/aggregation/sdkHash/{sdkHash}/daily
  - GET /v3/ssp-api/user-ad-data-report/sdk/{sdkHash}
generated: '2026-08-06'
method: generated
source: >-
  https://docs.adjoe.io/rewarded-solutions/reporting-apis/revenue-api,
  https://docs.adjoe.io/rewarded-solutions/reporting-apis/user-ad-data-report-api
---

# Pull adjoe Playtime publisher revenue and user ad data

adjoe publishes **no OpenAPI** for these endpoints — this skill is grounded on the reporting documentation pages,
whose paths, parameters, dimensions, status codes and rate-limit headers are quoted below as published.

## Authenticate

Send the **publisher token** in an `X-API-KEY` header. Get it from the adjoe Monetize Dashboard:
profile icon (top right) > **MY PROFILE** > **Publisher token**.

Note the casing: adjoe uses `X-API-KEY`, justtrack uses `X-API-Key`. They are different APIs with different tokens.

## 1. Daily revenue, all SDKs

```
GET https://prod.adjoe.zone/v2/ssp-api/aggregation/daily
```

Query parameters:

- `start_at` (required) — `YYYY-MM-DD`
- `stop_at` (required) — `YYYY-MM-DD`
- `group_by` (optional) — comma-separated dimensions; **defaults to `date,sdk_hash,platform`**

Metrics always present in each row: `Revenue` (float, USD), `eCPM` (string — "Effective cost per 1,000 impressions
(USD), formatted to 2 decimal places"), `OfferwallShown`, `SDKBootups`, `FirstImpression`, `CoinSum`, `ViewCount`.

Dimensions appear **only if you requested them in `group_by`**. Eighteen are available, including `date`, `country`,
`platform`, `age`, `gender`, `sdk_version`, `placement` and `app_id`.

## 2. Daily revenue, one SDK

```
GET https://prod.adjoe.zone/v2/ssp-api/aggregation/sdkHash/{sdkHash}/daily
```

Same query parameters. `sdkHash` must belong to your account — a hash you do not own returns **`404`, not `403`**.

## 3. Per-user ad data report

```
GET https://prod.adjoe.zone/v3/ssp-api/user-ad-data-report/sdk/{sdkHash}?date=YYYY-MM-DD
```

- `date` is required and **must not be a future date**.
- `200` returns `text/csv` — a header row plus one row per user.
- `202` returns `application/json`: `{"error": "report is pending generation"}`.

**Do not treat that `202` as a failure.** adjoe reuses the `error` key for a success-path state. Poll until you get
`200` with `text/csv`. Note the version skew: this report is on `/v3/ssp-api` while revenue is on `/v2/ssp-api`.

## Respect the rate limit

Published, and the only rate limit anywhere in the AppLike Group estate:

- **5 requests per second sustained**, per publisher
- **burst of 10**, per publisher
- `429` on exceed

Headers to read on every response:

| Header | Meaning |
|---|---|
| `X-RateLimit-Limit` | burst size |
| `X-RateLimit-Remaining` | requests available |
| `X-RateLimit-Reset` | seconds until replenishment |
| `Retry-After` | present on `429` responses only |

Back off on `Retry-After`. The report endpoint publishes no rate limit — apply the same budget defensively.

## Status codes

`200` OK · `202` report pending (report endpoint) · `400` invalid parameters or date format · `401` missing or
invalid publisher token · `404` SDK or report not found · `429` rate limit exceeded · `500` server error.

## Cross-references

- `rate-limits/applike-rate-limits.yml`
- `authentication/applike-authentication.yml`
- `errors/applike-problem-types.yml`
