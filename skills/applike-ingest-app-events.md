---
name: applike-ingest-app-events
description: >-
  Send batches of in-app events to justtrack server-to-server, with correct deduplication keys, partial-success
  handling and a safe retry loop.
api: justtrack AppEvent API
base_url: https://app-events.justtrack.io
spec: openapi/applike-justtrack-app-events-openapi.yml
operations:
  - postAppEventBatch
generated: '2026-08-06'
method: generated
source: openapi/applike-justtrack-app-events-openapi.yml, https://docs.justtrack.io/api/app-events/appevent-api/
---

# Ingest in-app events into justtrack

One operation does all of it: `postAppEventBatch` — `POST https://app-events.justtrack.io/appevents/v1`.
It is a **Pro-plan** feature.

## Authenticate

Send the organization API key in the `X-API-Key` header. Generate it in the justtrack dashboard under
**User profile > API keys > Generate new key**. There is no scope model — the key carries the organization's full
entitlements, so treat it as a root credential.

An unauthenticated request returns `401` with `{"apiKey":"no api key provided"}`.

## Shape the request

The body is an `InputBatch` — an **array of `AppEventBatch` objects**. Each batch is scoped to exactly one
app/user combination:

- `batchId` — uuid4, exactly 36 characters. **You** generate it. This is the deduplication key.
- `app` — the app identity (`App`).
- `user` — the subject (`User`); a justtrack user id or your own custom user id.
- `events[]` — one or more `AppEvent`.

Each `AppEvent` requires:

- `id` — uuid4. "Globally unique id of the event." **You** generate it. This is the per-event deduplication key.
- `event` — the event name, e.g. `level_success`.
- `value` — the measurement.
- Exactly one of `unit` (`count` | `seconds` | `milliseconds`) **or** `currency` (ISO 4217, 3 characters). They are
  mutually exclusive — sending both is a `400`.
- `dimensions` — a free-form object for your own attributes.
- `happenedAt` — ISO 8601.

## Handle the response

| Status | Meaning | What to do |
|---|---|---|
| `200` | Everything committed | Done. |
| `207` | Partial success | The body is an array of `{batchId, statusCode, error}`. **Retry only those batchIds.** Everything else committed. |
| `400` | Bad request input | Fix the payload. Do not retry unchanged. |
| `401` | Unauthorized | Check the `X-API-Key` header. |
| `500` | Internal server error | Retry with backoff. |
| `502` | Bad Gateway while committing | The provider's own guidance: "please try again after a short backoff." |

## Retry safely

Because **you** supply both `batchId` and every `events[].id`, a verbatim replay after `500` or `502` is safe —
justtrack deduplicates on those identifiers. Do **not** regenerate the uuids on retry; that is what turns a retry
into a duplicate.

Note what is *not* here: there is no `Idempotency-Key` header on this API. The idempotency lives in the payload.

## Batch atomicity

From the provider's own schema description: *"A batch of AppEvents, all for one app user combination. If one event
is invalid, the whole batch is rejected."* So keep batches small enough that one bad event does not cost you a large
commit, and always key your retry off the returned `batchId` rather than resending the whole request.

## Rate limits

None are published for this API, and the OpenAPI document declares no `429`. Self-throttle conservatively and treat
`502` as the backpressure signal.

## Cross-references

- `conventions/applike-conventions.yml` — idempotency, pagination and error conventions across the group
- `errors/applike-problem-types.yml` — the full status/envelope catalog
- `overlays/applike-justtrack-app-events-overlay.yaml` — the idempotency and retry contract expressed as spec annotations
