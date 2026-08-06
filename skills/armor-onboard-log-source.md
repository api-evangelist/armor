---
name: Onboard a log source into Armor SIEM
description: Register a new log source with Armor log management, allocate its endpoint and open the ACL so the source can ship logs.
api: openapi/armor-log-management-openapi-original.yml
operations:
  - getLogSourceTypes
  - checkHostnameAvailability
  - getLogSources
  - createLogSource
  - getLogGroups
  - getLogAcls
  - createLogAcl
  - getLogEndpoints
  - allocateLogEndpoint
provider: armor
generated: '2026-08-06'
method: generated
source: openapi/ (operationIds verified verbatim against the published Armor contracts)
---

# Onboard a log source into Armor SIEM

Register a new log source with Armor log management, allocate its endpoint and open the ACL so the source can ship logs.

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

**Deprecation warning.** `createLogSource`, `updateLogSource`, `deleteLogSource`, `getLogEndpoints`,
`allocateLogEndpoint`, `getLogAcls`, `createLogAcl`, `updateLogAcl` and `checkHostnameAvailability` are all
flagged `deprecated: true` in the published contract. Armor publishes **no deprecation policy and no Sunset
header**, so there is no stated removal date — treat this flow as at-risk and confirm the replacement with
Armor support before automating it.

1. `getLogSourceTypes` (`GET /meta/logs/log-source-types`) — the supported source types.
2. `checkHostnameAvailability` (`POST /meta/logs/sources/actions/check-unique-name`) — names must be unique.
3. `getLogSources` (`GET /logs/sources`) — confirm the source is not already registered.
4. `createLogSource` (`POST /logs/sources`) — register it. Not idempotent; step 3 is the guard.
5. `getLogEndpoints` (`GET /logs/endpoints`) then `allocateLogEndpoint`
   (`POST /logs/endpoints/actions/allocate`) — allocate the ingestion endpoint.
6. `getLogAcls` (`GET /logs/acls`) then `createLogAcl` (`POST /logs/acls`) — permit the shipping network.
7. `getLogGroups` (`GET /logs/groups`) — confirm the source landed in the right group.

## See also

- `conventions/armor-conventions.yml`
- `errors/armor-problem-types.yml`
- `authentication/armor-authentication.yml`
- `scopes/armor-scopes.yml`
