---
name: applike-manage-campaign-bids
description: >-
  Create a campaign in justtrack, list campaigns, read current bids with their operation status, and upload a batch
  of bids through the Management API.
api: justtrack Management API
base_url: https://api.justtrack.io
spec: openapi/applike-justtrack-management-openapi.yml
operations:
  - POST /management/v1/campaign
  - POST /management/v1/campaigns
  - POST /management/v1/bids
  - POST /management/v1/bids/upload
generated: '2026-08-06'
method: generated
source: openapi/applike-justtrack-management-openapi.yml, https://docs.justtrack.io/api/management/management-api/
---

# Create a campaign and manage its bids

`https://api.justtrack.io`, `X-API-Key` header, **Pro plan**. The published OpenAPI declares no `operationId`; the
camelCase names below come from `overlays/applike-justtrack-management-overlay.yaml`.

## Understand the default first

From the provider's own description of `POST /management/v1/campaign`:

> "Typically, we automatically track campaigns in justtrack when we receive the first click or impression. However,
> you can also use this API to create a campaign manually."

So **do not create campaigns you do not need**. Check for the auto-tracked campaign first.

## 1. List campaigns

`POST /management/v1/campaigns` (`listCampaigns`) — "Get a paginated list of campaigns for your organization."

Read via POST: the `ListCampaignsFilter` and the `page` object go in the body. Same `offset`/`limit` rules as
everywhere else on this API (`limit: 0` -> default 100, max 1000).

Responses: `200`, `500`. Note this operation declares **no `400` and no `401`** in the spec — a malformed filter or
a bad key will still fail, but the contract does not describe how.

## 2. Create a campaign only if needed

`POST /management/v1/campaign` (`createCampaign`) with a `CreateCampaignRequest`.

A `Campaign` carries `id`, `name`, `appId`, `partnerId`, `platform`, `type`, `countryCodes[]`, and optionally
`goalName`, `optimizationType`, `promoCode`, plus `createdAt`/`updatedAt`.

`countryCodes` is required with at least one entry. If the connection was created with
`multiCountryCampaignAllowed: false`, a multi-country campaign will be rejected — see
`applike-onboard-app-and-partner`.

**No idempotency key.** Retrying a timed-out create can produce a duplicate campaign. Re-run `listCampaigns` before
retrying.

## 3. Read current bids

`POST /management/v1/bids` (`fetchCurrentBidsWithStatus`) — "This API provides with the bids within justtrack. In
addition, it exposes the status of the latest operation associated with the bid."

Each `BidOutput` is:

- `value` — a `Bid`: number, double, minimum 0, **"bid value in USD"**
- `campaignId`, `partnerId` — required
- `countryCode`, `adSetId`, `sourceId` — optional narrowing
- `status` — "current status of the latest bid operation"

That `status` field is the whole point of this endpoint: bid upload is asynchronous, so this is how you find out
what happened to the batch you sent.

## 4. Upload bids

`POST /management/v1/bids/upload` (`uploadBids`) — "With this API you can upload a batch of bids, similar to the CSV
upload. The same hierarchy, rules, and limitations apply."

Responses: `204` (accepted, no body), `400`, `500`. On `400` the body is an `UploadBidsInvalidBidResponse` carrying
`InvalidBidOutput` entries — read those to find which rows were rejected rather than resubmitting blind.

Because the success response is `204` with no body, **you cannot confirm the outcome from this call**. Poll
`POST /management/v1/bids` and read `status` to confirm the batch applied.

## Errors and retries

- Flat `{"error": "<string>"}` envelope; no RFC 9457, no stable error codes.
- No published rate limit and no `429` declared anywhere on this API — self-throttle.
- `500` description names the escalation path: *"Please try again, or contact us at support@justtrack.io if the
  error persists."*

See `errors/applike-problem-types.yml` and `conventions/applike-conventions.yml`.
