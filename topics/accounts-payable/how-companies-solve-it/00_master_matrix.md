# Master Matrix — How Each Company Solves Each AP Problem

*The "real vs": AP pipeline stages (rows) × companies (columns). Each cell = how they solve it. June 2026. Source-grounded in `companies/` + the AP primer.*

Legend: **●** strong/deep · **◐** partial/present · **○** thin/light · **✗** gap / not shipped · *(vendor-claimed numbers are vendor-claimed)*

## The grid

| AP problem (stage) | BILL | Tipalti | Stampli | Vic.ai | Ramp | Request Finance | Routable | Altitude |
|---|---|---|---|---|---|---|---|---|
| **Intake** (channels) | ● email-inbox + network + upload | ● email/API + Supplier Hub | ◐ invoice hub | ◐ VicInbox + ERP-fed | ◐ email/upload | ● **invoice = on-chain Request** + CSV | ● **API-first** + CSV + portal | ○ Bill Pay PDF/CSV (new 2026) |
| **Capture / extract** | ● AI Coding Agent (~99% hdr) | ● Invoice Capture Agent | ● Billy (since 2018) | ● Autopilot (>1B invoices) | ● vision-LLM + OCR | ◐ Smart Invoice Capture | ◐ OCR via OpenAI | ○ light OCR (vendor/amt/IBAN) |
| **GL coding** | ● ML, 250M-bill corpus | ● Auto-coding | ● per-customer learning | ● correction loops | ● ~60% auto @99% (claim) | ◐ via Request Accounting | ○ not documented | ✗ minimal |
| **Match** (2/3/4-way) | ○ no true 3-way (ref only) | ● **genuine 2/3-way** (+Approve.com) | ◐ adding via P2P | ● Autopilot PO match | ◐ via Procurement (Venue) | ✗ no PO match | ◐ "PO-matching" (shallow) | ✗ none |
| **Exception UX** | ◐ queue (no auto-escalate) | ◐ clerk queue | ● **collaboration-on-invoice** | ◐ correction loop | ◐ agent flags ~3% | ○ thin | ○ thin | ○ thin |
| **Approval** | ◐ rules/thresholds | ◐ rules + Approver Agent | ● collab routing | ◐ autonomous routing | ● policy-at-swipe (preventive) | ● **Gnosis Safe multisig** (m-of-n) | ◐ rules | ● **Squads multisig + on-chain SpendingLimit/time-lock** |
| **Rails** | ◐ ACH/check/wire/card (batch) | ● 196-country, Global ACH+SWIFT | ◐ ACH/check/card/intl | ◐ VicPay (own rails) | ◐ card-led + ACH | ● wallet-to-wallet 18 chains + fiat off-ramp | ● ACH/RTP/FedNow/SWIFT **+ stablecoin (Brale)** | ● USDC/Solana + ACH/SEPA via PSPs |
| **Money model** | **FBO float** | customer pre-fund (non-interest) | **no float** (commodity) | funding acct (undisclosed) | no-hold (partner banks) | **self-custodial** (no float) | prefunded balance (FBO-like) | **self-custodial** (no float) |
| **Monetization** | float ~$162M + txn + sub + FX | **FX spread 1.5–3.5%** + sub + fees | **SaaS** | SaaS + interchange/float | **interchange** + sub | sub + 0.5% off-ramp (near-free crypto) | sub ($1,250/mo) + per-txn | **reserve-yield "rewards"** spread + interchange |
| **Onboarding portal** | ◐ BILL Network | ● Supplier Hub (27 langs) | ◐ | ◐ Plaid Vendor Portal | ○ | ◐ crypto + fiat-KYB | ● white-label PII-holding | ○ Grid API |
| **Tax (W-8/9, 1099/1042-S)** | ◐ W-9 Agent; filing thin | ● **KPMG engine, TIN, 1099/1042-S** | ○ thin | ○ not surfaced | ○ collect only | ✗ **gap** (no native) | ● W-9/W-8/1099/1042 | ✗ none (KYB via Sumsub only) |
| **ERP sync** | ● 2-way ×5 ERPs | ● **deepest NetSuite OneWorld** (but fails ~monthly) | ● **70+ ERPs, 4–6wk deploy** | ● autonomous posting | ● 30+, AI close (Plus tier) | ◐ QBO/Xero/NetSuite + crypto-acct | ● "99.8%" 4 ERPs | ✗ **none shipped** ("coming soon") |
| **Audit / close** | ◐ recon report | ● close + recon | ◐ | ◐ | ● AI month-end close | ● **on-chain audit trail** + Request Accounting | ◐ webhooks | ○ on-chain record only, no GL bridge |
| **AI architecture** | pipeline + agents bolted on | rules-gateway + agents | invoice-hub + Billy | autonomy-first STP | **agent-with-tools** (unified) | OCR (AI not the pitch) | API (no agent) | **code-enforced** smart-account |
| **Segment** | SMB→low-mid | mid-market/enterprise global | mid-market | upper-mid/enterprise | SMB→enterprise (US) | crypto-native (EVM) | marketplaces/payouts | crypto-native (Solana) |

## Who's strongest at each stage (the "best-in-class per problem")

| Stage | Strongest | Why |
|---|---|---|
| Intake/capture/code | **Bill.com / Vic.ai / Stampli** (tie) | proprietary-data coding flywheels; but **extraction is commoditizing** — not a moat |
| Matching (2/3-way) | **Tipalti** | genuine header+line 3-way via Approve.com procurement layer |
| Exception UX | **Stampli** | collaboration-on-the-invoice — wins mid-market on usability |
| Approval/execution | **Altitude** (then Request) | code-enforced multisig — approval *is* the on-chain signature; can't be overridden |
| Rails/cross-border | **Tipalti** (fiat) / **Request, Altitude** (crypto) | 196-country local rails vs wallet-to-wallet USDC |
| Monetization integrity | **Stampli** (no-float) / **Altitude** (yield-to-customer) | software/yield-share beats float-middleman conflict |
| Onboarding + tax | **Tipalti / Trolley** (Trolley = deepest 1099/1042-S/DAC7) | tax-as-moat; **crypto-native players are thinnest here** |
| ERP sync | **Tipalti** (depth) / **Stampli** (breadth+speed) | NetSuite OneWorld bidirectional; also the #1 complaint |
| AI architecture | **Ramp** | agent-with-tools + unified agent + closed-loop data |

## The three findings that repeat across every stage

1. **The rail is not the moat.** Routable bolting stablecoin onto its API (Brale, 2025) proves rails are swappable. The moat is **onboarding + tax + ERP sync + orchestration + code-enforced execution**.
2. **Extraction is commoditized; the moat moved up-stack** to proprietary coding data, deep ERP sync, the agent-orchestration layer, and (crypto-only) code-enforced execution.
3. **No incumbent has all four defensible layers.** TradFi has data + ERP depth but software-only enforcement and domestic rails; crypto-native has self-custody + code-enforcement but is thin on tax + ERP + matching. **The open intersection is the build target** (see [07_build_implications.md](./07_build_implications.md)).

→ Per-stage deep dives: [01](./01_intake_capture_code.md) · [02](./02_match_exception_approval.md) · [03](./03_pay_rails_float.md) · [04](./04_onboarding_tax_compliance.md) · [05](./05_erp_sync_record_close.md) · [06](./06_ai_layer_and_architecture.md) · build spec: [07](./07_build_implications.md)
