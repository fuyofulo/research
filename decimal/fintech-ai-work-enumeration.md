# What Work Fintech AI Companies Are Paid To Do

An exhaustive enumeration of the kinds of work that fintech AI companies are getting paid to do, drawn from existing research on Bill.com, Tipalti, Brex, Ramp Business, Mercury, Deel, Monk, Flex, Mercury, Altitude, Slash, Meow, BVNK, Bridge, Velocity, plus the AI-in-fintech research and the 18-company landscape analysis.

**Not filtered. Not ranked. Not opinionated about what Decimal should build.** Just listed, so we can look at it together and decide. The decision about which of these to take on, and in what shape, comes after.

Each item names the *work* (operational task an agent does), which *companies ship it* today, and *who pays for it* (the customer persona that values the work enough to pay).

---

## 1. Document & input handling — "read whatever comes in"

The agent ingests whatever the customer (or the customer's vendor) throws at it.

- **Read invoice PDFs** *(Bill.com, Tipalti, Brex, Ramp, Monk, Flex, every player)* — finance ops paying for "no manual data entry"
- **Read photographed receipts** *(Brex, Bill.com, Ramp)* — employees paying with "save me 10 min per receipt"
- **Read signed contracts** *(Monk)* — finance/RevOps paying for "turn the contract into a billing schedule without me retyping it"
- **Read invoice emails with attachments** *(Bill.com, Brex)* — AP teams paying for "I don't have to download the PDF first"
- **Read CSV uploads** *(everyone)* — ops people paying for "I can import my contractor list"
- **Read bank-feed transactions** *(Mercury, Brex)* — founders paying for "categorize every transaction without me labeling it"
- **Read card-transaction streams** *(Brex, Ramp)* — finance teams paying for "real-time spend visibility without manual entry"
- **Read inbound from Slack / chat / integrated apps** *(implicit across all)* — ops paying for "send me requests in the channel I already use"
- **Multi-page document handling** *(every player handles this; some better than others)* — AP teams who have 20-page POs
- **Multi-invoice-per-document splitting** *(Tipalti, Bill.com)* — AP teams getting batched PDFs from large vendors
- **Handle encrypted / password-protected documents** *(Tipalti exception queue surfaces these)* — large enterprises with security requirements

---

## 2. Data extraction & structured-data generation — "turn the input into fields"

- **Extract vendor identity** (name, address, contact, email) *(everyone)*
- **Extract payment amount + currency** *(everyone)*
- **Extract line items** (description, quantity, unit price, tax per line) *(Tipalti, Monk, Ramp procurement)* — finance teams paying for "show me what the money was for"
- **Extract due date and payment terms** *(Bill.com, Tipalti)* — AP teams who need scheduling
- **Extract invoice number / PO number / external reference** *(every AP player)* — bookkeepers who need a reconciliation key
- **Extract bank account / wallet address / routing details** *(Bill.com, Tipalti; Decimal already)* — payment-execution layer
- **Extract payment method preferences from the contract** *(Monk)* — finance teams aligning to vendor expectations
- **Confidence scoring per field** *(Brex Audit Agent layer, Tipalti)* — anyone wanting human review only for low-confidence
- **Extract from messy / handwritten / scanned-fax sources** *(Tipalti exception queue specifically)* — enterprises with long-tail-vendor messiness

---

## 3. Coding & categorization — "assign the right account to the thing"

Once the data is extracted, the agent decides where to file it in the customer's books.

- **Assign GL accounts to invoices and bills** *(Bill.com Invoice Coding Agent — trained on 250M invoices; Tipalti automated coding; Brex Expense AI; Ramp Agents for AP)* — bookkeepers paying for "I stop coding 50 invoices a month myself"
- **Assign cost centers / departments** *(Brex, Ramp)* — controllers needing departmental P&L
- **Assign classes / locations / projects** *(QBO classes / Plus tier features; Ramp)* — companies with project-based accounting
- **Assign expense category to a card transaction** *(Brex Expense AI, Ramp, Mercury)* — every cardholder
- **Categorize transactions from bank feed** *(Mercury, Brex, Ramp)* — startups doing their own books
- **Apply the customer's historical coding patterns to new invoices** *(Bill.com explicitly — "learns your coding patterns")* — controllers paying for "the agent learned how *we* code"
- **Predict the right expense account when it's ambiguous** *(every player)*

---

## 4. Approval & policy work — "who needs to approve this, and is it OK"

The work-side of approvals, not the code-enforcement side.

- **Determine who needs to approve based on rules** *(Brex Audit Agent, Ramp Agents for Controllers, Bill.com smart routing)* — finance teams paying for "stop having me figure out who signs what"
- **Auto-approve low-risk items, escalate edge cases** *(Brex 99% autonomous expense processing; Ramp 85%+ auto-approval)* — controllers paying for "I only look at the weird ones"
- **Surface policy violations before they reach the approver** *(Ramp natural-language procurement intake — intercepts violations at request time)* — finance teams paying for "stop bringing me requests that should never have been submitted"
- **Explain why a request was blocked** *(Ramp policy-violation explanations)* — employees paying for "tell me what would make this work"
- **Route through complex multi-level approval chains** *(Bill.com, Tipalti)* — mid-market companies with formal SOPs
- **Apply department-budget rules** *(Ramp, Brex)* — department heads
- **Apply vendor-specific approval requirements** *(Ramp)* — finance teams with vendor-tier policies
- **Audit-agent layer reviewing the primary agent's decisions** *(Brex — "LLM as judge")* — enterprise controllers paying for "even the AI is double-checked"

---

## 5. Vendor / counterparty management — "know who you're paying"

- **Onboard a new vendor end-to-end** *(Deel for contractors; Bill.com for AP vendors)* — ops paying for "I don't fill out the new-vendor form anymore"
- **Generate locally-compliant contractor agreements** *(Deel — country-localized; ~150 jurisdictions)* — startups hiring abroad without legal counsel
- **Collect tax forms (W-9, W-8BEN, 1099)** *(Deel, Tipalti)* — anyone managing US tax exposure
- **Sync vendor list with QuickBooks / NetSuite / Xero** *(Bill.com, Ramp, Monk)* — bookkeepers
- **Deduplicate vendor records across systems** *(implicit; nobody markets this explicitly)*
- **Classify worker as employee vs independent contractor** *(Deel AI Worker Classifier — 90%+ accuracy, 15 countries, Queen's University-backed)* — startups avoiding misclassification fines
- **Country-specific worker classification compliance** *(Deel)*
- **Vendor enrichment** (pull website, registration info, beneficial-owner data) *(no AI player names this explicitly; Bill.com Network does discovery)*
- **Vendor risk assessment / scoring** *(less defined; nobody really ships this well)*
- **Surface vendor payment history when needed** *(every player implicitly)*

---

## 6. Payment execution & scheduling — "actually pay the bill"

- **Schedule payments by due date** *(Bill.com, Tipalti)* — finance teams paying for "stop late fees"
- **Recommend payment timing based on cash flow optimization** *(Bill.com explicitly — "intelligent payment scheduling")* — CFOs managing cash
- **Choose payment method** (ACH / wire / virtual card / stablecoin / etc.) *(Ramp Agents for AP — "recommend payment method")* — finance teams optimizing cost per payment
- **Send payments via ACH** *(Bill.com, Tipalti, every US AP player)*
- **Send payments via wire** *(Tipalti, Bill.com)*
- **Send payments via virtual card** *(Brex, Ramp — per-vendor virtual cards)*
- **Issue per-vendor virtual cards** *(Brex, Ramp — automatic categorization downstream)* — controllers paying for "every vendor has its own card, so categorization is automatic"
- **Handle multi-currency payouts** *(Deel — 150+ currencies)*
- **Apply FX hedging** *(Deel)*
- **Execute the payment with the right rail given destination** *(implicit across cross-border players)*

---

## 7. Reconciliation & matching — "make the books tie out"

- **Match outbound payments to source invoices** *(everyone does this, but Tipalti makes it explicit with PO matching)*
- **Match incoming USDC / wires / ACH to expected receipts (cash application)** *(Monk explicitly — "cash application")* — controllers paying for "I don't manually match deposits to invoices"
- **Match bank-feed transactions to recorded transactions** *(Mercury, Brex)* — bookkeepers doing reconciliation
- **Match payments to POs at line-item level** *(Tipalti)* — enterprises with formal PO processes
- **Match contract obligations to invoices** *(Monk)* — RevOps reconciling billing to contract terms
- **Resolve ERP sync conflicts** *(Tipalti — explicit "AI resolves sync conflicts between Tipalti and customer's ERP")* — IT/finance teams who hate sync drift
- **Month-end close reconciliation** *(Mercury — "monthly closes faster with automatic reconciliations")*
- **Generate reconciliation reports** *(every player)*
- **Surface exceptions for human review** *(Tipalti exception queue; Monk human-in-the-loop fallback)* — controllers paying for "I only touch the broken ones"

---

## 8. Outbound communication & vendor relations — "the agent talks to vendors / customers"

- **Reply to vendor inquiry emails (where is my payment, when is it coming)** *(Monk collections agent can do this)* — ops paying for "stop me from doing customer support for our AP"
- **Send overdue-payment reminders (dunning)** *(Monk — multi-channel, escalating tone)* — RevOps paying for "I don't chase late customers myself anymore"
- **Upload documents into customer-specific procurement portals** *(Monk explicitly — agents log into Ariba/Coupa-style portals and submit docs)* — sales/RevOps paying for "I don't fill out Coupa for every Fortune 500 client"
- **Engage with overdue customers via voice** *(Monk — voice agents)*
- **Send approval requests via Slack** *(Brex pattern; widely implied)*
- **Notify signers when proposals are ready** *(every multisig product including Decimal)*
- **Escalate dunning tone over time** *(Monk — context-aware escalation)* — RevOps paying for "the agent gets firmer as the invoice ages"
- **Negotiate over email or voice** *(Monk has this; rare otherwise)*

---

## 9. Reporting & analytics — "tell me what's going on"

- **Generate cash-flow summaries** *(Mercury — "continuous summaries with burn rate, cash position, runway")*
- **Generate burn-rate / runway reports** *(Mercury)* — startup founders paying for "I always know how many months I have"
- **Generate spend-by-category breakdowns** *(Ramp, Brex)* — controllers
- **Generate vendor-spend breakdowns** *(Ramp, Brex)*
- **Generate weekly CFO / executive report** *(implied in Mercury, Ramp)* — founders without finance teams
- **Auto-generate workforce reports** *(Deel — workforce reporting agent)*
- **Generate budget-variance reports** *(Ramp)*
- **Generate approval-bottleneck reports** *(Ramp explicit — "surfaces outstanding POs, budget variance, approval bottlenecks")*
- **Respond to natural-language report requests in plain English** *(Ramp explicit — "ask in plain English and Ramp generates the report")*
- **Generate end-to-end procurement visibility (request → PO → payment)** *(Ramp full procurement reporting)*

---

## 10. Forecasting & planning — "predict what's coming"

- **Project runway from current burn + scheduled payouts** *(Mercury)*
- **Forecast cash flow** *(Mercury, Flex Owner Intelligence)* — founders / owners
- **Alert when cash drops below runway threshold** *(Mercury API-driven alerts)*
- **What-if simulations ("if we hire X, runway becomes Y")** *(Mercury implied; Flex Owner Intelligence)*
- **Margin-change alerts** *(Mercury — "alerts to margin changes")*
- **Identify subscription consolidation opportunities** *(Ramp — "you have two overlapping CRMs")*
- **Identify unused-license / dormant-vendor** *(Ramp)*
- **Surface renewal dates 90 days out with pricing benchmarks** *(Ramp Renewal Intelligence)* — finance teams negotiating contracts
- **Business health scoring** *(Flex Owner Intelligence)*

---

## 11. Procurement & sourcing — "the buying side of payouts"

- **Take in employee purchase request in plain English** *(Ramp natural-language intake)* — employees who hate procurement forms
- **Pre-fill the request based on context** *(Ramp)*
- **Source vendors for a given need** *(Ramp Zero-Touch Sourcing)* — procurement teams paying for "the agent finds candidates"
- **Run RFx process, score responses, recommend winner** *(Ramp — "single conversation replaces weeks of vendor research")*
- **Review contract terms before signing** *(Ramp Procurement Agent)*
- **Conduct compliance due diligence (security / legal / finance)** *(Ramp explicit — "saves ~2 hours of manual research per request")*
- **Custom compliance checks for security / legal / finance teams** *(Ramp)*
- **Negotiate pricing using benchmarks** *(Ramp Renewal Intelligence — "pricing benchmarks across millions of transactions")*

---

## 12. Risk, anomaly, fraud — "catch the bad stuff"

- **Flag first-time / new payees** *(implicit in every player; Decimal already discussed)* — controllers paying for "tell me when I'm paying someone new"
- **Flag wallet / account changes for known vendors (BEC signal)** *(rare; this is Decimal's natural advantage with on-chain identity)*
- **Flag duplicate invoices** *(Bill.com explicit — "predictive algorithms detect duplicates"; Tipalti)*
- **Flag abnormal amounts vs historical pattern** *(every player handles versions of this)*
- **Detect anomalous spend** *(Mercury, Ramp anomaly detection)*
- **Detect potential fraud broadly** *(Bill.com "predictive algorithms monitor for anomalies or signs of fraud")*
- **Audit agent reviewing other agents' decisions for accuracy + policy** *(Brex explicit — "LLM as judge")*
- **Detect margin changes** *(Mercury)*
- **Flag policy violations before they reach an approver** *(Ramp — natural-language intake intercepts these)*
- **Suspicious-large-payment-vs-historical-average alerts** *(every player)*

---

## 13. Integration & sync — "keep all the systems consistent"

- **Sync with QuickBooks** *(every player ships this)* — bookkeepers
- **Sync with NetSuite** *(Bill.com, Monk, Tipalti)* — mid-market controllers
- **Sync with Salesforce** *(Monk)*
- **Sync with Xero** *(every player)*
- **Sync with Coupa** *(Ramp procurement integration)*
- **Sync with ERPs broadly** *(every enterprise player)*
- **Resolve sync conflicts automatically** *(Tipalti — explicit AI capability)*
- **Push transactions to the customer's GL** *(every player)*
- **Pull COA from source-of-truth and use it locally** *(Ramp pattern — "QBO is the source of truth for COA")*
- **Maintain consistency across systems despite divergent updates** *(BILL has explicit "source of truth" selection)*
- **API integration with HRIS systems** *(Deel)*
- **Bidirectional sync where applicable** *(Bill.com, Acctual)*

---

## 14. Hiring, classification, payroll — "the people side"

- **Classify a worker as employee vs independent contractor** *(Deel AI Worker Classifier)* — founders avoiding fines
- **Generate country-localized employment contracts** *(Deel — 150 jurisdictions)*
- **Onboard an EOR employee** *(Deel — "minutes for contractors, days for EOR employees")*
- **Manage IT provisioning (devices, software, access)** *(Deel device management module)*
- **Handle tax documents (1099, W-8BEN, etc.)** *(Deel, Tipalti)*
- **Country-specific employment law compliance** *(Deel — adapts to new laws automatically)*
- **Tax compliance per jurisdiction** *(Tipalti, Deel)*
- **Calculate salary in 150+ currencies** *(Deel)*
- **Apply FX hedging on payroll** *(Deel)*
- **Misclassification risk monitoring throughout the contract term** *(Deel — ongoing, not just at onboarding)*

---

## 15. Accounts receivable & collections — "money owed to you"

- **Generate invoices from contract terms (auto-billing)** *(Monk billing engine)*
- **Bill for usage-based pricing** *(Monk)*
- **Bill for tiered pricing** *(Monk)*
- **Bill for milestone-based contracts** *(Monk)*
- **Send invoices to customers** *(every AR player)*
- **Track unpaid invoices and aging** *(every AR player)*
- **Send multi-channel dunning communications** *(Monk)*
- **Apply cash to invoices (cash application)** *(Monk explicitly)*
- **Resolve cash-application exceptions** *(Monk human-in-the-loop)*
- **Upload remittance documents into customer procurement portals** *(Monk agents)*

---

## 16. Tax & compliance — "regulators sleep well"

- **Apply correct tax treatment per country** *(Tipalti)*
- **Generate tax documents (1099, W-8BEN, country-specific forms)** *(Deel, Tipalti)*
- **Sanctions screening** *(BVNK — institutional)* — enterprises with regulatory exposure
- **KYB / business verification** *(BVNK, Deel, every regulated player)*
- **Worker classification compliance** *(Deel)*
- **Revenue recognition compliance (ASC 606)** *(Monk — explicit ASC 606 handling)* — public-company-adjacent SaaS
- **Country-specific employment compliance** *(Deel — 150+ jurisdictions, auto-updating)*
- **Travel Rule compliance for crypto / stablecoin volume** *(BVNK)*
- **Automated tax filing preparation** *(implied across multiple players)*

---

## 17. Conversational support / assistant work — "the chat surface"

- **Answer policy questions for employees** *(Brex Assistant)* — every employee who's confused about a policy
- **Help employees file expenses** *(Brex Assistant — auto-populates expense docs from calendar, org, past expenses)*
- **Personalized onboarding support** *(BILL Assistant)*
- **Provide instant first-line support, escalate to human only when needed** *(Deel)*
- **Answer natural-language questions about company finances** *(Ramp explicit — "ask in plain English"; implied across Brex, Mercury)* — founders / CFOs paying for "I get answers instead of building reports"
- **Generate ad-hoc reports on plain-English request** *(Ramp)*
- **Provide guidance during setup / configuration** *(Bill.com)*

---

## Patterns worth noticing (not decisions, just observations)

A handful of cross-cutting observations from the list above. These aren't picks of "what Decimal should do" — just things to flag for the next conversation.

- **Several distinct types of customer pay for very different bundles of this work.** A startup founder using Mercury pays mostly for §9, §10, §17. A controller at a 500-person company using Bill.com pays for §1–§7, heavily §3 + §4. A RevOps person at a SaaS company using Monk pays for §15 + §8 + §1 (contracts). A CFO at a global startup using Deel pays for §14 + §16. The work bundles are not the same.
- **Some work has a sharp "the agent does it autonomously" headline** — Brex 99% expense, Ramp 85% controller, Bill.com 80% manual reduction, Monk full collections agents. These are the loudest pieces of marketing.
- **Some work is invisible quality-of-life** — sync, reconciliation, exception handling. Customers expect it to exist but don't shop on it.
- **Some work depends on data corpora the incumbents have spent years building** — invoice coding, vendor categorization, spend benchmarking. Hard for a new entrant to match on accuracy from cold start.
- **Some work is mostly *language* and structure, not specialized data** — anything that's "draft a contract / reply to an email / generate a report from existing data." LLMs are good enough off-the-shelf for these without years of training corpora.
- **A few kinds of work appear in *zero* products on this list** — cross-border-corridor-intelligent payment routing, code-enforced-policy-respecting agent drafting, on-chain-settlement-aware reconciliation. These are the whitespace items.

---

## Reference

Source documents:
- `outputs/ai-in-fintech-research.md` — full feature deep-dive on the 8 fintech AI companies
- `outputs/competitor-landscape.md` — 18-company landscape with per-company profiles
- `outputs/decimal-feature-catalog.md` — earlier feature catalog from competitor research
- `/Users/fuyofulo/research/ai_crypto/companies/` — original company research notes

Companies referenced: Bill.com, Tipalti, Brex, Ramp Business, Mercury, Deel, Monk, Flex, Altitude, Slash, Meow, BVNK, Bridge, Velocity, Kast, Credible Finance, Ramp Network, Corgi, Blockworks, Frames.ag.
