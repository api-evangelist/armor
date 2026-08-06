---
name: Triage an Armor MDR incident
description: Pull the open incident queue from the Armor SOC, enrich one incident with the Armor Intelligence Platform analysis and per-entity threat intelligence, and write findings back as a comment.
api: openapi/armor-mdr-public-openapi-original.yml
operations:
  - listIncidents
  - getIncidentDetails
  - getIncidentAipData
  - fetchEntityForIncident
  - addIncidentComment
  - getCommentAttachments
provider: armor
generated: '2026-08-06'
method: generated
source: openapi/ (operationIds verified verbatim against the published Armor contracts)
---

# Triage an Armor MDR incident

Pull the open incident queue from the Armor SOC, enrich one incident with the Armor Intelligence Platform analysis and per-entity threat intelligence, and write findings back as a comment.

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

1. `listIncidents` (`GET /incidents`) — list the incidents Armor's SOC has raised for the account.
2. `getIncidentDetails` (`GET /incidents/{issueKey}`) — pull the full record for the one you are working.
3. `getIncidentAipData` (`GET /aip/incident/{incidentKey}`) — the Armor Intelligence Platform's AI-processed
   analysis: threat indicators and recommendations. This is the analyst-replicating layer, not raw telemetry.
4. `fetchEntityForIncident` (`GET /aip/incident/{incidentId}/entity/{value}`) — for each suspicious entity
   (host, user, IP, hash) named in step 3, pull entity threat intelligence.
5. `getCommentAttachments` (`GET /incidents/{issueKey}/comment/{commentId}`) — read any evidence the SOC attached.
6. `addIncidentComment` (`POST /incidents/{issueKey}/comments`) — write the triage conclusion back.
   **This is the only write in this skill and it is not idempotent — post once, then re-read with
   `getIncidentDetails` rather than retrying.**

## See also

- `conventions/armor-conventions.yml`
- `errors/armor-problem-types.yml`
- `authentication/armor-authentication.yml`
- `scopes/armor-scopes.yml`
