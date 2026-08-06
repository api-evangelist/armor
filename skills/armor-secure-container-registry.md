---
name: Connect a container registry to Armor container security
description: Stand up Armor container security: subscribe the account, create the cloud connector, register a container registry, and read back scanned images and deployed sensors.
api: openapi/armor-container-security-openapi-original.yml
operations:
  - getAccountDetails
  - createSubscription
  - getAwsBaseConfig
  - getAllConnectors
  - createConnector
  - getConnectorDetail
  - getAllRegistries
  - getVendorTypes
  - createRegistry
  - getRegistryDetail
  - getAllImages
  - getImageDetail
  - getAllSensors
provider: armor
generated: '2026-08-06'
method: generated
source: openapi/ (operationIds verified verbatim against the published Armor contracts)
---

# Connect a container registry to Armor container security

Stand up Armor container security: subscribe the account, create the cloud connector, register a container registry, and read back scanned images and deployed sensors.

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

This API is served on the `/containers` path prefix of the compliance host
(`https://compliance.api.secure-prod.services/containers`), not on its own host.

1. `getAccountDetails` (`GET /accounts`) — account-specific installation details.
   `createSubscription` (`POST /accounts`) if the account is not yet subscribed.
2. `getAwsBaseConfig` (`GET /connectors/aws-base`) — the AWS configuration values the connector needs.
3. `getAllConnectors` (`GET /connectors`) — check first, then `createConnector` (`POST /connectors`).
   Confirm with `getConnectorDetail` (`GET /connectors/{id}`). Not idempotent.
4. `getVendorTypes` (`GET /registries/vendor-types`) — supported registry vendors.
   `getAllRegistries` (`GET /registries`), then `createRegistry` (`POST /registries`), verified with
   `getRegistryDetail` (`GET /registries/{id}`).
5. `getAllImages` (`GET /images`) and `getImageDetail` (`GET /images/{id}`) — scan results per image.
6. `getAllSensors` (`GET /sensors`) — the runtime sensors deployed into the customer's clusters.

## See also

- `conventions/armor-conventions.yml`
- `errors/armor-problem-types.yml`
- `authentication/armor-authentication.yml`
- `scopes/armor-scopes.yml`
