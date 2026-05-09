# Ramp Business — Developer Experience

*Stream 5: Ramp Developer API, OAuth scopes, webhooks, SCIM, AI/Agent APIs, integrations, pricing, gotchas, peer comparison*
*Compiled 2026-05-09. Confidence labels: ✅ high, 🟡 medium, 🔴 low/uncertain.*

---

## 1. What is Ramp Business and what do you integrate with?

Ramp Business (`ramp.com`, **not** `ramp.network` which is a fiat-to-crypto on-ramp) is a corporate-spend-management fintech that bundles charge cards, expense management, accounts payable / Bill Pay, procurement, travel, and accounting automation into one stack ✅ ([Ramp homepage](https://ramp.com/)). For developers, the integration surface is the **Ramp Developer API** at `docs.ramp.com/developer-api/v1` plus a recently-released **Ramp MCP server** and **Ramp Agent Cards** (Visa Intelligent Commerce-based virtual cards for AI agents) ✅ ([Ramp Developer Platform](https://ramp.com/developer-tools), [Ramp Agent Cards launch](https://stabledash.com/news/2026-03-11-ramp-launches-agent-cards-to-enable-secure-autonomous-ai-spending), [ramp-public/ramp_mcp](https://github.com/ramp-public/ramp_mcp)). Ramp's ICP is mid-market and growing-enterprise finance teams; the API is positioned as the primitives layer beneath that — transactions, cards, bills, vendors, users, custom records — that lets ERPs, FP&A tools, and (newer) agent platforms plug into the same data plane finance teams use through the UI.

---

## 2. The Ramp Developer API — base URL, auth, versioning, sandbox

| Attribute | Value | Confidence | Source |
|---|---|---|---|
| Production base URL | `https://api.ramp.com/developer/v1` | ✅ | [Getting Started](https://docs.ramp.com/developer-api/v1/guides/getting-started) |
| Sandbox base URL | `https://demo-api.ramp.com/developer/v1` | ✅ | [Accessing the Developer API](https://support.ramp.com/hc/en-us/articles/46681939909907-Accessing-the-Developer-API) |
| OAuth token endpoint | `POST /developer/v1/token` (sandbox: `demo-api.ramp.com`) | ✅ | |
| API version | `v1` (path-versioned) | ✅ | URL evidence above |
| Auth | OAuth 2.0 — three grant types: `client_credentials`, `authorization_code`, `refresh_token`. PKCE supported on auth-code flow. | ✅ | [Authorization scopes](https://docs.ramp.com/developer-api/v1/overview/scopes) |
| Token TTL | `client_credentials` → 10 days; `authorization_code` & `refresh_token` → 1 hour | ✅ | [Composio: Ramp OAuth](https://composio.dev/auth/ramp) |
| Refresh tokens | Do not expire; require `client_id` + `client_secret` to use (mitigates leak risk) | ✅ | [What to do if OAuth credentials are leaked](https://support.ramp.com/hc/en-us/articles/25329686691603-What-to-do-if-OAuth-credentials-are-leaked) |
| Who can authorize | Only Admin or Business Owner role; non-admins cannot grant scopes | ✅ | |
| App creation | Settings → Developer → Create New App (separate apps per environment) | ✅ | |

Example client-credentials handshake:

```bash
# 1) Get token
curl -X POST https://api.ramp.com/developer/v1/token \
  -u "$CLIENT_ID:$CLIENT_SECRET" \
  -d "grant_type=client_credentials&scope=transactions:read receipts:write"

# 2) Call API
curl https://api.ramp.com/developer/v1/transactions \
  -H "Authorization: Bearer $ACCESS_TOKEN"
```

Two practical gotchas: (a) you must build **two completely separate apps** for sandbox vs production — credentials and webhook subscriptions are not shared 🟡; (b) scopes are bound at issuance, so changing scopes requires a new token — there is no "incremental consent" flow ✅.

---

## 3. Endpoint catalog

The full surface is documented at `docs.ramp.com/developer-api/v1/`.

| Resource group | Sample endpoints | Capabilities | Confidence |
|---|---|---|---|
| **Cards** | `GET/POST /cards`, `POST /cards/deferred` (physical/virtual issuance), `PATCH /cards/{id}` (update display name, owner, restrictions), `POST /cards/{id}/suspension`, `DELETE /cards/{id}/suspension` | Issue physical/virtual cards, freeze/unfreeze, set spend restrictions, change owner. Statement balance lives under transfers. | ✅ |
| **Transactions** | `GET /transactions`, `GET /transactions/{id}`, `GET /transactions?sync_status=SYNC_READY`, sync-status updates | List/filter, fetch ready-to-sync, dispute is **UI-only** (no public dispute endpoint observed) | ✅ list, 🟡 dispute |
| **Reimbursements** | `GET/POST /reimbursements`, `POST /receipts` (with `reimbursement_id`) | List, filter by direction (B2U / U2B), state, sync status, date ranges. OCR auto-creates draft from uploaded receipt. | ✅ |
| **Bills / Bill Pay** | `GET/POST /bills`, `GET /bills/drafts`, `POST /bills/{id}/...` payment ops | Create draft bill, finalize, pay (ACH/wire/card). Bills paid via card also surface in Transactions linked by `bill.details.transaction_ids`. | ✅ |
| **Vendors** | `GET/POST /vendors`, `GET/POST /vendor-bank-accounts`, vendor approvals | CRUD vendors, attach bank accounts, configure approval flows. | ✅ |
| **Users / Departments / Locations** | `GET/POST /users`, `GET/POST /departments`, `GET/POST /locations` | CRUD with `custom_fields` like Cost Center, Employee ID, Region, Team. | ✅ |
| **Receipts / Memos** | `POST /receipts` (multipart, OCR auto-link), receipts integrations endpoint | Upload receipt, link to txn or reimbursement; receipts:read / receipts:write scopes. Memos as transaction-attached metadata. | ✅ |
| **Custom Fields / Custom Records** | `POST /accounting/field-options`, `POST /custom-records/configure/native-tables` | Extend Ramp objects with bespoke fields; add ERP-style classifications. | ✅ |
| **Limits / Spend Programs** | `GET/POST /limits`, `GET/POST /spend-programs` | Programmatic spend control creation. | ✅ |
| **Statements / Transfers** | `GET /statements`, `GET /transfers` | Read statement-balance transfers (ACH/wire); paying down card balance. | ✅ |
| **Approvals / Policies** | Mostly UI; vendor-edit approval flows configurable via Policies | Vendor approvals exposed; spend-policy programmatic configuration is partial. | 🟡 |
| **Travel / Itineraries** | No first-party Travel API endpoints found. Itineraries auto-generated from receipts forwarded to `receipts@ramp.com` or via Priceline-backed bookings inside the UI. | Trips are **read-only via UI**; no programmatic itinerary creation endpoint surfaced publicly. | 🔴 |
| **Webhooks** | `POST /webhooks`, `GET/PATCH/DELETE /webhooks/{id}` | Manage subscriptions; events listed below. | ✅ |
| **Leads** | `GET /leads`, `POST /leads` (referrals), `leads:read` / `leads:write` | Partner referral / lead-handoff (mostly for partner program). | 🟡 |
| **Accounting / Sync** | `/accounting/...` — push GL accounts, fields, status updates back to Ramp | Underpins NetSuite/Intacct/QBO connectors. | ✅ |
| **Agent Cards (VIC)** | Issue tokenized credentials via API/MCP/CLI; per-transaction, single-use | Built on Visa Intelligent Commerce; merchant-locked, spend-capped, native to MCP. | 🟡 |

---

## 4. Webhooks

Ramp ships a developer-managed webhook subscription model ✅ ([Webhooks reference](https://docs.ramp.com/developer-api/v1/webhooks)).

- **Subscription model**: `POST /developer/v1/webhooks` with `url` and `subscribed_events` array. CRUD via the same path.
- **Signing scheme**: HMAC-SHA256 with a per-subscription secret. The secret historically required tech-support involvement to rotate 🟡. Header naming follows the de facto Ramp standard (`X-Ramp-Signature` / similar) — **note** this is the Ramp Business webhook scheme; the unrelated Ramp Network product uses ECDSA over the JSON body in `X-Body-Signature`, which is a frequent source of confusion 🟡.
- **Events** (partial list, from public docs and community references): `transaction.created`, `transaction.updated`, `card.created`, `card.suspended`, `bill.created`, `bill.paid`, `reimbursement.created`, `reimbursement.approved`, `transfer.completed`, `user.created`, `user.deactivated` 🟡 — Ramp's published catalog is not exhaustive in indexed search excerpts.
- **Delivery semantics**: HTTPS POST with JSON body. No rich public retry-policy spec found; community references suggest exponential backoff with eventual deactivation on persistent 4xx — **treat as undocumented** 🔴.
- **Replay protection**: Signed timestamp pattern is standard practice; precise headers were not captured in publicly indexed pages 🔴.
- **Practical advice**: Treat webhooks as best-effort and reconcile via paged `GET /transactions` polls — many production Ramp integrations do exactly this.

```python
# Verify a Ramp Business webhook (defensive pattern; verify exact header name in your portal)
import hmac, hashlib

def verify(secret: bytes, body: bytes, signature_header: str) -> bool:
    expected = hmac.new(secret, body, hashlib.sha256).hexdigest()
    return hmac.compare_digest(expected, signature_header)
```

---

## 5. SCIM 2.0

Ramp's SCIM is **enterprise-grade and on every plan including Free**, which is unusually generous ✅ ([SCIM provisioning docs](https://support.ramp.com/hc/en-us/articles/39078698246547-Setting-up-SCIM-and-managing-user-provisioning)).

- **IdPs supported**: Okta, Microsoft Entra (Azure AD), Rippling — first-class. OneLogin/JumpCloud via SAML SSO but SCIM is more limited there 🟡.
- **Capabilities**: Invite users, sync attributes (department, location, custom fields), deactivate users on offboarding.
- **Custom user-field mapping**: Microsoft Entra requires schema URN prefix `urn:ietf:params:scim:schemas:extension:ramp:2.0:User:<attr>` ✅.
- **Known limitations**:
  - Department **and** location must be set on every user — missing either silently fails to provision ✅.
  - Sync latency: up to 5 minutes typical, sometimes longer 🟡.
  - **Ramp does not support IdP-initiated SAML** — SP-initiated only ✅.
- **Endpoint catalog**: standard SCIM 2.0 (`/Users`, `/Groups`, `/Schemas`, `/ServiceProviderConfig`).

---

## 6. OAuth scopes

From [docs.ramp.com/developer-api/v1/overview/scopes](https://docs.ramp.com/developer-api/v1/overview/scopes):

| Scope | What it enables | Confidence |
|---|---|---|
| `business:read` | Read business profile / entity info | ✅ |
| `accounting:read` / `accounting:write` | GL accounts, field options, sync status | ✅ |
| `bills:read` / `bills:write` | List, create, pay bills | ✅ |
| `cards:read` / `cards:write` | List/issue/freeze cards | ✅ |
| `transactions:read` | List/get transactions, sync status | ✅ |
| `users:read` / `users:write` | CRUD users, invitations | ✅ |
| `departments:read` / `departments:write` | Org structure | ✅ |
| `locations:read` / `locations:write` | Org structure | ✅ |
| `limits:read` / `limits:write` | Spend limits / programs | ✅ |
| `vendors:read` / `vendors:write` | Vendor CRUD, bank accounts | ✅ |
| `merchants:read` | Merchant lookup | ✅ |
| `receipts:read` / `receipts:write` | Receipt upload / link | ✅ |
| `reimbursements:read` / `reimbursements:write` | Reimbursements | ✅ |
| `transfers:read` | Statement-balance transfers | ✅ |
| `offline_access` | Receive refresh token | ✅ |

The pattern is `<resource>:<read|write>`. There is **no `*:admin`** super-scope — least-privilege design throughout, which is a positive DX signal ✅.

---

## 7. AI / Intelligence APIs

This is where Ramp is moving fastest in 2025–26.

- **Ramp MCP server** (Model Context Protocol) — open-sourced at [ramp-public/ramp_mcp](https://github.com/ramp-public/ramp_mcp). Built with FastMCP. Implements an in-memory SQLite ETL over the Developer API to let Claude/other LLMs answer "give me an overview of my business's spend in the past year" without blowing context windows ✅ ([ZenML LLMOps writeup](https://www.zenml.io/llmops-database/mcp-server-for-natural-language-business-data-analytics)).
- **Ramp AP Agents** — autonomous agents inside Bill Pay that auto-code line items, run fraud heuristics, recommend approvals, optimize payment timing for cashback. Reported at GA: 85% first-pass coding accuracy, $1M+ fraud caught, 90% approval-recommendation acceptance ✅ ([AP just became autonomous](https://ramp.com/blog/ramp-ap-agents-announcement)).
- **Ramp Agent Cards** (March 2026) — virtual cards built on **Visa Intelligent Commerce (VIC)** for AI agents. Tokenized, single-use, merchant-scoped, spend-capped. Provisioned via API, MCP, or CLI ✅.
- **Receipt OCR / categorization** — exposed *implicitly* via `POST /receipts`. When you upload a receipt, the OCR + multimodal RAG pipeline (Azure AI under the hood, per Microsoft case study) extracts merchant + line items and auto-creates draft reimbursements / matches to txns ✅.
- **No standalone "categorize this transaction" endpoint** is publicly documented. AI categorization is a side-effect of normal endpoints. 🟡

**Net**: Ramp is genuinely AI-forward, but the AI is mostly **bundled into existing data endpoints** rather than exposed as a separate inference API. The two real "AI surfaces" you can call from outside are (a) the MCP server for natural-language analytics and (b) Agent Cards for spend-issuance-as-a-service to your own agents.

---

## 8. Sandbox quality

| Capability | Sandbox? | Confidence |
|---|---|---|
| Separate `demo-api.ramp.com` host with its own credentials | ✅ Yes | ✅ |
| Issue virtual/physical cards | ✅ Virtual yes; physical simulated | 🟡 |
| Create/pay bills end-to-end | 🟡 Partial — bill creation works; ACH simulation is mocked, not full clearing-cycle realism | 🟡 |
| Simulate fake card transactions | 🟡 Limited — there is **no public "simulate authorization"** endpoint analogous to Stripe Issuing's `POST /test_helpers/issuing/transactions/create_force_capture`. Most teams seed via the sandbox UI. | 🟡 |
| Trigger webhooks on demand | 🟡 No public "send test event" endpoint surfaced; you must drive the underlying state change. | 🟡 |
| User/Department/Location CRUD | ✅ Yes | ✅ |
| OAuth flows fully testable | ✅ Yes | ✅ |
| SCIM testable | 🟡 Yes via Okta/Entra preview tenants | 🟡 |

**Verdict**: Sandbox is real, isolated, and good for OAuth + read-side workflows, but **transaction simulation lags Stripe Issuing meaningfully**. A weekend hack against the sandbox feels like a partly-staged set: convincing for `GET` flows, less so for the closed-loop write flows you'd want for testing approval bots.

---

## 9. Rate limits

- Ramp documents rate limiting at [docs.ramp.com/developer-api/v1/overview/rate-limiting](https://docs.ramp.com/developer-api/v1/overview/rate-limiting) ✅ but specific QPS tiers are not surfaced in indexed search excerpts and appear to be set per-app and per-endpoint family at issuance time 🟡.
- 429 response includes a `Retry-After` header per Ramp's own docs and standard expectations 🟡.
- **Practical observation**: Compare to Bill.com's documented 18,000 calls per developer key per hour ([BILL API](https://www.bill.com/product/api)) — Ramp's published transparency is **lower** than Bill.com's and noticeably lower than Stripe's. This is the single largest documentation-quality gap in Ramp's API.

---

## 10. Idempotency

- Ramp **does** support `Idempotency-Key` header on POST endpoints ✅.
- **TTL on the idempotency key**: not publicly documented — assume 24h as a defensive default 🔴.
- **Important**: 429 rate-limited calls bypass the idempotency layer (rate-limiter runs first), so a retried call can produce a different result. Same pitfall applies to Stripe and most modern APIs — handle with backoff + same key.

---

## 11. SDK availability

| Language | Availability | Source |
|---|---|---|
| OpenAPI spec | 🟡 Reportedly at `/openapi/developer-api.json`, also Postman collection on [postman.com/apifyi/ramp-api](https://www.postman.com/apifyi/ramp-api/overview) | 🟡 |
| Python | ❌ No first-party SDK; community: r0aringthunder/ramp-api wrapper | ✅ |
| Node / TypeScript | ❌ No first-party SDK | ✅ |
| Go | ❌ No first-party SDK | ✅ |
| Ruby | ❌ No first-party SDK | ✅ |
| Rust | ❌ Third-party `ramp-api` crate exists ([docs.rs/ramp-api](https://docs.rs/ramp-api)) | ✅ |
| MCP server | ✅ Official, open-source ([ramp-public/ramp_mcp](https://github.com/ramp-public/ramp_mcp)) | ✅ |

This is a notable gap relative to Brex (which publishes a Postman collection and OpenAPI but also lacks first-party SDKs) and a much bigger gap relative to Stripe Issuing (where every major language has an officially maintained SDK). Ramp's bet seems to be: ship MCP + OpenAPI + Postman; let the community/Composio/Pipedream do the wrapper work.

---

## 12. Documentation quality (1–10 scoring)

| Area | Score | Notes |
|---|---|---|
| Auth / OAuth | 8 | Three grants, PKCE, refresh tokens, leak playbook — solid. |
| Cards | 7 | Clear endpoints; physical-card lifecycle docs thinner than Stripe Issuing. |
| Transactions | 8 | Filter set is rich; `sync_status=SYNC_READY` is a thoughtful affordance. |
| Bill Pay | 7 | Strong list/create coverage. |
| Webhooks | 5 | Event catalog incomplete in public surface; signing-secret rotation requires support; retry policy not published. |
| SCIM | 8 | Well-documented IdP wizards, custom-field URN scheme. |
| AI APIs | 6 | MCP is great. AP-Agent and Agent-Card programmatic surfaces are early-access and reference docs are sparse. |
| Sandbox | 6 | Exists, isolated, but transaction-simulation tooling is weak. |
| Rate limits | 4 | Concept page exists; numbers not transparent. |
| OpenAPI / Postman | 7 | Available, public Postman collection. No officially-versioned multi-language SDKs. |

**Overall**: 6.7/10. Above average for a fintech, well below Stripe-tier.

---

## 13. Integrations marketplace

Ramp markets "1,000+ integrations" today. Based on [NetSuite Integration](https://ramp.com/integrations/netsuite) and [Merge HRIS case study](https://www.merge.dev/case-studies/ramp):

| Category | Examples | Notes |
|---|---|---|
| Accounting / ERP | NetSuite, Sage Intacct, QuickBooks Online, QuickBooks Desktop, Microsoft Dynamics 365 F&O, Microsoft Dynamics Business Central, Xero, Workday Financial Management, Acumatica, Sage X3, Sage 50, Oracle Fusion Cloud, Zoho Books, FreshBooks | First-party. Deepest integration is NetSuite. |
| HRIS | Rippling, Gusto, Workday HCM, ADP, BambooHR, Sequoia, Paylocity, Justworks, TriNet | Built on Merge's unified API → 30+ HRIS connectors |
| Travel | Navan (cross-listing), Priceline (embedded into Ramp Travel) | Ramp Travel has supplanted older Comtravo-style integrations |
| Procurement | Coupa, ServiceNow | More limited than full Ramp Procurement |
| SSO | Okta, Microsoft Entra, OneLogin, Google Workspace, JumpCloud | Mostly SAML; SCIM on Okta + Entra + Rippling |
| Data warehouse | Snowflake, BigQuery, Redshift, Databricks | Reverse-ETL via Hightouch is a popular path |
| Comms | Slack (deep), Microsoft Teams | Slack supports `/ramp` slash commands and admin alerts |
| iPaaS | Zapier, Make, Pipedream, Tray.io, Workato, Composio (for AI agents) | These multiply effective coverage to thousands of apps |

---

## 14. Public partner showcase

- **Quanta** — accounting automation product built on Ramp API for enriched transaction context ✅ ([Quanta partner spotlight](https://ramp.com/blog/technology-partner-spotlight-quanta)).
- **Composio** — exposes Ramp as a tool surface for AI agents with managed OAuth ✅.
- **Pipedream / Make / Zapier / Tray.io** — listed app integrations powered by Ramp's API.
- **Hightouch** — operational-analytics syncs out of Ramp's data warehouse to other SaaS systems.
- **MPP (Merchant Payments Protocol) launch partners list** — Ramp is one of 100+ launch service providers alongside Browserbase, DoorDash, Nubank, Revolut ✅.

---

## 15. Pricing for developers

- **Free for any Ramp customer** to use the Developer API ✅. Admin/owner role required to mint credentials.
- **No per-call charges** documented.
- The base **Ramp Free** plan ($0/user/month) **includes API access, SCIM, and SSO** ✅. Plus is $15/user/month for advanced workflow features unrelated to API metering.
- Practical implication: a solo dev signing up for a Ramp Free account today gets the same API surface a $50M-ARR customer does. This is dramatically more open than Concur (gated) or Coupa (enterprise-only).

---

## 16. Common dev pitfalls

1. **Sandbox-vs-prod confusion** — separate apps required; webhook subscriptions and OAuth credentials don't carry over ✅.
2. **Admin-only OAuth grants** — non-admins literally can't authorize a third-party app, so embedded apps need to scope-onboard via an admin flow ✅.
3. **Token TTL mismatch** — `client_credentials` tokens last 10 days but `authorization_code` tokens last 1 hour ✅.
4. **SCIM department-and-location requirement** — users without both fields silently fail provisioning ✅.
5. **Webhook secret rotation** — historically required tech-support involvement; not self-serve in all cases 🟡.
6. **No published rate-limit numbers** — production teams discover caps the hard way 🟡.
7. **Refresh token doesn't expire but is bound to client_id+client_secret** — devs still confuse "long-lived" with "doesn't need rotation" ✅.
8. **Travel itineraries are not programmatically creatable** — automation must rely on receipt forwarding ✅.
9. **Custom-field schema URN prefix for Entra** — easy to miss `urn:ietf:params:scim:schemas:extension:ramp:2.0:User:` ✅.

---

## 17. Peer comparison — DX matrix

| Capability | **Ramp** | **Brex** | **Mercury** | **Navan** | **Stripe Issuing** | **Coupa** | **Concur** | **Bill.com** |
|---|---|---|---|---|---|---|---|---|
| OpenAPI spec public | 🟡 yes | ✅ yes | ✅ yes | 🟡 yes | ✅ yes | 🟡 partial | 🟡 partial | ✅ yes |
| Sandbox quality | 6/10 | 7/10 | 7/10 | 6/10 | **9/10** | 5/10 | 5/10 | 6/10 |
| OAuth 2.0 (PKCE) | ✅ | ✅ | ✅ (PKCE) | ✅ | API key + restricted keys | API key | OAuth | OAuth |
| Webhook signing | HMAC-SHA256 🟡 | HMAC | JSON merge-patch | yes | **Stripe-Signature ts+v1** | yes | yes | yes |
| SCIM 2.0 | ✅ Okta/Entra/Rippling, free | ✅ | partial | partial | n/a | enterprise | enterprise | partial |
| Rate-limit transparency | 4/10 | 6/10 | 6/10 | 5/10 | **9/10** | 5/10 | 4/10 | **8/10 (18k/hr)** |
| Official SDKs | none (MCP only) | none (Postman) | none | partial | **Py/JS/Go/Ruby/Java/PHP/.NET** | none | partial | partial |
| Free dev tier | **Yes (Free plan)** | Yes (sandbox) | Yes | gated | Yes (test mode) | gated | gated | yes |
| Doc quality (overall) | 7/10 | 8/10 | 7/10 | 6/10 | **10/10** | 6/10 | 5/10 | 7/10 |
| AI/agent API exposure | **Best in class** (MCP + Agent Cards on VIC) | Limited | Limited | Some | Issuing-as-platform | Limited | Limited | Limited |
| Card issuance API | ✅ | ✅ | n/a (banking) | partial via card | ✅ infra-grade | n/a | n/a | n/a |
| Bill Pay API | ✅ + AP Agents | ✅ | partial | n/a | n/a | ✅ enterprise | ✅ | ✅ (industry leader by share) |

**Read of the matrix**: Stripe Issuing is the DX leader for raw card-issuing infrastructure; Ramp leads on **AI-agent integration** (MCP server + VIC-based Agent Cards) and on **enterprise plumbing** (free SCIM, rich endpoint surface). Brex is the closest direct competitor on developer experience and matches Ramp on most axes except AI-agent surfacing, where Ramp is currently ahead.

---

## 18. The "weekend integration" feasibility test

**Test 1 — Slack bot that posts new transactions:**

Feasibility: **High** ✅. Two viable paths:

- *Webhook path* (preferred): subscribe to `transaction.created`, ship a Slack `chat.postMessage` from a serverless function. ~1 evening for a competent dev.
- *Polling path*: cron `GET /transactions?from_date=...` every 60s. Simpler, more reliable than webhooks given rate-limit unknowns. ~3 hours.

The MVP fits in <100 lines of code. The Pipedream Ramp+Slack integration already exists as a no-code reference.

**Test 2 — AI agent that approves bills based on prior context:**

Feasibility: **Medium–High** 🟡. Realistic 1–2 weekend project:

- Use Ramp MCP server to give Claude/GPT context on prior similar bills, vendor history, and accounting categories.
- For each new bill (`bill.created` webhook or `GET /bills?status=draft`), prompt the LLM with policy + history to produce an approve/reject + reasoning.
- Auto-approve if confidence above threshold; otherwise post to Slack for human review.

What blocks a fully production-grade version: (a) **approval-policy programmatic configuration is partial** — Ramp's policy engine has UI-only knobs you can't replicate via API; (b) no published rate limits make the polling design fragile; (c) Ramp Agent Cards are early-access — if you want the agent to actually pay (not just approve), you need the VIC pathway, which is an allowlist program today.

**Net**: A solo Solana dev can absolutely ship a credible Ramp integration in a weekend. The MCP server collapses 80% of the LLM-reasoning code into config. The friction is on the *write* side, not the *read* side.

---

## 19. AI x crypto angle

This is the most interesting axis for the user.

- **Agent Cards are the wedge**. Ramp Agent Cards are tokenized, single-use, merchant-locked Visa credentials issued via API/MCP/CLI to autonomous agents ✅. Combined with Ramp's policy engine, this is an **off-chain corporate-spend rail for agents** that the rest of the stack hasn't built yet.
- **MPP / x402 / AP2 alignment**: Ramp is publicly listed among the 100+ launch participants for **MPP (Merchant Payments Protocol)** — the agent-checkout layer that complements x402 (HTTP 402 for stablecoin micropayments) and AP2 (Google's mandate-based agent-payments protocol with verifiable credentials and Coinbase involvement) ✅.
- **Ramp does not natively support x402**. There's no `402 Payment Required` or USDC-settlement endpoint in the Ramp Developer API. The Ramp surface is **fiat rails, agent-issued**.
- **Bridge opportunity**: a thin shim — "x402 facilitator that issues Ramp Agent Cards on demand" — is a buildable side-project. Agent calls protected resource → 402 returned → facilitator issues a single-use VIC token for the merchant in question → call retried with that card. This sidesteps the on-chain settlement entirely while preserving the x402 UX. To my knowledge this exact pattern is not yet a public product 🔴.
- **Reverse direction**: Ramp's own cashback-on-bill-pay flow uses Visa rails, not stablecoins. There's no surfaced "pay this bill in USDC" endpoint. If Ramp ships Bridge/USDC corridors (Stripe, Mercury, and Brex have all moved this way), the integration story flips and stablecoin-funded bill pay becomes addressable. 🔴 No public roadmap commitment from Ramp on that.
- **For a Solana dev specifically**: the most directly addressable "AI x crypto x Ramp" idea is a connector that lets Solana-native agent infrastructure (e.g., agent kits using SPL/USDC) orchestrate **fiat corporate spend through Ramp Agent Cards** when the merchant doesn't accept stablecoins. The agent treats Ramp as a fiat actuator. The trust anchor is whatever AP2 mandate / on-chain attestation you mint before requesting a card.

---

## 20. Verdict for the user

**Build on Ramp's API when:**
- You're shipping an AI-agent product that needs **autonomous corporate-spend execution** with real-world card acceptance (the VIC + Agent Cards stack is currently best-in-class for this).
- Your buyer is a finance team and you need **deep accounting/ERP context** to be useful (Ramp's data model is the cleanest in the category).
- You need **free SCIM and SSO** to ship enterprise-ready quickly.
- You want to publish into Ramp's partner directory and monetize against the Ramp customer base ✅.

**Skip Ramp's API when:**
- You need **infrastructure-grade card issuing** for a non-finance audience → Stripe Issuing wins on DX, simulation, SDKs.
- You need **stablecoin-native** payment rails today → use x402/AP2 directly with Coinbase or Crossmint; Ramp is not on-chain.
- You need **transparent, published rate limits** for a high-QPS read workload → Bill.com or Stripe are easier to plan around.
- You need **first-party SDKs** in your language → wait for them or write your own (the OpenAPI spec exists).

**Solana-developer-specific recommendation**: Ramp is **the most interesting fintech API surface to bridge into the agent-payments narrative right now**. Two concrete bets worth a weekend each:

1. **x402 → Ramp Agent Card facilitator**: open-source shim that translates HTTP 402 challenges into one-shot Ramp Agent Card issuance for fiat-only merchants. Differentiates from on-chain-only x402 facilitators.
2. **AP2-mandated Ramp spend agent**: a Solana-side smart-account that holds spending mandates (cryptographically signed by the company's on-chain treasury controller) and gates Ramp Agent Card issuance via those mandates. Use Solana for the audit trail, Ramp for the actuator. This sits cleanly in the AI x crypto problem-space the user is hunting.

Both leverage Ramp's clearest 2026 product bet (Agent Cards) and slot into the x402/AP2/MPP convergence that's emerging as the agentic-payments protocol layer — without requiring Ramp itself to ship anything new on-chain.

---

## Sources

- [Ramp Developer Platform](https://ramp.com/developer-tools)
- [Ramp API docs](https://docs.ramp.com/)
- [Ramp API docs — Authorization / Scopes](https://docs.ramp.com/developer-api/v1/overview/scopes)
- [Ramp API docs — OAuth 2.0 guide](https://docs.ramp.com/developer-api/v1/guides/oauth)
- [Ramp API docs — Getting Started](https://docs.ramp.com/developer-api/v1/guides/getting-started)
- [Ramp API docs — Webhooks](https://docs.ramp.com/developer-api/v1/webhooks)
- [Ramp API docs — Cards API](https://docs.ramp.com/developer-api/v1/reference/rest/cards)
- [Ramp API docs — Bills API](https://docs.ramp.com/developer-api/v1/reference/rest/bills)
- [Ramp API docs — Ramp MCP](https://docs.ramp.com/developer-api/v1/ramp-mcp)
- [Accessing the Developer API — Ramp Support](https://support.ramp.com/hc/en-us/articles/46681939909907-Accessing-the-Developer-API)
- [Setting up SCIM and managing user provisioning — Ramp](https://support.ramp.com/hc/en-us/articles/39078698246547-Setting-up-SCIM-and-managing-user-provisioning)
- [AP Agents available in Ramp Bill Pay](https://support.ramp.com/hc/en-us/articles/47024360747027-AP-Agents-available-in-Ramp-Bill-Pay)
- [Ramp Slack Integration](https://ramp.com/integrations/slack)
- [Ramp NetSuite Integration](https://ramp.com/integrations/netsuite)
- [Ramp Pricing](https://ramp.com/pricing)
- [Ramp Technology Partner Program](https://ramp.com/technology-partnerships)
- [Ramp Intelligence](https://ramp.com/intelligence)
- [AP just became autonomous — Ramp](https://ramp.com/blog/ramp-ap-agents-announcement)
- [Virtual Cards for AI Agents — Ramp blog](https://ramp.com/blog/virtual-cards-for-ai-agents)
- [Ramp Launches Agent Cards (Stabledash)](https://stabledash.com/news/2026-03-11-ramp-launches-agent-cards-to-enable-secure-autonomous-ai-spending)
- [Microsoft customer story — Ramp + Azure AI](https://www.microsoft.com/en/customers/story/23693-ramp-azure-ai-services)
- [Stripe customer story — Ramp's global card program](https://stripe.com/customers/ramp)
- [Visa Intelligent Commerce for Agents — Visa Developer](https://developer.visa.com/use-cases/visa-intelligent-commerce-for-agents)
- [ramp-public/ramp_mcp on GitHub](https://github.com/ramp-public/ramp_mcp)
- [Ramp MCP server (ZenML LLMOps)](https://www.zenml.io/llmops-database/mcp-server-for-natural-language-business-data-analytics)
- [Ramp Postman public collection](https://www.postman.com/apifyi/ramp-api/overview)
- [Composio: Configure OAuth credentials for Ramp](https://composio.dev/auth/ramp)
- [Brex Developer Portal](https://developer.brex.com/)
- [Mercury API docs](https://docs.mercury.com/docs/welcome)
- [Stripe Issuing](https://stripe.com/issuing)
- [BILL API](https://www.bill.com/product/api)
- [Crossmint — Agentic Payments Protocols Compared (MPP, ACP, AP2, x402)](https://www.crossmint.com/learn/agentic-payments-protocols-compared)
- [Google Cloud — Announcing AP2 Agent Payments Protocol](https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol)
- [ChainCatcher — The payment moment of AI agents (mentions Ramp in MPP launch list)](https://www.chaincatcher.com/en/article/2262929)
- [Ramp Technology Partner Spotlight: Quanta](https://ramp.com/blog/technology-partner-spotlight-quanta)
- [apidog — How to use Ramp API](https://apidog.com/blog/ramp-api/)
