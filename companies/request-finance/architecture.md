# Request Finance — Architecture

*Product modules, the custody/money-movement model, chains, multisig, fiat, tax, integrations, fees, tech*
*Compiled 2026-06-06*

Confidence: ✅ high · 🟡 medium · 🔴 low/inferred.

---

## 1. Product modules

Markets itself as "Bill.com + NetSuite + Expensify for crypto and fiat." ✅
- **Accounts Payable** — AI OCR bill capture ("Smart Invoice Capture") → custom approval workflows (auto-assign approvers, email notify) → **batch-pay hundreds of vendors in one click across chains/currencies**; scheduling, vendor DB, audit-ready records.
- **Accounts Receivable / Invoicing** — create/send fiat- or crypto-denominated invoices; payer gets a link, pays in their chosen token, you receive your specified token **directly in your own wallet**. Recurring invoicing at protocol level.
- **Payroll / batch payments** — reusable templates, pay hundreds of contractors/employees monthly via CSV, individually or batch.
- **Expenses** — submission/approval + corporate cards (virtual + physical) on newer plans.
- **Accounting ("Request Accounting," ex-Consola Finance)** — crypto bookkeeping, reconciliation, cost-basis, reporting; competes with Cryptio/Bitwave/TaxBit rather than depending on them.

## 2. The custody / money-movement model (the critical section)

**Crypto AP/AR/payroll = genuinely non-custodial.** ✅
- An invoice = an on-chain **Request** (payer, payee, amount, wallet, chain, currency, due date encoded in a Request ID).
- The API **returns unsigned transaction calldata; the integrator/user signs & broadcasts.** Request never holds keys or funds. Smart contract pays payee **wallet-to-wallet, directly.**
- Payment detection is **reference-based** (subgraphs/The Graph watch the chain to mark invoices paid). Request *observes*; it doesn't move money.

**Contrast with the TradFi AP incumbents:**

| | Money model | Float? |
|---|---|---|
| **Bill.com** | FBO clearing accounts — pulls customer funds, holds during clearing | **Yes — earns ~$162M float** |
| **Tipalti** | Customer **pre-funds** a non-interest account; Tipalti disburses | No customer interest; FX-spread monetized |
| **Request (crypto spine)** | Payer wallet → payee wallet, atomic on-chain | **None — holds nothing, pre-funds nothing** |

This is a structurally different model and Request's genuine differentiator — *the same one Decimal has* (self-custody, no FBO float).

**The hybrid caveat — where Request now DOES touch money:** ⚠️
- **Crypto→fiat off-ramp** (Request Technologies / ex-Pay.so): crypto converted to fiat, settled to a bank via a regulated partner after KYB. Routes value through partner infra. 🟡
- **Global USD Account:** a fundable, custodial-style fiat balance held with an (undisclosed) banking partner. 🔴
- **Corporate cards** + **Aleo private payments** use **custodial partner wallets.** 🟡

→ Non-custodial on the crypto side; **fintech-like custodial on the fiat side** since 2024–26. The clean "no custody" claim is now only partially true.

## 3. Chains & stablecoins ⚠️ (consumer app vs developer API differ)

- **Consumer app / currency registry:** broad — markets "18 blockchains and 350+ cryptocurrencies," registry lists 40+ incl. Ethereum, Polygon, Arbitrum, Optimism, Base, Gnosis, BNB, Avalanche, Celo, Tron, **Solana (+ devnet)**, Sui, Ton, Starknet, Bitcoin, etc. So **Solana is technically listed** — but peripheral. 🟡
- **Developer API:** narrow, EVM-first — Ethereum, Arbitrum, Optimism, Base, Polygon, BNB + Tron (non-EVM) + Sepolia. **Solana is NOT in the API.** Cross-chain USDC on 5 EVM chains; only native USDC (no bridged USDC.e). ✅
- **Reality:** architecturally EVM-first; Solana ~6% of transactions. Treat Solana as listed-but-peripheral, not first-class. 🔴

Stablecoins: USDC (native), USDT, DAI, EURC; invoices can be fiat-denominated, crypto-paid. ✅

## 4. Multisig / approvals ✅

- **Native Gnosis Safe integration** (connect a Safe in-app or open Request inside the Safe Apps sidebar).
- Internal approver routing (email-notified) + batch approve.
- Approval and payment split into two steps so multisig signers see exactly what's paid; batch-pay via Safe's MultiSend (many transfers, one tx); 2nd+ signer co-signs in Request or in Safe.
- Thresholds inherit from the Safe's m-of-n policy + Request's approver routing. Newer "Finance Controls" adds spend policy on the fiat/card side.

## 5. Fiat support ✅

Far more than crypto-only now:
- **Rails:** ACH, Wire, SEPA, SWIFT, SPEI (MXN), Faster Payments (GBP) + stablecoins.
- **Crypto→fiat off-ramp:** pay in USDC (Polygon/Ethereum/Arbitrum) → recipient gets fiat; 15+ fiat currencies, 190+ countries; KYB required; 1–3 business days.
- **Fiat-in:** Global USD Account funded by bank transfer/card.

## 6. Tax / compliance 🟡

- Strong **audit trail** (tamper-proof on-chain record per invoice, receipt matching, one-click auditor export).
- MiCA-readiness; KYB for fiat.
- **W-8/W-9 collection + 1099 generation: UNCONFIRMED** — no clear evidence of a native US tax-form module like Tipalti/Trolley/Deel. **Likely a real gap vs Tipalti.** 🔴

## 7. Accounting integrations ✅

Two-way sync with **QuickBooks Online, Xero, NetSuite** (NetSuite gated to top plan); CSV fallback; native **Request Accounting** (ex-Consola) for crypto bookkeeping/cost-basis/reporting.

## 8. Fees / pricing ⚠️ (model shifted)

- **Legacy crypto-invoice model:** no subscription; **payer pays 0.1%/invoice capped at $2.** ✅
- **Current subscription model:** Basic **$250/mo** (5 users/cards, 1 virtual acct) · Pro **$500/mo** (20 users/cards, 3 accts, accounting integrations) · Premium **$1,250/mo** (unlimited, 5 accts, NetSuite). ~17% off annual.
- **Transaction fees:** **0 processing fee on stablecoin payouts**; **fiat payouts 0.5% flat + rail fee** (ACH/Wire $10, SWIFT $30); funding fees 0.10% stablecoin / 0.20% USD / 0.60% EUR/BRL/MXN/GBP.
- **Revenue model:** subscriptions (primary new lever) + **fiat off-ramp/funding fees** + likely card interchange + legacy 0.1% crypto fee. → Request now monetizes like a fintech on the **custodial fiat side**, while the non-custodial crypto rail is near-free.

## 9. Tech architecture ✅

- **Request Network protocol** (Ethereum-anchored; not a chain). Request metadata stored on **IPFS**, CIDs anchored on **Gnosis Chain**; **The Graph** subgraphs index events for payment detection; invoice details can be encrypted off-chain.
- **Developer API (api.request.finance):** REST/JSON, API-key or OAuth; `POST /invoices` (off-chain draft) → convert to on-chain request (returns requestId + payment links) → `GET` status. **Returns unsigned calldata; integrator signs (non-custodial).**
- **Recurring payments:** EVM-only, EIP-712 + ERC-20 permit; not on Tron.
- Related standard: **ERC-7856** (chain-specific payment requests). 🟡

---

## What Decimal should take from this

Request proves the **non-custodial, wallet-to-wallet, multisig-gated AP model works at $1B+ scale** — validation for Decimal's core architecture. But two structural facts define the opening:
1. **Request is EVM-first; Solana is peripheral.** Decimal's Solana-native + Squads-native stack is a genuinely differentiated rail position.
2. **Request's hybrid drift (custodial fiat off-ramp, Global USD Account, accounting acquisitions, US tax-form gap) maps the exact table-stakes Decimal will face next** — and where Decimal can either partner (off-ramp via Bridge/BVNK; tax via Trolley/Toku) or build.
