---
name: applike-onboard-app-and-partner
description: >-
  Register an app in justtrack, connect it to an advertising partner, and configure that partner's features — the
  full onboarding flow through the Management API.
api: justtrack Management API
base_url: https://api.justtrack.io
spec: openapi/applike-justtrack-management-openapi.yml
operations:
  - POST /management/v1/app
  - POST /management/v1/apps
  - POST /management/v1/partners
  - PUT /management/v1/app/{appId}/connection/{partnerId}
  - GET /management/v1/app/{appId}/connection/{partnerId}
  - POST /management/v1/partner-configurations
  - POST /management/v1/partner-configuration/{feature}
  - PUT /management/v1/partner-configuration/{feature}
generated: '2026-08-06'
method: generated
source: openapi/applike-justtrack-management-openapi.yml, https://docs.justtrack.io/api/management/management-api/
---

# Onboard an app and connect an advertising partner

Everything here is `https://api.justtrack.io`, `X-API-Key` header, **Pro plan**.

> The published OpenAPI document declares **no `operationId` on any operation**, so steps below are grounded on
> method + path. The camelCase names in parentheses are the ones API Evangelist assigns in
> `overlays/applike-justtrack-management-overlay.yaml` — they are not names justtrack ships.

## 1. Create the app

`POST /management/v1/app` (`createApp`) with a `CreateAppRequest`.

An `App` carries `id`, `name`, `bundleId`, `platform`, `storeId`, `createdAt`, `updatedAt`.

Responses: `200`, `400`, `401`, `403`, `500`. A `403` here means your organization is not entitled to create apps —
the key has no scopes, so this is an account-level entitlement, not a permission you can widen on the key.

**There is no `Idempotency-Key` header on this operation.** A retry after a timeout may create a second app. Before
retrying, call `POST /management/v1/apps` (`listApps`) and check whether the app landed.

## 2. Find the app again

`POST /management/v1/apps` (`listApps`) — "Get a paginated list of your organization's apps."

Note the shape: this is a **read via POST**, with the filter and the page object in the request body.

```
page: { offset: <int, >= 0>, limit: <int, 0..1000> }
```

`limit: 0` means "use the default of 100"; the maximum is 1000. There is no cursor and no next-link — advance
`offset` yourself.

## 3. List available partners

`POST /management/v1/partners` (`listPartners`) — "Get a paginated list of partners available to your organization."

A `Partner` is `{id (integer >= 1), name, createdAt, updatedAt}`. Around thirty integrated partners are documented
(AppLovin, ironSource, Unity, Google Ads, Apple Search Ads, Moloco, Liftoff, Mintegral, Digital Turbine, adjoe, …).

## 4. Connect the app to the partner

`PUT /management/v1/app/{appId}/connection/{partnerId}` (`connectPartner`) — "Connect your app to a partner. If this
app-partner connection already exists, update the connection details."

This is a `PUT` upsert, which makes it the one genuinely **safe-to-retry** write in this flow.

The `AppPartnerConnection` requires:

- `campaignTypes[]` — "List of campaign types this partner can run."
- `defaultChannelId` — "justtrack internal ID for the channel used by default to create campaigns."
- `multiCountryCampaignAllowed` — boolean.
- `trackingUrlSlug` — "a unique string to identify this partner among others on tracking urls."

Read it back with `GET /management/v1/app/{appId}/connection/{partnerId}` (`getAppPartnerConnection`). A `404` there
means the connection does not exist; a `400` means the ids are malformed.

## 5. Configure the partner's features

Two steps, in order:

1. `POST /management/v1/partner-configurations` (`listConfigurations`) — "Get a paginated list of keys used to
   configure features for the partners that are available to your organization." This tells you which keys exist.
2. `PUT /management/v1/partner-configuration/{feature}` (`configurePartner`) — "Configure a feature for a given app
   and partner."

Verify with `POST /management/v1/partner-configuration/{feature}` (`listConfiguredFeatures`) — "Get a paginated list
of configured features for a given app and partner."

Both write paths can return `403` when the organization is not entitled to that partner feature.

## Errors

Every error is a flat `{"error": "<string>"}` — no RFC 9457 problem details, no stable error codes. The `401` on this
API declares **no response body**, so you cannot distinguish "no key" from "revoked key" from the payload.

See `errors/applike-problem-types.yml`.
