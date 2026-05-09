# Ramp Network — Developer Experience

*Stream 5: Widget integration, REST API, sandbox quality, KYC handoff, webhook signing, SDK quality, pricing, gotchas, peer comparison*
*Compiled 2026-05-09*

> **Note on naming:** This report is exclusively about **Ramp Network** (rampnetwork.com / docs.rampnetwork.com / @ramp-network on npm) — the fiat↔crypto on/off-ramp founded by Szymon Sypniewicz and Przemek Kowalczyk in 2017. It is **not** Ramp Business (ramp.com / docs.ramp.com), the corporate-spend / expense-management unicorn. Several search results conflate the two; only statements that clearly belong to Ramp Network are credited.

---

## 1. Baseline — what is Ramp Network?

Ramp Network ("Ramp Swaps Ltd", London) is a fiat-to-crypto on-ramp and crypto-to-fiat off-ramp infrastructure provider. Developers integrate it as a **payment-and-compliance widget** so an end user inside their wallet/dApp can buy crypto with a card, Apple Pay, Google Pay, SEPA Instant, Open Banking, or PIX, or sell crypto and receive fiat back to their card or bank. The integrator never touches money, never holds the card data, and Ramp owns the KYC/AML stack. Ramp claims 150+ countries, 38+ assets, and historical partner customers including MetaMask, Trust Wallet, Brave, Ledger, Sorare, and Axie Infinity ✅ ([Quicknode builders guide](https://www.quicknode.com/builders-guide/tools/ramp-network-by-ramp-swaps), [Ramp on Solana — SolanaCompass](https://solanacompass.com/projects/ramp)).

For a Solana developer specifically: SOL has been live for years, USDC on Solana and (since April 2026) USDT on Solana with **0-fee USD↔USDT conversions** are supported as a flagship route ✅ ([The Defiant — USDT live on Solana with Ramp + Privy](https://thedefiant.io/news/defi/usdt-live-solana-plasma-ethereum-ramp-privy-rt2zgt), [The Block — Ramp 0 USDT/USD](https://www.theblock.co/post/398354/peter-thiel-backed-unicorn-ramp-rolls-out-0-conversions-between-usdt-and-dollars-across-product-suite)).

---

## 2. Integration paths

Ramp officially supports four integration modes, each documented separately ([Integration Types Guide — rampnetwork.com](https://rampnetwork.com/blog/choosing-on-ramp-network-integration-type), [docs.rampnetwork.com Welcome](https://docs.rampnetwork.com/)):

| Mode | What it is | Pros | Cons | Use when |
|---|---|---|---|---|
| **Hosted (redirect)** | Send the user to `https://buy.ramp.network/?hostApiKey=…&swapAsset=SOLANA_SOL&userAddress=…` ✅ ([Hosted quick-start](https://docs.rampnetwork.com/web/quick-start-hosted)) | Zero JS dependencies; works from any backend, mobile webview, even an email link; survives CSP nightmares | User context-switches away; no inline events without `finalUrl` redirect; harder to brand | MVPs, prototypes, no-frontend backends, links from Discord/email |
| **Overlay (JS SDK)** | Same SDK, widget renders as a modal floating over your dApp ✅ ([Overlay quick-start](https://docs.rampnetwork.com/web/quick-start-overlay)) | One line `.show()`; receives `PURCHASE_CREATED`, `WIDGET_CLOSE`, etc. via `.on()` | Z-index conflicts are the #1 reported foot-gun ✅ ([Tips & Tricks](https://docs.rampnetwork.com/tips-tricks)) | Default for most dApps and wallets |
| **Embedded (iframe via SDK)** | SDK mounts the iframe into your DOM container, no overlay | Tight visual integration; no modal | You handle layout, scrolling, mobile sizing yourself | Wallets that want the ramp inline as a "Buy" tab |
| **Native mobile SDK** | iOS (Swift, v4.x), Android (Kotlin), React Native, Flutter ([ramp_flutter v2](https://pub.dev/packages/ramp_flutter)) — each wraps a WebView around the same widget | Native "open / close" lifecycle; postMessage bridge to receive purchase events ([Android SDK docs](https://docs.rampnetwork.com/mobile/android-sdk), [RN SDK](https://docs.rampnetwork.com/mobile/react-native-sdk), [iOS SDK](https://docs.rampnetwork.com/mobile/ios-sdk)) | Still ultimately a WebView — not a true native UI | Native mobile wallets (e.g., a Solana Mobile Saga app) |
| **REST API (host-api v3)** | Server-to-server quotes, asset list, sale-status fetches — but **not a full white-label flow**. The widget still owns checkout/KYC/payments. ✅ ([REST v3 Reference](https://docs.rampnetwork.com/rest-api-v3-reference)) | Pre-fetch quotes, render asset selectors in your own UI, reconcile orders | You can get *quotes* and *order status* but you cannot drive the full purchase from your backend; KYC/payment must still happen inside the Ramp UX | Showing live "you'll receive ~X SOL for $100" before launching the widget; reconciliation jobs |

There is **no fully-headless white-label** mode where the integrator collects card details and Ramp settles purely server-side. The closest thing is **Off-Ramp Native Flow**, where the widget owns fiat/KYC, but emits a `SEND_CRYPTO` event so the integrator's wallet code signs and broadcasts the on-chain crypto transfer locally instead of asking the user to switch to their wallet ✅ ([Off-Ramp Native Flow](https://docs.rampnetwork.com/off-ramp-native-flow/integration)). This is materially better DX than Manual Flow off-ramps (where the user has to copy a deposit address from Ramp into their wallet).

---

## 3. Widget SDK — `@ramp-network/ramp-instant-sdk`

| Property | Value | Confidence |
|---|---|---|
| Latest version | **6.2.0** (web SDK) | ✅ ([npm](https://www.npmjs.com/package/@ramp-network/ramp-instant-sdk), confirmed via [Bundlephobia](https://bundlephobia.com/package/@ramp-network/ramp-instant-sdk)) |
| Last published (web) | ~3 months before query date (i.e., ~Feb 2026) | 🟡 (search snippet, not direct npm fetch) |
| Weekly downloads | ~4,249/week | 🟡 |
| Language | TypeScript, fully typed | ✅ |
| GitHub | [RampNetwork/ramp-instant-sdk](https://github.com/RampNetwork/ramp-instant-sdk), ~38 stars, 17 PRs / 15 merged in past year, ~20h avg PR close time | 🟡 ([Ecosyste.ms issue stats](https://issues.ecosyste.ms/hosts/GitHub/repositories/RampNetwork/ramp-instant-sdk)) |
| iOS SDK | `ramp-sdk-ios` v4.x | 🟡 |
| Android SDK | `ramp-instant-sdk-android` (Kotlin) | ✅ |
| React Native | [`ramp-sdk-rn`](https://github.com/RampNetwork/ramp-sdk-rn) | ✅ |
| Flutter | [`ramp_flutter` v2.0.0](https://pub.dev/packages/ramp_flutter) | ✅ |
| License | Apache-2.0-style (typical for Ramp packages) | 🟡 |

**API surface — minimum viable example** ✅ ([SDK Reference](https://docs.rampnetwork.com/sdk-reference)):

```ts
import { RampInstantSDK } from '@ramp-network/ramp-instant-sdk';

new RampInstantSDK({
  hostAppName: 'My Solana Wallet',
  hostLogoUrl: 'https://mywallet.app/logo.png',
  hostApiKey: process.env.NEXT_PUBLIC_RAMP_API_KEY!, // staging or prod
  swapAsset: 'SOLANA_SOL,SOLANA_USDC',               // pin assets
  userAddress: 'BASE58_SOLANA_PUBKEY',
  fiatCurrency: 'USD',
  fiatValue: '100',
  defaultFlow: 'ONRAMP',                              // or 'OFFRAMP'
  enabledFlows: ['ONRAMP', 'OFFRAMP'],
  webhookStatusUrl: 'https://api.mywallet.app/ramp/webhook?userId=u_123',
  // url: 'https://app.demo.ramp.network'             // staging override
})
  .on('PURCHASE_CREATED', (e) => console.log(e.payload.purchase.id))
  .on('WIDGET_CLOSE', () => closeModal())
  .on('*', (e) => analytics.track('ramp_event', e))
  .show();
```

Constructor accepts ~30 params (most optional): branding (`hostAppName`, `hostLogoUrl`, `variant`), asset pinning (`swapAsset`, `offrampAsset`, `userAddress`), pre-fill (`fiatValue`, `fiatCurrency`, `userEmailAddress`, `userCountry`), flow control (`defaultFlow`, `enabledFlows`, `useSendCryptoCallback`), redirect (`finalUrl`), and webhook routing (`webhookStatusUrl`) ✅ ([Configuration](https://docs.rampnetwork.com/configuration)).

**Events** ✅ ([Events](https://docs.rampnetwork.com/events)):

| Event | When |
|---|---|
| `WIDGET_CONFIG_DONE` | Widget mounted and ready |
| `WIDGET_CLOSE` / `WIDGET_CLOSE_REQUEST_CONFIRMED` | User exits |
| `PURCHASE_CREATED` | On-ramp order created (not yet settled) |
| `OFFRAMP_SALE_CREATED` | Off-ramp sale created |
| `SEND_CRYPTO` (with native flow) | Widget asks integrator wallet to broadcast the crypto leg |
| `*` | Catch-all (great for analytics) |

A nice DX touch: the SDK is chainable (`.on().on().show()`), and `purchaseViewToken` returned on `PURCHASE_CREATED` is the secret you'll later need on the REST status endpoint.

---

## 4. REST API — `api.ramp.network/api/host-api/v3`

| Aspect | Detail | Confidence |
|---|---|---|
| Production base URL | `https://api.ramp.network/api/host-api/v3` (note: also commonly written `api.rampnetwork.com`) | ✅ ([REST v3 Reference](https://docs.rampnetwork.com/rest-api-v3-reference)) |
| Sandbox/staging | Confirmed staging environment exists; demo widget at `https://app.demo.ramp.network` and historical Firebase URL `https://ri-widget-staging.firebaseapp.com/` | ✅ ([Testing Environment](https://docs.rampnetwork.com/testing-environment)) |
| API versions | v1 (legacy), v2 (legacy), **v3 (current)** | ✅ |
| Auth | Query parameter `?hostApiKey=xxx` (not a header). Optional on most read endpoints — supplying it returns `enabledFeatures` listing your custom-enabled features | ✅ ([API Keys](https://docs.rampnetwork.com/api-keys)) |
| Content type | JSON in / JSON out, errors are `{code: "..."}` objects | ✅ |
| Rate limits | "All endpoints are subject to rate limiting" — limit is **per origin IP** | 🟡 ([Rate Limiting](https://docs.rampnetwork.com/rate-limiting)) — public docs do not publish a numeric RPS/RPM limit |
| Idempotency | **Not documented as a first-class feature.** No `Idempotency-Key` header pattern (vs. Stripe). Reads are safe; the user-flow side effects live inside the widget, not the REST API | 🔴 |
| OpenAPI spec | **Not publicly published as a downloadable openapi.json.** TypeScript interface fragments embedded in docs | 🔴 |
| Postman collection | Not officially provided | 🔴 |

### Endpoint catalogue (v3, what's documented)

| Method | Path | Purpose |
|---|---|---|
| `GET` | `/host-api/v3/assets` | List supported on-ramp assets, chains, decimals, min/max purchase, network fees ✅ |
| `POST` | `/host-api/v3/onramp/quote/all` | Quote across all payment methods (CARD, APPLE_PAY, GOOGLE_PAY, MANUAL_BANK_TRANSFER, AUTO_BANK_TRANSFER, PIX). Body: `{cryptoAssetSymbol, fiatCurrency, fiatValue \| cryptoAmount}` ✅ |
| `GET` | `/host-api/v3/onramp/purchase/{id}?secret={purchaseViewToken}` | Fetch purchase status — `id` from the SDK event/webhook, secret is the `purchaseViewToken` 🟡 |
| `POST` | `/host-api/v3/offramp/quote/all` | Off-ramp quote across CARD, AMERICAN_BANK_TRANSFER, SEPA, SPEI, PIX 🟡 |
| `GET` | `/host-api/v3/offramp/sale/{id}?secret=…` | Sale status retrieval 🟡 |

**Example call** ✅:

```bash
curl -X POST 'https://api.ramp.network/api/host-api/v3/onramp/quote/all?hostApiKey=YOUR_KEY' \
  -H 'content-type: application/json' \
  -d '{"cryptoAssetSymbol":"SOLANA_SOL","fiatValue":100,"fiatCurrency":"USD"}'
```

Response includes `appliedFee`, `baseRampFee`, `cryptoAmount`, `fiatValue` per payment method, and an `asset` block (address, chain, decimals, logoUrl, purchase limits) — perfect for rendering an in-house "you'll get X SOL" ticker before launching the widget.

**Verdict on the REST API:** It's a **support API for the widget**, not a replacement for it. There is no equivalent of Stripe's `POST /v1/crypto/onramp_sessions` "create a session, get a client_secret, you handle the rest" pattern. The widget is mandatory.

---

## 5. Sandbox quality

| Question | Answer |
|---|---|
| Does Ramp have a sandbox? | Yes — `app.demo.ramp.network` (web) + staging `hostApiKey` ✅ ([Testing Environment](https://docs.rampnetwork.com/testing-environment)) |
| Self-serve sandbox key? | Partially — getting the staging `hostApiKey` typically still requires emailing partner@ramp.network and filling a form ✅ ([API Keys](https://docs.rampnetwork.com/api-keys), [Getting Started](https://docs.rampnetwork.com/getting-started)). There is **no "sign up, click 'Get test key', start coding in 90 seconds"** Stripe-style developer dashboard. |
| Test cards (e.g., `4242…`)? | **Not officially documented.** Demo environment relies on selecting "Manual Bank Transfer" and switching country to a European one to simulate a successful purchase ✅ ([Are there test payments?](https://support.rampnetwork.com/en/articles/110247-are-there-any-test-payments-available-on-the-demo-environment)) |
| Can you simulate KYC approval? | **No automatic bypass.** Demo still requires KYC. To unlock larger test amounts, you have to email the partnerships team to flag your staging account as "verified" ✅ ([Does staging require KYC?](https://support.ramp.network/en/articles/110152-does-the-staging-environment-require-me-to-do-a-kyc-verification)). This is a real friction point. |
| Can you simulate off-ramp settlement? | The demo connects testnets: Ethereum Sepolia/Rinkeby, Polygon Mumbai, Ronin, Celo Alfajores, Tezos Ghostnet, Flow, **Solana** (devnet) ✅ ([What testnets connect to staging?](https://support.ramp.network/en/articles/13320-what-testnets-connect-to-the-staging-environment)). Other chains (BTC, etc.) are mocked — you won't see a real explorer tx. Min purchase €0.05. |

**Score: 5/10.** A real sandbox exists and supports Solana devnet, but: no published test cards, KYC still required by default, no programmatic webhook simulator, no headless "force purchase to RELEASED" toggle. Compared to Coinbase's `pay-sandbox.coinbase.com/?sessionToken=…&user_id=sandbox-user-1234` ([Coinbase Onramp Sandbox launch post](https://www.coinbase.com/developer-platform/discover/launches/onramp-sandbox)), MoonPay's documented test-card flow ([MoonPay sandbox](https://dev.moonpay.com/docs/faq-sandbox-testing)), and Stripe's `4242 / 000000 / 000000000` triple ([Stripe Crypto sandbox](https://docs.stripe.com/crypto/onramp/api-reference)), Ramp's sandbox is the weakest of the major ramps. 🟡

---

## 6. KYC handoff

Ramp **does the KYC** — the integrator never sees ID docs and never has to integrate a Persona/Onfido/Sumsub flow themselves. ✅ ([What ID verification?](https://support.rampnetwork.com/en/articles/9890-what-id-verification-guidelines-does-ramp-network-follow))

- **Vendors used in the backend (per public sources):** GBG and **Onfido** for EU/UK 1+1 / 2+2 electronic verification 🟡 — attribution slightly uncertain because some Onfido-related help articles surface from the Ramp Business support site (a different company); conservatively treat as "Onfido-class vendor."
- **Sumsub interop:** Documented partnership pattern lets a merchant who already KYC'd a user via Sumsub share the Sumsub `applicantId` with Ramp to bypass duplicate KYC ✅ ([Alchemy Pay's Ramp-shared KYC docs](https://alchemypay.readme.io/docs/ramp-shared-kyc)).
- **Tier structure:** Four tiers based on jurisdiction, asset, frequency. Ramp does not publish exact thresholds publicly.
- **White-label KYC?** No — KYC happens inside the Ramp widget UI under the Ramp brand, not yours. You can co-brand chrome but not KYC.

For a Solana dev: this is a feature, not a bug. Outsourcing KYC to Ramp is the **whole point** of using a ramp instead of building one.

---

## 7. Webhooks

| Aspect | Detail | Confidence |
|---|---|---|
| Events | **On-ramp:** `CREATED`, `RELEASED`, `RETURNED`. **Off-ramp:** `CREATED`, `RELEASED`, `EXPIRED` ✅ ([Webhooks](https://docs.rampnetwork.com/webhooks)) |
| Transport | HTTP POST, JSON body | ✅ |
| Subscription | Per-purchase via `webhookStatusUrl` SDK config (you can append `?userId=…` and Ramp will preserve it) ✅ |
| Signing scheme | **ECDSA secp256k1, sha256 digest**, signature in `X-Body-Signature` header, base64-encoded. Body is canonicalized via `fast-json-stable-stringify` (deterministic key order) before signing ✅ |
| Public key distribution | Ramp publishes a public PEM (`ramp-network.public.pem`); each webhook is signed with their private key — verify with their public key | ✅ |
| Replay protection | **Not built-in.** No timestamp tolerance like Stripe's `t=…,v1=…`. You must idempotency-key on the purchase `id` yourself | 🔴 |
| Secret rotation | Public-key rotation; not customer-managed HMAC secrets | ✅ (this is unusual — most peers use HMAC-SHA256, Ramp uses asymmetric ECDSA) |
| Retry | 4 retries, 3-minute interval, then dropped ✅ |
| Delivery guarantee | At-most ~5 deliveries; **no permanent dead-letter queue** documented | 🟡 |

The ECDSA-instead-of-HMAC choice is interesting. Pros: integrators can verify signatures from a publicly-known key; no shared secret to leak from the integrator side. Cons: it's an unusual pattern that web devs have to look up; libraries like `crypto.createVerify('sha256')` or `secp256k1` work but it's not as one-line as `crypto.createHmac('sha256', secret)`.

**Verifier sketch (Node.js):**

```ts
import crypto from 'node:crypto';
import stringify from 'fast-json-stable-stringify';

export function verifyRampWebhook(body: object, sigHeader: string, pubKeyPem: string) {
  const message = Buffer.from(stringify(body));   // canonical JSON
  const signature = Buffer.from(sigHeader, 'base64');
  const verifier = crypto.createVerify('sha256');
  verifier.update(message);
  verifier.end();
  return verifier.verify(pubKeyPem, signature);
}
```

⚠ **Important gotcha:** if you pass query params on `webhookStatusUrl` (e.g., `?userId=u_123`), do **not** include them when re-serializing for verification — only the JSON payload body is signed ✅.

---

## 8. Pricing for the integrator

Ramp's pricing model has two layers ✅ ([Pricing Policy](https://rampnetwork.com/pricing-policy), [Baseline fees for partners](https://support.rampnetwork.com/en/articles/31326-what-are-the-baseline-fees-for-integration-partners), [How can I earn?](https://support.rampnetwork.com/en/articles/61154-how-can-i-earn-from-my-ramp-network-integration)):

1. **End-user fee = Ramp Network fee + Network fee + (optional) integrator "Fees on Top".** Card payments typically 2.9–4.9%, bank transfer ~0.49–2.9% (figures vary by region/asset/method). 🟡
2. **Integrator revenue:** you set your own "Fees on Top" as a % of net fiat. Ramp recommends staying under ~1% to avoid hurting conversion. ✅
3. **Payouts:** in USDC/USDT. Monthly if accrued ≥ €5,000 / $5,000 in a month, otherwise **every 3 months**. ✅
4. **Negotiable baseline:** large partners can negotiate reduced base fees through partner@ramp.network. ✅

So unlike Coinbase's "0-fee USDC and we eat the cost" pitch, Ramp's model is **closer to Transak**: integrator can earn a take-rate, but the user pays it. There is no built-in "pay the user's fee out of your treasury" path documented.

---

## 9. API key management

- **No public self-serve developer dashboard for Ramp Network.** You request a key via a web form and email follow-up; Ramp issues both staging and production keys ✅ ([API keys explained](https://support.rampnetwork.com/en/articles/13064-ramp-network-integration-api-keys-explained)).
- One key per entity; cannot be shared.
- Production keys gate **enabled features** — you'll get a baseline set; advanced features (custom branding, certain payment methods, off-ramp, native flow) are toggled on Ramp's side and surfaced via the `enabledFeatures` field in the quote response ✅.
- **No per-key permissions / scopes / restricted keys** like Stripe's `rk_live_*` or Vercel's tokens. 🔴
- **Testing without commercial agreement?** You can play with the demo widget on `app.demo.ramp.network` without a key, but to get a real `hostApiKey` you need to fill the form. There's no "instant test keys, sign a contract later" path à la Transak/MoonPay/Stripe.

This is the **biggest friction point for a weekend solo dev** — see §14.

---

## 10. Documentation quality scoring

| Area | Score | Rationale |
|---|---|---|
| Widget integration (web) | **8/10** | Three quick-start pages (hosted/overlay/embedded), copy-pasteable code, full param table, demo repo. ✅ |
| Mobile SDKs | **7/10** | Coverage is solid for iOS/Android/RN/Flutter; example repos exist. Missing: end-to-end "buy SOL on devnet from a Solana Mobile dApp" tutorial. 🟡 |
| REST API | **5/10** | Endpoints are documented as TypeScript interfaces in prose, but **no OpenAPI/Postman**, no comprehensive curl examples, no error catalog. 🟡 |
| KYC | **3/10** | Almost nothing for developers — the topic is split across a marketing blog, support help-center articles, and partner emails. No "what your user will see at each tier, by jurisdiction" matrix. 🔴 |
| Webhooks | **7/10** | Signing scheme documented with Node and Python verifier code; events listed; retry policy explicit. Lacks: timestamp/replay docs, dead-letter handling, simulator. 🟡 |
| Off-ramp (incl. Native Flow) | **7/10** | Native Flow integration page is thorough on `useSendCryptoCallback` + `SEND_CRYPTO`/`SEND_CRYPTO_RESULT` round-trip. Lacks: end-to-end Solana sample. 🟡 |
| Code samples | **6/10** | The [demo-embedded-widget](https://github.com/RampNetwork/demo-embedded-widget) repo exists, plus framework-specific READMEs. No multi-chain reference dApp. |
| OpenAPI / Postman | **2/10** | None published. 🔴 |

**Aggregate doc score: ~6/10.** Strongest where the SDK widget lives, weakest at REST/KYC/sandbox tooling.

---

## 11. Gotchas / common dev pitfalls

From [Tips & Tricks](https://docs.rampnetwork.com/tips-tricks), [Technical Issues collection](https://support.rampnetwork.com/en/collections/195336-technical-issues), and the small set of GitHub issues:

1. **Wrong key in wrong environment** — staging `hostApiKey` against `buy.ramp.network` (or vice-versa) → "Someone made an error integrating Ramp Network." This is the single most common error. ✅
2. **Z-index conflict** — your modal overlay sits above the widget; Ramp recommends raising the widget `z-index` or lowering yours ✅.
3. **CSP / iframe-ancestors** — embedded mode breaks if your Content-Security-Policy doesn't whitelist `*.ramp.network` 🟡.
4. **Card-decline issues** — issuer 3DS rejections are common in EM markets; Ramp's only mitigation is to fall back to bank transfer. No detailed acceptance-rate dashboard surfaced for partners 🟡.
5. **KYC re-prompt loops in demo** — devs frequently can't get past KYC in staging because the demo account gets re-flagged; you have to email partnerships ✅.
6. **`webhookStatusUrl` query-param signature mismatch** — easy to miss that signature only covers JSON body, not the URL custom params; many devs report 400s when verifying ✅.
7. **`swapAsset` symbol naming** — Ramp uses `CHAIN_SYMBOL` notation (`SOLANA_SOL`, `SOLANA_USDC`, `ETH_USDC`, `MATIC_MATIC`). Mixing up `SOL_SOL` vs `SOLANA_SOL` silently filters the asset out 🟡.
8. **Missing required configuration** (no `hostAppName` / `hostLogoUrl`) → widget shows error page instead of starting ✅.
9. **No idempotency key on REST** → duplicate quote requests under flaky network can produce mismatched fees vs what the user sees in the widget 🔴.
10. **Stack Overflow tag is essentially empty** — Ramp Network has very low public Q&A surface; almost all support is via partner email or Intercom on the help center ✅. This means **debugging in production tends to require a partner manager**, not Stack Overflow.

---

## 12. Open-source SDK examples

Confirmed real consumers visible on GitHub / npm / pub.dev:
- [`RampNetwork/demo-embedded-widget`](https://github.com/RampNetwork/demo-embedded-widget) — official reference dApp for the embedded mode ✅
- [`TravisSCode/basicintegramp`](https://github.com/TravisSCode/basicintegramp) — community hosted-mode minimal example ✅
- [`@ramp-network/ramp-instant-sdk` on CodeSandbox](https://codesandbox.io/examples/package/@ramp-network/ramp-instant-sdk) — auto-collated public usages
- Mobile demos: [`ramp-sdk-flutter`](https://github.com/RampNetwork/ramp-sdk-flutter) example app, [`ramp-sdk-rn`](https://github.com/RampNetwork/ramp-sdk-rn) example app
- Wallets that historically ship the SDK: MetaMask, Trust Wallet, Brave Browser, Ledger, Sorare, Axie Infinity, Loopring, GameStop, Opera ✅ ([Quicknode](https://www.quicknode.com/builders-guide/tools/ramp-network-by-ramp-swaps))

For a Solana dev, the absence of a ready-made *Solana-specific* example dApp is notable — you'll be the one writing it. 🟡

---

## 13. Peer comparison matrix

| Capability | **Ramp Network** | MoonPay | Transak | Onramper | Stripe Crypto | Coinbase On-Ramp |
|---|---|---|---|---|---|---|
| Self-serve sandbox key | 🔴 form + email | ✅ instant via dashboard | ✅ instant via dashboard | ✅ 14-day trial via dashboard | ✅ instant in test mode | ✅ instant via CDP |
| Sandbox simulates KYC bypass | 🔴 partial | ✅ "skip docs" button | ✅ documented sandbox creds | ✅ inherits from providers | ✅ `000000` codes | ✅ `sandbox-` user prefix |
| Public OpenAPI spec | 🔴 none | 🟡 partial | 🟡 partial | ✅ yes | ✅ yes | ✅ yes |
| TypeScript SDK | ✅ `@ramp-network/ramp-instant-sdk` | ✅ `@moonpay/moonpay-react` | ✅ `@transak/transak-sdk` | ✅ `@onramper/widget` | ✅ `@stripe/crypto` | ✅ `@coinbase/onchainkit` |
| iOS / Android SDK | ✅ both, plus RN + Flutter | ✅ both | ✅ both + Flutter | ✅ web-first | 🟡 web-first | ✅ both via OnchainKit |
| Webhooks | ✅ ECDSA secp256k1 | ✅ HMAC-SHA256 | ✅ HMAC-SHA256 | ✅ HMAC-SHA256 | ✅ HMAC-SHA256 (Stripe std) | ✅ HMAC-SHA256 |
| Idempotency keys (REST) | 🔴 not first-class | 🟡 partial | 🟡 partial | ✅ | ✅ Stripe-grade | ✅ |
| Published rate limits | 🔴 "exists, not numeric" | 🟡 numeric in docs | 🟡 numeric in docs | ✅ | ✅ | ✅ |
| KYC handoff | ✅ Ramp owns it | ✅ MoonPay owns it | ✅ Transak owns it | ✅ provider-by-provider | ✅ Stripe owns it | ✅ Coinbase owns it |
| Free tier / 0-fee path | 🟡 0-fee USDT/USD only ([April 2026 launch](https://www.theblock.co/post/398354/peter-thiel-backed-unicorn-ramp-rolls-out-0-conversions-between-usdt-and-dollars-across-product-suite)) | 🔴 | 🔴 | 🔴 | 🔴 | ✅ 0-fee USDC |
| Public list price | 🟡 ranges only | ✅ explicit % | ✅ explicit % | 🟡 aggregator | ✅ explicit | ✅ explicit |
| White-label REST checkout | 🔴 widget mandatory | 🟡 partial | 🟡 partner-tier | ✅ "Headless" mode | 🟡 hosted-only | 🟡 |
| Solana SOL on-ramp | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Solana USDC on-ramp | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ (0-fee) |
| Solana USDT on-ramp | ✅ ([Apr 2026](https://thedefiant.io/news/defi/usdt-live-solana-plasma-ethereum-ramp-privy-rt2zgt)) | 🟡 | ✅ | ✅ | 🔴 | 🔴 |
| Time-to-first-test (hours) | **~24–72h** (waiting for key email) | ~1h | ~1h | ~1h | ~30 min | ~1h |

**Honest summary of where Ramp loses points to peers:**
- **Self-serve dev onboarding** is the clearest gap — Transak, MoonPay, Stripe, Coinbase all let you click a button and get a test key. Ramp wants to talk to you first.
- **No OpenAPI / Postman** — measurable artifact deficit.
- **Sandbox is weakest** of the major five.
- **Idempotency / rate-limit transparency** are below industry standard.

**Where Ramp wins:**
- 4 mobile SDKs (web, iOS, Android, RN, Flutter) — broader native footprint than Stripe or Coinbase.
- 0-fee USD↔USDT on Solana is a genuinely competitive feature for stablecoin-heavy products in 2026.
- **Off-Ramp Native Flow** — better UX than MoonPay's "copy address, paste in wallet" off-ramp, comparable to or better than Transak's.
- ECDSA webhook signing is overkill for most use cases but is more robust than shared HMAC.

---

## 14. The "weekend integration" feasibility test

**Realistic timeline for a competent solo Solana dev:**

| Step | Time |
|---|---|
| Read [getting-started](https://docs.rampnetwork.com/getting-started) + [overlay quick-start](https://docs.rampnetwork.com/web/quick-start-overlay) | 30 min |
| Fill the API-key form, send email to integrations@rampnetwork.com | 15 min |
| **Wait for Ramp to reply with staging + prod keys** | **24h–3 business days** ⚠ |
| `npm i @ramp-network/ramp-instant-sdk`, drop in widget with `swapAsset: 'SOLANA_SOL,SOLANA_USDC'`, point to demo URL | 1–2h |
| Wire `PURCHASE_CREATED` and `WIDGET_CLOSE` to your UI | 30 min |
| Stand up `/ramp/webhook` endpoint, verify ECDSA signature | 1–2h (verifier code is non-trivial first time) |
| End-to-end test purchase on demo (Manual Bank Transfer EU country) | 30 min |
| Off-ramp Native Flow with Solana wallet adapter | 3–4h (no Solana-specific sample) |
| Brand polish, error states, decline copy | 2h |

**Pure-coding time: ~1 day. Wall-clock time: blocked by the email loop for the API key.** A weekend integration is feasible **only if you submit the key request on Friday morning and accept that you may not start coding against a real key until Monday.**

By contrast, with Coinbase On-Ramp / Stripe Crypto / Transak, you could go live on a Sunday night.

For the "I want to ship a demo to a hackathon judge tomorrow" case: use **hosted mode + the public demo key on the demo URL** to prototype, but you cannot launch to real users without a production key.

---

## 15. Verdict for a Solana developer

**Use Ramp Network when:**
- You're shipping a **production wallet or dApp** with real users in **Europe/UK** — Ramp's UK FCA registration and EEA Open Banking coverage are a real moat ✅.
- You need **Solana SOL + USDC + USDT on-ramp** with native flow off-ramp inside a self-custodial Solana wallet, and you want **0-fee USDT/USD conversions** as a flagship UX win ✅.
- You're already partner-friendly (have a real product, can fill a form, can wait 1–3 business days for a key).
- You want **good native mobile SDKs** (iOS/Android/RN/Flutter) — Ramp's mobile coverage genuinely outclasses Stripe Crypto and Coinbase On-Ramp here.
- You want **the integrator-fee revenue share** (set your own % up to ~1%, monthly USDC/USDT payouts).

**Don't use Ramp Network when:**
- You need to **prototype tonight** without filling a partner form → use Coinbase On-Ramp (CDP) or Stripe Crypto for instant sandbox keys.
- You need a **fully headless server-to-server flow** where your backend collects card data → Ramp does not offer this, and likely won't (regulatory choice). Use Stripe Crypto if you need Stripe-grade composability, or Onramper's headless mode for aggregation.
- You need a **deep open-source ecosystem** to copy from (Stack Overflow, public OpenAPI/Postman, broad GitHub samples) — Ramp's developer footprint is thinner than peers.
- You're optimizing for **0-fee USDC** on-ramp specifically → Coinbase's USDC 0-fee is the cleaner play unless you specifically want USDT.
- You need **maximum acceptance** in EM/LatAm and don't want to A/B test routes → Onramper's aggregator routinely beats single-provider conversion ([Onramper claims 80%+ vs 40–60% single](https://www.onramper.com/)).

**Concrete recommendation for a Solana dev considering integration:**

1. **Decision tree:** if you need to ship to real Solana mainnet users in EU/UK and want strong stablecoin UX, **email partnerships now** so the key is waiting when you start coding.
2. **Don't pick Ramp as your only ramp** if you have meaningful US/LATAM/APAC volume. Either layer **Onramper** in front to aggregate, or run **Coinbase On-Ramp + Ramp** side-by-side and route by user country.
3. **Build a small reconciliation worker** (cron) that uses the v3 REST `GET /onramp/purchase/{id}` to fix any missed webhook deliveries — Ramp's 4-retry policy is acceptable but not bulletproof, and there is no public dead-letter UI.
4. **Test the off-ramp Native Flow on Solana devnet early.** It is the highest-value Ramp feature for Solana wallets and also the least documented end-to-end.

**One-line takeaway:** Ramp is a **mature, mobile-strong, EU/UK-anchored ramp with very good widget DX and below-average sandbox/REST/devkey DX**, and it's a defensible default for a Solana dApp/wallet that targets European users — provided the developer plans for a 24–72h API-key onboarding lag instead of an instant Stripe-style start.

---

## Sources

- [Welcome to Ramp Network Docs](https://docs.rampnetwork.com/)
- [Getting Started](https://docs.rampnetwork.com/getting-started)
- [SDK Reference](https://docs.rampnetwork.com/sdk-reference)
- [Configuration](https://docs.rampnetwork.com/configuration)
- [Events](https://docs.rampnetwork.com/events)
- [Webhooks](https://docs.rampnetwork.com/webhooks)
- [Tips & Tricks](https://docs.rampnetwork.com/tips-tricks)
- [REST API V3 Reference](https://docs.rampnetwork.com/rest-api-v3-reference)
- [Off-Ramp Native Flow Integration](https://docs.rampnetwork.com/off-ramp-native-flow/integration)
- [API Keys](https://docs.rampnetwork.com/api-keys)
- [Rate Limiting](https://docs.rampnetwork.com/rate-limiting)
- [Testing Environment](https://docs.rampnetwork.com/testing-environment)
- [Web Hosted Quick-Start](https://docs.rampnetwork.com/web/quick-start-hosted)
- [Web Overlay Quick-Start](https://docs.rampnetwork.com/web/quick-start-overlay)
- [Web Embedded Quick-Start](https://docs.rampnetwork.com/web/quick-start-embedded)
- [Mobile Quick-Start](https://docs.rampnetwork.com/quick-start-mobile-apps)
- [Android SDK](https://docs.rampnetwork.com/mobile/android-sdk)
- [iOS SDK](https://docs.rampnetwork.com/mobile/ios-sdk)
- [React Native SDK](https://docs.rampnetwork.com/mobile/react-native-sdk)
- [Flutter SDK](https://docs.rampnetwork.com/mobile/flutter-sdk)
- [npm: @ramp-network/ramp-instant-sdk](https://www.npmjs.com/package/@ramp-network/ramp-instant-sdk)
- [Bundlephobia: ramp-instant-sdk v6.2.0](https://bundlephobia.com/package/@ramp-network/ramp-instant-sdk)
- [GitHub: RampNetwork/ramp-instant-sdk](https://github.com/RampNetwork/ramp-instant-sdk)
- [GitHub: ramp-sdk-flutter](https://github.com/RampNetwork/ramp-sdk-flutter)
- [GitHub: ramp-sdk-rn](https://github.com/RampNetwork/ramp-sdk-rn)
- [GitHub: demo-embedded-widget](https://github.com/RampNetwork/demo-embedded-widget)
- [pub.dev: ramp_flutter](https://pub.dev/packages/ramp_flutter)
- [Help Center — API keys explained](https://support.rampnetwork.com/en/articles/13064-ramp-network-integration-api-keys-explained)
- [Help Center — KYC limits](https://support.rampnetwork.com/en/articles/441-what-are-the-kyc-limits-and-requirements)
- [Help Center — Test payments on demo](https://support.rampnetwork.com/en/articles/110247-are-there-any-test-payments-available-on-the-demo-environment)
- [Help Center — Testnets connected to staging](https://support.ramp.network/en/articles/13320-what-testnets-connect-to-the-staging-environment)
- [Help Center — Baseline fees for partners](https://support.rampnetwork.com/en/articles/31326-what-are-the-baseline-fees-for-integration-partners)
- [Help Center — Off-ramp Native vs Manual](https://support.ramp.network/en/articles/13065-off-ramp-integration-types-native-flow-vs-manual-flow-off-ramp)
- [Pricing Policy](https://rampnetwork.com/pricing-policy)
- [Quicknode — Ramp builders guide](https://www.quicknode.com/builders-guide/tools/ramp-network-by-ramp-swaps)
- [SolanaCompass — Ramp on Solana](https://solanacompass.com/projects/ramp)
- [The Defiant — USDT on Solana with Ramp + Privy](https://thedefiant.io/news/defi/usdt-live-solana-plasma-ethereum-ramp-privy-rt2zgt)
- [The Block — Ramp 0-fee USDT/USD](https://www.theblock.co/post/398354/peter-thiel-backed-unicorn-ramp-rolls-out-0-conversions-between-usdt-and-dollars-across-product-suite)
- [Cointelegraph — Ramp Multichain Wallet launch](https://cointelegraph.com/news/ramp-network-self-custodial-wallet-third-party-dependencies)
- [Alchemy Pay — Ramp shared KYC docs](https://alchemypay.readme.io/docs/ramp-shared-kyc)
- [MoonPay sandbox testing](https://dev.moonpay.com/docs/faq-sandbox-testing)
- [Stripe Crypto onramp API reference](https://docs.stripe.com/crypto/onramp/api-reference)
- [Coinbase Onramp Sandbox launch](https://www.coinbase.com/developer-platform/discover/launches/onramp-sandbox)
