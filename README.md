# Armor

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

Armor (legal name Armor Defense Inc.) is a cybersecurity company headquartered in Plano, Texas, founded as FireHost in 2009 by Chris Drake and rebranded as Armor as its portfolio expanded from secure cloud hosting into managed security. Armor sells vendor-agnostic, cloud-native managed detection and response (Armor MDR), compliant managed private cloud (Armor Enterprise Cloud), the Armor Agent workload protection agent (formerly Armor Anywhere), and compliance and offensive-security professional services, to more than 1,700 organizations across 40 countries with a 24/7 follow-the-sun SOC operating from Plano, London, Singapore and Pune. Armor publishes a public developer portal at developer.armor.com that serves sixteen machine-readable contracts through ReDoc: four Swagger 2.0 documents for the original v1 Armor Services API on api.armor.com (account management, infrastructure, security and support, 254 operations) and twelve OpenAPI 3.0.3 documents for the v2 platform on *.api.secure-prod.services (accounts, agent management, compliance and CSPM, container security, incident management, infrastructure management, log management, notifications, webhooks, the unified MDR public API, and the ARMOR-PSK and FH-AUTH authentication contracts). Armor also publishes a detailed first-party llms.txt at armor.com/llms.txt and holds SOC 2 Type II, HITRUST CSF, PCI DSS Level 1 Service Provider, ISO 27001, TX-RAMP Level 2, HIPAA and Data Privacy Framework attestations.

**Areas:** Company · Cybersecurity · Managed Detection and Response · Cloud Security · Compliance · SIEM · Vulnerability Management · Endpoint Security · Threat Intelligence · Managed Private Cloud · CSPM · Container Security

## Armor on APIs.io

Everything profiled for Armor is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/armor/](https://apis.io/providers/armor/)** — or go straight to one of the APIs or properties below.

### APIs (70)

- [Armor Access Control Lists API](https://apis.io/apis/armor/armor-access-control-lists-api/) — Operations for managing ACLs (deprecated)
- [Armor Account API](https://apis.io/apis/armor/armor-account-api/) — Account management operations
- [Armor Account Management API](https://apis.io/apis/armor/armor-account-management-api/) — The Account Management API from Armor — 47 operation(s) for account management.
- [Armor Account Primary Billing API](https://apis.io/apis/armor/armor-accountprimarybilling-api/) — The AccountPrimaryBilling API from Armor — 1 operation(s) for accountprimarybilling.
- [Armor Active Response API](https://apis.io/apis/armor/armor-activeresponse-api/) — The ActiveResponse API from Armor — 1 operation(s) for activeresponse.
- [Armor Advanced Backup API](https://apis.io/apis/armor/armor-advanced-backup-api/) — The Advanced Backup API from Armor — 38 operation(s) for advanced backup.
- [Armor AIP - Entity Intelligence API](https://apis.io/apis/armor/armor-aip-entity-intelligence-api/) — Threat intelligence data for security entities
- [Armor AIP - Incident Data API](https://apis.io/apis/armor/armor-aip-incident-data-api/) — AI-processed incident data and analytics
- [Armor Assessments API](https://apis.io/apis/armor/armor-assessments-api/) — Assessment account management
- [Armor Authentication API](https://apis.io/apis/armor/armor-authentication-api/) — FH-AUTH authentication flow endpoints. ## Flow Overview 1. POST `/auth/authorize` with credentials → receive authorization code 2. POST `/auth/token` with…
- [Armor Cloud Connections API](https://apis.io/apis/armor/armor-cloud-connections-api/) — Cloud connection management operations
- [Armor Connector API](https://apis.io/apis/armor/armor-connector-api/) — Connector management operations
- [Armor CSPM Connector API](https://apis.io/apis/armor/armor-cspm-connector-api/) — Cloud Security Posture Management cloud connectors
- [Armor CSPM Control Remediation API](https://apis.io/apis/armor/armor-cspm-control-remediation-api/) — CSPM control remediation information
- [Armor CSPM Policies API](https://apis.io/apis/armor/armor-cspm-policies-api/) — CSPM policy management
- [Armor CSPM Policy Controls API](https://apis.io/apis/armor/armor-cspm-policy-controls-api/) — CSPM policy controls management
- [Armor CSPM Report API](https://apis.io/apis/armor/armor-cspm-report-api/) — CSPM report operations
- [Armor CSPM Report Configuration API](https://apis.io/apis/armor/armor-cspm-report-configuration-api/) — CSPM report configuration management
- [Armor CSPM Resources API](https://apis.io/apis/armor/armor-cspm-resources-api/) — CSPM resource management
- [Armor CSPM Summary API](https://apis.io/apis/armor/armor-cspm-summary-api/) — CSPM cloud connector summary
- [Armor CSPM Usage API](https://apis.io/apis/armor/armor-cspm-usage-api/) — CSPM cloud connector usage
- [Armor Defender - Investigation API](https://apis.io/apis/armor/armor-defender-investigation-api/) — Investigation package and live response operations
- [Armor Defender - Machine Actions API](https://apis.io/apis/armor/armor-defender-machine-actions-api/) — Execute and manage actions on Microsoft Defender machines
- [Armor Defender - Machines API](https://apis.io/apis/armor/armor-defender-machines-api/) — Microsoft Defender machine/device management
- [Armor Detection Rules API](https://apis.io/apis/armor/armor-detection-rules-api/) — Operations for retrieving and managing detection rules
- [Armor Detections API](https://apis.io/apis/armor/armor-detections-api/) — The detection resource enables an API customer to build a webhook detection configuration.
- [Armor EDR API](https://apis.io/apis/armor/armor-edr-api/) — Endpoint Detection and Response operations
- [Armor Events API](https://apis.io/apis/armor/armor-events-api/) — The event-type resource enables an API user to maintain the event types.
- [Armor Flow Sources API](https://apis.io/apis/armor/armor-flow-sources-api/) — Operations for managing flow sources
- [Armor Health API](https://apis.io/apis/armor/armor-health-api/) — Service health and monitoring endpoints
- [Armor Health Monitoring Status API](https://apis.io/apis/armor/armor-health-monitoring-status-api/) — Health monitoring status operations
- [Armor Image API](https://apis.io/apis/armor/armor-image-api/) — Image management operations
- [Armor Infrastructure API](https://apis.io/apis/armor/armor-infrastructure-api/) — The Infrastructure API from Armor — 35 operation(s) for infrastructure.
- [Armor JSM - Incidents API](https://apis.io/apis/armor/armor-jsm-incidents-api/) — Security incident management
- [Armor JSM - Metrics API](https://apis.io/apis/armor/armor-jsm-metrics-api/) — Metrics aggregation and reporting
- [Armor JSM - Organizations API](https://apis.io/apis/armor/armor-jsm-organizations-api/) — JSM organization management
- [Armor JSM - Service Requests API](https://apis.io/apis/armor/armor-jsm-service-requests-api/) — Service request management
- [Armor Keys API](https://apis.io/apis/armor/armor-keys-api/) — The Keys API from Armor — 2 operation(s) for keys.
- [Armor Log Endpoints API](https://apis.io/apis/armor/armor-log-endpoints-api/) — Operations for managing log endpoints
- [Armor Log Groups API](https://apis.io/apis/armor/armor-log-groups-api/) — Operations for managing log groups
- [Armor Log Sources API](https://apis.io/apis/armor/armor-log-sources-api/) — Operations for managing log sources
- [Armor Malware Configuration API](https://apis.io/apis/armor/armor-malware-configuration-api/) — Malware configuration APIs. These APIs are only available for specific partners.
- [Armor Meta API](https://apis.io/apis/armor/armor-meta-api/) — Meta resources and utility operations
- [Armor Network Services API](https://apis.io/apis/armor/armor-network-services-api/) — The Network Services API from Armor — 23 operation(s) for network services.
- [Armor Notifications API](https://apis.io/apis/armor/armor-notifications-api/) — The notification resource enables an API customer to build a webhook notification configuration.
- [Armor Preferences API](https://apis.io/apis/armor/armor-preferences-api/) — The Preferences resource describes a list of user-level preferences.
- [Armor Registry API](https://apis.io/apis/armor/armor-registry-api/) — Registry management operations
- [Armor Reports - MSR API](https://apis.io/apis/armor/armor-reports-msr-api/) — Monthly Security Report file management and retrieval
- [Armor Scheduled Tasks API](https://apis.io/apis/armor/armor-scheduled-tasks-api/) — The tasks resource enables an API customer to schedule, cancel and view agent CLI operations.
- [Armor Secure Notes API](https://apis.io/apis/armor/armor-secure-notes-api/) — The secure notes resource allows users to securely store and manage sensitive information such as passwords, credentials, and other confidential data.
- [Armor Security Analytics API](https://apis.io/apis/armor/armor-security-analytics-api/) — The Security Analytics API from Armor — 2 operation(s) for security analytics.
- [Armor Security API](https://apis.io/apis/armor/armor-security-api/) — The Security API from Armor — 29 operation(s) for security.
- [Armor Security Detection Events API](https://apis.io/apis/armor/armor-security-detection-events-api/) — Security detection event operations
- [Armor Security Detections API](https://apis.io/apis/armor/armor-security-detections-api/) — Security detection operations
- [Armor Security Detections Overview API](https://apis.io/apis/armor/armor-security-detections-overview-api/) — Security detections overview operations
- [Armor Security Incidents API](https://apis.io/apis/armor/armor-security-incidents-api/) — The Security Incidents API from Armor — 2 operation(s) for security incidents.
- [Armor Sensor API](https://apis.io/apis/armor/armor-sensor-api/) — Sensor management operations
- [Armor Support API](https://apis.io/apis/armor/armor-support-api/) — The Support API from Armor — 16 operation(s) for support.
- [Armor Tags API](https://apis.io/apis/armor/armor-tags-api/) — Tag management operations
- [Armor TI - Customer Intelligence API](https://apis.io/apis/armor/armor-ti-customer-intelligence-api/) — Customer-specific threat intelligence
- [Armor TI - GraphQL API](https://apis.io/apis/armor/armor-ti-graphql-api/) — Proxy endpoint for OpenCTI GraphQL queries
- [Armor TI - Threat Actors API](https://apis.io/apis/armor/armor-ti-threat-actors-api/) — Retrieve threat actor intelligence data
- [Armor Toolbox API](https://apis.io/apis/armor/armor-toolbox-api/) — Infrastructure management toolbox operations
- [Armor Tours API](https://apis.io/apis/armor/armor-tours-api/) — The tours resource describes a list of UI tours that help users learn about features in the ARMOR Management Portal. The preferences stored in this resource…
- [Armor Trend API](https://apis.io/apis/armor/armor-trend-api/) — Trend AV report operations
- [Armor User API](https://apis.io/apis/armor/armor-user-api/) — User profile and account information
- [Armor Utilization API](https://apis.io/apis/armor/armor-utilization-api/) — The Utilization API from Armor — 2 operation(s) for utilization.
- [Armor VS Exclusions API](https://apis.io/apis/armor/armor-vs-exclusions-api/) — Vulnerability scan exclusions management
- [Armor VS Reports API](https://apis.io/apis/armor/armor-vs-reports-api/) — Vulnerability scan reports
- [Armor Vulnerability Scanning API](https://apis.io/apis/armor/armor-vulnerability-scanning-api/) — Vulnerability scanning operations

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Armor Webhooks Events](https://apis.io/asyncapis/armor/armor-webhooks-events/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [armor](https://apis.io/servers/armor/armor/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Armor Agentic Access](https://apis.io/agentic-access/armor/armor-agentic-access/)

#### Collections (70)

Postman and Open Collection request collections.

- [Armor Log Management Access Control Lists API](https://apis.io/collections/armor/open-armor-access-control-lists-api/)
- [Container Security Account API](https://apis.io/collections/armor/open-armor-account-api/)
- [Armor Services Account Management API](https://apis.io/collections/armor/open-armor-account-management-api/)
- [Armor Services Account Primary Billing API](https://apis.io/collections/armor/open-armor-accountprimarybilling-api/)
- [Armor Services Active Response API](https://apis.io/collections/armor/open-armor-activeresponse-api/)
- [Armor Services Advanced Backup API](https://apis.io/collections/armor/open-armor-advanced-backup-api/)
- [MDR Public AIP - Entity Intelligence API](https://apis.io/collections/armor/open-armor-aip-entity-intelligence-api/)
- [MDR Public AIP - Incident Data API](https://apis.io/collections/armor/open-armor-aip-incident-data-api/)
- [Armor Compliance Assessments API](https://apis.io/collections/armor/open-armor-assessments-api/)
- [Armor FH-AUTH Security Authentication API](https://apis.io/collections/armor/open-armor-authentication-api/)
- [Accounts Cloud Connections API](https://apis.io/collections/armor/open-armor-cloud-connections-api/)
- [Container Security Connector API](https://apis.io/collections/armor/open-armor-connector-api/)
- [Armor Compliance CSPM Connector API](https://apis.io/collections/armor/open-armor-cspm-connector-api/)
- [Armor Compliance CSPM Control Remediation API](https://apis.io/collections/armor/open-armor-cspm-control-remediation-api/)
- [Armor Compliance CSPM Policies API](https://apis.io/collections/armor/open-armor-cspm-policies-api/)
- [Armor Compliance CSPM Policy Controls API](https://apis.io/collections/armor/open-armor-cspm-policy-controls-api/)
- [Armor Compliance CSPM Report API](https://apis.io/collections/armor/open-armor-cspm-report-api/)
- [Armor Compliance CSPM Report Configuration API](https://apis.io/collections/armor/open-armor-cspm-report-configuration-api/)
- [Armor Compliance CSPM Resources API](https://apis.io/collections/armor/open-armor-cspm-resources-api/)
- [Armor Compliance CSPM Summary API](https://apis.io/collections/armor/open-armor-cspm-summary-api/)
- [Armor Compliance CSPM Usage API](https://apis.io/collections/armor/open-armor-cspm-usage-api/)
- [MDR Public Defender - Investigation API](https://apis.io/collections/armor/open-armor-defender-investigation-api/)
- [MDR Public Defender - Machine Actions API](https://apis.io/collections/armor/open-armor-defender-machine-actions-api/)
- [MDR Public Defender - Machines API](https://apis.io/collections/armor/open-armor-defender-machines-api/)
- [MDR Public Detection Rules API](https://apis.io/collections/armor/open-armor-detection-rules-api/)
- …and 45 more published on APIs.io

#### Overlays (16)

OpenAPI overlays, including conversational phrasing for each operation.

- [Armor Accounts Overlay](https://apis.io/overlays/armor/armor-accounts-overlay/)
- [Armor Agent Management Overlay](https://apis.io/overlays/armor/armor-agent-management-overlay/)
- [Armor Compliance Overlay](https://apis.io/overlays/armor/armor-compliance-overlay/)
- [Armor Container Security Overlay](https://apis.io/overlays/armor/armor-container-security-overlay/)
- [Armor Fh Auth Overlay](https://apis.io/overlays/armor/armor-fh-auth-overlay/)
- [Armor Incident Management Overlay](https://apis.io/overlays/armor/armor-incident-management-overlay/)
- [Armor Infrastructure Management Overlay](https://apis.io/overlays/armor/armor-infrastructure-management-overlay/)
- [Armor Log Management Overlay](https://apis.io/overlays/armor/armor-log-management-overlay/)
- [Armor Mdr Public Overlay](https://apis.io/overlays/armor/armor-mdr-public-overlay/)
- [Armor Notifications Overlay](https://apis.io/overlays/armor/armor-notifications-overlay/)
- [Armor Psk Auth Overlay](https://apis.io/overlays/armor/armor-psk-auth-overlay/)
- [Armor V1 Account Management Overlay](https://apis.io/overlays/armor/armor-v1-account-management-overlay/)
- [Armor V1 Infrastructure Overlay](https://apis.io/overlays/armor/armor-v1-infrastructure-overlay/)
- [Armor V1 Security Overlay](https://apis.io/overlays/armor/armor-v1-security-overlay/)
- [Armor V1 Support Overlay](https://apis.io/overlays/armor/armor-v1-support-overlay/)
- [Armor Webhooks Overlay](https://apis.io/overlays/armor/armor-webhooks-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Armor Authentication](https://apis.io/security/armor/armor-authentication/)
- [Armor Domain Security](https://apis.io/security/armor/armor-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Armor Scopes](https://apis.io/scopes/armor/armor-scopes/)

#### Plans and pricing (2)

Published plans, tiers and prices.

- [Armor Plans Pricing](https://apis.io/plans/armor/armor-plans-pricing/)
- [Armor Price Estimates](https://apis.io/plans/armor/armor-price-estimates/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.armor.com/)
- [Documentation](https://developer.armor.com/)
- [API reference](https://developer.armor.com/)
- [Pricing](https://www.armor.com/solutions/pricing)
- [Sign up](https://amp.armor.com/)
- [Support](https://www.armor.com/forms/under-attack)
- [Blog](https://res.armor.com/resources/?fwp_type=blog&_type=blog)
- [Compliance](https://www.armor.com/why-armor/trusted-expertise)
- [Terms of service](https://armor.pub/docs/Armor-General-Terms-of-Service.pdf)
- [Privacy policy](https://www.armor.com/legal/privacy-policy)
- [GitHub](https://github.com/armor)
- [Status](https://status.armor.com/)

## API Evangelist rating

**Kin Score 60.0** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 58.5 |
| Contract governance | 18.2 |
| Operational transparency | 18.4 |
| Developer ergonomics | 54.2 |
| Access clarity | 71.1 |

**Agent readiness 36.5** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | negotiable (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | — |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | documented (partial credit) |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | mostly |

**Regulatory alignment 39.2** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/armor/](https://apis.io/providers/armor/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Armor: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/armor/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
