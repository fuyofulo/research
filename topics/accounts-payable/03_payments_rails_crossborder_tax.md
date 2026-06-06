# 3 — Payments, Rails, Cross-Border & Tax

*How money actually leaves the company — and the compliance attached to it.*

## The payment rails (cost / speed / use)

| Rail | Cost (typical) | Speed | Reversible? | Best AP use |
|---|---|---|---|---|
| **Paper check** | ~$3–6 all-in (est.) | Days | Yes (stop-pay) | Long-tail vendors, no bank details, float |
| **ACH (standard)** | ~$0–1.50 | 1–2 biz days | Limited | Default bulk US B2B |
| **Same-Day ACH** | low + premium | Same day | Limited | Faster B2B (limit rising to **$10M, Sept 2027**) |
| **Wire (Fedwire/CHIPS)** | $15–30 domestic | Minutes–same day | **No** | High-value, urgent, final |
| **Virtual / commercial card** | buyer *earns* 1–2% rebate; supplier pays ~2–3% | ~instant auth | Chargeback | Where supplier accepts; rebate + float |
| **RTP / FedNow** | ~$0.25–1 | Instant, 24/7 | **No** | Just-in-time supplier pay, Request-for-Payment |
| **SWIFT correspondent** | $30–50+ + 1–3% FX spread | 1–5 days | Hard | Cross-border default (legacy) |
| **Local rails + central FX** | low + tighter FX | same-day/instant last leg | varies | Modern cross-border |
| **Stablecoin** | low marginal + on/off-ramp FX | near-instant, 24/7 | **No** | Cross-border, hard corridors (emerging) |

**Key mechanics to know:**
- **ACH** = batched, not real-time, banking-days only. Governed by **NACHA** rules; switched by two operators (FedACH, The Clearing House EPN); **ODFI** = payer's bank, **RDFI** = supplier's bank. B2B credits use SEC codes **CCD/CTX**. Same-Day ACH limit path: $25K → $100K (2020) → $1M (2022) → **$10M (Sept 17, 2027)**.
- **Wire** = real-time gross settlement, **irrevocable** — a key fraud risk (no clawback). Fedwire (Fed) + CHIPS (The Clearing House).
- **Virtual cards** = buyer earns a **rebate** (~1–1.5%, funded by interchange) + float; **the supplier eats the ~2–3% fee** → the well-known **"acceptance problem"** (20–35% self-serve acceptance, 70%+ in managed mid-market programs). Visa moved B2B vCard interchange to a flat ~2% (Oct 2025) to ease resistance.
- **RTP (2017, The Clearing House) + FedNow (2023, Fed)** = instant, 24/7, irrevocable, ISO 20022 (rich data + Request-for-Payment). **>$2T combined in 2025**; RTP alone ~$1.3T (up ~428% YoY). Frictions: value caps, many banks can *receive* but not *send*, irrevocability.
- **Why US checks persist** (a genuine US anomaly): remittance data on the stub, universality (anyone with an address, no bank-detail collection), float, ERP inertia — despite checks being the **most-defrauded** instrument.

## Cross-border AP — why it's hard

A **stack of frictions**, each adding cost/time:
1. **FX conversion margin** — the biggest *hidden* cost. Providers quote worse than the interbank/mid-market rate and pocket the **spread (~1–3%+)**, usually un-itemized and larger than the explicit wire fee.
2. **Explicit wire fees** (~$30–50+).
3. **Intermediary/correspondent "lifting" fees** — each correspondent bank in the chain can deduct a fee (OUR / SHA / BEN charge options decide who pays).
4. **Beneficiary bank receiving fee.**
5. **Float** captured during multi-day transit.

**SWIFT is a *messaging* network, not a rail** — money actually moves via **correspondent banking** (chains of banks holding **nostro/vostro** accounts), which is why it's slow, opaque, unpredictable. The **modern fintech model**: convert FX once at a tighter spread, then **pay out over the destination country's local rail** (SEPA, UK Faster Payments, India IMPS/UPI, Brazil Pix, Mexico SPEI), collapsing the correspondent chain. Bank-detail format mismatches (IBAN vs routing vs IFSC vs sort code) are a major source of payment errors.

## Float & working capital

Payment *timing* is a financial decision, not just operational:
- **DPO (Days Payable Outstanding)** = (AP ÷ COGS) × days. **Higher DPO = cash held longer = better buyer working capital** — but stretching it strains suppliers. APQC median ~**40 days**.
- **Early-pay / dynamic discounting** — buyer uses its own cash to pay early for a discount (e.g., 2/10 net 30); the implied annualized return often beats money-market yield.
- **Supply-chain finance / reverse factoring** — a **third-party funder** pays the supplier early based on the *buyer's* (stronger) credit; buyer repays the funder at the original due date. *(Cautionary tale: Greensill's 2021 collapse — SCF can disguise debt as trade payables and is funding-fragile.)*
- **Who earns the float:** in a direct bank payment the buyer holds it until funds leave; via a **platform/FBO model**, the platform earns it. An **FBO ("For Benefit Of") account** is a pooled custodial account a platform holds *on behalf of* customers; while customer money sits there in transit, **the platform/partner bank earns interest** — which can be a *primary* revenue line, and creates a conflict of interest (slow payments can be profitable for the intermediary). *(This is the structural fact behind the Bill.com float-revenue model in the company research.)*

## Vendor onboarding & banking validation

- **Validate bank details:** routing+account (US), IBAN+BIC (EU/world), sort code (UK), IFSC (India) — each with checksum rules. **Micro-deposits** (confirm tiny test amounts) or instant account-verification prove account control.
- **Payment-error prevention:** format/checksum validation, **name-on-account matching** (UK Confirmation of Payee; EU **Verification of Payee mandated Oct 2025**), and detecting bank-detail changes.
- **BEC is the dominant fraud vector** — impersonation + changed bank details. Defense: out-of-band callback verification, dual approval, locked vendor master.
- **Sanctions/OFAC screening** — paying a sanctioned party (SDN list) is **strict-liability**. **KYB** verifies the supplier is a real entity (UBOs, incorporation, tax IDs).

## Tax & compliance

**US information reporting & withholding:**
- Collect the right form *first*: **W-9** (US persons, captures TIN) or **W-8 series** (foreign: W-8BEN individuals, W-8BEN-E entities, plus ECI/IMY/EXP).
- Year-end: **1099-NEC** (services ≥ $600 to non-employees; threshold **rising to $2,000 from 2026** — verify effective year), **1099-MISC** (rents/other), **1042-S** (US-source income to foreign persons, with Form 1042).
- **TIN matching** against IRS records prevents B-notices; missing/invalid TIN triggers **24% backup withholding**. *(Clean W-9 + TIN-match at onboarding prevents a costly withholding burden later.)*

**VAT/GST:** on the payables side, the buyer cares about **input VAT** — recoverable *only if the supplier invoice is valid/compliant*. A bad invoice = lost VAT deduction (a direct cash cost). **Reverse charge** shifts VAT accounting to the buyer in many cross-border B2B cases.

**E-invoicing mandates / Continuous Transaction Controls (CTC) — the 2025–2027 wave (important):**
- A government requirement that invoices be issued in a **structured electronic format** and often **reported to/cleared by the tax authority**. Two models: **clearance/CTC** (tax authority validates *before/at* issuance — pioneered in LATAM) vs **post-audit** (audited later — the old EU model, being replaced).
- **Why it matters for AP:** the *buyer* can increasingly only receive, validate, and (for VAT) deduct invoices that are properly cleared/structured — changing AP from "key in a PDF" to "ingest structured data + verify clearance."
- **Status:** LATAM mature (Brazil NF-e, Mexico CFDI/SAT/PAC, Chile). EU transitioning under **ViDA** (adopted Mar 2025; intra-EU B2B e-invoicing + digital reporting mandatory **2030**) — France (Sept 2026 receive / phased issue), Germany (receive since Jan 2025, issue from 2027), Poland KSeF (live Feb 2026), Belgium Peppol (Jan 2026). India GST e-invoicing (IRP/IRN, threshold ₹5cr). Malaysia MyInvois (phased through 2026). **Peppol** is the dominant interoperability network (~1.4M companies).

## Stablecoins in B2B AP (2025–26 snapshot)

Stablecoins (USD-pegged tokens, chiefly **USDT/USDC**) are moving into real B2B flows, mainly to solve cross-border friction. Directional figures (methodology-dependent): **~$226B B2B stablecoin payments in 2025** (~60% of "real-economy" stablecoin payments, ~733% YoY); monthly B2B volume rose from <$100M (early 2023) to >$3B (mid-2025); Visa's stablecoin settlement ~$4.5B annualized run-rate (Jan 2026). Enablers: Stripe/Bridge, Circle (USDC, MiCA-compliant), Visa/Mastercard settlement. Regulatory tailwind: US **GENIUS Act (2025)** + EU **MiCA**. **Honest caveats:** on/off-ramp FX still costs money, accounting/tax treatment is unsettled, sanctions/AML still apply, and **vendor willingness to receive stablecoins is the limiting factor** — the same acceptance problem that dogs virtual cards.

→ Next: [04_controls_fraud_roles_audit.md](./04_controls_fraud_roles_audit.md)
