# Altitude / Grid — Developer Experience

*Stream 6: Grid API quality, sandbox, KYB embed, idempotency, webhooks, passkey flow, signer infra, SDK quality, pricing, gotchas, and head-to-head vs. Bridge / Privy / Turnkey / Stripe / SpherePay*
*Compiled 2026-05-05*

> **Scope.** This is a developer-experience deep-dive on **Grid** — the public REST API operated by Squads Labs that powers Altitude under the hood. Architecture, program IDs, on-chain PDAs, IDL, and CPI graph are covered in [`architecture.md`](architecture.md). This file does NOT repeat that. Instead: docs quality, sandbox quality, KYB integration, idempotency/errors, webhooks (or lack thereof), passkey flow, signer infra, SDK quality, pricing, gotchas, and a head-to-head against Bridge / Privy / Turnkey / Stripe / SpherePay.

The headline up front for the impatient reader: **Grid is unusually polished for a Solana-native API**. There is a real OpenAPI 3.1 spec at a stable URL, a public Mintlify docs site, a clean TS SDK with React Native bindings, a self-serve dashboard with sandbox keys, idempotency keys and a structured error envelope, an embedded-wallet abstraction over Privy + Turnkey + Passkey behind a single REST surface, and Sumsub-powered KYB flows. ✅ It is materially better than 90% of "stablecoin API" landing pages translated into reality. **However**, the moment you cross the line from "smart-account toy" into "actual neobank weekend project," you fall off a cliff: KYB, on/off-ramp, virtual accounts, fee sponsorship, multisig proposals, and KYC are **all enterprise-tier-only** behind a sales gate. There are also no public webhooks, no published rate limits, no Python SDK, and the Solana-side multisig SDK that everyone actually consumes (`@sqds/multisig`, 25k weekly downloads) is **distinct** from the Grid SDK (`@sqds/grid`, ~2.5k weekly downloads, only ~6 months old) and has known sharp edges. 🟡

---

## 1. Endpoint catalog (the actual API surface)

Grid publishes a real OpenAPI 3.1.0 spec at [`https://grid.squads.xyz/api-docs/openapi.json`](https://grid.squads.xyz/api-docs/openapi.json) — **162 KB, 51 paths, 211 schemas, 13 tag groups, MIT-licensed**. ✅ This alone puts Grid ahead of most Solana-native APIs (Helio, SpherePay, Lulo all publish docs but no machine-readable OpenAPI at a stable URL of comparable completeness).

Auth is bog-standard `Authorization: Bearer <UUID-style key>` with the `bearer_auth` scheme defined globally. ✅ Every mutating endpoint accepts an optional `x-idempotency-key` header. ✅ Network selection is via `x-grid-environment: sandbox | devnet | mainnet` (older docs in `architecture.md` said only `devnet | mainnet`; the OpenAPI spec confirms `sandbox` is a real, distinct first value). 🟡 The base URL is `https://grid.squads.xyz` (the developer-facing docs at `developer-api.squads.so` are an older alias for the same backend).

### Full path catalog

Reproduced verbatim from the OpenAPI spec:

| Tag | Method | Path | Summary |
|---|---|---|---|
| accounts | POST | `/api/grid/v1/accounts` | Create email or signers account |
| accounts | POST | `/api/grid/v1/accounts:custom` | Create with mixed email + pubkey signers |
| accounts | POST | `/api/grid/v1/accounts/verify` | Verify email OTP, deploy account |
| accounts | GET | `/api/grid/v1/accounts/{address}` | Get account state |
| accounts | PATCH | `/api/grid/v1/accounts/{address}` | Update policies |
| accounts | GET | `/api/grid/v1/accounts/{address}/balances` | Balance list |
| accounts | GET | `/api/grid/v1/accounts/{address}/transfers` | Transfer history |
| auth | POST | `/api/grid/v1/auth` | Initiate email auth (returns OTP) |
| auth | POST | `/api/grid/v1/auth/verify` | Complete email auth |
| auth | POST | `/api/grid/v1/auth/refresh-session` | Refresh expired session (Privy two-tier) |
| transactions | POST | `/api/grid/v1/accounts/{address}/transactions` | Prepare arbitrary tx |
| transactions | POST | `/api/grid/v1/accounts/{address}/submit` | Submit signed tx (single or batch) |
| spending-limits | POST/GET/PATCH/DELETE | `/api/grid/v1/accounts/{address}/spending-limit[s]` | CRUD on `SpendingLimit` PDA |
| spending-limits | POST | `…/spending-limit/{id}/transactions` | Use a spending limit (single-shot transfer) |
| standing-orders | POST/GET/DELETE | `…/standing-order[s]` | Recurring transfer intents |
| trade | POST | `/api/grid/v1/trade/quote` | Get a Jupiter quote (only `jupiter` venue enum) |
| payments | POST | `/api/grid/v1/accounts/{address}/payment-intent` | v1 payment intent |
| payments | POST | `/api/grid/v1/accounts/{address}/payment-intents` | v1.5 payment intent (paginated list) |
| payments | POST | `/api/grid/v2/accounts/{address}/payment-intents` | v2 payment intent (current) |
| payments | GET | `/api/grid/v2/accounts/{address}/payment-intents/{id}` | Get v2 intent |
| external-accounts | GET/POST/DELETE | `/api/grid/v1/accounts/{address}/external-accounts[/{id}]` | Bank account on-file |
| virtual-accounts | POST/GET | `/api/grid/v1/accounts/{address}/virtual-account[s]` | Get a USD/EUR virtual account number |
| kyc | POST/GET | `/api/grid/v1/accounts/{address}/kyc[/{id}]` | KYC link issuance + status |
| passkeys | POST | `/api/grid/v1/passkeys` | Create passkey session (returns hosted-UI URL) |
| passkeys | POST | `/api/grid/v1/passkeys/auth` | Authorize existing passkey |
| passkeys | POST | `/api/grid/v1/passkeys/submit` | Submit WebAuthn response |
| passkeys | POST | `/api/grid/v1/passkeys/account` | Deploy passkey-controlled smart account |
| passkeys | GET | `/api/grid/v1/passkeys/account/{addr}` | Get passkey account |
| passkeys | GET/POST | `/api/grid/v1/passkeys/find` | Lookup passkey by authenticator |
| passkeys | POST | `/api/grid/v1/accounts/{addr}/passkeys/transaction` | Add passkey to existing account |
| passkeys | DELETE | `…/passkeys/{passkey_address}/transaction` | Remove passkey |
| proposals | GET/POST | `…/proposals` | List + create multisig proposals (**enterprise-only**) |
| proposals | POST | `…/proposals/{id}/vote` and `/vote-and-execute` | Voting |
| compliance | full CRUD | `/api/compliance/v1/entities[/{id}]` | KYB entity (**enterprise-only**) |
| compliance | GET | `/api/compliance/v1/entities/{id}/kyb` and `/kyb-link` | Sumsub WebSDK link |
| compliance | POST | `/api/compliance/v1/entities/{id}/tos` | TOS acceptance with IP + UA capture |
| compliance | POST | `/api/compliance/v1/entities/import-sumsub` and `/providers/bridge/import` | Bring-your-own approval |
| compliance | GET | `…/rfis` | Sumsub Requests for Information |

51 paths total. ✅ Grouping: 6 accounts, 4 spending-limits, 4 standing-orders, 3 transactions, 5 payments (v1+v2), 12 passkeys, 5 KYC/external-accounts/virtual-accounts, 4 auth, 4 proposals, 9 compliance/KYB, 1 trade. The five "Grid modules" marketed at [squads.xyz/grid](https://squads.xyz/grid) (Core / Yield / Trading / Cards / Data) map onto the spec as: Core ≈ accounts+passkeys+auth, Trading ≈ trade+payment-intent, Cards ≈ **not in OpenAPI yet** 🔴, Yield ≈ **not in OpenAPI yet** 🔴, Data ≈ balances+transfers. **The Cards and Yield modules are marketed but not present as documented endpoints — at minimum the OpenAPI spec does not expose them as of 2026-05-05.** This is a real gap between marketing and developer docs.

### Schema quality

The 211 schemas are coherent, well-typed, and use OpenAPI 3.1 nullables correctly (`type: ["string", "null"]` rather than the old `nullable: true` hack — though there are a few legacy holdovers). ✅ Discriminated unions are done with `oneOf` + a literal `type` enum, e.g., `CreateAccountRequestPayload` is `oneOf` `{type: "email", ...}` or `{type: "signers", ...}`. The response envelope is consistent: every success returns `{ data: <typed>, metadata: { request_id, timestamp } }`, which gives you a server-side correlation ID for support tickets — a small but high-leverage detail most APIs miss. ✅

The error envelope is structured. From the docs:

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Human readable error message",
    "details": "Additional context"
  }
}
```

Plus a `GridErrorDetail` for per-field validation errors:

```ts
{ field: string; code: string; message: string; suggestion?: string; documentation?: string }
```

✅ Of note: a `documentation` field that links from the error to the relevant docs page. That is a Stripe-tier detail.

### Docs quality, per module

Per-module score (1-10), based on reading the Mintlify-rendered docs at `developers.squads.so` and the raw `llms-full.txt` (15,596 lines):

| Module | Score | Rationale |
|---|---:|---|
| Core (accounts, transactions) | **8/10** | Quickstart with full TS code; both SDK and REST tabs; OTP/passkey flows complete; clear sandbox vs production warnings (e.g., "addresses differ between environments"). Missing: backend-language non-TS examples beyond cURL. |
| Passkeys | **9/10** | Two integration tracks (hosted-UI iframe vs custom-domain WebAuthn proxy). Explicit ES256 / `userPresent: true` / 60-second challenge constraints documented. Error code table. Password-manager support matrix (Chrome / Apple / Yubikey / 1P / Dashlane ✅; NordPass ❌). Best in the API. |
| Spending limits | **7/10** | Full CRUD documented, deterministic addressing called out, but no end-to-end "card-style spending limit" tutorial — the canonical Altitude UX is left as an exercise. |
| Payments | **7/10** | v1 → v2 evolution visible; `fee_config` breaking change documented with migration; intent → deposit → next_action pattern is clear. Missing: webhooks for status (only "may trigger if configured" — no shape, no signing scheme, no replay-protection guidance). 🟡 |
| KYC / KYB / compliance | **6/10** | Sumsub WebSDK URL flow, RFIs, TOS acceptance with IP capture documented. **But: enterprise-only.** No sandbox simulation of "force-approve KYB," no documented webhook for status-changes. 🟡 |
| Trading | **3/10** | One endpoint (`/trade/quote`), one venue enum (`jupiter`). The "thousands of tokens" marketing → just a thin Jupiter wrapper. No execution endpoint in the OpenAPI spec at all. 🟡 |
| Cards | **0/10** | **Not in OpenAPI spec at all.** The marketed Cards module is invisible to a developer reading docs. 🔴 |
| Yield | **0/10** | Same — marketed but not in spec. The pricing table even lists "Yield integrations (coming soon)." 🔴 |
| Data | **5/10** | `GET /balances` and `GET /transfers` exist; pagination via `limit/offset`; no `since-cursor` style streaming; no webhook subscription. |

**Average: ~5/10 across the marketed surface, ~7/10 across what is actually shipped.** A serious developer gets very far on Core + Passkeys + Spending Limits + Payments. Anything else is a sales conversation.

---

## 2. Authentication & key management for developers

Self-serve. ✅ The dashboard at [`grid.squads.xyz/dashboard`](https://grid.squads.xyz/dashboard) issues sandbox and production keys without contact-sales gating for the **Basic** ($0) and **Pro** ($499/mo) tiers. The quickstart ([Quickstart](https://developers.squads.so/grid/v1/accounts/quickstart)) sends you straight there.

Two key types are exposed by the SDK config:
- `apiKey` — **server-side only**, full access to your tenant
- `appId` — **client-side safe**, requires a domain whitelist configured in the dashboard

This split is right out of the Stripe / Plaid playbook and shows a level of API-design taste most Solana-native infra hasn't reached. ✅ ([GridApiConfig reference](https://developers.squads.so/grid/v1/sdk-reference/typescript/reference/latest/interfaces/GridApiConfig))

Three environments — `sandbox`, `devnet`, `mainnet`. The first is the default in the quickstart and is **architecturally distinct from devnet** (a dedicated test environment, not just Solana devnet pointing at the same backend). 🟡 The docs explicitly warn "Grid accounts do not have the same address in sandbox and production. **DO NOT** send funds to the same address in both environments." This implies separate program-config PDA counters per environment — clean.

What is NOT documented: **per-key permissions/scopes** (read-only vs. read-write, scoped-to-account, scoped-to-endpoint). Bridge has these. Stripe has these. Grid does not appear to. 🔴 **No webhook signing secrets** are documented anywhere I could find — because there are effectively no public webhooks (see §6).

---

## 3. Sandbox quality

This is more useful than I expected, and worse than I expected, simultaneously.

**What works in sandbox** ✅:
- Full email + OTP account creation flow (the Privy backend in sandbox emails real OTPs to your real inbox).
- Passkey creation against the hosted iframe — biometric prompts, smart-account deployment, the full ceremony.
- Smart-account deployment, transaction prepare/submit, spending-limit enforcement.
- "Devnet funding" — every passkey-created sandbox account is **automatically airdropped 1 USDC** so you can test transfers end-to-end on day one. Documented at [Passkeys Introduction](https://developers.squads.so/grid/v1/accounts/passkeys/introduction). That is a small thing that saves ~30 minutes the first time. ✅

**What is broken or limited** 🟡:
- KYB simulation: `/api/compliance/v1/entities/{id}/kyb-link` returns a real Sumsub WebSDK URL even in sandbox. There is no documented "fast-forward to approved" toggle. You either complete the Sumsub flow with their sandbox identities or you wait. 🔴 vs. Bridge, which exposes a documented sandbox path to push KYC/KYB to approved programmatically.
- ACH/wire/SEPA simulation: virtual-accounts and the payment-intent v2 surface accept `payment_rail: SWIFT|ACH|SEPA` etc., but there is **no documented sandbox-only "force-settle" or "force-fail" hook** the way Bridge ([Bridge sandbox docs](https://apidocs.bridge.xyz/get-started/introduction/quick-start/setting-up-sandbox)) does explicitly. You get a payment intent, you get a `next_action: await_funding`, and then you're effectively talking to the partner-PSP sandbox (Bridge / Infinite) which Grid has not abstracted. 🔴 This means **end-to-end fiat-rail testing is a multi-vendor sandbox dance**.
- Card issuance in sandbox: no public sandbox surface exists because no public Cards endpoints exist in the OpenAPI spec. 🔴
- Trading in sandbox: `POST /trade/quote` proxies to Jupiter regardless of environment. There is no sandbox Jupiter; you get real Jupiter quotes against real mints. Calling submit/execute in sandbox would land on Solana devnet (assuming the underlying RPC is devnet); Jupiter's devnet support has historically been spotty.

**Verdict.** Sandbox is good enough to ship Core + Passkeys + Spending Limits + Solana-only stablecoin transfers with confidence in a weekend. It is **not** good enough to validate fiat-rail onboarding or card issuance without going to staging on real money.

---

## 4. KYB integration for developers

Sumsub-backed. ✅ Confirmed both via the OpenAPI spec (`GenerateKybLinkResponsePayload.url` is described as "KYB verification URL to redirect the user to"; one endpoint is literally `POST /api/compliance/v1/entities/import-sumsub`) and the docs ("Generates a Sumsub WebSDK verification link"). Sumsub is the same KYC vendor used by Binance, Bybit, OKX, Bitget — heavyweight but legitimate.

The flow for an embedding developer:

1. `POST /api/compliance/v1/entities` with `{ type: "business", name, email, external_id }` — returns an entity UUID. ✅
2. `GET /api/compliance/v1/entities/{id}/kyb-link` — returns `{ url, expires_at: now+30min }`. ✅ Redirect or iframe the URL to the user.
3. User completes Sumsub WebSDK ceremony.
4. Poll `GET /api/compliance/v1/entities/{id}/kyb` for `compliance_status` (one of `not_started | pending | in_progress | in_review | partially_approved | action_required | approved | rejected | suspended`). 🟡 **Polling is the documented path; webhooks "may trigger if configured" but the configuration UI and event shape are not in public docs.**
5. Once `approved`, call `POST /api/compliance/v1/entities/{id}/distribute` to fan-out the approved KYB record to all configured PSP partners (Bridge, MoonPay, Infinite, Due) — and `POST /api/compliance/v1/entities/{id}/providers/bridge/import` if the customer was already KYB-approved at Bridge. ✅ This "distribute" step is a real differentiator: Grid sells "approve once, route everywhere," abstracting the PSP fan-out that you would otherwise have to build yourself. ✅
6. `POST /api/compliance/v1/entities/{id}/tos` accepts ToS with `client_ip` + `client_user_agent` + `acceptance_method` (checkbox / click / link / api) for audit compliance. ✅ Good audit-trail hygiene.

Approval timelines are not committed to in docs. The KYC docs note "verification typically takes 1-3 business days." ✅ Consistent with Sumsub's stated SLAs.

**RFIs (Requests for Information)** are first-class: `GET /api/compliance/v1/entities/{id}/rfis` returns paginated RFI items. ✅ Good. Most stablecoin APIs hide RFIs behind dashboard UIs, forcing email shuffling.

**The big asterisk: the entire `/api/compliance/v1` namespace is enterprise-tier-only per the [pricing page](https://developers.squads.so/grid/v1/pricing).** A developer on Basic ($0) or Pro ($499/mo) cannot call any KYB endpoint. So as a self-serve developer, you can't even *test* the KYB integration end-to-end without a sales conversation. 🔴

---

## 5. Idempotency, error handling, rate limits

### Idempotency

Idempotency is **first-class**. ✅ All mutating endpoints (create-account, create-payment-intent, create-external-account, etc.) accept an `x-idempotency-key` header (the OpenAPI spec confirms it as an explicit parameter on each handler). The TS SDK's `LastResponse` interface exposes `idempotencyKey` on every successful response so you can correlate retries. ([LastResponse interface](https://developers.squads.so/grid/v1/sdk-reference/typescript/reference/latest/interfaces/LastResponse))

```ts
const response = await gridClient.createAccount({ email: 'user@example.com' });
console.log('Request ID:', response.lastResponse?.requestId);
console.log('Idempotency Key:', response.lastResponse?.idempotencyKey);
```

What is NOT documented: **TTL on idempotency keys** (Bridge says explicitly 24h; Stripe says 24h; Grid's docs are silent), and **whether key-collision against a different body returns 422 or wins-or-fails**. 🟡 Bridge documents this precisely ([Bridge idempotency](https://apidocs.bridge.xyz/api-reference/introduction/idempotence)) — Grid's omission is a real gap.

### Error envelope

Already covered in §1: `{ error: { code, message, details } }` with per-field `GridErrorDetail` carrying `code`, `field`, `suggestion`, and a `documentation` URL. ✅ The TS SDK throws `GridError` (with `error.statusCode`, `error.lastResponse?.requestId`) rather than returning a discriminated union — this is the same pattern Stripe's TS SDK uses and most engineers prefer. ✅

A real example error code from the docs: `missing_fee_config` thrown when a non-enterprise customer submits a payment intent without a `fee_config` object. ✅

### Rate limits

**Not publicly documented.** 🔴 No `Retry-After` semantics, no per-key/per-endpoint quota table, no 429 example. The fact that Squads-Grid has an internal repo titled `api-rate-limiting-assessment` (visible at [github.com/Squads-Grid](https://github.com/Squads-Grid)) suggests rate limiting exists on the backend, but the contract with the developer is unknown. The pricing page hints at "MAU caps" (1k Basic, 5k Pro, custom Enterprise) but those are billing thresholds, not request quotas. This is a meaningful gap vs Stripe / Bridge / Privy — all three publish 429 contracts.

### Retries

The SDK config exposes `retryAttempts` and `timeout` ✅ as first-class properties, so the SDK auto-retries idempotent calls. The backoff strategy is not documented but is presumably exponential with jitter.

---

## 6. Webhooks

This is the biggest single gap in Grid's developer experience. 🔴

The string `webhook` appears **three times** in the entire 15,596-line `llms-full.txt` corpus:
- "Receive real-time status updates via webhooks" (marketing copy in the KYC overview)
- "Some statuses trigger webhooks if configured" (KYC status doc)
- An HMAC mention that turns out to be about HKDF, not webhook signing

There is **no public**:
- Webhook event catalog (no `payment_intent.completed`, `kyb.approved`, etc.)
- Payload shape spec
- Signing scheme (no documented HMAC-SHA256 secret, no Svix, no Ed25519 signature header)
- Delivery-guarantee statement (at-least-once with retry? at-most-once?)
- Replay-protection / timestamp-tolerance window
- Dashboard UI documented for adding endpoints

For a payments API this is a **showstopper for production**. The architecturally honest implication is that Grid is still in "long-poll" mode: you call `GET /payment-intents/{id}` until the status changes. That works for the SDK example flow, but it does not scale to a serious neobank that needs reliable async event handling for ACH settlement (T+1 to T+3) and KYB approval (1-3 business days).

Compare:
- Bridge ([apidocs.bridge.xyz](https://apidocs.bridge.xyz)) — full webhook spec, documented signing
- Stripe — Svix-style HMAC headers, replay-window guidance, retry tables
- Privy ([docs.privy.io](https://docs.privy.io)) — webhook events for wallet creation, MFA changes
- Helio / SpherePay — both publish webhook signing

Grid as of 2026-05-05 is the outlier. Either webhooks exist as a private/enterprise feature exposed only via dashboard UI, or they are genuinely on the roadmap. Either way, **a self-serve developer cannot rely on Grid for production async event handling today**. 🔴

---

## 7. Passkey + smart-account creation flow (line counts and ergonomics)

This is the part of Grid that is genuinely *good*. The full happy-path from "user lands on app" to "first stablecoin payment sent" in the SDK is roughly:

```ts
import { GridClient } from "@sqds/grid";
import { Keypair } from "@solana/web3.js";

// 1) Init client
const grid = new GridClient({
  environment: "sandbox",
  apiKey: process.env.GRID_API_KEY!,
  baseUrl: "https://grid.squads.xyz",
});

// 2) Generate session secrets (Privy HPKE keypair, kept server-side)
const sessionSecrets = await grid.generateSessionSecrets();

// 3) Create the user account via email
const user = await grid.createAccount({ email: "founder@example.com" });

// 4) Verify OTP — also deploys the Solana smart-account PDA
const session = await grid.completeAuthAndCreateAccount({
  user, otpCode: "123456", sessionSecrets,
});

// 5) Add a $5,000/week spending limit  (uses the on-chain SpendingLimit PDA)
await grid.createSpendingLimit(session.address, {
  amount: 5_000_000_000n,           // 5,000 USDC
  mint: "EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v",
  period: "Week",
  destinations: [],                  // anywhere
});

// 6) Build, prepare, sign, and send a payment
const tx = await buildSplTransfer(...);                         // your code
const prepared = await grid.prepareArbitraryTransaction(session.address, {
  transaction: tx.toBase64(),
});
const sent = await grid.signAndSend({
  sessionSecrets, session, transactionPayload: prepared, address: session.address,
});
```

That is **~25 lines of TypeScript** end-to-end for "create user → deploy smart account → set spending policy → send first payment." ✅ The ergonomics are very Stripe-like; the `signAndSend` collapsing of "sign + submit" is the right call for 90% of integrations.

Where it gets harder: the moment you want **multisig with non-email-EOA signers** (the canonical Squads-shaped product), you need a 2-of-3 mixed-signer account, which uses `/accounts:custom`:

```ts
const acct = await grid.createCustomAccount({
  policies: {
    threshold: 2,
    signers: [
      { type: "email",  email: "cfo@co.com", provider: "turnkey",
        permissions: ["CAN_INITIATE","CAN_VOTE","CAN_EXECUTE"] },
      { type: "email",  email: "ceo@co.com", provider: "turnkey",
        permissions: ["CAN_VOTE","CAN_EXECUTE"] },
      { type: "pubkey", address: "7xK...abc",
        permissions: ["CAN_VOTE"] },
    ],
  },
});
```

✅ Clean. But the *moment* you try to use this with the proposal endpoint (`POST /accounts/{addr}/proposals`), you hit a **403 Forbidden — proposals are an enterprise-tier feature**, per the [proposals docs](https://developers.squads.so/grid/v1/api-reference/endpoint/proposals/create). 🔴 So the headline "build a Squads multisig in 10 lines" is true only if you don't actually need the multi-party voting flow that defines a multisig.

### Passkey creation flow

The hosted-iframe path is genuinely the best passkey UX I've seen in Solana-land:

```ts
// 1) Server requests session
const { url, sessionKey } = await grid.createPasskeySession({
  appName: "MyNeobank",
  redirectUrl: window.location.origin + "/callback",
});
// 2) Frontend renders <iframe src={url} /> (60-sec validity)
// 3) User does Touch ID / FaceID / Yubikey
// 4) postMessage event yields { passkeyAddress, smartAccountAddress }
```

ES256 only (algorithm `-7`); user-presence required; 60-second challenge expiry; supports Chrome / Apple Passwords / Yubikey / 1Password / Dashlane (NordPass excluded). ✅ ([Passkeys Introduction](https://developers.squads.so/grid/v1/accounts/passkeys/introduction)) The "advanced integration" path lets you host the WebAuthn ceremony on `auth.yourcompany.com` and use Grid as a proxy — credible for enterprise branding requirements. ([Custom Domain](https://developers.squads.so/grid/v1/accounts/passkeys/advanced-integration))

---

## 8. Embedded wallet / signer infrastructure — the Privy-or-Turnkey-or-passkey question answered

This was the big open question from `architecture.md`. The OpenAPI spec resolves it definitively. The `GridMPCProvider` enum is:

```
"privy" | "dynamic" | "passkey" | "turnkey" | "external"
```

✅ ([GridMPCProvider in openapi.json](https://grid.squads.xyz/api-docs/openapi.json)) **Grid does not roll its own MPC.** It is an aggregator/orchestrator over Privy + Turnkey + Dynamic + raw passkeys + external (your-own) signers. The default is **Privy** ([Primary Provider Integration](https://developers.squads.so/grid/v1/api-reference/advanced/privy-signing)) with Turnkey as the secondary. The docs even describe automatic provider fallback: "if the requested provider (default: Privy) is unavailable or times out, the endpoint falls back to the alternate provider. When a fallback occurs, the response includes `requested_provider` (the originally requested provider) and `fallback_reason` (`timeout` or `provider_error`)." ✅

This is a **genuinely smart architectural call**. The neobank-app developer pays for one Squads SaaS subscription and gets multi-vendor key redundancy "for free" — Grid handles the failover. Privy and Turnkey would each separately bill the developer if integrated directly, plus the developer would have to write the failover orchestration. ✅

The session-key pattern uses **TEE-based HPKE encryption** via Privy's Trusted Execution Environment, with ChaCha20-Poly1305 and ECDH key derivation per [Privy signing guide](https://developers.squads.so/grid/v1/api-reference/advanced/privy-signing). ✅ This is the correct shape; the cryptographic detail in the docs is unusually thorough for a payments API.

Refresh-session has a **two-tier model**: short-lived (15 min) auth tokens within a 24-hour session, with `Privy` getting "full support for two-tier session refresh" and `Turnkey` listed as "Coming soon." 🟡 So Privy is the privileged provider in practice today.

---

## 9. SDK quality (deeper than architecture.md)

| Package | Latest | Last publish | Weekly DLs | Notes |
|---|---|---|---:|---|
| [`@sqds/grid`](https://www.npmjs.com/package/@sqds/grid) | **3.1.2** | 2026-03-06 | **2,499** | The Grid REST SDK; created Aug 2025; 29 versions in ~7 months. ✅ |
| [`@sqds/grid-react-native`](https://www.npmjs.com/package/@sqds/grid-react-native) | 1.0.5 | 2026-03-06 | 56 | Expo / RN bindings, used by Squads' own neobank-example-app. 🟡 small DL count. |
| [`@sqds/grid-crypto`](https://www.npmjs.com/package/@sqds/grid-crypto) | 1.0.0 | 2026-03-06 | — | HPKE / ChaCha / canonicalization helpers, factored out of `@sqds/grid` 3.0+. ✅ |
| [`@sqds/multisig`](https://www.npmjs.com/package/@sqds/multisig) | 2.1.4 | 2025-08-15 | **25,915** | The Solana V4 multisig SDK; `architecture.md` covers this. ✅ |
| `@sqds/sdk` (legacy V3) | 2.0.4 | 2023-03-14 | ~700 | Abandoned. |
| [`squads-multisig`](https://crates.io/crates/squads-multisig) | 2.1.0 | 2025-04-08 | 29,593 recent | Rust client for V4. ✅ |
| [`squads-multisig-program`](https://crates.io/crates/squads-multisig-program) | 2.0.0 | 2024-01-08 | 29,758 recent | Rust on-chain CPI bindings. 🟡 stale (1y+) |
| `@sqds/smart-account` | not published | — | — | Source in `Squads-Protocol/smart-account-program` repo; no npm release. 🟡 |

### What's in the box (`@sqds/grid` 3.1.2)

The package has 17 runtime dependencies and a dist/index.d.ts type entry. ([npm metadata](https://registry.npmjs.org/@sqds/grid)) Notable dependencies:
- `@hpke/chacha20poly1305` + `@hpke/core` — Privy TEE encryption primitives
- `@noble/curves` + `@noble/ciphers` + `@noble/hashes` — auditable crypto
- `@solana/web3.js` (legacy 1.x — not the new v2 yet) 🟡
- `@turnkey/crypto` — Turnkey's KMS helpers
- `canonicalize` — JSON canonicalization for signing
- `jose` — JWT/JWE handling
- MIT-licensed.

### Type quality

Service-layer architecture as of 2.0.0 ([changelog](https://developers.squads.so/grid/v1/sdk-reference/typescript/reference/latest/changelog)): `AccountService`, `AuthService`, `BankingService`, `PasskeyService`, `SpendingLimitService`, `TransactionService`, `UtilityService` — clean separation. ✅ An `AccountManager` exposes a reactive event-emitter `client.account.on('change', ...)` for live state. ✅ Errors are thrown (not returned), responses always wrap data in `{ data, lastResponse }`. ✅

### Breaking change pattern

Grid SDK shipped 3.0.0 in early 2026 with a snake_case → camelCase breaking change for TypeScript consistency. ✅ Justified, but two majors in 7 months for an SDK that is supposed to be your production dependency is meaningful churn. 🟡

### Backbone SDK (`@sqds/multisig`) — known sharp edges

Open issues from [github.com/Squads-Protocol/v4](https://github.com/Squads-Protocol/v4):
- **#174 (Feb 2026, open)**: `multisigCreateV2` crashes with `TypeError: null is not an object (evaluating 'pubkey.toBase58')` when `treasury: null` is passed despite the type appearing optional. Regression introduced in 2.1.4. ([issue](https://github.com/Squads-Protocol/v4/issues/174)) 🔴
- **#159 (Jul 2025, open, 2 comments)**: clap arg parsing in the CLI's `transaction_create` is wrong for multi-byte messages. 🟡
- **#150 (Apr 2025, open)**: docs don't explain how to serialize the `--transaction-message` CLI argument, leaving users to guess. 🟡
- **#148 (Feb 2025, open)**: a multisig created via `@sqds/multisig` on devnet does not appear in the Squads website UI — UI/SDK address-derivation drift. 🟡
- **#145 (Dec 2024, open)**: Rust SDK's `execute_message` only adds tx-level signers, blocking anyone trying to make a Squads-controlled multisig itself sign a `bpf_loader_upgradeable::upgrade` for program upgrades. 🔴 **This is a real Solana-developer pain.**
- **#135 (Nov 2024, open)**: edge case where vote changes on Approved proposals don't reset the timelock — a security-relevant ergonomics gap.

Trends: open issues skew toward CLI/SDK polish and multisig-specific edge cases, not core protocol bugs (consistent with the Certora FV record). ✅ But response time is uneven — issue #174 has had **zero comments** since Feb 2026.

---

## 10. Pricing for developers

Published. ✅ At [developers.squads.so/grid/v1/pricing](https://developers.squads.so/grid/v1/pricing):

| Feature | **Basic** | **Pro** | **Enterprise** |
|---|---|---|---|
| Price | **Free** | **$499/mo** | Custom |
| MAU cap | 1,000 Grid Account MAUs | 5,000 MAUs | Custom |
| Fault tolerance | ✅ | ✅ | ✅ |
| Send/receive any Solana asset | ✅ | ✅ | ✅ |
| Pay tx fees in USDC or SOL | ✅ | ✅ | ✅ |
| Automation policies | Create + manage | + fully managed | ✅ |
| Onchain passkey 2FA | ✅ | ✅ | ✅ |
| Arbitrary tx support | ✅ | ✅ | ✅ |
| **Fee sponsorship** | 🔴 | ✅ (billed in arrears) | ✅ |
| **On/off-ramp (ACH/SEPA/Wire)** | 🔴 | 🔴 | ✅ |
| **Virtual accounts** | 🔴 | 🔴 | ✅ |
| **KYC / KYB ops** | 🔴 | 🔴 | ✅ |
| **Multisig proposals** | 🔴 | 🔴 | ✅ |

**Translation**: **Basic and Pro are essentially "self-custody Solana wallet-as-a-service with stablecoin send/receive."** Anything that touches fiat, KYB, multi-party approval, or paymaster fee sponsorship is enterprise-only. The $499/mo Pro tier almost-but-not-quite gives you a real product — its main upgrade over Basic is fee sponsorship and "fully managed automations." If you are building a real B2B fintech (the Altitude shape), **you are an enterprise customer from day one**, and the dashboard self-serve flow is essentially a proof-of-concept tier.

This is the same "fintech PLG ceiling" pattern that Bridge, Stripe Treasury, Mercury, and Brex all use. It's not a flaw — it's an industry norm. 🟡 But the user-quote-worthy implication is: **the $0 tier and the $499 tier are demo-ware for serious payment products.**

---

## 11. Gotchas and common dev pitfalls

From issues, error tables, and the docs themselves:

1. **Sandbox addresses ≠ production addresses** — explicitly called out three times in docs. Sending production funds to a sandbox-derived account is irrecoverable. 🔴
2. **Passkey challenge has a 60-second window**. If your iframe takes >60s to load (slow mobile network), the WebAuthn ceremony fails. Code defensively. 🟡
3. **`fee_config` is required for non-Enterprise customers** — added as a breaking change in payment-intent v2; missing it returns `missing_fee_config`. 🟡
4. **The fee payer must sign the transaction** even if it's a separate address from the smart-account signer. The API auto-adds them as a required signer; if your wallet adapter doesn't expect this you'll get a "missing required signature" error from the cluster. 🟡
5. **`multisigCreateV2(treasury: null)` crashes** in `@sqds/multisig` 2.1.4 (issue #174). Always pass an explicit treasury or stay on 2.1.3. 🔴
6. **Transaction buffers needed for >1232-byte tx** — Altitude's batch-payment shape requires the `transaction_buffer_*` instruction sequence; the OpenAPI spec exposes this transparently but the SDK doc does not call it out as a 1232-byte threshold. Easy to hit and hard to debug. 🟡 ([SAP transaction buffer pattern, in `architecture.md`](architecture.md))
7. **Compute units / priority fees** — the SDK does not set CU limits or priority fees by default. For mainnet under load you will silently fail. The `prepareArbitraryTransaction` returns a fully-built tx; you have to inject `ComputeBudgetProgram.setComputeUnitLimit` + `setComputeUnitPrice` yourself. 🟡 Not in the quickstart.
8. **Lookup tables** — not supported via the public Grid API for arbitrary transactions as far as I can see; the prepared payload encodes a base64 v0 transaction but the docs do not discuss ALT compression. For complex Jupiter routes that hit the 1232-byte limit this matters. 🟡
9. **Anchor version** — the SAP is on Anchor 0.29; if your CPI client is on a newer Anchor (0.31+ have switched to `solana-program` 2.0), expect type-coercion friction. 🟡
10. **`@sqds/grid` SDK churn** — two majors (2.0 and 3.0) in 7 months. 3.0 introduced camelCase breaking. 3.1 added optional `feeConfig` to `createPaymentIntent`. Read changelogs before bumping. 🟡
11. **No public webhooks** ⇒ you must build a polling worker for KYB and ACH settlement. Plan for it. 🔴
12. **Proposals (multisig voting) are 403 on Basic + Pro** ⇒ you cannot ship a 2-of-3 treasury product on the Pro tier. 🔴

---

## 12. Open-source SDK examples — projects shipping on this

**171 public package.json files reference `@sqds/multisig`**, **21 reference `@sqds/grid`** (per GitHub code search). Notable real users:

| Repo | Description | Comment |
|---|---|---|
| [Squads-Grid/neobank-example-app](https://github.com/Squads-Grid/neobank-example-app) | Squads' own RN/Expo neobank skeleton (31 stars; React 19 + RN 0.81 + Expo 54) | The canonical "weekend project" reference. ✅ |
| [solana-foundation/explorer](https://github.com/solana-foundation/explorer) | The official Solana explorer | Uses `@sqds/multisig` to decode multisig accounts. ✅ |
| [helium/helium-program-library](https://github.com/helium/helium-program-library) | Helium DAO programs | Uses `@sqds/multisig` for treasury management. ✅ |
| [LayerZero-Labs/devtools](https://github.com/LayerZero-Labs/devtools) | LayerZero V2 cross-chain dev kit | Uses `@sqds/multisig` in their Solana adapter. ✅ |
| [hyperlane-xyz/hyperlane-monorepo](https://github.com/hyperlane-xyz/hyperlane-monorepo) | Hyperlane cross-chain protocol | Also a Solana consumer of `@sqds/multisig`. ✅ |
| [Mythic-Project/governance-ui](https://github.com/Mythic-Project/governance-ui) | Realms governance UI fork | Uses `@sqds/multisig` for treasury governance. ✅ |
| [sendaifun/solana-agent-kit](https://github.com/sendaifun/solana-agent-kit) | "Connect any AI agents to Solana" | AI-x-crypto, integrates `@sqds/multisig` as a "tool plugin." ✅ Especially relevant to your research thesis. |
| [faremeter/faremeter](https://github.com/faremeter/faremeter) | x402 / agent-payment universal framework | Another agent-payment consumer. ✅ |
| [convergence-rfq/convergence-sdk](https://github.com/convergence-rfq/convergence-sdk) | RFQ / OTC trading SDK | Uses Squads for treasury custody. |
| [a-khushal/bountyforge](https://github.com/a-khushal/bountyforge) | "AI agents that forge bounties into SOL" | Uses `@sqds/grid`. ✅ AI-x-crypto. |
| [adlonymous/subsave](https://github.com/adlonymous/subsave) | Subscriptions → yield-bearing instruments | Uses `@sqds/grid`. |
| [darkresearch/mallory](https://github.com/darkresearch/mallory) | Opinionated RN crypto-x-AI chat boilerplate | Uses `@sqds/grid` for embedded wallet. ✅ |
| [epicexcelsior/grid-sdk-cli](https://github.com/epicexcelsior/grid-sdk-cli) | Community CLI for Grid | Indicates community traction. ✅ |
| [Mirrorworld-universe/kronus-ui](https://github.com/mirrorworld-universe/kronus-ui) | Gaming wallet UI | `@sqds/multisig` for ownership. |

The pattern: `@sqds/multisig` is **load-bearing infrastructure** in serious Solana projects (Helium, Hyperlane, LayerZero, Solana Foundation explorer). `@sqds/grid` is **early-but-real**, with ~20 consumers including AI-x-crypto agent-payment frameworks (sendai, faremeter, mallory, bountyforge) — which is actually well-aligned with your AI × crypto research thesis. ✅

---

## 13. Comparison to peer dev experiences

| Dimension | **Grid (Squads)** | **Bridge.xyz** | **Privy** | **Turnkey** | **Stripe Issuing/Atlas** | **Mercury/Brex** | **Sphere Labs** | **Helio** |
|---|---|---|---|---|---|---|---|---|
| Self-serve sandbox keys | ✅ Basic free, instant | 🔴 contact-sales for sandbox | ✅ free 50k sigs/mo + $1M vol | ✅ usage-based, sandbox auto | ✅ Stripe-class | 🔴 sales | ✅ self-serve | ✅ self-serve |
| Public OpenAPI spec | ✅ at `grid.squads.xyz/api-docs/openapi.json` | ✅ | partial | partial | ✅ Stripe-class | partial | ✅ | partial |
| TypeScript SDK | ✅ `@sqds/grid` (3.1.2, MIT) | ✅ | ✅ industry-standard | ✅ very good (multi-package) | ✅ | TS partial | ✅ | ✅ |
| Rust SDK | ✅ `squads-multisig` 2.1.0 for the multisig program | 🔴 | 🔴 | partial | 🔴 | 🔴 | 🔴 | 🔴 |
| Python SDK | 🔴 | 🔴 | 🔴 | partial | ✅ | 🔴 | 🔴 | 🔴 |
| Webhooks (signed) | 🔴 not public | ✅ | ✅ | ✅ | ✅ Stripe-class | ✅ | ✅ | ✅ |
| Idempotency keys | ✅ | ✅ 24h TTL documented | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Rate-limit contract | 🔴 not documented | ✅ | ✅ | ✅ | ✅ | ✅ | partial | partial |
| Embedded wallet | ✅ orchestrates Privy+Turnkey+Passkey under one API | 🔴 (custody only) | ✅ flagship product | ✅ flagship product | 🔴 | 🔴 | 🔴 | 🔴 |
| KYB | ✅ Sumsub-backed; enterprise-only | ✅ flagship; included in mid tier | 🔴 | 🔴 (relies on partners) | ✅ Atlas — Stripe-class | ✅ | ✅ | partial |
| ACH/SEPA/Wire | ✅ enterprise-only | ✅ flagship | 🔴 | 🔴 | partial | ✅ | ✅ | partial |
| Card issuance | 🟡 marketed but no public endpoints | ✅ | 🔴 | 🔴 | ✅ flagship | ✅ | partial | 🔴 |
| Self-custody/MPC architecture | ✅ on-chain multisig + MPC providers | 🔴 fully custodial | ✅ MPC-only | ✅ MPC + TEE | 🔴 | 🔴 | 🔴 | 🔴 |
| Solana-native? | ✅ | partial (multi-chain) | ✅ | ✅ | 🔴 | 🔴 | ✅ | ✅ |
| Free tier exists? | ✅ Basic ($0) | 🔴 | ✅ generous | partial | ✅ generous | 🔴 | partial | partial |
| Production-ready for fintech? | 🟡 only on Enterprise | ✅ | ✅ wallets only | ✅ wallets only | ✅ | ✅ | ✅ | partial |

**The unique position of Grid** in this matrix: it is the **only** API that combines (a) Solana-native on-chain multisig with formally verified custody, (b) Privy/Turnkey-style embedded-wallet orchestration, and (c) ACH/SEPA/wire fiat rails — and exposes it as one REST surface. Bridge has the fiat rails but not the embedded wallet. Privy + Turnkey have the wallet but not the rails. Stripe Atlas + Mercury have neither the on-chain self-custody nor the Solana programmability. The architecturally-honest reading: **Grid is the only API where one developer can plausibly build "a self-custodial neobank on Solana" without stitching three vendors together.** ✅

The architecturally-honest counter: **the pricing is arranged so that you hit the enterprise gate the moment you actually need to put fiat in or out.** So in practice you're going to talk to sales anyway — at which point Bridge + Privy + your own glue is a viable alternative.

---

## 14. Gas-abstraction / fee-sponsorship implementation

The fee-sponsorship model is implemented at the Solana protocol level via the standard `feePayer` distinct-from-signer pattern, surfaced through the `fee_config` field on payment intents and on `prepareArbitraryTransaction`:

```json
{
  "fee_config": {
    "currency": "sol",
    "payer_address": "<paymaster-pubkey>"
  }
}
```

The flow per [docs](https://developers.squads.so/grid/v1/api-reference/endpoint/payment-intents/post):

1. Developer submits a payment intent with `fee_config`.
2. API builds the tx, simulates compute + signature + ATA-rent costs.
3. **Appends a repayment instruction** that transfers the fee from `payer_address` to the Grid paymaster.
4. Returns the prepared tx with a `fee` object showing the exact charged amount.
5. The paymaster signs and pays the on-chain SOL fee; the developer's `payer_address` reimburses in either SOL or USDC.

✅ This is a clean, transparent paymaster pattern. **USDC fees** are mediated by the appended repayment ix — no Token-2022 fee-delegation magic, just plain SPL-Token transfer composed atomically. 🟡 No mention of using Token-2022's `TransferFee` / `InterestBearing` extensions; this would matter only if you cared about confidential transfers, which Altitude doesn't.

**Cost model**: enterprise customers can set `self_managed_fees: true` to skip simulation and fully bypass the Grid paymaster. ✅ Pro customers use the paymaster and are billed in arrears for SOL spent. Basic gets none of this.

The "1M wallets for 2.5 SOL total" claim from the Grid landing page reduces to ~2.5 microSOL per smart-account creation — achievable because the SAP defers rent allocation until first execution (per `architecture.md` §6). ✅

---

## 15. The "weekend payroll app" feasibility test

**Question**: Can a competent solo Solana dev ship a small payment/payroll product on top of Grid in a weekend (≈16 hours of focused work)?

**Honest answer**: **For a Solana-only stablecoin payroll, yes. For a USD-in/USD-out payroll, no.** ✅ / 🔴

**What you get for free in a weekend on Basic ($0) tier:**
- ✅ Email + OTP onboarding for both payer and recipients (~25 lines TS)
- ✅ Smart-account deployment per user with passkey 2FA
- ✅ On-chain spending limits (e.g., "$5,000/employee/month")
- ✅ Stablecoin USDC transfers, batch payments via tx buffers
- ✅ Real-time balance + transfer history endpoints
- ✅ Typed TS SDK with reactive event emitter for the dashboard
- ✅ React Native bindings if you want a mobile companion app (`neobank-example-app` as a starting template)
- ✅ Solana fees absorbed by Grid paymaster on Pro

**What blocks the weekend:**
- 🔴 **No fiat in/out without Enterprise.** Cannot accept USD payroll funding via ACH or pay out to non-crypto-native employees. Dominant blocker for a real payroll product.
- 🔴 **No KYB without Enterprise.** Cannot legally onboard the employer entity.
- 🔴 **No multi-approver workflows on free/Pro.** "CFO must approve payroll above $50k" requires the proposals endpoint, which is enterprise-only.
- 🔴 **No webhooks.** You'll write a polling worker for ACH settlement (which doesn't exist on free tier anyway) and KYB approvals (also enterprise).
- 🟡 **Cards out of reach.** Marketed but no public endpoints.

**Realistic weekend scope**: A "stablecoin-only payroll dashboard for a crypto-native team that already custodies USDC and wants programmable allowances" — fully shippable. Looks identical to a Squads multisig dashboard but with email-based UX and policy-enforced spending. That is meaningful and would be hard to build on bare Solana SDKs alone (you would need to write the multi-vendor MPC integration, the Squads tx-buffer logic, and the spending-limit enforcement yourself — Grid collapses all three to a few REST calls). ✅

**Realistic 2-week scope on Enterprise pricing**: A real US-regulated stablecoin payroll product that takes ACH and pays USDC. This is genuinely feasible because Bridge does the regulated heavy-lift, Sumsub does the KYB, Privy/Turnkey do the keys, and Grid orchestrates all four. You write the UX. That is a real business.

---

## 16. The "should I use this" verdict

**Build on Grid if:**
- Your product is Solana-native and stablecoin-denominated
- You want passkey-first / email-first UX without writing WebAuthn yourself
- You want self-custodial smart accounts with on-chain spending limits, formally-verified custody, and Privy/Turnkey embedded wallets behind one API
- You have either a tiny Solana-only crypto-treasury product (free tier works) or a pre-existing Enterprise budget (the real product unlocks)
- You value MIT-licensed TS SDK with React Native, OpenAPI spec, idempotency keys, and structured errors

**Do NOT build on Grid if:**
- You need fiat rails on the cheap — Bridge directly is more honest
- You need real-time async event handling — you'll be writing pollers
- You need card issuance or yield surfaces today — they are marketed, not yet shipped to docs
- You need a Python SDK
- You need to ship a multi-approver business product on a $499/mo budget (proposals are 403)
- You need rate-limit / SLA contracts in writing

**The synthesis**: Grid is **the cleanest Solana-native fintech API in 2026**, with developer-experience polish that materially exceeds Sphere Labs, Helio, and Lulo. ✅ The architectural choices — orchestrating Privy + Turnkey + Sumsub + Bridge under a single REST surface, with on-chain Squads custody as the source of truth — are correct and hard to replicate. 🟢 But the product is fundamentally **gated** at the moment you cross from "Solana toy" to "regulated fintech," and the two key gaps (no public webhooks, no documented rate limits) are unforced errors that will cost developers time. 🔴

For a Solana developer evaluating "should I build my next product on this": Grid is a **strong yes for crypto-native B2B treasury / agent-payment / stablecoin-first products**, a **conditional yes for self-serve MVPs that you intend to upgrade to Enterprise as soon as a real customer appears**, and a **no for self-serve fintech-with-fiat** until Pro-tier ramps and webhooks are public.

---

## Sources

- [Grid OpenAPI 3.1 spec](https://grid.squads.xyz/api-docs/openapi.json)
- [Grid Developer Platform welcome](https://developers.squads.so/welcome)
- [Grid Quickstart](https://developers.squads.so/grid/v1/accounts/quickstart)
- [Grid Pricing](https://developers.squads.so/grid/v1/pricing)
- [Grid Authentication Methods](https://developers.squads.so/grid/v1/accounts/authentication-methods)
- [Grid Passkeys Introduction](https://developers.squads.so/grid/v1/accounts/passkeys/introduction)
- [Grid Passkeys Integration Guide](https://developers.squads.so/grid/v1/accounts/passkeys/integration-guide)
- [Grid Passkeys Custom Domain (Advanced)](https://developers.squads.so/grid/v1/accounts/passkeys/advanced-integration)
- [Grid Privy/MPC Provider Integration](https://developers.squads.so/grid/v1/api-reference/advanced/privy-signing)
- [Grid Payment Intent (v1)](https://developers.squads.so/grid/v1/api-reference/endpoint/payment-intents/post)
- [Grid Proposals (enterprise-only)](https://developers.squads.so/grid/v1/api-reference/endpoint/proposals/create)
- [Grid TypeScript SDK Changelog](https://developers.squads.so/grid/v1/sdk-reference/typescript/reference/latest/changelog)
- [Grid LastResponse interface](https://developers.squads.so/grid/v1/sdk-reference/typescript/reference/latest/interfaces/LastResponse)
- [Grid GridApiConfig interface](https://developers.squads.so/grid/v1/sdk-reference/typescript/reference/latest/interfaces/GridApiConfig)
- [Grid GridErrorDetail interface](https://developers.squads.so/grid/v1/sdk-reference/typescript/reference/latest/interfaces/GridErrorDetail)
- [@sqds/grid on npm](https://www.npmjs.com/package/@sqds/grid)
- [@sqds/grid-react-native on npm](https://www.npmjs.com/package/@sqds/grid-react-native)
- [@sqds/grid-crypto on npm](https://www.npmjs.com/package/@sqds/grid-crypto)
- [@sqds/multisig on npm](https://www.npmjs.com/package/@sqds/multisig)
- [squads-multisig on crates.io](https://crates.io/crates/squads-multisig)
- [Squads-Protocol/v4 on GitHub](https://github.com/Squads-Protocol/v4)
- [Squads-Protocol/v4 issue #174 — multisigCreateV2 null-treasury bug](https://github.com/Squads-Protocol/v4/issues/174)
- [Squads-Protocol/v4 issue #145 — multisig program upgrade signer bug](https://github.com/Squads-Protocol/v4/issues/145)
- [Squads-Protocol/v4 issue #135 — vote changes don't reset timelock](https://github.com/Squads-Protocol/v4/issues/135)
- [Squads-Protocol/v4-examples on GitHub](https://github.com/Squads-Protocol/v4-examples)
- [Squads-Grid/neobank-example-app on GitHub](https://github.com/Squads-Grid/neobank-example-app)
- [Squads-Grid org on GitHub](https://github.com/Squads-Grid)
- [Bridge.xyz Idempotency](https://apidocs.bridge.xyz/api-reference/introduction/idempotence)
- [Bridge.xyz Sandbox](https://apidocs.bridge.xyz/get-started/introduction/quick-start/setting-up-sandbox)
- [Bridge.xyz Cards Sandbox](https://apidocs.bridge.xyz/platform/cards/sandbox/sandbox)
- [Privy Pricing](https://www.privy.io/pricing)
- [Privy Solana embedded wallet docs](https://docs.privy.io/guide/expo/embedded/solana)
- [Turnkey Embedded Wallets Overview](https://docs.turnkey.com/embedded-wallets/overview)
- [Turnkey Pricing](https://www.turnkey.com/pricing)
- [SpherePay API](https://spherepay.co/products/api)
- [Squads "Grid" landing](https://squads.xyz/grid)
- [Squads "Altitude" landing](https://squads.xyz/altitude)
- [Squads on X — Grid public launch](https://x.com/SquadsProtocol/status/1966616137791123961)
