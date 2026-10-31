# Oxide

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

Oxide Computer Company builds a rack-scale cloud computer: integrated server sleds (Gimlet), a rack-level switch (Sidecar), Oxide's own illumos distribution (Helios), the Propolis/bhyve hypervisor and the Crucible distributed block store, all driven by a single control plane called Nexus. Nexus exposes the Oxide Region API, a 315-operation OpenAPI 3.0.3 REST contract covering silos, projects, instances, disks, snapshots, images, VPCs, subnets, firewall rules, floating and ephemeral IPs, IP pools, affinity groups, alerts and webhook receivers, audit log, metrics/OxQL, hardware inventory, BGP/BFD networking, SAML and SCIM identity, support bundles and system update. Because the product is a rack a customer owns, the API is served from the customer's own control-plane domain rather than a vendor-hosted endpoint. Oxide publishes first-party Rust, TypeScript and Go SDKs, an `oxide` CLI, a Terraform provider and a Packer plugin, and develops essentially the entire stack in the open on GitHub.

**Areas:** Cloud Computing · Infrastructure · Compute · Virtualization · Networking · Storage · Hardware · On-Premises · Private Cloud · Open Source

## Oxide on APIs.io

Everything profiled for Oxide is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/oxide-computer/](https://apis.io/providers/oxide-computer/)** — or go straight to one of the APIs or properties below.

### APIs (30)

- [Oxide Affinity API](https://apis.io/apis/oxide-computer/oxide-computer-affinity-api/) — Anti-affinity groups give control over instance placement.
- [Oxide Console Auth API](https://apis.io/apis/oxide-computer/oxide-computer-console-auth-api/) — API for console authentication
- [Oxide Current User API](https://apis.io/apis/oxide-computer/oxide-computer-current-user-api/) — Information pertaining to the current user.
- [Oxide Disks API](https://apis.io/apis/oxide-computer/oxide-computer-disks-api/) — Virtual disks are used to store instance-local data which includes the operating system.
- [Oxide Experimental API](https://apis.io/apis/oxide-computer/oxide-computer-experimental-api/) — Experimental, unstable interfaces, primarily for use by Oxide personnel
- [Oxide External Subnets API](https://apis.io/apis/oxide-computer/oxide-computer-external-subnets-api/) — External subnets that can be attached to instances.
- [Oxide Floating Ips API](https://apis.io/apis/oxide-computer/oxide-computer-floating-ips-api/) — Floating IPs allow a project to allocate well-known IPs to instances.
- [Oxide Images API](https://apis.io/apis/oxide-computer/oxide-computer-images-api/) — Images are read-only virtual disks that may be used to boot virtual machines.
- [Oxide Instances API](https://apis.io/apis/oxide-computer/oxide-computer-instances-api/) — Virtual machine instances are the basic unit of computation. These operations are used for provisioning, controlling, and destroying instances.
- [Oxide Ip Pools API](https://apis.io/apis/oxide-computer/oxide-computer-ip-pools-api/) — IP pools are collections of external IPs that can be allocated and attached to instances.
- [Oxide Login API](https://apis.io/apis/oxide-computer/oxide-computer-login-api/) — Authentication endpoints
- [Oxide Metrics API](https://apis.io/apis/oxide-computer/oxide-computer-metrics-api/) — Silo-scoped metrics
- [Oxide Policy API](https://apis.io/apis/oxide-computer/oxide-computer-policy-api/) — System-wide IAM policy
- [Oxide Projects API](https://apis.io/apis/oxide-computer/oxide-computer-projects-api/) — Projects are a grouping of associated resources such as instances and disks within a silo for purposes of billing and access control.
- [Oxide Silos API](https://apis.io/apis/oxide-computer/oxide-computer-silos-api/) — Silos represent a logical partition of users and resources.
- [Oxide Snapshots API](https://apis.io/apis/oxide-computer/oxide-computer-snapshots-api/) — Snapshots of virtual disks at a particular point in time.
- [Oxide Subnet Pools API](https://apis.io/apis/oxide-computer/oxide-computer-subnet-pools-api/) — Subnet pools are collections of external subnets that can be allocated and attached to instances.
- [Oxide System/alerts API](https://apis.io/apis/oxide-computer/oxide-computer-system-alerts-api/) — Alerts deliver notifications for events that occur on the Oxide rack
- [Oxide System/audit Log API](https://apis.io/apis/oxide-computer/oxide-computer-system-audit-log-api/) — These endpoints relate to audit logs.
- [Oxide System/hardware API](https://apis.io/apis/oxide-computer/oxide-computer-system-hardware-api/) — These operations pertain to hardware inventory and management. Racks are the unit of expansion of an Oxide deployment. Racks are in turn composed of sleds,…
- [Oxide System/ip Pools API](https://apis.io/apis/oxide-computer/oxide-computer-system-ip-pools-api/) — IP pools are collections of external IPs. Linking a pool to a silo makes it available for allocation by users in that silo.
- [Oxide System/metrics API](https://apis.io/apis/oxide-computer/oxide-computer-system-metrics-api/) — Metrics provide insight into the operation of the Oxide deployment. These include telemetry on hardware and software components that can be used to…
- [Oxide System/networking API](https://apis.io/apis/oxide-computer/oxide-computer-system-networking-api/) — This provides rack-level network configuration.
- [Oxide System/silos API](https://apis.io/apis/oxide-computer/oxide-computer-system-silos-api/) — Silos represent a logical partition of users and resources.
- [Oxide System/status API](https://apis.io/apis/oxide-computer/oxide-computer-system-status-api/) — Endpoints related to system health
- [Oxide System/subnet Pools API](https://apis.io/apis/oxide-computer/oxide-computer-system-subnet-pools-api/) — Subnet pools are collections of external subnets. Linking a pool to a silo makes it available for allocation by users in that silo.
- [Oxide System/support Bundles API](https://apis.io/apis/oxide-computer/oxide-computer-system-support-bundles-api/) — Support bundles collect debugging information from the rack for use by Oxide support.
- [Oxide System/update API](https://apis.io/apis/oxide-computer/oxide-computer-system-update-api/) — Upload and manage system updates
- [Oxide Tokens API](https://apis.io/apis/oxide-computer/oxide-computer-tokens-api/) — API clients use device access tokens for authentication.
- [Oxide Vpcs API](https://apis.io/apis/oxide-computer/oxide-computer-vpcs-api/) — Virtual Private Clouds (VPCs) provide isolated network environments for managing and deploying services.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Oxide Computer Alerts Webhooks](https://apis.io/asyncapis/oxide-computer/oxide-computer-alerts-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [oxide-computer-mcp.yml](https://apis.io/servers/oxide-computer/oxide-computer-mcp-yml/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Oxide Computer Region Api Overlay](https://apis.io/overlays/oxide-computer/oxide-computer-region-api-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Oxide Computer Authentication](https://apis.io/security/oxide-computer/oxide-computer-authentication/)
- [Oxide Computer Domain Security](https://apis.io/security/oxide-computer/oxide-computer-domain-security/)
- [Oxide Computer Vulnerability Disclosure](https://apis.io/security/oxide-computer/oxide-computer-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Oxide Computer Plans Pricing](https://apis.io/plans/oxide-computer/oxide-computer-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Oxide Computer Rate Limits](https://apis.io/rate-limits/oxide-computer/oxide-computer-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://oxide.computer)
- [Documentation](https://docs.oxide.computer)
- [Getting started](https://docs.oxide.computer/guides/quickstart)
- [API reference](https://docs.oxide.computer/api)
- [Support](https://oxide.computer/contact)
- [Blog](https://oxide.computer/blog)
- [Privacy policy](https://oxide.computer/privacy-policy)
- [GitHub](https://github.com/oxidecomputer)

## API Evangelist rating

**Kin Score 46.2** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 47.7 |
| Contract governance | 4.5 |
| Operational transparency | 36.8 |
| Developer ergonomics | 73.2 |
| Access clarity | 10.5 |

**Agent readiness 28.1** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 26.5** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/oxide-computer/](https://apis.io/providers/oxide-computer/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Oxide: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/oxide-computer/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
