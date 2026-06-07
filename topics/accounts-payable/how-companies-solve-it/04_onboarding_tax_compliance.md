# Stage 4 — Vendor Onboarding + Tax + Compliance

*The front of the funnel — and the least-automated stage (~7% fully automated). Pure table-stakes: get it wrong and you can't pay, pay a fraudster, or eat an IRS/OFAC penalty. This is where the build-vs-partner line is sharpest, and where crypto-native AP is thinnest.*

## The problem

Self-service **supplier onboarding portal** (vendor enters own bank/tax data; PII stays current) · **bank-detail validation** (checksum/format per geography, micro-deposits or instant verification, **name-on-account matching** — EU Verification of Payee mandated Oct 2025) · **BEC/bank-change fraud defense** (the #1 vector, ~$2.8B/yr, 63% of orgs — locked vendor master + out-of-band callback + dual approval) · **KYB** · **OFAC/sanctions** (strict-liability) · **tax-form collection** (W-9 / W-8 family; missing TIN → 24% backup withholding) · **1099/1042-S filing + TIN matching** · **VAT + the 2025–27 e-invoicing-mandate wave** (turns AP from "key a PDF" to "ingest structured data + verify clearance").

## How each company solves it

| Company | Onboarding | Bank validation | KYB/OFAC | Tax forms | 1099/1042-S | TIN match | Verdict |
|---|---|---|---|---|---|---|---|
| **Tipalti** | ● Supplier Hub (27 langs) | ~26K payment rules | OFAC at onboarding **+ every payment** | W-9/W-8/8233 | **● e-file via Tax1099** | daily | **tax-as-moat (KPMG-reviewed)** |
| **Trolley** *(cluster)* | ● white-label portal | TradFi rails | KYB/OFAC | W-9/W-8 | **● deepest: 1099+1042-S+DAC7+OECD** | yes | **the blueprint to copy** |
| **Toku** *(cluster)* | EOR onboarding | partner-rail | EOR-grade | W-8/W-9 | payroll-side | yes | **token-comp tax (409A/83b)** — unique |
| **Rise** *(cluster)* | payroll onboarding | smart-contract; FinCEN MSB | KYB; SOC2; EOR/AOR | W-8/W-9 | 1099 | yes | solid but generic |
| **Bill.com** | BILL Network (~7M) | ACH micro-deposit | MSB BSA/OFAC | **W-9 Agent** (AI) | not native (partner) | not surfaced | collection automated, filing thin |
| **Routable** | ● white-label PII-holding | **Plaid** | **KYB via AiPrise/Trulioo** | W-9/W-8 | 1099/1042 | yes | strong TradFi orchestration |
| **Ramp** | light | bank verify | MSB OFAC/BSA | collect W-9 | limited | not surfaced | card-led; AP-tax not the focus |
| **Stampli** | around invoice hub | Direct Pay | Billy fraud detect | light | **not a focus** | no | UX leader; thin on tax |
| **Vic.ai** | Plaid Vendor Portal | Plaid | light | not surfaced | not surfaced | no | AI leader; tax not the pitch |
| **Request Finance** | crypto + fiat-KYB only | wallet addr; fiat KYB via VASP | KYB for fiat (Lithuania VASP) | **✗ GAP (unconfirmed native)** | **✗ likely none** | no | **real AP-tax gap** |
| **Altitude** | Grid API | PSP-bridged | **KYB via Sumsub** (enterprise tier) | **✗ none** | **✗ none** | no | **KYB-only; no AP-tax** |

## The spectrum — tax/compliance as moat vs thin

```
MOAT ◄──────────────────────────────────────────────────────► GAP
Trolley   Tipalti    Routable   Rise   Bill.com   Ramp/Stampli/Vic   Request   Altitude
└─ payout/mass-payment specialists ─┘                   └── crypto-native: thinnest ──┘
```

The deepest tax/compliance lives in the **payout specialists** (Trolley, Tipalti) and their cousin Routable — because their customers pay thousands of distributed/foreign payees, forcing them to own onboarding+tax or be useless. **AI-spend platforms** (Ramp/Stampli/Vic.ai) treat tax as a checkbox. **Crypto-native AP (Request, Altitude) are the thinnest of all** — they solved wallet-to-wallet movement and KYB-for-fiat, but neither ships native W-8/W-9 → 1099/1042-S. None of the crypto-native players (nor any of these companies) ships e-invoicing/CTC clearance — an industry-wide gap.

## Build implication — the sharpest build-vs-partner line in the whole pipeline

**BUILD (product differentiation):**
- **Self-service onboarding portal** — the white-label, PII-holding portal is the durable moat + data asset (Routable spent 8 years on it; it's Tipalti's signature "Supplier Hub"). For crypto-native: wallet-address validation + change controls.
- **Bank-detail validation + vendor-master fraud controls** — checksum/format, micro-deposit orchestration, name-matching, **locked vendor master with out-of-band callback on bank changes + dual approval + audit trail.** This is where BEC is defeated and is a trust differentiator.
- **ERP sync** (Stage 5) — table stakes, own it.

**PARTNER / WHITE-LABEL (regulated, penalty-bearing, specialist depth you won't beat):**
- **Tax filing (W-8/9 → 1099/1042-S → DAC7, TIN matching)** — partner **Trolley** (or **Toku** for token-comp). Even Tipalti partners Tax1099.com for e-filing.
- **Sanctions/OFAC** — partner a screening vendor (strict-liability; don't roll your own).
- **KYB** — partner **Sumsub** (Altitude), **Persona, AiPrise/Trulioo, Plaid**.
- **VAT / e-invoicing clearance** — partner a **Sovos/Pagero/Peppol-access-point** type (a moving regulatory target across dozens of jurisdictions).

**The hard part:** the further right you go (tax, sanctions, e-invoicing), the more it's **liability, not features** — strict-liability OFAC, IRS B-notices/backup-withholding, lost input-VAT, a per-country-per-year mandate wave. That's why it's the least-automated stage and **a table-stakes gap most crypto-native AP products haven't solved.** A crypto-native AP product that **builds** the buildable pieces (onboarding portal, bank/wallet validation, fraud-locked vendor master, ERP sync) and **partners** the regulated pieces (Trolley/Toku for tax, Sumsub for KYB, a screening vendor for OFAC, Sovos-type for e-invoicing) closes the exact gap that makes Request and Altitude thin today — on the open Solana rail nobody occupies.

*Gaps: TIN-matching confirmed native only for Tipalti; e-invoicing/CTC not a shipped feature for any company in the corpus (industry-wide gap); BILL native 1099 e-filing unconfirmed (inferred thin/partner).*
