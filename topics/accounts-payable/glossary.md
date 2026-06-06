# AP Glossary

*Quick-reference definitions for the terms used across this primer.*

## Core concepts
- **Accounts Payable (AP)** — short-term obligations owed to suppliers for goods/services received but not yet paid; also the function that pays them. A current liability.
- **Accounts Receivable (AR)** — money owed *to* you by customers. The mirror of AP.
- **Accrual** — a cost incurred but not yet invoiced, booked at period-end as an estimate; reverses to AP when the invoice arrives.
- **Trade credit** — a supplier letting you pay later (e.g., Net 30).
- **Liability** — a present obligation expected to be settled by an outflow of resources.
- **Subledger** — the detailed AP record per invoice/payment; must reconcile to the GL **control account** (the single summary AP balance in the General Ledger).

## The cycle
- **Procure-to-Pay (P2P)** — requisition → PO → receipt → invoice → payment → accounting. AP owns the back half.
- **Source-to-Pay (S2P)** — P2P plus upstream sourcing/contracting/onboarding.
- **Purchase Requisition** — internal request to buy (pre-PO).
- **Purchase Order (PO)** — buyer's binding commitment to a vendor (items, qty, price); the match reference.
- **Goods Receipt Note (GRN)** — proof of what was actually received; the 3rd leg of the 3-way match.
- **Invoice** — the vendor's bill; the source document that creates a payable.
- **Credit memo / vendor credit** — a negative invoice (returns/overcharges) reducing what's owed.
- **Remittance advice** — notice to the vendor of which invoices a payment covers.
- **Vendor master** — authoritative record of approved payees (tax ID, W-9/W-8, validated bank details).
- **AP aging** — unpaid invoices bucketed by age (Current, 1–30, 31–60, 61–90, 90+).

## Matching & controls
- **2-way match** — invoice vs PO (qty + price).
- **3-way match** — invoice vs PO vs receipt (adds "only pay for what you got").
- **4-way match** — adds inspection/acceptance.
- **Tolerance** — allowed variance before a **matching hold** blocks payment.
- **Segregation of Duties (SoD)** — split processing / approval / payment / reconciliation across people.
- **Delegation of Authority (DoA)** — matrix of who approves what, up to what amount.
- **Maker-checker / four-eyes** — preparer ≠ approver; dual authorization.
- **COSO** — the internal-control framework auditors expect.
- **SOX 302 / 404** — CEO/CFO certify statements (302); document + test internal control over financial reporting (404).
- **Positive pay** — bank service matching presented checks/payments against an issued list to stop fraud.

## Payments & rails
- **ACH** — batched US electronic transfer (1–2 days); governed by **NACHA**; **ODFI** = payer's bank, **RDFI** = payee's bank.
- **Same-Day ACH** — faster ACH windows; limit rising to **$10M (Sept 2027)**.
- **Wire (Fedwire/CHIPS)** — real-time gross settlement; **irrevocable**.
- **RTP / FedNow** — instant, 24/7, irrevocable rails (The Clearing House 2017 / Fed 2023); ISO 20022.
- **Virtual card (vCard)** — single-use card number; buyer earns rebate, **supplier pays ~2–3% interchange** (the "acceptance problem").
- **Interchange** — fee the supplier's bank pays the buyer's card issuer; funds buyer rebates.
- **SWIFT** — cross-border *messaging* network (not a rail); money moves via **correspondent banking** (nostro/vostro accounts).
- **Local rails** — in-country systems: SEPA (EU), Faster Payments/Bacs/CHAPS (UK), IMPS/NEFT/UPI (India), Pix (Brazil), SPEI (Mexico).
- **FX spread / margin** — the markup over the mid-market rate; the biggest hidden cross-border cost (~1–3%+).

## Working capital
- **DPO (Days Payable Outstanding)** — avg days to pay suppliers = (AP ÷ COGS) × days. Higher = more working capital.
- **2/10 Net 30** — 2% discount if paid within 10 days, else full at 30.
- **Dynamic discounting** — buyer uses own cash to pay early for a discount.
- **Reverse factoring / supply-chain finance** — third-party funder pays supplier early on the *buyer's* credit; buyer repays at due date.
- **Float** — economic benefit of holding money in transit.
- **FBO ("For Benefit Of") account** — pooled custodial account a platform holds on behalf of customers; the platform/partner bank can earn interest on the in-transit balance.

## Tax & compliance
- **W-9** — collects TIN from US persons.
- **W-8 series** — establishes foreign status (W-8BEN individuals, W-8BEN-E entities, ECI/IMY/EXP).
- **1099-NEC / 1099-MISC** — US info returns (services ≥ $600 → $2,000 from 2026 / rents/other).
- **1042-S** — reports US-source income paid to foreign persons.
- **TIN matching** — verify name+TIN with IRS to avoid B-notices.
- **Backup withholding** — 24% withheld when TIN is missing/invalid.
- **VAT/GST input tax** — supplier-charged tax the buyer can recover *only if the invoice is compliant*.
- **E-invoicing mandate / CTC (Continuous Transaction Controls)** — government requirement for structured e-invoices, often cleared by the tax authority (clearance model) vs audited later (post-audit).
- **Peppol** — the dominant cross-border e-invoicing interoperability network (4-corner model).
- **OFAC / SDN list** — US sanctions screening; paying a sanctioned party is strict-liability.
- **KYB (Know Your Business)** — verifying a supplier is a real legal entity (UBOs, incorporation, tax IDs).

## Automation & AI
- **OCR** — optical character recognition (image → text).
- **IDP (Intelligent Document Processing)** — OCR + ML + NLP reading any layout template-free.
- **EDI** — older structured machine-to-machine document exchange (e.g., X12 810 invoice).
- **Touchless / straight-through processing (STP)** — invoice processed end-to-end with zero human touch (honest average ~33%).
- **Agentic AI / autonomous AP** — agents that take action within guardrails, not just suggest.
- **Exception** — an invoice that can't process straight-through (mismatch, missing PO, duplicate).
