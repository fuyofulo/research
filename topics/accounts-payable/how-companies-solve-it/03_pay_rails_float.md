# Stage 3 — Payment: Rails, Money-Movement Model & Monetization

*The economic core: how money leaves, whether they hold float, and how they make money on payments.*

## The problem

**Rails** each have a cost/speed/reversibility profile (check ~$3–6; ACH ~$0–1.50/1–2d; Same-Day ACH → $10M limit Sept 2027; wire $15–30 irrevocable; RTP/FedNow instant 24/7; virtual card — buyer earns ~1–2% rebate, supplier eats ~2–3% = the "acceptance problem"; cross-border SWIFT $30–50 + **1–3%+ hidden FX spread** vs local rails; stablecoin emerging).

**Four money-movement MODELS** (the economic core):
1. **FBO / float-clearing** — platform pools customer cash, holds in transit, **earns the interest** = revenue + structural conflict (slow pay is profitable). → Bill.com, Melio.
2. **Customer pre-fund (non-interest)** — customer funds a non-interest account; platform monetizes elsewhere. → Tipalti.
3. **Payments-as-commodity (no float)** — refuses to hold/float; monetizes software. → Stampli, Mercury.
4. **Self-custodial on-chain** — wallet→wallet atomic; **float collapses to zero**; the issuer earns reserve yield. → Request, Altitude.

## How each company solves it

| Company | Rails | Model | Float? | Monetization |
|---|---|---|---|---|
| **Bill.com** | ACH/check/wire/card (batch, no RTP) | **FBO clearing** | **YES — depends on it** | txn ~$866M + **float ~$162M (~11%, compressing)** + sub + hidden intl FX |
| **Tipalti** | Global ACH (local rails) + SWIFT + card; 196 countries | customer pre-fund (non-interest) | customer earns $0; Tipalti's own float undisclosed | **FX spread 1.5–3.5% (hidden in rate)** + platform fee + per-txn + implementation |
| **Stampli** | ACH/check/vCard/intl | **no float** ("payments are a commodity") | **NO** | **SaaS subscription**; payment fees minimal |
| **Vic.ai** | VicPay (own rails) | funding account (FBO-like) | undisclosed | SaaS + likely interchange/float; no US txn fee |
| **Ramp** | card-led + ACH/check/wire | no-hold (partner banks) | no AP float | **card interchange** (core) + sub |
| **Request Finance** | wallet-to-wallet 18 chains + fiat off-ramp | **self-custodial** (crypto); custodial on fiat | **NO** on crypto | **0 fee on stablecoin payouts**; sub (new primary) + **0.5% off-ramp** + funding fees |
| **Routable** | ACH/RTP/FedNow/SWIFT **+ stablecoin (Brale)** | prefunded balance (FBO-like) | yes (balance) | sub ($1,250/mo) + per-txn |
| **Altitude** | USDC/Solana + ACH/SEPA via PSPs | **self-custodial** smart-account | **NO** | **reserve-yield "rewards" spread** + card interchange; "no platform fees" |
| *Melio* | ACH free/card 2.9%/check/instant | **FBO** (Evolve) | **YES** | card take-rate + float + syndication (~35%) |
| *Mercury* | direct bank→vendor ("no middleman") | deposit-banking, no FBO | **NO AP float** | net interest margin on deposits + interchange |

## The central contrast — float-middleman vs no-float vs self-custodial

- **Float-middleman (BILL, Melio):** an FBO account sits between payer and payee; the platform/partner bank earns the interest. For BILL it's explicit, material, disclosed (~$162M, ~11%) — and embodies the conflict: **slow payments are profitable.** It's ~100% margin but **rate-cycle-fragile** (compressing every quarter). BILL's own audit calls float *"a vulnerability disguised as revenue."*
- **No-float (Stampli, Mercury):** refuse the float game, monetize software. Stampli's *"payments are a commodity, not a revenue generator"* is the **TradFi-side validation of the on-chain thesis** — a respected AP leader voluntarily gives up float/interchange and still builds a business.
- **Self-custodial on-chain (Request, Altitude):** wallet→wallet, float collapses to zero. The economics don't disappear — they **move upstream to who earns the stablecoin reserve yield** (the issuer, e.g. Circle). **Altitude's key innovation:** it can't pay "interest" (GENIUS Act bars *issuers* from yield), so as a *third party* it collects the reserve interest as "incentives" and **rebates a discretionary slice as "rewards," keeping the spread.** The float BILL captures as a middleman becomes, on-chain, reserve yield captured at the issuer level and partially shared *back to the customer* — a more transparent, customer-favorable locus.

## Spectrum — what each monetization costs the customer

| Monetization | Hidden cost | Transparency |
|---|---|---|
| Float income (BILL, Melio) | your idle cash earns the *platform* interest; settlement delay baked in | opaque; conflict of interest |
| FX spread (Tipalti, BILL intl) | 1.5–3.5% buried in the rate | **most opaque** cross-border cost |
| Card interchange + rebate | supplier eats ~2–3% (acceptance problem) | visible to supplier, invisible to buyer |
| Per-transaction fees | small, direct | transparent |
| SaaS subscription | flat, predictable | **most transparent** |
| Reserve-yield "rewards" (Altitude) | customer *gains*; platform keeps spread; legally fragile | novel |

**Why "the rail is swappable":** Routable's **Brale stablecoin add (2025)** is the proof — stablecoin slots behind the same payouts API as just another rail, *payee chooses* fiat or USDC. The durable value is the orchestration/compliance layer, not the rail. No one wins on "we can move money."

## Build implication

- **Rails:** USDC on Solana for the wallet-to-wallet core (~$0.01/txn) + **partner for fiat off-ramp** (Bridge/BVNK — what Altitude/Request/Routable already do) so non-crypto vendors still get paid. **Payee choice (fiat *or* stablecoin behind one API) is mandatory** — vendor acceptance is the same limiter that dogs virtual cards.
- **Monetize WITHOUT being a float-middleman** (the point of going on-chain): (1) **SaaS subscription** (cleanest, proven); (2) **transparent FX spread** on off-ramp (beats incumbents' hidden 1.5–3.5% — the single most-attackable surface); (3) **yield-share/reserve-rewards** (Altitude model, GENIUS-shaped — fragile, geofence-dependent); (4) off-ramp/funding fees + interchange if you issue cards.
- **Regulatory shape:** money transmission is the floor (MTL + FinCEN MSB + OFAC/BSA — BILL's 20-yr license stack is "invisible-but-expensive infrastructure"). Still need KYB + OFAC-before-every-payment + a tax module. The rewards path is GENIUS-Act-shaped and geofence-dependent (Altitude geofences EEA/SG/Japan, routes rewards through a BVI entity).
- **The hard part:** NOT moving USDC. It's the orchestration the rail rides on — onboarding, tax, multi-entity ERP sync, time-to-value. **Self-custody collapses float and lets you return yield to the customer (a genuinely better economics story than the float-middleman) — but the moat is the boring middleware, not the chain.**

*Gaps: Tipalti's own float capture + Vic.ai's banking partner undisclosed; Altitude's exact yield instrument + 3.25%-vs-5% discrepancy unresolved; Routable/Request sponsor banks unnamed.*
