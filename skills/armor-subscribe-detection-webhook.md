---
name: Subscribe to Armor security detections over webhooks
description: Register a webhook subscription so Armor pushes security detections to your endpoint, with a transform that reshapes the delivered payload.
api: openapi/armor-webhooks-openapi-original.yml
operations:
  - getEventTypes
  - getDetectionConfiguration
  - createDetectionConfiguration
  - updateDetectionConfiguration
  - deleteDetectionConfiguration
  - getNotificationConfigurations
  - createNotificationConfiguration
provider: armor
generated: '2026-08-06'
method: generated
source: openapi/ (operationIds verified verbatim against the published Armor contracts)
---

# Subscribe to Armor security detections over webhooks

Register a webhook subscription so Armor pushes security detections to your endpoint, with a transform that reshapes the delivered payload.

## Authenticate first (every skill below assumes this)

Armor's preferred scheme is **OAuth2 (Scoped)** — a single `authorization` header carrying **both** an
ID token and a scoped access token, comma-separated.

1. `POST https://sts.armor.com/adfs/oauth2/authorize?response_type=id_token&response_mode=form_post&client_id=<client>&redirect_uri=https://api.armor.com/`
   with form body `AuthMethod=FormsAuthentication`, `UserName`, `Password`. Follow the 302.
   The response body is an **HTML form** — parse the `Context` input for MFA, or the `id_token` input if MFA is off.
   Use client `d467ba47-2382-44cd-8779-5fb9a3abf69b` for non-interactive service accounts (the account must
   already be excluded from MFA by an approved support ticket); otherwise use the default client and complete
   MFA with `AuthMethod=AzureMfaServerAuthentication`.
2. `POST https://api.armor.com/auth/token?scope=openid+email+profile+*:<system>` with
   `authorization: Bearer <id_token>` and a request body of exactly `null`. Read `assertion` (the access token).
   **Scopes you lack permission for are silently dropped from the returned `scope` list — always compare
   requested vs returned before assuming you can act.**
3. Call the API with `authorization: Bearer <id_token>,<access_token>` and, for v1 and `/me`,
   `X-Account-Context: <armor_account_id>`.

`operationId`s for the auth surface itself: `authorize`, `exchangeToken`, `refreshToken`, `getCurrentUser`
(`openapi/armor-fh-auth-openapi-original.yml`). Access tokens live **15 minutes**; the authorization code
lives **2 minutes**.

## Rules that apply to every Armor call

- **There is no idempotency contract.** No `Idempotency-Key` header exists on any of Armor's 427 operations.
  Never blind-retry a `POST`/`PUT`/`DELETE`. On a timeout, re-read state with the matching `GET` first.
- **Errors are not RFC 9457.** Expect one of six envelopes. On `api.armor.com` the richest is
  `{"ErrorCode","Message","Detail","ReferenceId"}` — quote `ReferenceId` in any support ticket.
- **Rate limits are undocumented.** No `RateLimit`/`Retry-After` headers are declared. Back off on 429.
- **Pagination is inconsistent.** v1 uses the `x-pagesize` / `x-range` headers; v2 mixes `limit`/`offset`,
  `pageNumber`/`pageSize`, `skip`/`top` and `nextPageToken`. Read the operation, do not assume.

## Steps

Armor publishes **no AsyncAPI document**; this subscription API is the machine-readable event surface, and
the delivered payload schema is only discoverable at runtime.

1. `getEventTypes` (`GET /security/detection/event-type`) — **this is the event catalogue.** It requires an
   OAuth token, so enumerate it at runtime rather than hard-coding event names.
2. `getDetectionConfiguration` (`GET /security/detection`) — read the account's existing detection subscriptions
   before creating another.
3. `createDetectionConfiguration` (`POST /security/detection`) — register the endpoint, the default labels and
   the transform. Not idempotent; a repeated POST creates a second subscription and duplicate deliveries.
4. `updateDetectionConfiguration` (`POST /security/detection/{detection_id}`) — change it.
   `deleteDetectionConfiguration` (`POST /security/detection/delete/{detection_id}`) — remove it.
   Note both use `POST`, not `PUT`/`DELETE`.
5. `getNotificationConfigurations` / `createNotificationConfiguration` (`/security/notification`) — the same
   pattern for operational notifications.
6. The objects delivered are the same detections `listDetections` returns in
   `openapi/armor-incident-management-openapi-original.yml` — use that API to backfill or reconcile.

## See also

- `conventions/armor-conventions.yml`
- `errors/armor-problem-types.yml`
- `authentication/armor-authentication.yml`
- `scopes/armor-scopes.yml`
