---
name: Contain a machine through Microsoft Defender
description: Find an affected machine in Armor-managed Microsoft Defender for Endpoint, execute a containment action such as isolation or a scan, and collect the investigation package.
api: openapi/armor-mdr-public-openapi-original.yml
operations:
  - getMachines
  - executeMachineAction
  - getMachineActions
  - getMachineAction
  - getPackageUri
  - getLiveResponseResult
provider: armor
generated: '2026-08-06'
method: generated
source: openapi/ (operationIds verified verbatim against the published Armor contracts)
---

# Contain a machine through Microsoft Defender

Find an affected machine in Armor-managed Microsoft Defender for Endpoint, execute a containment action such as isolation or a scan, and collect the investigation package.

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

**Consequence warning.** `executeMachineAction` isolates machines and runs live-response commands on
production hosts. It is a `POST` with **no idempotency key**. A retry after a timeout can queue a second
action. Always reconcile with `getMachineActions` before re-issuing.

1. `getMachines` (`GET /defender/machines`) — locate the machine and its id.
2. `executeMachineAction` (`POST /defender/machineactions/{machineId}`) — issue the action (isolation, scan,
   investigation package collection). Record the returned action id.
3. `getMachineAction` (`GET /defender/machineactions/{actionId}`) — poll until the action completes.
4. `getPackageUri` (`GET /defender/packageuri/{actionId}`) — get the download URI for a collected
   investigation package.
5. `getLiveResponseResult` (`GET /defender/liveresponseresult/{actionId}/{commandId}`) — retrieve the output
   of a live-response command.
6. `getMachineActions` (`GET /defender/machineactions`) — audit every action taken across the estate.

## See also

- `conventions/armor-conventions.yml`
- `errors/armor-problem-types.yml`
- `authentication/armor-authentication.yml`
- `scopes/armor-scopes.yml`
