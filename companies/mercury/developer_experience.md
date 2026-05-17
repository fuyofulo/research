# Mercury (mercury.com) — Developer Experience Deep Dive

**Scope:** This document covers Mercury's banking API, webhooks, SDK ecosystem, sandbox, integration surface, official MCP server, agent-payments posture, and stablecoin stance. It compares Mercury to Brex / Ramp / Stripe Treasury / Modern Treasury / Plaid and identifies AI × crypto bridge opportunities.

**Subject identity:** "Mercury" = **mercury.com**, US fintech / startup business-banking platform founded by **Immad Akhund** (2017, SF). Banking services provided through partner banks (Choice Financial Group, Column N.A., Evolve Bank & Trust, Patriot Bank for credit) under FDIC insurance. Not to be confused with Mercury Layer (Bitcoin), Mercury Insurance, Mercury Systems, Mercury Marine, Mercuryo.io, or any "Mercury.ai" / "Mercury.global" property.

**Date stamp:** Research current to **2026-05-17**. Several Mercury surfaces (CLI, hosted MCP, OCC charter approval) launched within the last 12 months — flag time-sensitive items.

**Confidence legend:** ✅ verified across two+ independent sources or directly on mercury.com docs surface · 🟡 single source / inference · 🔴 contested / unverified / known unknown

---

## 1. The Mercury API

### 1.1 Base URL & environments

| Environment | Base URL | Confidence |
|---|---|---|
| Production | `https://api.mercury.com/api/v1/` | ✅ |
| Sandbox | `https://api-sandbox.mercury.com/api/v1/` | ✅ |
| Hosted MCP (read-only over OAuth) | `https://mcp.mercury.com/mcp` | ✅ |

Confirmed in Mercury's developer docs (referenced at [docs.mercury.com getting-started](https://docs.mercury.com/docs/getting-started) and [docs.mercury.com using-mercury-sandbox](https://docs.mercury.com/docs/using-mercury-sandbox)) and corroborated by third-party trackers [apitracker.io/a/mercury-co](https://apitracker.io/a/mercury-co) and [Mercury - API, Developer Portal & Open Banking, openbankingtracker.com](https://www.openbankingtracker.com/provider/mercury). The base path `/api/v1/` matches the prompt exactly. ✅

The sandbox is a true parallel surface — same routes, same payload shapes, separate token. Per [Using the Mercury Sandbox, docs.mercury.com](https://docs.mercury.com/docs/using-mercury-sandbox): "When you log into a sandbox environment, it skips the normal onboarding process and instead drops you into the Home page, which is pre-loaded with dummy data including organizations, accounts, transactions, and account balances." Switching to production is "a seamless process, requiring only a change in API keys" per [mercurydocumentation.com banking-sandbox](https://mercurydocumentation.com/banking-sandbox-developers-payment-automation). This is a noteworthy strength — many US business-banking API providers either lack a sandbox entirely or gate it behind sales contact.

### 1.2 Authentication

Mercury supports **three** authentication models. ✅

1. **Bearer token (recommended modern path)** — `Authorization: Bearer <api_key>` against a key minted from the dashboard's Settings -> API Tokens page. Confirmed by [Using the access token, docs.mercury.com](https://docs.mercury.com/reference/using-the-access-token).
2. **HTTP Basic auth (legacy / historical)** — API key as the username, empty password. Per [Getting Started, docs.mercury.com](https://docs.mercury.com/reference/getting-started-with-your-api): "The Mercury API utilizes basic authentication over HTTPS to authenticate actions, using your API key for the basic auth username and no value or empty string for the password." Mercury notes both forms are accepted; Basic is essentially a historical artifact from the v0 docs era.
3. **OAuth 2.0** (for third-party integrations) — Authorization Code Grant with PKCE. Per [Integrations with OAuth2, docs.mercury.com](https://docs.mercury.com/docs/integrations-with-oauth2): "Mercury's OAuth2 implementation supports the Authorization Code Grant Type and Authorization Code Flow with Proof Key for Code Exchange (PKCE)." Crucially: **OAuth access requires prior approval by Mercury's partnerships team.** You submit a form, Mercury reviews "security, use case fit, and regulatory considerations," and if approved you receive a `client_id` / `client_secret` plus sandbox credentials. ✅

A canonical bearer-auth call looks like:

```bash
curl -s https://api.mercury.com/api/v1/accounts \
  -H "Authorization: Bearer secret-token:mercury_production_..." \
  -H "Accept: application/json"
```

OAuth Dynamic Client Registration (RFC 7591) is supported specifically at the hosted MCP endpoint `https://mcp.mercury.com/mcp` — clients can self-register without manual Mercury intervention. This is a forward-looking choice and means consumer AI clients (Claude Desktop, ChatGPT, Cursor) can on-board without Mercury approval, **for read-only MCP use only.** ✅

### 1.3 Obtaining an API key

- **Self-serve, dashboard-gated, plan-limited.** Login -> Settings -> API Tokens -> "Generate a new token." Token is shown **once**; copy-on-create. Per [docs.mercury.com getting-started](https://docs.mercury.com/docs/getting-started) and corroborating walkthroughs at [thedigitalmerchant.com](https://thedigitalmerchant.com/accounting-software-that-integrates-with-mercury/). ✅
- **No plan gating on the API itself** — Mercury's business banking is "free to use, with no account minimums, overdraft fees, monthly fees, or account opening fees" per [mercury.com/pricing](https://mercury.com/pricing). However, several adjacent capabilities cost money: mass payments via API, Treasury management, non-USD payments, and the NetSuite integration ($35/month plan tier) per [puzzle.io Mercury accounting guide](https://puzzle.io/blog/mercury-bank-accounting-integration-guide) and [Integration FAQs, support.mercury.com](https://support.mercury.com/hc/en-us/articles/28777021143828-Integration-FAQs). 🟡
- **Token scoping** is genuinely fine-grained: Read-Only, Read-Write, and Custom (specific scope grants). Per [Security best practices, docs.mercury.com](https://docs.mercury.com/docs/security-best-practices): "Read Only tokens can fetch all available data on your Mercury account and should be created if you don't need to initiate transactions or manage recipients via the API." Tools called without the right scope return 403. ✅

### 1.4 Endpoint surface

| Endpoint | Method | Purpose | Verified |
|---|---|---|---|
| `/accounts` | GET | List all accounts (cursor pagination: `limit`, `order`, `start_after`, `end_before`) | ✅ [Get all accounts](https://docs.mercury.com/reference/getaccounts) |
| `/account/{id}` | GET | Single account detail | ✅ |
| `/account/{id}/transactions` | GET | Per-account transactions | ✅ [/account/:id/transactions](https://docs.mercury.com/reference/transactions-1) |
| `/account/{id}/cards` | GET | List cards on account | ✅ [Get cards for account](https://docs.mercury.com/reference/getaccountcards) |
| `/transactions` | GET | Cross-account paginated transactions with date/status/category filters | ✅ [Transactions API now available, changelog](https://docs.mercury.com/changelog/apiv1transactions-now-avaliable) |
| `/account/{id}/statements` | GET | Statement retrieval (Treasury accounts supported) | ✅ |
| `/recipients` | GET | List recipients (name, status, ACH / wire / check / intl-wire routing) | ✅ [/recipients](https://docs.mercury.com/reference/recipients-1) |
| `/recipients` | POST | Create a new recipient | ✅ |
| `/account/{id}/transactions` | POST | Send money (ACH, wire, check) to existing recipient - supports `idempotency-key`. Maps to "createTransaction." | ✅ [Send money to a recipient](https://docs.mercury.com/reference/createtransaction) |
| `/account/{id}/request-send-money` | POST | Queue an approval-required transfer | ✅ [request-send-money](https://docs.mercury.com/reference/accountidrequestsendmoney) |
| `/webhooks` | POST/GET/DELETE | Create / list / delete webhook endpoints | ✅ [Create a new webhook endpoint](https://docs.mercury.com/reference/createwebhook) |
| Invoicing API | various | Create / send / track invoices (one-shot only; recurring **not yet supported** in API) | ✅ [Invoicing API now available, changelog](https://docs.mercury.com/changelog/invoicing-api-now-available) |

**Read vs read-write:** Mercury exposes both. Reads (`GET /accounts`, `/transactions`, `/statements`, `/recipients`) require any token; writes (POST recipient, POST transaction) require a write-scoped token, and recipient-add flows can require admin approval depending on workspace policy. ✅

**Notable absence:** Mercury does **not** expose a "create account" / sub-account API. You cannot programmatically open new Mercury accounts for end-users — Mercury is not a BaaS (Banking-as-a-Service) provider in the Stripe Treasury / Column / Unit / Treasury Prime sense. It is a first-party API for your own Mercury workspace's funds. This is the single biggest architectural distinction vs Stripe Treasury / Modern Treasury / Column. 🟡

**Payment rails supported via API:** ACH, domestic wire, international wire, and check (sent on the customer's behalf). RTP / real-time payments are limited to accounts on the Column N.A. partner bank — per [Receiving real-time payments (RTP), support.mercury.com](https://support.mercury.com/hc/en-us/articles/39968809104148-Receiving-real-time-payments-RTP), incoming RTP is supported but the article does not document an API-level "send RTP" call. **FedNow is not documented as a supported send rail in the public API as of May 2026.** 🟡

### 1.5 Rate limits

🔴 **Not publicly documented.** Mercury's published docs do not enumerate request-per-minute caps, burst windows, or a stated 429 policy. Multiple third-party walkthroughs (e.g. apitracker.io, openbankingtracker.com) silently sidestep the question. Practitioner experience reports describe rough soft-limits around ~10 req/s for sustained workloads with backoff on bursts, but this is not authoritative. Treat rate limits as **a known unknown - verify by direct contact with api@mercury.com before high-volume integrations.** 🔴

### 1.6 Idempotency

✅ Mercury supports an `idempotency-key` on the `POST /account/{id}/transactions` endpoint (and consistent across mass-payment flows). The community CLI [ex3ndr/mercury-cli](https://github.com/ex3ndr/mercury-cli) exposes a `--idempotency-key` flag mirroring this, and [the createTransaction reference](https://docs.mercury.com/reference/createtransaction) calls it out under "Handling Idempotency (Preventing Double Payments)." Mercury's docs are explicit that re-using a key returns the original response without re-debiting funds — standard Stripe-style semantics.

### 1.7 OpenAPI spec / Postman

🟡 Mercury's documentation site (built on ReadMe.com per its `docs.mercury.com/reference` URL pattern) supports OpenAPI-driven rendering and "Try It" consoles. ReadMe generally exposes a Postman / Insomnia / curl export per endpoint. There is **no publicly hosted "spec.yaml" or "openapi.json" with a stable URL** that I could verify; the spec is consumable interactively via the docs UI but not (visibly) downloadable as a single artifact. By contrast, [Brex publishes an OpenAPI spec at developer.brex.com](https://developer.brex.com/) and Stripe ships an OpenAPI artifact on GitHub. **This is a meaningful gap for codegen-first teams.** 🟡

A community-maintained Python client [trix-solutions/mercury on GitHub](https://github.com/trix-solutions/mercury) and the PyPI [mercury-bank-api](https://pypi.org/project/mercury-bank-api/) package implicitly serve as informal type contracts.

---

## 2. Webhooks

### 2.1 Event types

Mercury's webhook system was promoted out of beta in 2024-2025 — per [Webhooks now available, changelog](https://docs.mercury.com/changelog/webhooks-now-avaliable) and [Webhooks, docs.mercury.com](https://docs.mercury.com/reference/webhooks). Supported event categories cover:

- Transaction lifecycle (posted, pending, returned, failed)
- Account changes
- Recipient changes
- Card lifecycle events (issued, frozen, modified)
- Invoicing events (newly added 2025-2026)

Mercury supports **configurable filters** at the subscription level — you can subscribe per event type and per field path, "to reduce noise" per [webhooks reference](https://docs.mercury.com/reference/webhooks). This is more granular than Brex (which historically streams a fixed event set) but less granular than Stripe (which has a registry of ~150+ event types). ✅

### 2.2 Signing scheme

**HMAC-SHA256 over the raw request body**, with the signature in the `x-mercury-signature` header. ✅ Verified across Mercury's reference page and the community npm package [@paperos/mercury-bank](https://www.npmjs.com/package/@paperos/mercury-bank) which performs raw-bytes hashing in middleware before JSON parse (a correct implementation pattern).

Canonical Node.js verifier:

```javascript
const crypto = require('crypto');

function verifyMercuryWebhook(rawBody, signatureHeader, secret) {
  const expected = crypto
    .createHmac('sha256', secret)
    .update(rawBody)            // raw bytes, NOT parsed JSON
    .digest('hex');
  return crypto.timingSafeEqual(
    Buffer.from(signatureHeader, 'hex'),
    Buffer.from(expected, 'hex')
  );
}
```

Python equivalent:

```python
import hmac, hashlib

def verify_mercury_webhook(raw_body: bytes, signature: str, secret: str) -> bool:
    expected = hmac.new(
        secret.encode(),
        raw_body,
        hashlib.sha256
    ).hexdigest()
    return hmac.compare_digest(signature, expected)
```

The signature is **hex-encoded** (not base64, unlike Stripe). The secret is the per-webhook-endpoint "Partner Secret" exposed at endpoint-creation time. ✅

### 2.3 Retries

Mercury **retries failed deliveries with exponential backoff**, and treats any non-2xx response as a delivery failure. ✅ The exact backoff curve and dead-letter / give-up threshold are not publicly documented (🟡) — most modern fintechs converge on a 24-72-hour total retry window across ~8-16 attempts; Mercury's policy is presumed similar. Subscribe-level filters reduce delivery volume and therefore the cost of retries.

---

## 3. SDKs & community packages

Mercury **does not ship official, first-party SDKs in any language**. ✅ The path is "consume the REST API directly" or use community wrappers. This is a deliberate choice vs Stripe / Plaid / Modern Treasury (which all maintain official SDKs in 5+ languages).

| Package | Lang | Source | Status |
|---|---|---|---|
| `@paperos/mercury-bank` | TS/Node | [npm](https://www.npmjs.com/package/@paperos/mercury-bank) | Community, focused on webhook validation middleware ✅ |
| `mercury-bank-api` | Python | [PyPI](https://pypi.org/project/mercury-bank-api/) | Community CLI + client ✅ |
| `trix-solutions/mercury` | Python | [GitHub](https://github.com/trix-solutions/mercury) | Community ✅ |
| `Oxiin/mercury-api` | Python | [GitHub](https://github.com/Oxiin/mercury-api) | Python CLI wrapper ✅ |
| `ex3ndr/mercury-cli` | Go/TS | [GitHub](https://github.com/ex3ndr/mercury-cli) | Pre-dates official CLI - independent build by Steve Korshakov ✅ |
| `MercuryTechnologies/mercury-cli` | Go | [GitHub](https://github.com/MercuryTechnologies/mercury-cli) - **official, May 2026** | ✅ Installed via `curl https://cli.mercury.com/install.sh` or `go install github.com/MercuryTechnologies/mercury-cli/cmd/mercury@latest` |

**No official Go, Java, Ruby, C#, Swift, or Kotlin SDK exists.** No Go SDK as a library — only the official CLI binary. 🟡

The **Mercury CLI** ([cli.mercury.com](https://cli.mercury.com/install.sh)) is the headline 2026 developer launch and matters for AI-agent use cases because LLM coding agents (Claude Code, Cursor agent mode) can shell out to it. Rajat Suri (founder, Lyft / Lima) [posted on X](https://x.com/rajatsuri/status/2049551073388740841) about "vibe coding" with the Mercury CLI in October 2025 — illustrating exactly the agent-friendly workflow Mercury VP Product Ryan Wiggins discussed at GA launch. ✅

---

## 4. Sandbox

Mercury operates a **fully functional, pre-populated sandbox** at `https://demo.mercury.com/dashboard` (UI) and `https://api-sandbox.mercury.com/api/v1/` (API). ✅

Key properties:
- Pre-seeded organizations, accounts, transactions, balances
- Token created independently inside the sandbox UI (Settings -> API Tokens)
- Visual confirmation: API actions (create recipient, send transaction) appear in the sandbox UI
- No real money flows; identical schemas to production
- Promotion to production = swap the bearer token; **no code changes** required
- Per [mercurydocumentation.com banking-sandbox](https://mercurydocumentation.com/banking-sandbox-developers-payment-automation), webhooks are triggerable in sandbox

**Sandbox is a strength relative to peers.** Brex requires sales contact for sandbox in many cases; Ramp's sandbox (per [Pipedream Ramp Sandbox integration](https://pipedream.com/apps/ramp-sandbox/integrations/modern-treasury)) is more developer-friendly. Mercury's no-friction self-serve sandbox is a key dev-experience win. ✅

---

## 5. Integrations & marketplace

### 5.1 Accounting

- **QuickBooks Online** — direct, free integration. Multi-daily sync, GL code assignment, AI categorization. ✅ [Integrating with QuickBooks Online, support.mercury.com](https://support.mercury.com/hc/en-us/articles/28775977522068-Integrating-with-QuickBooks-Online)
- **Xero** — direct, free. **One-way sync only** (Mercury -> Xero). ✅ [Integrating with Xero](https://support.mercury.com/hc/en-us/articles/28777055778580-Integrating-with-Xero)
- **NetSuite** — direct, but gated behind a paid plan tier at $35/month. ✅ [Integrating with NetSuite](https://support.mercury.com/hc/en-us/articles/28743190951572-Integrating-with-NetSuite)
- All accounting integrations are **direct** (not Plaid-mediated). Mercury's AI categorization learns from prior categorizations. 🟡

### 5.2 Payroll / HR

Per [HR & payroll system (HRIS) integration, support.mercury.com](https://support.mercury.com/hc/en-us/articles/34715964836116-HR-payroll-system-HRIS-integration):

- **Gusto** ✅
- **Deel** ✅
- **Justworks** ✅
- **Paycor** ✅
- **QuickBooks Online Payroll** ✅
- **Square Payroll** ✅
- **Workday** ✅
- **Rippling - explicitly NOT integrated.** Per the support page: "Rippling does not provide open API access and imposes prohibitive ongoing costs, preventing Mercury from offering an integration." ✅ — this is a notable public callout.

### 5.3 Plaid

Mercury appears on [Plaid's institution list](https://plaid.com/institutions/mercury/) with support for **Assets, Auth, Balance, and Transactions** Plaid products. ✅ This means third-party apps (QuickBooks, lending platforms, accounting tools) can fetch Mercury account data via Plaid without Mercury OAuth approval. Mercury also uses Plaid in the reverse direction (Mercury account -> external US bank link).

### 5.4 Stripe (Mercury Invoicing's card-payments rail)

In 2024, Mercury selected **Stripe as the payment partner for Mercury Invoicing** — when an invoice is paid by card, funds route through the customer's Stripe account and into their Mercury bank account. ✅ [stripe.com customers/mercury](https://stripe.com/customers/mercury). This is a customer-Stripe-account, not a Stripe-on-behalf-of-Mercury, so the relationship is integration not embedded.

### 5.5 "Mercury Connect" marketplace?

🔴 **No "Mercury Connect" marketplace exists in the Stripe-App-Marketplace or Brex-Embedded sense.** Searches for "Mercury Connect" hit a CRM product (unrelated CRM tool of the same name), Mercur Connect (Medusajs marketplace tool), and Mercury Network (real-estate appraisal). What Mercury has instead:

- A [partnerships program at mercury.com/partnerships](https://mercury.com/partnerships) for accounting firms / VCs / lenders
- The OAuth integration path described in section 1.2
- A "Raise" software-stack catalog of recommended third-party tools (Gusto, Rippling, Deel) at [mercury.com/raise/software-stack](https://mercury.com/raise/software-stack/) — note: **Rippling appears in the curation despite no API integration; Mercury still recommends it.**

There is no public listing of OAuth-approved third-party apps. Mercury hasn't built an embedded-finance-style developer ecosystem comparable to Stripe Apps, Shopify App Store, or QuickBooks marketplace. **This is structural and intentional — Mercury is not pursuing a platform-of-platforms strategy.** 🟡

---

## 6. MCP Server (the AI × crypto-relevant part)

### 6.1 Mercury's official hosted MCP

✅ **Mercury is one of a small number of US banks/fintechs that has shipped a first-party, hosted MCP server.** Key facts:

- **Endpoint:** `https://mcp.mercury.com/mcp` ([What is Mercury MCP, docs.mercury.com](https://docs.mercury.com/docs/what-is-mercury-mcp))
- **Transport:** Streamable HTTP (the most current MCP spec, not stdio) ✅
- **Authentication:** OAuth 2.0 + RFC 7591 Dynamic Client Registration. No API key copy/paste; one-click install from supported clients. ✅
- **Scope:** **Read-only** at the official endpoint. Mercury explicitly says "limited to read-only actions" — the MCP cannot send payments or modify accounts. Per [What is Mercury MCP, docs.mercury.com](https://docs.mercury.com/docs/what-is-mercury-mcp). ✅
- **Tool surface:** **34 tools** registered, organized by resource family — Accounts, Transactions, Recipients, Send Money, Cards, Statements, Treasury, Invoicing, Webhooks ([Mercury MCP server - 34 tools, Speakeasy catalog](https://www.speakeasy.com/product/mcp-gateway/catalog/mercury), [Supported tools on Mercury's MCP](https://docs.mercury.com/docs/supported-tools-on-mercury-mcp)). Critically: **the MCP server registers all 34 but the OAuth scopes limit what actually executes** — write-flavored tools (e.g. send-money) return 403 with `isError: true` rather than completing. So you see them, but they are nerfed. ✅
- **Supported clients:** Claude Desktop, ChatGPT (Plus/Pro/Team/Enterprise via Connectors / Developer Mode), Cursor, Google AI Studio, Windsurf, any RFC-7591 MCP client. ✅
- **Connection guide:** [Connecting Mercury MCP, docs.mercury.com](https://docs.mercury.com/docs/connecting-mercury-mcp).

CEO **Immad Akhund**'s strategic framing, per [sources.news on Mercury's AI strategy](https://sources.news/p/mercury-ceo-give-ai-the-money): *"I don't think Claude is going to go build a bank ... if you try to fight the future, I think you're going to lose out on the opportunity."* And per [implicator.ai](https://www.implicator.ai/the-dashboard-is-losing-the-account-mercury-bank-is-testing-the-replacement/): "Mercury's strategy is not that an AI should run the bank account, but rather that the dashboard is becoming only one surface for it." This is a measured, security-first take — *not* "agent-pays-on-its-own."

### 6.2 Community MCPs

The community has filled the read-write gap. The most relevant repos:

| Repo | Maintainer | Notes |
|---|---|---|
| [dragonkhoi/mercury-mcp](https://github.com/dragonkhoi/mercury-mcp) | Khoi Le (Dragonkhoi) | Simple MCP server, MIT/permissive. Auto-installable for Claude Desktop via Smithery. Surface-area: accounts, transactions, recipients. ✅ |
| [jbdamask/mcp-mercury-banking](https://github.com/jbdamask/mcp-mercury-banking) | John Damask | Python MCP, **read-only**, tested with Claude Desktop. Authored before the official Mercury MCP existed. Detailed blog at [johndamask.substack.com](https://johndamask.substack.com/p/20250309-mcp-for-mercury-bank). ✅ |
| [klodr/mercury-invoicing-mcp](https://github.com/klodr/mercury-invoicing-mcp) | klodr | **The interesting one.** Full Invoicing API support — including recurring-invoice management — plus read-write banking, accounts receivable, webhooks, and "built-in safety guards." Listed at [Glama](https://glama.ai/mcp/servers/klodr/mercury-invoicing-mcp). ✅ |

**klodr/mercury-invoicing-mcp is the model for a meaningful AI × crypto bridge** because it (1) goes beyond the official MCP's read-only ceiling, (2) supports invoicing (the natural settlement primitive), and (3) bakes in safety guards (per-call approval prompts, spend caps). Anyone building an AI × crypto product on top of Mercury should study this repo's pattern.

### 6.3 Toolkits exposing Mercury

- [Mercury MCP - Composio Toolkit](https://docs.composio.dev/toolkits/mercury_mcp) — exposed as a Composio-managed connector
- [Mercury MCP Server - MintMCP](https://www.mintmcp.com/servers/mercury)
- [PulseMCP Mercury listing](https://www.pulsemcp.com/servers/mercury)
- [Pipedream Mercury app](https://mcp.pipedream.com/app/mercury) — for ETL / workflow chaining

Mercury is **listed in the [openbankingtracker.com Agentic Banking & MCP](https://www.openbankingtracker.com/agentic-banking-and-mcp) directory** as one of the named institutions with a live MCP — putting it ahead of every megabank and the vast majority of US fintechs as of May 2026.

---

## 7. Agent payments

### 7.1 Visa Intelligent Commerce / Mastercard Agent Pay

- **Mercury IO is a Mastercard credit card** ([Mercury IO Mastercard Review, fitsmallbusiness](https://fitsmallbusiness.com/mercury-io-mastercard-review/), [Qualifying for IO, support.mercury.com](https://support.mercury.com/hc/en-us/articles/28768794858772-Qualifying-for-IO)). Issued by Patriot Bank, N.A. under Mastercard license. ✅
- **No publicly disclosed Mercury participation** in Mastercard's Agent Pay or Visa Intelligent Commerce Connect programs. Mastercard's Agent Suite (announced [Q1 2026, mastercard.com](https://www.mastercard.com/us/en/news-and-trends/press/2026/january/mastercard-launches-agent-suite-to-ready-enterprises-for-a-new-e.html)) and Santander's Europe-first AI-agent payment ([March 2, 2026, mastercard.com](https://www.mastercard.com/global/en/news-and-trends/stories/2026/agentic-commerce-rules-of-the-road.html)) don't reference Mercury. Visa Intelligent Commerce Connect (April 2026 launch) likewise doesn't list Mercury as a participating issuer. 🔴
- Mercury's debit cards are also Mastercard-rail (via partner banks). So the **rail-side enablement for Agent Pay is technically present**, but Mercury hasn't surfaced a developer-visible "agent commerce" credential mode. 🟡

### 7.2 x402

- **x402 foundation members include Anthropic, Visa, Google, Circle, AWS, Vercel, Coinbase, Cloudflare.** Mercury is **not** a listed foundation member ([x402.org](https://www.x402.org/)). 🔴
- x402 fundamentally relies on **USDC on Base settlement** with onchain payment receipts. Because Mercury is fiat-only (see section 8), it is not natively compatible. A Mercury account cannot, as of May 2026, sign or pay an x402 invoice without an intermediary stablecoin layer. 🔴

### 7.3 LangChain / LlamaIndex / Anthropic SDK

- **No first-party LangChain or LlamaIndex tool** for Mercury at present (zero hits in either's official tools directory as of May 2026). 🟡
- **Anthropic Claude integration is the MCP itself** (Mercury MCP works natively in Claude Desktop, Claude Code, the Anthropic Agent SDK via remote MCP support). ✅
- Community LangChain wrappers around Mercury exist as user-built tools but are not part of the LangChain Hub canon. 🟡

### 7.4 Mercury's actual posture

Per [implicator.ai](https://www.implicator.ai/the-dashboard-is-losing-the-account-mercury-bank-is-testing-the-replacement/) (May 2026): *"Mercury's CLI and read-only MCP server show where agentic banking is starting: reports, transaction cleanup, and finance workflows outside the dashboard ... early users mostly build reports, clean transactions, and prepare finance work before payments enter the flow."* Translation: **Mercury is publicly conservative on agent-initiated payments.** The product team has chosen "AI explains your money" over "AI moves your money" as the v1 surface. ✅

---

## 8. Crypto / stablecoin

### 8.1 The historical position

Mercury has carried a long-running ambivalence. ✅

- Mercury markets a "web3" page ([mercury.com/web3](https://mercury.com/web3)) claiming "Mercury is the no-brainer banking product for every cryptocurrency startup" and "supports thousands of crypto and web3 startups, DAOs, and funds."
- **But** Mercury simultaneously says it cannot accept "crypto exchange businesses, crypto trading companies, crypto funds, and p2p activities" — and does not support Money Services Businesses or exchanges. Per [OffshoreCorpTalk thread on Mercury for crypto](https://www.offshorecorptalk.com/threads/purchasing-crypto-with-mercury.46806/). 🟡
- Mercury **does not hold or transmit crypto.** Account balances are fiat-only. You can wire fiat to Coinbase or Gemini (fee-free outbound wires to those exchanges, displayed business-name on the wire), and Mercury markets that workflow on the web3 page — but you cannot custody USDC, USDT, PYUSD, or any tokenized asset in a Mercury account. ✅

### 8.2 2024-2025 account closures

The "crypto-friendly" branding suffered a meaningful credibility hit in **July 2024**, when Mercury closed accounts of businesses in 13 African countries (Nigeria, Zimbabwe, Mali, others), Ukraine, Venezuela, Croatia, Philippines, and Pakistan. ✅ Reported by [TechCrunch](https://techcrunch.com/2024/07/23/mercury-bank-fintech-sanctions-ukraine-nigeria/), [Techpoint Africa](https://techpoint.africa/2024/07/23/mercury-bank-closes-african-accounrs/), [TechCabal](https://techcabal.com/2024/07/23/us-bank-mercury-to-close-accounts-of-nigerian-startups/). The cited rationale was compliance — FATF Greylist exposure — rather than blanket anti-crypto policy. But the practical effect was disproportionate impact on web3 startups, which skew toward those geographies.

### 8.3 2025-2026 crypto position

🔴 **No public evidence of a stablecoin policy reversal.** As of May 2026:

- Mercury still does not support USDC, PYUSD, USDT, or any tokenized fiat on-balance.
- No public integration with [Bridge.xyz](https://www.bridge.xyz/) (Stripe-acquired, $1.1B, Oct 2024), [BVNK](https://bvnk.com/) (Mastercard-acquiring, $1.8B, March 2026), or [MoonPay](https://www.moonpay.com/) (now offers fiat-to-stablecoin virtual accounts in NY via the Iron acquisition).
- No public integration with Circle's USDC issuance directly.
- Competitor [Slash.com](https://www.slash.com/lp/mercury-business) explicitly markets itself as the "Mercury alternative that holds USDC/USDT" — and Mercury has not responded with a product launch.

The asymmetry vs Brex / Ramp / Mercury's own MCP capabilities is telling: **Mercury has shipped agent-AI infrastructure ahead of stablecoin infrastructure**, which is the exact inverse of where the AI × crypto frontier is forming. This is the central AI × crypto thesis gap (section 11). 🟡

---

## 9. Documentation quality

**Docs URL:** [docs.mercury.com](https://docs.mercury.com/docs/welcome) (welcome), [docs.mercury.com/reference](https://docs.mercury.com/reference) (API reference), [docs.mercury.com/changelog](https://docs.mercury.com/changelog) (versioned changelog). Built on the ReadMe.com platform. ✅

**Strengths:**
- Clean separation of conceptual ("docs/") vs reference ("reference/") routes
- Interactive "Try It" console with prefilled curl examples on each endpoint
- Versioned changelog with dated launches (Webhooks -> Transactions API -> Invoicing API -> MCP)
- Dedicated MCP section that doubles as a how-to for AI-tool installation
- Code samples in multiple languages on most endpoints

**Weaknesses:**
- **No downloadable OpenAPI spec / Postman collection** with stable URL (🟡)
- **No public rate-limit documentation** (🔴)
- Sparse worked examples for end-to-end workflows (e.g. "ingest invoice -> reconcile -> pay via ACH" tutorial absent)
- Auth section spans two pages with overlapping advice on Basic vs Bearer — minor confusion for new readers
- No SDK quickstart because no official SDK exists
- OAuth third-party integration docs are thin (the page essentially says "fill out a form")

**Comparison:** Stripe's docs remain the industry benchmark; Modern Treasury has a famously high-bar interactive doc surface; Plaid's quickstart is best-in-class. Mercury's docs are **substantively better than Brex's** (Brex has historically had spotty public docs), **roughly on par with Ramp's**, and **clearly behind Stripe / Plaid / Modern Treasury**. 🟡

---

## 10. Peer comparison matrix

| Dimension | Mercury | Brex | Ramp | Stripe Treasury | Modern Treasury | Plaid |
|---|---|---|---|---|---|---|
| **Self-serve API key** | ✅ Dashboard, free | 🟡 Dashboard, account-required | ✅ Dashboard, free | ✅ Dashboard, free | 🟡 Sales-assisted | ✅ Dashboard, free |
| **OAuth 2.0 (3rd-party)** | ✅ Approval-required, PKCE | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Public OpenAPI spec** | 🔴 No downloadable spec | ✅ ([developer.brex.com](https://developer.brex.com/)) | ✅ | ✅ (on GitHub) | ✅ | ✅ |
| **Webhook HMAC signing** | ✅ HMAC-SHA256 (`x-mercury-signature`, hex) | ✅ | ✅ | ✅ (`Stripe-Signature`, t=...,v1=...) | ✅ | ✅ |
| **Sandbox** | ✅ Free, self-serve, pre-populated | 🟡 Limited / sales-gated | ✅ | ✅ (test mode) | ✅ | ✅ |
| **First-party SDKs** | 🔴 None | ✅ (TS, Python) | 🟡 (limited) | ✅ (TS, Py, Go, Java, Ruby, .NET, PHP) | ✅ (TS, Py) | ✅ (TS, Py, Java, Go, Ruby) |
| **Official hosted MCP** | ✅ `mcp.mercury.com/mcp` - 34 tools, read-only | 🔴 None public | 🟡 Ramp MCP server - partial | 🟡 No, Stripe Agent Toolkit in TS/Py SDK | 🔴 None | 🔴 None |
| **Agent SDK / toolkit** | 🟡 CLI + MCP only | 🔴 | 🟡 Some agent tooling | ✅ Stripe Agent Toolkit (LangChain, AI SDK, OpenAI) | 🔴 | 🔴 |
| **Stablecoin support** | 🔴 Fiat only | 🟡 (cross-border on roadmap) | 🟡 (limited stablecoin reimbursement pilots) | ✅ via Bridge (Stripe-owned) | 🟡 (corridors, USDC settlement on roadmap) | 🟡 (Plaid Transfer + stablecoin partnerships emerging) |
| **x402 integration** | 🔴 No | 🔴 | 🔴 | 🟡 (foundation member, no native x402 endpoint) | 🔴 | 🔴 |
| **Rate limits documented** | 🔴 Not public | 🟡 Mentioned, no concrete RPS | 🟡 | ✅ Stripe publishes 100 RPS soft / 25 write | ✅ | ✅ |
| **Idempotency keys** | ✅ | ✅ | ✅ | ✅ (industry-defining `Idempotency-Key` header) | ✅ | 🟡 (request_id) |
| **Sub-account / BaaS** | 🔴 No | 🟡 Embedded for select partners | 🟡 | ✅ (Treasury platform - Financial Accounts API) | ✅ (Virtual Accounts) | 🔴 |
| **Crypto MCP / DeFi bridge** | 🔴 No | 🔴 | 🔴 | 🟡 (Bridge + Agent Toolkit) | 🔴 | 🔴 |

**Verdict for Mercury:** Best-in-class on **sandbox** and **official MCP**, mid-pack on **webhooks** and **OAuth**, weak on **OpenAPI spec / SDK breadth / rate limits docs**, and **dead last on stablecoin / x402** among modern fintech APIs.

---

## 11. AI × crypto bridge opportunities

Mercury sits in an awkward "two halves of two trends" position. The AI half is genuinely ahead of the curve; the crypto half is **structurally behind** because Mercury is a US-fiat-only banking surface with no roadmap toward holding tokenized money. Where a third party could profitably build:

### 11.1 Mercury -> stablecoin bridge MCP

**Product shape:** Unofficial MCP server that wraps Mercury's read-only data + a stablecoin off-ramp (Bridge.xyz now Stripe, BVNK now Mastercard, or Circle direct) to enable "USDC payouts from Mercury balance via natural-language instruction."

**Why it works:** Mercury already permits fee-free outbound wires to Coinbase/Gemini ([mercury.com/web3](https://mercury.com/web3)). The cycle Mercury -> Coinbase USDC -> x402 payee is technically feasible today but requires 3+ surface hops. An MCP-orchestrated agent could compress this into one tool call. Klodr/mercury-invoicing-mcp's pattern (write tools + safety guards) is the template.

**Defensibility:** Mercury has publicly chosen the conservative path and CEO Immad Akhund has stated "I don't think Claude is going to go build a bank" — meaning Mercury is unlikely to ship a competing first-party write-MCP imminently.

### 11.2 Mercury -> x402 agent gateway

**Product shape:** A LangChain / Anthropic-SDK tool that exposes Mercury balance + spending power as collateral for an x402-paying agent, with a stablecoin lender (Aave / Maple / Morpho) bridging the timing.

**Why it works:** x402 needs USDC. Mercury holds USD. The gap is a real-time fiat->USDC swap with credit-line semantics. Companies like Bridge / Brale / BVNK have the rails. A wrapper that says "agent has $X spending power, x402 payments execute with same-day USD->USDC settle behind the scenes" creates Mercury-compatible agent payments without Mercury changing its product.

### 11.3 Mercury MCP -> on-chain treasury analytics

**Product shape:** MCP server that joins Mercury's read-only transaction stream with Coinbase / Gemini / wallet on-chain data to produce unified treasury views ("how much of my burn went to crypto exchanges this quarter," "what's my effective stablecoin exposure," "categorize my onchain receipts").

**Why it works:** Mercury's MCP exposes transactions; on-chain explorers expose another half. Most AI × crypto startups want this view, and **no one ships it as a single MCP today.** Bonus: this is fully read-only, so no security objections.

### 11.4 Recurring-invoicing MCP for crypto-native B2B

klodr/mercury-invoicing-mcp already proves recurring-invoice tooling sells. Combine with USDC settlement (rails: Bridge, BVNK, Iron/MoonPay) and you get **invoice-to-USDC factoring for Mercury customers without Mercury needing to do anything.** This is a real product right now.

### 11.5 Compliance / KYB shield for closed accounts

Mercury's 2024 account-closure wave hurt thousands of web3 startups in FATF-greylisted countries. A neutral "Mercury-account-survival-as-a-service" — automated KYB hygiene, address-of-record management, geographic diversification — is a niche but real product, with Mercury's MCP as the data surface and Slash / Brex / Rho as fallback rails.

---

## 12. Known unknowns

1. **Exact API rate limits** — not publicly documented; treat as inquiry-required before high-volume production usage. 🔴
2. **Mercury OpenAPI spec stable URL** — interactive only on docs.mercury.com; no public spec.yaml. 🔴
3. **Webhook retry curve** — confirmed exponential backoff, but exact attempts / total window not documented. 🟡
4. **OAuth approval timelines and bar** — "varies by complexity" per docs; no public median or rejection criteria. 🟡
5. **Mercury MCP write-tool roadmap** — official position is read-only; whether and when write-tools get gated GA is uncertain. 🟡
6. **OCC bank charter timing** — preliminary conditional approval in May 2026 per [Banking Dive](https://www.bankingdive.com/news/fintech-mercury-apply-occ-national-bank-charter-fdic-fed-jon-auxier-sofi/808411/); full charter unresolved. 🟡
7. **FedNow send support** — RTP receive confirmed (Column N.A. accounts only); FedNow / RTP outbound via API not documented. 🟡
8. **Mercury IO + Mastercard Agent Pay** — IO is a Mastercard credential, but no public participation in Agent Pay disclosed. 🔴
9. **Any private Mercury-Bridge / Mercury-Circle / Mercury-BVNK conversation** — not visible from public sources. 🔴
10. **Stripe Treasury exact webhook signing format change in 2025-2026** and other peers' delta movement — used best-effort May 2026 sources, but a single doc change could shift the comparison matrix in section 10. 🟡

---

## Sources

- [Mercury - Automate Finance Tasks with API Access, mercury.com/api](https://mercury.com/api)
- [Welcome to Mercury's API docs, docs.mercury.com/docs/welcome](https://docs.mercury.com/docs/welcome)
- [Getting Started, docs.mercury.com/docs/getting-started](https://docs.mercury.com/docs/getting-started)
- [Getting Started with your API, docs.mercury.com/reference/getting-started-with-your-api](https://docs.mercury.com/reference/getting-started-with-your-api)
- [Using the access token, docs.mercury.com/reference/using-the-access-token](https://docs.mercury.com/reference/using-the-access-token)
- [Integrations with OAuth2, docs.mercury.com/docs/integrations-with-oauth2](https://docs.mercury.com/docs/integrations-with-oauth2)
- [Security best practices, docs.mercury.com/docs/security-best-practices](https://docs.mercury.com/docs/security-best-practices)
- [What is Mercury MCP?, docs.mercury.com/docs/what-is-mercury-mcp](https://docs.mercury.com/docs/what-is-mercury-mcp)
- [Connecting Mercury MCP, docs.mercury.com/docs/connecting-mercury-mcp](https://docs.mercury.com/docs/connecting-mercury-mcp)
- [Supported tools on Mercury's MCP, docs.mercury.com/docs/supported-tools-on-mercury-mcp](https://docs.mercury.com/docs/supported-tools-on-mercury-mcp)
- [Using the Mercury Sandbox, docs.mercury.com/docs/using-mercury-sandbox](https://docs.mercury.com/docs/using-mercury-sandbox)
- [Webhooks Reference, docs.mercury.com/reference/webhooks](https://docs.mercury.com/reference/webhooks)
- [Create a new webhook endpoint, docs.mercury.com/reference/createwebhook](https://docs.mercury.com/reference/createwebhook)
- [Webhooks now available (changelog), docs.mercury.com/changelog/webhooks-now-avaliable](https://docs.mercury.com/changelog/webhooks-now-avaliable)
- [Invoicing API now available (changelog), docs.mercury.com/changelog/invoicing-api-now-available](https://docs.mercury.com/changelog/invoicing-api-now-available)
- [Transactions API now available (changelog), docs.mercury.com/changelog/apiv1transactions-now-avaliable](https://docs.mercury.com/changelog/apiv1transactions-now-avaliable)
- [Get all accounts, docs.mercury.com/reference/getaccounts](https://docs.mercury.com/reference/getaccounts)
- [Account transactions, docs.mercury.com/reference/transactions-1](https://docs.mercury.com/reference/transactions-1)
- [Get cards for account, docs.mercury.com/reference/getaccountcards](https://docs.mercury.com/reference/getaccountcards)
- [Send money to a recipient (createTransaction), docs.mercury.com/reference/createtransaction](https://docs.mercury.com/reference/createtransaction)
- [Request send money, docs.mercury.com/reference/accountidrequestsendmoney](https://docs.mercury.com/reference/accountidrequestsendmoney)
- [Recipients, docs.mercury.com/reference/recipients-1](https://docs.mercury.com/reference/recipients-1)
- [Mercury Treasury, mercury.com/treasury](https://mercury.com/treasury)
- [Mercury IO Credit, mercury.com/credit](https://mercury.com/credit)
- [Mercury Web3 page, mercury.com/web3](https://mercury.com/web3)
- [Mercury Invoicing, mercury.com/invoicing](https://mercury.com/invoicing)
- [Mercury Pricing, mercury.com/pricing](https://mercury.com/pricing)
- [Mercury Partnerships, mercury.com/partnerships](https://mercury.com/partnerships)
- [Mercury Raise Software Stack, mercury.com/raise/software-stack](https://mercury.com/raise/software-stack/)
- [Qualifying for IO, support.mercury.com](https://support.mercury.com/hc/en-us/articles/28768794858772-Qualifying-for-IO)
- [Integrating with QuickBooks Online, support.mercury.com](https://support.mercury.com/hc/en-us/articles/28775977522068-Integrating-with-QuickBooks-Online)
- [Integrating with Xero, support.mercury.com](https://support.mercury.com/hc/en-us/articles/28777055778580-Integrating-with-Xero)
- [Integrating with NetSuite, support.mercury.com](https://support.mercury.com/hc/en-us/articles/28743190951572-Integrating-with-NetSuite)
- [HR & payroll system integration, support.mercury.com](https://support.mercury.com/hc/en-us/articles/34715964836116-HR-payroll-system-HRIS-integration)
- [Receiving real-time payments (RTP), support.mercury.com](https://support.mercury.com/hc/en-us/articles/39968809104148-Receiving-real-time-payments-RTP)
- [Mercury API & Data Solutions, plaid.com/institutions/mercury](https://plaid.com/institutions/mercury/)
- [Mercury Streamlines Collections with Stripe-Powered Invoicing, stripe.com/customers/mercury](https://stripe.com/customers/mercury)
- [Mercury - APIs, PSD2, Open Banking, openbankingtracker.com/provider/mercury](https://www.openbankingtracker.com/provider/mercury)
- [Agentic Banking & MCP, openbankingtracker.com](https://www.openbankingtracker.com/agentic-banking-and-mcp)
- [Mercury API tracker, apitracker.io/a/mercury-co](https://apitracker.io/a/mercury-co)
- [Mercury MCP - 34 tools (Speakeasy catalog), speakeasy.com/product/mcp-gateway/catalog/mercury](https://www.speakeasy.com/product/mcp-gateway/catalog/mercury)
- [Mercury MCP Server, mintmcp.com/servers/mercury](https://www.mintmcp.com/servers/mercury)
- [Mercury (Pipedream), mcp.pipedream.com/app/mercury](https://mcp.pipedream.com/app/mercury)
- [Mercury MCP - Composio Toolkit, docs.composio.dev/toolkits/mercury_mcp](https://docs.composio.dev/toolkits/mercury_mcp)
- [Mercury Tests Banking CLI as Agents Enter Finance, implicator.ai](https://www.implicator.ai/the-dashboard-is-losing-the-account-mercury-bank-is-testing-the-replacement/)
- [Why Mercury's CEO isn't afraid of giving his product to AI, sources.news](https://sources.news/p/mercury-ceo-give-ai-the-money)
- [Inside Mercury's $650M Revenue Machine (Lex podcast)](https://lex.substack.com/p/podcast-inside-mercurys-650m-revenue)
- [Fintech Mercury applies for OCC bank charter, bankingdive.com](https://www.bankingdive.com/news/fintech-mercury-apply-occ-national-bank-charter-fdic-fed-jon-auxier-sofi/808411/)
- [Mercury submits US national bank charter application, fintechfutures.com](https://www.fintechfutures.com/fintech/mercury-applies-for-us-national-bank-charter)
- [Mercury LinkedIn - Mercury CLI launch](https://www.linkedin.com/posts/mercuryhq_our-developer-suite-just-got-a-new-addition-activity-7454924870217519105-NFmW)
- [Rajat Suri on X - Mercury CLI vibe coding](https://x.com/rajatsuri/status/2049551073388740841)
- [Mercury closes accounts in 13 African countries, TechCrunch (2024)](https://techcrunch.com/2024/07/23/mercury-bank-fintech-sanctions-ukraine-nigeria/)
- [Mercury Bank closes African accounts, techpoint.africa](https://techpoint.africa/2024/07/23/mercury-bank-closes-african-accounrs/)
- [I Don't Understand Mercury, fintechtakes.com (Alex Johnson)](https://fintechtakes.com/articles/2024-07-22/i-dont-understand-mercury/)
- [Slash vs Mercury (Mercury alternatives), slash.com](https://www.slash.com/blog/mercury-bank-alternatives)
- [Purchasing Crypto with Mercury, offshorecorptalk.com](https://www.offshorecorptalk.com/threads/purchasing-crypto-with-mercury.46806/)
- [Best Crypto-Friendly Business Banks 2026, fitsmallbusiness.com](https://fitsmallbusiness.com/best-crypto-friendly-business-banks/)
- [Mercury IO Mastercard Review, fitsmallbusiness.com](https://fitsmallbusiness.com/mercury-io-mastercard-review/)
- [Mercury Corporate Credit Card Review 2026, startupsavant.com](https://startupsavant.com/service-reviews/mercury-io-mastercard)
- [Mercury Business Account 2026 Review, NerdWallet](https://www.nerdwallet.com/business/banking/reviews/mercury-banking)
- [Bridge - Stablecoin Infrastructure, bridge.xyz](https://www.bridge.xyz/)
- [Visa Intelligent Commerce Connect, banklesstimes.com](https://www.banklesstimes.com/articles/2026/04/09/visa-unveils-intelligent-commerce-connect-to-power-ai-agent-payments/)
- [Mastercard Agent Pay launch, mastercard.com](https://www.mastercard.com/us/en/news-and-trends/press/2026/january/mastercard-launches-agent-suite-to-ready-enterprises-for-a-new-e.html)
- [Mastercard Agent Pay Goes Live in Europe (Santander), ai2.work](https://ai2.work/blog/mastercard-agent-pay-goes-live-first-ai-payment-in-europe-2026)
- [x402.org](https://www.x402.org/)
- [Mercury Bank Accounting Integration Guide, puzzle.io](https://puzzle.io/blog/mercury-bank-accounting-integration-guide)
- [@paperos/mercury-bank, npm](https://www.npmjs.com/package/@paperos/mercury-bank)
- [mercury-bank-api, PyPI](https://pypi.org/project/mercury-bank-api/)
- [dragonkhoi/mercury-mcp, GitHub](https://github.com/dragonkhoi/mercury-mcp)
- [jbdamask/mcp-mercury-banking, GitHub](https://github.com/jbdamask/mcp-mercury-banking)
- [klodr/mercury-invoicing-mcp, GitHub](https://github.com/klodr/mercury-invoicing-mcp)
- [trix-solutions/mercury, GitHub](https://github.com/trix-solutions/mercury)
- [Oxiin/mercury-api, GitHub](https://github.com/Oxiin/mercury-api)
- [ex3ndr/mercury-cli, GitHub](https://github.com/ex3ndr/mercury-cli)
- [MercuryTechnologies/mercury-cli, GitHub](https://github.com/MercuryTechnologies/mercury-cli)
- [klodr mercury-invoicing-mcp on Glama](https://glama.ai/mcp/servers/klodr/mercury-invoicing-mcp)
- [johndamask Substack - MCP for Mercury Bank](https://johndamask.substack.com/p/20250309-mcp-for-mercury-bank)
- [PulseMCP Mercury listing](https://www.pulsemcp.com/servers/mercury)
- [Brex Developer Portal, developer.brex.com](https://developer.brex.com/)
- [Stripe Treasury, docs.stripe.com/treasury](https://docs.stripe.com/treasury)
- [Modern Treasury Getting Started, docs.moderntreasury.com](https://docs.moderntreasury.com/platform/reference/getting-started)
- [Ramp vs Brex 2026, getkleercard.com](https://www.getkleercard.com/blogs/ramp-vs-brex)
- [Top Mercury Alternatives, ramp.com/blog/top-mercury-alternatives](https://ramp.com/blog/top-mercury-alternatives)
- [Top Brex Alternatives, ramp.com/blog/top-brex-alternatives](https://ramp.com/blog/top-brex-alternatives)
- [BVNK Stablecoin Payments Guide, docs.bvnk.com](https://docs.bvnk.com/bvnk/use-cases/stablecoin-payments-for-platforms/prepare-for-integration/)
