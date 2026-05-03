# Bridge.xyz: Developer Experience, Integration Reality, and Pricing Economics

*Research date: 3 May 2026 | Acquired by Stripe Feb 4, 2025 ($1.1B). Operating as "Bridge by Stripe."*

> **Methodology note:** Direct WebFetch was denied; data below comes from Google search snippets that surface chunks of `apidocs.bridge.xyz` and blog pages, plus third-party reporting. Bridge marketing flagged 🔴; verifiable structural claims (endpoint shapes, status enums, etc. that appeared verbatim in multiple results) ✅; reasoned inferences 🟡.

---

## 1. The actual onboarding experience

### Self-serve signup vs sales-led: hybrid

**✅ Verified:** A developer can go to `dashboard.bridge.xyz/login`, "create your free developer account" and land in a dashboard immediately. So step one is genuinely self-serve.

**✅ Verified:** Production access requires more — per Bridge's own docs surface, "developers will have to sign a contract and pass KYB before getting access to a dashboard" (specifically a *production* dashboard with real funds; sandbox is gated behind less). The marketing site funnels real volume conversations through `sales@bridge.xyz`.

**🟡 Inferred:** The pattern is essentially "PLG funnel for sandbox + sales call for any meaningful production use." This is consistent with every customer story (Meow, Cenoa, Airtm, Slash, Dakota) reading like a managed integration rather than a swipe-card-and-go.

### KYB process

**✅ Verified findings (from `apidocs.bridge.xyz/docs/business-ownership-documents` and `customers/kyclinks` snippets):**

- **Timeline:** "KYB reviews typically happen same business day, up to next business day." This is genuinely fast for the regulated category.
- **Status state machine:** `not_started` → `under_review` → `approved` | `incomplete` | `awaiting_questionnaire` | `awaiting_ubo` | `paused` | `offboarded` | `rejected`. A customer can jump straight from `not_started` to `rejected` with no review (most common cause: "tax identification number is entered incorrectly" — without a valid TIN, Bridge cannot verify any other information).
- **Documents required:** Business ownership documents confirming "all individual ultimate beneficial owners who own 25% or more of the underlying entity." Without an attestation from a control person, ownership structure must be confirmed by a provided document.
- **Dashboard support:** The dashboard shows what KYB/KYC/UBO information is missing and lets the developer upload directly without restarting workflows.

### Sandbox access

**✅ Verified:** Sandbox API keys are generated from the developer dashboard (`apidocs.bridge.xyz/docs/developer-dashboard`).

**✅ Verified sandbox limitations** (these are documented and matter a lot for DX):
- **No payments-related webhooks fire in sandbox.**
- "Sandbox is subject to arbitrary rate limits; we may drop your requests anytime."
- No real money movement.
- **Plaid does not work in sandbox.**
- No testnet support.
- Virtual Accounts, Static Memos, Liquidation Addresses, and Transfers are created with **dummy data**.
- **Wallets and Stablecoin Issuance are only supported in Production** (so you literally cannot test the wallet product without going live).

This is the single biggest hidden DX gotcha — you can mock-build a Transfer flow in sandbox, but you cannot validate the webhook contract you'll receive in production, and you cannot exercise wallets at all until you're approved.

### Production approval

**🟡 Inferred:** No public criteria. Customer stories suggest approval criteria heavily weight:
- Use case clarity (treasury, payouts, cards, issuance — clearly defined wins)
- Ownership transparency (sub-25% UBOs)
- Geography (US, EU, LATAM markets get fastest paths; high-risk geos get rejected)

### Minimum volume requirements

**✅ Verified:** Marketing line for Mexico says "no minimum volume requirements" 🔴 (this is a market-entry pitch, not a generalized policy).

**🟡 Inferred:** For Open Issuance and meaningful enterprise pricing, Bridge clearly operates on commitment-based tiers (the Routefusion/BVNK comparison piece confirms "BVNK and Bridge require sales engagement for pricing"). No specific public volume floor was found.

---

## 2. Real pricing — what we actually know

Bridge has **no public rate card**. Here's what is verifiable from primary sources, leaks, and competitor comparisons.

### From Bridge's own Fee Disclosure Statement (`bridge.xyz/legal/fee-disclosure-statement/overview`)

**✅ Verified:** Three official fee categories disclosed:

1. **Service Charge** — "If partners through which you obtain Bridge Services opt to levy a fee… the decision to impose such a charge, including its amount, is determined solely by the Partner." (Translation: Bridge's customers set their own customer-facing markup.)
2. **Gas Fees** — passed through at cost, variable.
3. **Currency Conversion** — **"a currency spread on top of the actual exchange rate up to 1% of the transaction's fiat value, which may vary based on transaction."**

That **"up to 1%" FX spread cap** is the single most concrete pricing data point Bridge has ever published. It's a ceiling, not a floor — large customers presumably negotiate well below it.

### From the Developer Fees doc (`apidocs.bridge.xyz/platform/orchestration/fees-and-mins/devfees`)

**✅ Verified:**
- Developers set their own fees per request via `developer_fee_percent` parameter (e.g., `"1.0"` = 1%).
- Fee is always in source currency.
- Maximum 5 digits of precision (`0.00119` ok, `0.0000001` not).
- **Minimums are enforced *after* developer fees are deducted.** (E.g., $1 deposit with 1% dev fee = $0.99 net = below threshold = funds will not be credited or returned.)
- Default fiat minimum: 1 unit ($1). Default stablecoin minimum: 1 unit. Non-stablecoins: 2 units.

This is the "developer fee on top of Bridge's fee" model — Bridge takes its cut, developer takes their cut on top.

### Stablecoin Financial Accounts pricing (Stripe layer)

**✅ Verified:** Stripe charges **flat 1.5% per stablecoin payment** for USDC payments via Bridge infrastructure across 100+ countries.

**🔴 Marketing claim / criticism:** Yahoo Finance and others noted: "Stripe Charges 1.5% for Stablecoin Transfers That Cost $0.0002 On-Chain." Industry critics call this "predatory"; defenders say it's "already 50% cheaper than current alternatives."

### USDB Open Issuance reserve yield split

**✅ Verified language:** "Bridge passes through a portion of the Treasury bill yield to USDB holders." For Open Issuance (custom stablecoins): "Bridge shares the **majority of rewards** generated from your reserves directly with you" / "any returns on funds **net of issuance fees**" go to the issuer.

**🟡 Inferred:** No specific percentage published. Industry context: T-bills earn ~3-4%; "majority" suggests 60-80% to issuer, 20-40% to Bridge as the issuance/operations fee. **Not verified** — sales conversation territory.

### Card interchange split

**✅ Verified structure:** Card programs are issued by **Lead Bank** and managed by **Bridge Ventures, LLC**. Developers earn interchange on every swipe; FX conversion fees apply when users spend in non-stablecoin currencies.

**🔴 Not disclosed:** Specific bps split between issuer (Lead Bank), Bridge, and developer. Industry norms suggest Visa/MC keep ~0.10%, Lead Bank keeps ~0.15-0.30%, Bridge keeps ~0.30-0.50%, and the developer gets the residual ~1.0-1.5% on consumer credit-style interchange — but **none of this is publicly verified for Bridge specifically.**

### FX spreads by corridor

**🔴 Bridge corridor pricing is not public.** The only corridor-specific anchor data is from competitor BVNK's published rates (per Routefusion's comparison): **5–25 bps on major pairs (EUR, GBP, MXN, BRL); 30–90 bps on exotic pairs.** Bridge "market-leading FX rates" marketing language implies parity or better.

For USD↔MXN specifically, Bridge partners with Bitso for liquidity; competitive on this corridor is plausibly 15-30 bps based on the corridor's depth, but **this is inference, not data.**

### Pricing competitive matrix (verified data only)

| Provider | Public pricing? | FX spread | Per-rail | Notes |
|---|---|---|---|---|
| **Bridge** | No rate card; 1% FX cap in legal | "up to 1%" disclosed ceiling | Sales conversation | 1.5% via Stripe SFA |
| **BVNK** | Partial (Routefusion comparison) | 5–25 bps majors / 30–90 bps exotics | Volume-tiered | Now Mastercard (Mar 2026, $1.8B) |
| **Brale** | ✅ Yes — fully public | Not applicable (issuance) | Starting **$10/mo** + gas pass-through; **0 bps** for instant payouts | Most transparent in space |
| **Routefusion** | Transparent: per-tx + spread + settlement fee | Per-corridor table | Per-rail published | 185+ countries |
| **Crossmint** | Public pricing | 150+ countries on/offramp | Per-tx | All-in-one issuer |

The key takeaway: **Bridge is one of the *least* price-transparent vendors in the category.** Brale, Crossmint, and Routefusion all publish more.

---

## 3. Real developer testimonials and integration timelines

The single best public engineering-blog data point I found:

**✅ Verified — Slash Engineering:** Slash (US neobank) wrote in `slash.com/engineering/blog/banking-grade-stablecoin-rails`:
> "Built an MVP for stablecoin rails in two weeks; within a month they had real and significant volume."

Slash later launched **USDSL**, their own stablecoin via Bridge's Open Issuance (Aug 2025). Slash now processes ~$1B annualized volume, hit $1.4B valuation.

**✅ Other documented timelines:**
- **Cenoa** case study: "Bridge's modular APIs and fast deployment enabled Cenoa to go from integration to live rollout **in under a month**." Now live in 40+ markets across EMEA, LATAM, SEA.
- **Airtm:** Launched payouts via Bridge on Stellar in March 2024; processed $1.2B in stablecoin transaction volume in 2024; "nearly half of Airtm's total enterprise payout volume" flows through Bridge. "Average cost savings of 20% compared to alternatives like PayPal or Wise."
- **Meow:** Used Orchestration API to enable USDC send/receive from existing cash balances; replaced "weeks or months" of crypto-exchange onboarding pain.

**🟡 Inferred industry consensus** (from Routefusion comparison and ecosystem write-ups): **2–4 weeks** is the typical Bridge integration timeline for standard payouts/payins.

### Negative signal / complaints

**🔴 Not found:** I searched HN, Reddit (r/fintech, r/web3, r/cryptocurrency), and dev.to — no high-signal public complaints about Bridge DX surfaced in search results. The closest negative critique is the 1.5% Stripe stablecoin fee debate, which is a Stripe-pricing critique, not a Bridge-DX critique.

This is itself notable: either (a) Bridge's customers are NDA'd / under sales-led contracts that discourage public airing, or (b) DX is genuinely fine. Both are partly true.

### Compared to Stripe Payments DX

Bridge is **manifestly less mature** than Stripe Payments:
- No official SDKs in any language (verified — see §6)
- Sandbox can't test webhooks or wallets
- Pricing requires sales conversation
- KYB gating before production
- No public Postman collection from Bridge (only third-party)

But Bridge does adopt several Stripe-style patterns: HTTP Basic-style API key in `Api-Key` header, idempotency keys with 24h windows, webhook signature verification, JSON-everywhere REST.

---

## 4. The actual API surface

I could not pull `llms-full.txt` directly (WebFetch blocked), but search snippets surface the structural details below. ✅ items appeared verbatim in search results.

### Authentication ✅

- Header: `Api-Key: <your-key>` (HTTP-Basic style, no username/password).
- API base: `https://api.bridge.xyz/v0`
- Production keys and sandbox keys generated separately from dashboard.
- API keys now support **granular resource-level permissions** (Apr 2026 changelog) — restrict to specific resources: customers, transfers, wallets, webhooks.

### Idempotency ✅

- All write requests support `Idempotency-Key` header.
- 24-hour idempotency window. After expiry, reusing the same key returns **422 Unprocessable Entity**.

### Endpoints (verified surface, partial)

| Resource | Verified endpoints |
|---|---|
| **Customers** | `POST /v0/customers`, `GET /v0/customers/{id}`, `GET /v0/customers/{id}/kyc_link` |
| **KYC Links** | `POST /v0/kyc_links`, `GET /v0/kyc_links/{id}` |
| **Wallets** | `POST /v0/customers/{id}/wallets`, `GET /v0/customers/{id}/wallets/{walletId}`, `GET /v0/wallets`, `GET /v0/wallets/total_balances` |
| **Transfers** | `POST /v0/transfers`, `PUT /v0/transfers/{id}` (update), list endpoints |
| **Virtual Accounts** | `POST /v0/customers/{id}/virtual_accounts`, `GET /v0/customers/{id}/virtual_accounts/{vaId}` |
| **Liquidation Addresses** | `POST /v0/customers/{id}/liquidation_addresses`, update endpoints, "drains" sub-resource |
| **External Accounts** | `POST /v0/external_accounts`, `GET /v0/developers/external_accounts/{id}/fee` |
| **Webhooks** | `POST /v0/webhooks` (creates disabled by default), `PUT /v0/webhooks/{id}`, `POST /webhooks/send` for testing, `GET /v0/webhooks/upcoming_events` |
| **Cards** | issuance/management endpoints (specific paths not surfaced in search snippets) |
| **Issuance** | custom stablecoin endpoints under `/platform/issuance/custom` |

### Webhook system ✅

- **Categories:** `customer`, `kyc_link`, `transfer`, `card_transaction` (and more).
- **Event payload fields:** `api_version`, `event_id`, `event_category`, `event_type`, `event_object`, `event_object_changes` (optional), `event_created_at`.
- **Endpoint requirements:** HTTPS with valid X.509 cert. Bridge issues a PEM public key per endpoint.
- **Signature header:** `t=<timestamp>,v0=<base64-encoded signature>` (Stripe-style).
- **Endpoint starts in disabled state** — must be explicitly enabled via PUT.
- **Cards webhooks include:** `card_transaction.created`, `card_transaction.updated.status_transitioned`.

### Sample Transfer call (verbatim from docs surface) ✅

```bash
curl --location --request POST 'https://api.bridge.xyz/v0/transfers' \
--header 'Api-Key: <API Key>' \
--header 'Idempotency-Key: <Unique Idempotency Key>' \
--data-raw '{
  "amount": "10.0",
  "on_behalf_of": "cust_alice",
  "developer_fee": "0.5",
  "source": {"payment_rail": "ach_push", "currency": "usd"},
  "destination": {
    "payment_rail": "ethereum",
    "currency": "usdc",
    "to_address": "0xdeadbeef"
  }
}'
```

### Rate limits

**🔴 Production rate limits not publicly documented.** Sandbox is "subject to arbitrary rate limits."

### Error codes

**🟡 Surfaced:** 422 for idempotency reuse after expiry. Standard REST conventions implied. **No published error code table found.**

---

## 5. Bridge dashboard / product surface

**✅ Verified from "We've made major enhancements to the Bridge Dashboard" blog (`bridge.xyz/blog/everything-you-can-now-do-in-the-bridge-dashboard`):**

The dashboard at `dashboard.bridge.xyz` is genuinely featureful:

- **Cards tab:** activation funnels, transaction breakdown, decline reasons, customer card details, spend limit details, connected wallets, freeze cards, download monthly card statements.
- **Wallets tab:** view balances and transactions; search by wallet ID, customer ID, or customer email; manage internal treasury; move funds in/out of developer-owned wallets.
- **Customers tab:** manage accounts and payout details; "enable same-name payouts" allowing developer to choose what name appears on customer receipts.
- **Compliance:** see what KYB/KYC/UBO is missing, upload required docs directly.
- **Tasks on Homepage:** self-serve unmatched deposits — match, return, or update.
- **API Keys:** generate Production and Sandbox keys, with new granular resource-level permissions.

**🔴 Not found:** Public YouTube walkthroughs, screenshots in third-party reviews, or a public sandbox-vs-production dashboard comparison. The dashboard is gated by login.

---

## 6. SDKs and tooling

**✅ Verified:** **Bridge has no official SDK in any language.** Searches across npm and PyPI for `bridge-xyz`, `@bridge/`, `@bridge-xyz/`, `bridgexyz` returned zero official packages. The npm packages named "bridge" / "bridge-sdk" / "@nomad-xyz/sdk-bridge" are unrelated (Nomad cross-chain bridge protocol, not Bridge.xyz).

**✅ Verified community tooling:**

- **`lnflash/bridge-mcp`** (https://github.com/lnflash/bridge-mcp): A community MCP (Model Context Protocol) server wrapping Bridge.xyz APIs for AI assistants (Claude Desktop integration). Wraps customer management, wallet operations across Solana/Ethereum/Polygon/Base, virtual accounts, transfers, external account linking, webhooks, exchange rates. Listed in LobeHub's MCP registry. Single maintainer.
- **Postman public workspace:** `postman.com/material-pilot-3638775/public-workspace/collection/q022uvv/bridge-xyz-api` — third-party public collection (not an official Bridge collection).

**🔴 Not found:** Official OpenAPI/Swagger spec published. `apitracker.io` lists Bridge but doesn't link to a maintained spec. `apidocs.bridge.xyz/llms.txt` and `llms-full.txt` exist (the docs site uses Mintlify, which generates these for LLM consumption) — but I could not retrieve them with WebFetch denied.

---

## 7. Common gotchas (from real developers)

Pulled from docs surface and customer narratives:

1. **🔴 Sandbox does not fire payments-related webhooks.** You cannot test the most important developer integration concern — webhook contract — until production. (Documented limitation.)
2. **🔴 Wallets and Stablecoin Issuance are only available in Production.** No sandbox testing path.
3. **🔴 Plaid does not work in sandbox.** If your flow involves Plaid for ACH connection, you cannot test end-to-end.
4. **🔴 Memo-based blockchains (Stellar, Tron) require `blockchain_memo` to be included in deposits** — omitting it causes "significant delays" on offramps. Easy to miss.
5. **🔴 Liquidation addresses are unique per (source chain, source currency, destination)** — attempting to create a duplicate fails with API error.
6. **🔴 Prefunded Accounts deprecated as of Mar 24, 2026.** Bridge will continue support but all new development is steered toward Bridge Wallets. The "must fund and prime address before USDC can land" gotcha is now an artifact of the deprecated Prefunded model — newer wallet-based flows handle this differently.
7. **🔴 Transaction minimums apply *after* developer fees.** Not before. Will silently fail (no return) if net amount falls below floor.
8. **🔴 Idempotency-Key reuse after 24h returns 422 Unprocessable Entity.**
9. **🔴 Sandbox rate limits are arbitrary and undocumented** — your tests can be dropped without warning.
10. **🔴 KYB tax-ID errors cause hard rejection without review.** No retry path described in surfaced docs.

---

## 8. Integration patterns by use case

From `apidocs.bridge.xyz/get-started/guides/common-use-cases/*`:

### Cross-border payments
Source = ACH/SEPA/wire fiat → Bridge converts via stablecoin sandwich (USDC/USDT) → Destination = local rail (SPEI for MXN, Pix for BRL, FPS for GBP, NIBSS for NGN). Built on **Transfers API** with developer fee specified in source currency.

### Treasury management
Use **Virtual Accounts** + **USDB** to hold treasury in a yield-bearing stablecoin. Fiat deposits auto-convert to USDB; reserves earn T-bill yield (3-4%) which Bridge passes back majority share. Wallets API provides custody.

### Payroll
Source = developer's funded wallet → Transfers to many `on_behalf_of` customer destinations on local rails. Each contractor receives in their preferred local currency or stablecoin.

### Cards (B2C and B2B)
Issue branded Visa cards (Lead Bank issuer, Bridge Ventures manager). Cards spend directly from stablecoin balances (USDB or custom). Live in Africa, LATAM, US; **EU and APAC launching 2026**. Earn on interchange + FX conversion fees.

### Agentic payments
Documented as a use case but the surfaced material is mostly aspirational marketing. The pattern is: agents hold wallets via Wallets API, use Transfers for microtransactions on stablecoin rails. Tempo blockchain (Stripe's payments-purpose chain, "≥100k TPS, sub-1s finality") is positioned as the agentic payments substrate.

### Custom stablecoin issuance (Open Issuance)
POST against `/platform/issuance/custom` endpoints. Customize chains, reserve allocation, smart contracts, identity, branding. Bridge mints/burns and shares yield majority with issuer, net of issuance fees.

---

## 9. Volume tiers / customer segmentation

**🔴 No explicit public tier structure.** Implicit observed segmentation:

- **Free developer dashboard tier:** Anyone can sign up at `dashboard.bridge.xyz`. Sandbox API key. No real money.
- **Production / SMB:** Post-KYB, contract signed. Pricing per Fee Disclosure (≤1% FX, gas pass-through). Likely also some platform/per-tx fee not publicly listed.
- **Enterprise (Slash, Cenoa, Airtm, Meow, Dakota, Wirex tier):** Negotiated pricing, dedicated support, Open Issuance custom stablecoin, joint go-to-market.
- **Strategic (Coinbase, SpaceX, Scale AI, Stripe-internal):** Bespoke deals.

---

## 10. Real customer volume / spend data

**✅ Verified volume datapoints:**

- **Bridge platform total:** "Stablecoin volume more than quadrupled in 2025." Monthly processed volume grew from **~$1.2B in Q4 2025 to over $4.8B in Jan–Feb 2026** (per CoinDesk Feb 24, 2026). 30% MoM growth.
- **Stripe overall total:** $1.9T processed in 2025 (+34% YoY). Bridge handles "a large share of the $400B in global stablecoin payments."
- **Airtm:** $1.2B stablecoin volume in 2024; ~50% routed through Bridge.
- **Slash:** $1B annualized volume in stablecoin payments under a year after launch; $1.4B valuation.
- **Customer roster verified:** Coinbase, SpaceX (Starlink for emerging markets), Scale AI (contractor payouts), Meow, Cenoa (40+ markets), Dakota, Airtm, Wirex (US expansion), and Stripe's own Stablecoin Financial Accounts.

**🔴 Not found:** Per-customer monthly spend data; Stripe quarterly breakouts of Bridge revenue specifically (Stripe is private, no quarterly earnings breakouts).

---

## Bottom line — what to know if you're integrating Bridge today

**Strengths (verified):**
- Genuinely fast KYB (same/next business day)
- Mature multi-rail coverage (ACH, wire, SEPA, FPS, SPEI, Pix; chains include Ethereum, Solana, Polygon, Base, Tron, Stellar, Plasma, Tempo)
- Stripe-style API patterns (idempotency, signed webhooks, REST, JSON)
- Sub-month integration timelines for standard flows (Slash 2 weeks to MVP, Cenoa under 1 month to live)
- Functional dashboard for ops teams, not just developers
- Strong customer roster legitimizes the platform

**Weaknesses / risks (verified):**
- **Zero public pricing transparency** — only the legal disclosure mentions "≤1% FX." Brale, Crossmint, Routefusion all publish more.
- **No official SDKs** — only one community MCP server (lnflash/bridge-mcp)
- **Sandbox is a half-truth:** webhooks don't fire, wallets don't exist, Plaid doesn't work — most production-critical flows can't be exercised
- **Rate limits undocumented** in production; arbitrary in sandbox
- **No public error code reference** in surfaced docs
- **Production gated by KYB + contract** — not truly self-serve
- Prefunded Accounts deprecation (Mar 24, 2026) is a migration tax for older integrations

**Not yet verified / needs primary access:**
- Specific FX bps by corridor
- Card interchange split percentages
- Open Issuance reserve-yield split percentages
- Production rate limits
- Full webhook event taxonomy with payload schemas

If the priority is "get the actual numbers for FX corridors and Open Issuance splits," **a single sales call to `sales@bridge.xyz` will get you more than weeks of OSINT**. That is itself the most important DX finding: in 2026, Bridge still operates more like a regulated wholesale rail provider (think Western Union B2B desk) than a Stripe-style self-serve PaaS, despite the "Stripe of crypto" branding.

---

## Sources

- [Bridge — Welcome / Overview](https://apidocs.bridge.xyz/get-started/introduction/overview)
- [Bridge — Authentication](https://apidocs.bridge.xyz/api-reference/introduction/introduction)
- [Bridge — Idempotency](https://apidocs.bridge.xyz/api-reference/introduction/idempotence)
- [Bridge — Setting up sandbox](https://apidocs.bridge.xyz/get-started/introduction/quick-start/setting-up-sandbox)
- [Bridge — Setting up webhooks](https://apidocs.bridge.xyz/get-started/introduction/quick-start/setting-up-webhooks)
- [Bridge — Webhook signature verification](https://apidocs.bridge.xyz/platform/additional-information/webhooks/signature)
- [Bridge — Developer dashboard](https://apidocs.bridge.xyz/docs/developer-dashboard)
- [Bridge — Transaction Costs / Minimums](https://apidocs.bridge.xyz/docs/transaction-costs)
- [Bridge — Developer fees](https://apidocs.bridge.xyz/platform/orchestration/fees-and-mins/devfees)
- [Bridge — Pricing page](https://apidocs.bridge.xyz/docs/fees)
- [Bridge — Fee Disclosure Statement](https://www.bridge.xyz/legal/fee-disclosure-statement/overview)
- [Bridge — Business ownership documents](https://apidocs.bridge.xyz/docs/business-ownership-documents)
- [Bridge — KYC links for new customers](https://apidocs.bridge.xyz/platform/customers/customers/kyclinks)
- [Bridge — Transfers API](https://apidocs.bridge.xyz/platform/orchestration/transfers/transfer)
- [Bridge — Virtual accounts](https://apidocs.bridge.xyz/platform/orchestration/virtual_accounts/virtual-account)
- [Bridge — Liquidation address](https://apidocs.bridge.xyz/platform/orchestration/liquidation_address/liquidation_address)
- [Bridge — Cross-border payments use case](https://apidocs.bridge.xyz/get-started/guides/common-use-cases/cross-border-payments)
- [Bridge — Treasury management use case](https://apidocs.bridge.xyz/get-started/guides/common-use-cases/treasury-management)
- [Bridge — Payroll use case](https://apidocs.bridge.xyz/get-started/guides/common-use-cases/payroll)
- [Bridge — Custom Stablecoin (Open Issuance)](https://apidocs.bridge.xyz/platform/issuance/custom)
- [Bridge — Changelog](https://apidocs.bridge.xyz/changelog/changelog)
- [Bridge — Cards: Spend wallet balances](https://apidocs.bridge.xyz/get-started/guides/cards/spend)
- [Bridge — "Major enhancements to Bridge Dashboard" blog](https://www.bridge.xyz/blog/everything-you-can-now-do-in-the-bridge-dashboard)
- [Bridge — Meow Case Study](https://www.bridge.xyz/case-study/meow-case-study)
- [Bridge — Cenoa Case Study](https://www.bridge.xyz/case-study/cenoa-case-study)
- [Bridge — Airtm Case Study](https://www.bridge.xyz/case-study/airtm-case-study)
- [Bridge — Dakota Case Study](https://www.bridge.xyz/case-study/dakota-case-study)
- [Bridge — Introducing USDB](https://www.bridge.xyz/news/usdb)
- [Bridge — Stablecoin-enabled FX in Mexico](https://www.bridge.xyz/news/mxn-fx)
- [Stripe — Introducing Stablecoin Financial Accounts](https://stripe.com/blog/introducing-stablecoin-financial-accounts)
- [Stripe — Introducing Open Issuance from Bridge](https://stripe.com/blog/introducing-open-issuance-from-bridge)
- [Stripe — Use stablecoins in Financial Accounts (docs)](https://docs.stripe.com/financial-accounts/stablecoins)
- [Slash Engineering — Building Banking-Grade Stablecoin Rails](https://www.slash.com/engineering/blog/banking-grade-stablecoin-rails)
- [CoinDesk — Bridge sees stablecoin volume quadruple (Feb 2026)](https://www.coindesk.com/business/2026/02/24/stripe-s-bridge-sees-stablecoin-volume-quadruple-as-utility-insulates-from-crypto-winter)
- [Yahoo Finance — Stripe charges 1.5% for stablecoin transfers](https://finance.yahoo.com/news/stripe-charges-1-5-stablecoin-145737023.html)
- [Routefusion — Bridge vs BVNK vs Routefusion 2026](https://www.routefusion.com/blog/bridge-vs-bvnk-vs-routefusion-comparison)
- [Sam Boboev / Medium — Deep Dive: BVNK vs Bridge vs Zero Hash](https://medium.com/@samboboev/deep-dive-bvnk-vs-bridge-vs-zero-hash-stablecoin-payment-infrastructure-1235fd4e6d73)
- [Crossmint — Bridge Alternatives for Stablecoin Infrastructure](https://www.crossmint.com/learn/bridge-alternatives-for-stablecoin-infrastructure)
- [Brale — Pricing](https://brale.xyz/pricing)
- [GitHub — lnflash/bridge-mcp](https://github.com/lnflash/bridge-mcp)
- [LobeHub — Bridge MCP Server registry entry](https://lobehub.com/mcp/lnflash-bridge-mcp)
- [Postman — Bridge.xyz API public collection (third-party)](https://www.postman.com/material-pilot-3638775/public-workspace/collection/q022uvv/bridge-xyz-api)
- [a16z crypto — Stablecoins with Bridge founder & USDC creator (podcast)](https://a16zcrypto.com/posts/podcast/stablecoins-bridge-founder-circle-usdc-creator/)
- [Sequoia Capital — Partnering with Bridge](https://sequoiacap.com/article/partnering-with-bridge-a-better-way-to-move-money/)
- [Fortune — Bridge $58M funding](https://fortune.com/crypto/2024/08/29/bridge-stablecoins-sequoia-ribbit-index-haun-58-million/)
- [CNBC — Stripe closes $1.1B Bridge deal](https://www.cnbc.com/2025/02/04/stripe-closes-1point1-billion-bridge-deal-prepares-for-stablecoin-push-.html)
- [CoinDesk — BlindPay "next Bridge.xyz"](https://www.coindesk.com/consensus-hong-kong-2025-coverage/2025/01/23/the-next-bridge-xyz-blindpay-s-ceo-wants-to-revolutionize-global-payments)
- [Conviction — The Incredible Story of Bridge.xyz](https://conviction.finance/2024/bridge-xyz-the-stripe-of-crypto/)
- [Ledger Insights — Stripe rolls out stablecoin accounts in 101 countries](https://www.ledgerinsights.com/stripe-rolls-out-stablecoin-accounts-in-101-countries-as-bridge-launches-usdb/)
