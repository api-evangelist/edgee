# Edgee

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

Edgee is a French edge-native AI Gateway that sits between coding agents and LLM providers, intercepting, routing, compressing, metering and securing every request. Its OpenAI-compatible gateway API at edgee.io exposes chat completions, an Anthropic Messages endpoint, an OpenAI Responses endpoint, a model catalog of 230+ models across providers, token counting and a standalone compression endpoint, while a separate Console API at api.edgee.app handles organization management, gateway key management, BYOK provider keys and usage/cost export. A Rust CLI launches Claude Code, Codex, OpenCode, Cursor and VS Code Copilot through the gateway, and official TypeScript, Python, Go and Rust SDKs wrap the same surface. Edgee previously operated as an edge component runtime and data-collection platform at edgee.cloud; that documentation now redirects to the AI Gateway product at edgee.ai.

**Areas:** Company · Artificial Intelligence · LLM · AI Gateway · Agents · Developer Tools · Observability · FinOps · Edge Computing · Cost Management

## Edgee on APIs.io

Everything profiled for Edgee is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/edgee/](https://apis.io/providers/edgee/)** — or go straight to one of the APIs or properties below.

### APIs (7)

- [Edgee Console API](https://apis.io/apis/edgee/edgee-console/) — Management API for an Edgee organization: export AI Gateway usage and cost data as CSV or JSON, create/list/update/delete AI Gateway API keys, and configure…
- [Edgee Compress API](https://apis.io/apis/edgee/edgee-compress-api/) — Standalone token compression endpoint
- [Edgee Messages API](https://apis.io/apis/edgee/edgee-messages-api/) — Messages endpoints (Anthropic format)
- [Edgee Models API](https://apis.io/apis/edgee/edgee-models-api/) — Model management endpoints
- [Edgee Responses API](https://apis.io/apis/edgee/edgee-responses-api/) — Responses endpoints (OpenAI Responses API format)
- [Edgee Tokens API](https://apis.io/apis/edgee/edgee-tokens-api/) — Token estimation endpoints
- [Edgee Chat Completions API](https://apis.io/apis/edgee/edgee-chat-completions-api/) — Chat completion endpoints (OpenAI format)

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [edgee-mcp.yml](https://apis.io/servers/edgee/edgee-mcp-yml/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Edgee Gateway Overlay](https://apis.io/overlays/edgee/edgee-gateway-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Edgee Authentication](https://apis.io/security/edgee/edgee-authentication/)
- [Edgee Domain Security](https://apis.io/security/edgee/edgee-domain-security/)
- [Edgee Trust Center](https://apis.io/security/edgee/edgee-trust-center/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Edgee Plans Pricing](https://apis.io/plans/edgee/edgee-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Edgee Rate Limits](https://apis.io/rate-limits/edgee/edgee-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.edgee.ai/)
- [Documentation](https://www.edgee.ai/docs)
- [Getting started](https://www.edgee.ai/docs/quickstart)
- [API reference](https://www.edgee.ai/docs/api-reference)
- [Pricing](https://www.edgee.ai/pricing)
- [Sign up](https://www.edgee.ai/)
- [Support](https://www.edgee.ai/contact)
- [Changelog](https://www.edgee.ai/changelog)
- [Blog](https://www.edgee.ai/blog)
- [Compliance](https://trust.edgee.ai/)
- [Trust centre](https://trust.edgee.ai/)
- [Terms of service](https://www.edgee.ai/terms)
- [Privacy policy](https://www.edgee.ai/privacy)
- [GitHub](https://github.com/edgee-ai)
- [Status](https://status.edgee.ai/)

## API Evangelist rating

**Kin Score 58.4** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 50.9 |
| Contract governance | 4.5 |
| Operational transparency | 26.3 |
| Developer ergonomics | 73.2 |
| Access clarity | 92.1 |

**Agent readiness 33.4** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 27.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/edgee/](https://apis.io/providers/edgee/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Edgee: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/edgee/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
