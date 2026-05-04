# Bridge Off-Ramp & Country-Coverage Reality

*The truth about what Bridge actually does end-to-end vs what the marketing implies.*
*Date: 2026-05-04*

---

## TL;DR

**Bridge is much closer to "Stripe of stablecoins for the rich-corridor world" than "global stablecoin payments network."**

- ~5 countries with **production-grade direct fiat off-ramp** (US, EU, UK, MX, BR)
- ~20–30 countries with **Bridge-orchestrated off-ramp via opaque partners** — works, but degraded quality (slower, worse FX, occasional failures)
- The rest of the world: **USDC-to-wallet delivery only** — developer must find their own local off-ramper

The Stripe marketing line *"Stablecoin Financial Accounts in 101 countries"* is about being able to **hold a USDC balance** in those countries — NOT about Bridge being able to convert that USDC into local fiat in 101 countries. Two very different things, conflated on purpose.

---

## How USD → USDC actually happens (the virtual account)

When a developer creates a virtual account for an end-user via `POST /v0/customers/{id}/virtual_accounts`, Bridge issues the user real bank account/routing numbers. The flow when USD arrives:

1. **Bank layer (real USD lands somewhere real).** The virtual account is not a Bridge-issued account — it's actually a **Lead Bank** account (Lead Bank, Kansas City). Lead Bank is also the issuer behind Stripe Issuing, Coinbase debit, Phantom Cash, and many fintech card programs. When ACH/wire lands at the routing/account number Bridge gave you, the dollars sit at Lead Bank, credited to **Bridge's omnibus account**.

   - For non-USD virtual accounts:
     - EUR (SEPA) → **Modulr** (and Bridge's own EU entity, Bridge Building Sp. z o.o.)
     - GBP (FPS) → UK partner (Modulr likely)
     - MXN (SPEI) → undisclosed local Mexico bank partner
     - BRL (Pix) → undisclosed local Brazil bank partner
     - TRY (FAST) → undisclosed local Turkey partner (Cenoa case study confirms)

2. **Stablecoin mint layer (USDC has to come from somewhere).** Authentic USDC can only be minted by Circle. Bridge holds an institutional **Circle Mint** account. But Bridge does NOT call Circle Mint per-transaction (too slow — Circle settles same-day, sometimes T+1). Instead:

   - Bridge maintains an **operational USDC float on each supported chain** (Ethereum, Solana, Base, Tron, Stellar, Polygon, etc.) — pre-positioned inventory pools
   - When user's USD lands at Lead Bank, Bridge instantly releases USDC from that chain's float to the destination wallet
   - Periodically (hourly to daily depending on volume), Bridge **rebalances**: wires USD from Lead Bank → Circle Mint → fresh USDC mint → replenishes the float
   - **Stripe balance sheet acts as backstop** when a chain's float runs dry between rebalances — Stripe covers the temporary gap so payouts don't stall. This is the structural advantage the $1.1B acquisition unlocked.

3. **For other stablecoins:**
   - **USDT** — Bridge sources from market-makers / OTC desks (Tether's mint API has stricter access)
   - **USDB** — Bridge mints directly via its own issuance contract; reserves sit at BlackRock MMFs + Superstate tokenized T-bills + Lead Bank cash
   - **Open Issuance coins (CASH, mUSD, USDsui, USDH, DKUSD, USDSL, etc.)** — Bridge mints on behalf of the issuer; reserves split per Bridge's standard reserve model

4. **Forward-looking (OCC trust charter)**: once Bridge's OCC National Trust Bank charter goes final (conditional approval Feb 12, 2026; expect mid-to-late 2026), Bridge can hold USD reserves directly and reduce dependence on Lead Bank as cash custodian. Circle Mint is still required for USDC mint/burn — that doesn't go away — but the bank-partner layer collapses into Bridge itself.

---

## Recipient KYC — the "customer of customer" model

This is the source of the most confusion. Two layers:

### Layer 1 — Bridge KYBs the developer
Bridge's regulated relationship is with the company integrating it. They check incorporation docs, UBO ownership (≥25% beneficial owners), licensing posture, jurisdiction. Same-business-day KYB.

### Layer 2 — Someone has to KYC the end-users
This splits depending on the developer's business model:

**Model A — Developer holds its own MTL/MSB license** (Felix Pago, Airtm, Slash, ARQ, Cenoa, Phantom for CASH, etc.).
- Developer KYCs senders themselves, basic-info-collects recipients
- Bridge contractually relies on the developer's KYC representations
- Bridge does NOT directly KYC every Carlos sending money to every Maria
- This is the most common pattern — the fintech is the regulated entity for the end-user relationship

**Model B — Developer doesn't want license burden, so Bridge hosts the KYC**
- Developer calls `POST /v0/kyc_links`, embeds the returned URL in their UX
- User clicks through Bridge's hosted KYC flow (Persona under the hood)
- User becomes a Bridge "Customer" record
- Bridge is now the regulated counterparty for that user
- Useful for smaller fintechs, single-purpose apps, or businesses that don't want to be MSBs

### Recipients specifically (the person on the receiving end of fiat)

For most flows, the recipient does NOT do a fresh KYC. Their bank already KYC'd them when they opened the account; Bridge just pushes funds to that account.

What Bridge *does* check on the recipient:
- **OFAC / sanctions screening** on the account-holder name
- **Jurisdiction allowed-list** — can the destination country accept this payment
- **Source-of-funds at higher thresholds** — US: $10K+ triggers extra scrutiny; EU: lower

For larger amounts or some jurisdictions, Bridge requires the recipient to be registered as an `external_account` resource with full beneficiary details (name, address, sometimes ID). But this is registration, not full KYC.

**The nuance:** in remittance flows like Felix→Maria-in-Guadalajara, Maria's only "KYC" is that her BBVA Mexico account already exists. Bridge doesn't need her DOB, ID, etc. — the SPEI rail accepts the push because BBVA has already KYC'd her.

---

## Country coverage — the three tiers

### ✅ Tier 1 — Direct rails (Bridge owns the bank relationship)

End-to-end, single API call, predictable settlement, best FX, best uptime. Five corridors:

| Country | Rail | Banking partner | Live since |
|---------|------|----------------|-----------|
| US | ACH, Wire, RTP, FedNow | Lead Bank | 2023 |
| EU/Eurozone | SEPA | Modulr + Bridge Building Sp. z o.o. | 2024 |
| UK | Faster Payments (FPS) | UK partner (Modulr likely) | Jan 2026 (beta) → Mar 2026 (GA) |
| Mexico | SPEI | Local Mexico bank | April 2025 |
| Brazil | Pix | Local Brazil bank | November 2025 |

This is where Bridge's value proposition is fully intact. Most of the headline customer flows (ARQ, Felix Pago, Slash, Dakota, Stripe SFA) live primarily in this tier.

### 🟡 Tier 2 — Bridge-orchestrated via partner

Bridge has under-the-hood partnerships with local PSPs/exchanges. The developer still calls `POST /v0/transfers` with destination=local fiat and Bridge routes through the partner — the partner is opaque to the developer. So the developer is NOT on their own; they just get a thinner, less reliable, more-spread-y rail.

What "thinner" means in practice:
- Settlement times less predictable (minutes to hours rather than seconds)
- FX worse than Tier 1 (typically wider than the 1% disclosed cap; quoted per-transfer)
- Occasional partner failures requiring developer to handle retries
- Compliance edge cases where the partner rejects but Bridge had quoted

Approximate Tier 2 country list (not all publicly confirmed by Bridge):
- **LATAM (beyond MX/BR):** Argentina, Colombia, Peru, Chile, Ecuador — partners include Bitso, Koibanx
- **Africa:** Nigeria, Kenya, Ghana, South Africa — Yellow Card and similar aggregators
- **Turkey:** local partner via FAST (Cenoa case study confirms it works)
- **APAC:** Philippines, Vietnam, Indonesia — local partners

### 🔴 Tier 3 — Wallet-only (Bridge stops at USDC delivery)

For most countries outside the above two tiers, Bridge really is just delivering USDC to a wallet address. The developer has to find their own local off-ramper. Bridge effectively ends at "USDC to wallet"; the last-mile fiat conversion is the developer's problem.

Includes most of Asia (outside SE Asia partner countries), most of the Middle East, most of Africa beyond the Yellow Card-covered set, and any sanctioned/restricted jurisdictions where Bridge cannot route at all (Iran, NK, Cuba, Russia, etc.).

---

## On-ramp coverage (receiving into a virtual account)

The on-ramp side is **even narrower** than off-ramp because issuing a local-currency virtual account requires a bank-account-issuance relationship in that country.

Confirmed live:
- US (Lead Bank — full ACH, wire, RTP, FedNow account/routing)
- EU (Modulr — virtual IBANs)
- UK (Modulr/partner — virtual sort code/account #)
- Mexico (April 2025 — virtual CLABE for SPEI)
- Brazil (November 2025 — virtual BR code for Pix)
- Turkey (via Cenoa-style integration — virtual TR account for FAST)

Everywhere else: the user can hold a USDC balance, but cannot receive a local-currency deposit through a Bridge-issued virtual account.

---

## The marketing-vs-reality gap

Stripe markets *"Stablecoin Financial Accounts in 101 countries."* What this actually means:

- **A business in those 101 countries can hold a USDC balance with Stripe** ✅
- A business in those 101 countries can off-ramp USDC into its local currency on a production-grade rail ❌ (only ~5 countries qualify)
- A business in those 101 countries can issue virtual accounts in its local currency ❌ (only ~6 countries qualify)

The 101-country claim is about **holding** stablecoins, not about **cashing out to local currency** or **issuing local virtual accounts**. The off-ramp coverage is closer to ~5 production-grade direct-rail countries plus ~20-30 partnered countries with degraded quality.

---

## What this reveals about Bridge's actual business

1. **The real moat in Tier 1 is the bank-partner stack** (Lead Bank for USD, Modulr for EUR/GBP, undisclosed locals for MXN/BRL/TRY) plus the forthcoming OCC trust charter. This is hard to replicate but geographically narrow.

2. **The $20-25B annualized commercial scale is heavily concentrated in Tier 1 + LATAM-2 traffic**, not evenly distributed across the 101-country marketing claim. SpaceX/Starlink, Coinbase, Stripe SFA, Phantom Cash, ARQ, Felix Pago, Airtm, Cenoa, Slash, Dakota — substantially all their volume routes through the Tier 1 rails on at least one side.

3. **Open Issuance is partly a way to push the off-ramp problem onto issuers.** Phantom owns CASH→USD off-ramp UX inside the Phantom app; MetaMask owns mUSD→EUR via the MetaMask Card; Sui owns USDsui ecosystem off-ramp. Bridge issues the coin, the issuer's app handles the last mile. This lets Bridge expand "issuance footprint" without actually having to build off-ramp rails.

4. **The Stripe acquisition is more about the bank-partner relationships and the Stripe balance-sheet backstop than the API itself.** Pre-acquisition Bridge was a great API; post-acquisition Bridge is a great API with material liquidity backing it up and an OCC charter coming online.

5. **The competitive opportunity space sits in Tier 3.** Markets where Bridge stops at USDC-to-wallet are markets where a focused vertical/corridor-specific competitor with their own bank-partner stack on the destination side can carve out real ground — exactly the gap BVNK occupied before Mastercard acquired them in March 2026.

---

## Honest one-liner for Bridge

> "USD/EUR/GBP/MXN/BRL stablecoin orchestration with Stripe-grade liquidity, plus a Circle-Mint-style USDC mint/burn API everywhere else. Marketing wraps that as a global financial OS, but the actual production-grade off-ramp surface is a five-country list."
