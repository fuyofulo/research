# Velocity - Deep Dive

Date: 2026-05-07

## Executive summary

Velocity is building enterprise-grade stablecoin infrastructure for payments, settlement, treasury, liquidity, and FX. The current public positioning is "Money rewired for velocity": a CFO-facing platform that unifies payments, balances, liquidity, settlement, and programmable stablecoin rails into one platform.

They are not pitching as a crypto app. They are pitching as enterprise financial infrastructure. The buyer is the CFO/treasurer/risk/compliance team that wants faster settlement and better liquidity control without giving up governance, auditability, regulated partners, custody controls, and bank connectivity.

## What Velocity does

Public product surface:

- Payments: move fiat or stablecoins globally.
- Settlement: real-time settlement without banking cutoffs.
- Treasury: on-chain, productive, programmatic capital.
- API: transfers, quotes, wallets, beneficiaries, fees, Travel Rule, webhooks/authentication implied by docs.
- Stablecoin Payment Account: one place to manage fiat and stablecoin transactions.
- TMS/ERP integrations: connect treasury workflows to existing enterprise systems.
- Yield/rewards: available through third-party issuers/protocol partners, not guaranteed by Velocity.
- Compliance and custody stack: regulated custodians, compliance controls, institutional custody, bank/liquidity partners.

Sources: [homepage](https://www.velocity.xyz/), [docs landing](https://www.velocity.xyz/velocity-docs), [GlobeNewswire launch](https://www.globenewswire.com/news-release/2025/05/28/3089291/0/en/Velocity-comes-out-of-stealth-with-10M-to-power-the-Velocity-of-Money.html).

## Founding and team

Original launch materials said Velocity was founded by payment veterans Tom Greenwood and Eric Queathem. Greenwood previously founded Volt and IFX. Queathem spent nearly a decade at Worldpay and McKinsey, with experience across strategy, growth, and crypto/traditional payments markets.

Current public site emphasizes Eric Queathem and a broader leadership team:

- Eric Queathem, President on the About page; Founder/CEO in 2026 blog posts.
- Lukasz Anwajler, CTO.
- Steve Delpy, Chief Banking Officer.
- Mina Khattak, Head of BD & Partnerships.
- James Osborn, Head of Product.
- John Stathacopoulos, Head of Risk & Compliance.
- Stuart Barclay, Head of EMEA.
- Jan Hartmann, Head of APAC.
- Matt Larson, Head of Growth.
- Leila Foulon, Chief of Staff.

Current job listings describe a fast-growing team of about 25 people across London and Warsaw. LinkedIn search result lists 11-50 employees and about 2,999 followers.

Sources: [About](https://www.velocity.xyz/about), [GlobeNewswire launch](https://www.globenewswire.com/news-release/2025/05/28/3089291/0/en/Velocity-comes-out-of-stealth-with-10M-to-power-the-Velocity-of-Money.html), public Ashby job listing search snippets, [LinkedIn company search result](https://uk.linkedin.com/company/velocityxyz).

## Funding

Velocity announced a $10M pre-seed in May 2025. The launch release says the round was led by Activant Capital, with participation from Fuel Ventures, Triton Capital, Fabric Ventures, Commerce Ventures, Digital Space Ventures, and Preface Ventures. Strategic shareholders included current and former executives from Stripe, Worldpay, Visa, Circle, PayPal, and Google.

In October 2025, Velocity announced an investment from Dragonfly Capital. The public post does not disclose the amount.

Sources: [GlobeNewswire](https://www.globenewswire.com/news-release/2025/05/28/3089291/0/en/Velocity-comes-out-of-stealth-with-10M-to-power-the-Velocity-of-Money.html), [Velocity funding post](https://www.velocity.xyz/blog-post/velocity-raises-10-million), [Dragonfly post](https://www.velocity.xyz/blog-post/dragonfly-invests-in-velocity).

## Legal footprint

The primary UK holding entity found is Velocity Technology Holdings Limited, company number 16204089. Companies House shows:

- Active private limited company.
- Incorporated 23 January 2025.
- Registered office: 3rd Floor 1 Ashley Road, Altrincham, Cheshire, UK.
- SIC: activities of financial services holding companies and financial intermediation not elsewhere classified.
- Previous name: Velocity Lab Holdings Limited from 23 Jan 2025 to 29 Jan 2025.
- Confirmation statement marked overdue on the Companies House page as viewed.

Companies House PSC page lists Thomas Paul Greenwood and Eric Scott Queathem as active persons with significant control. Greenwood has more than 50% but less than 75% share/voting control and right to appoint/remove directors. Queathem has more than 25% but not more than 50% share/voting control.

Sources: [Companies House overview](https://find-and-update.company-information.service.gov.uk/company/16204089), [PSC page](https://find-and-update.company-information.service.gov.uk/company/16204089/persons-with-significant-control).

## Partners and infrastructure

Named public partners include:

- Fireblocks: strategic infrastructure partner for secure wallet architecture, approval flows, policy enforcement, segregation of assets, and operational resilience.
- Zodia Custody: custodian, backed by Standard Chartered, Northern Trust, and SBI; Velocity says Zodia underpins the digital asset layer for settlement flows.
- Dragonfly: investor.
- Paxos/USDG: partner quote says USDG is available through Velocity.
- Revolut: partner quote from Mazen ElJundi, Global Head of Expansion Markets.

The Trust Centre says Velocity has SOC 2 Type I, is working toward Type II, and lists compliance badges for DORA, GDPR, ISO/IEC 27001, SOC 2 Type I, and SOC 2 Type II. It also lists security grades for `api.velocity.xyz` and `portal.velocity.xyz`.

Sources: [Partners](https://www.velocity.xyz/partners), [Fireblocks post](https://www.velocity.xyz/blog-post/velocity-x-fireblocks-strategic-partnership), [Zodia post](https://www.velocity.xyz/blog-post/velocity-zodiacustody), [Trust Centre](https://trust.velocity.xyz/).

## Product maturity

Velocity is more real than a pure landing page:

- There is a portal domain.
- There is an API domain referenced by the trust center.
- There is a docs landing page with concrete integration steps.
- There are password-protected docs pages.
- There are named institutional partners.
- There are compliance/security artifacts behind gated Trust Centre access.
- Blog post says Velocity is live and working with a select group of enterprise partners/customers.

But the public surface is still limited:

- No public customer case studies.
- No public pricing.
- No open API reference without access.
- No public API keys/sandbox visible.
- No direct proof of payment volume.
- No clear disclosure of exact licenses held by Velocity itself versus partners.

## Competitive read

Velocity is dangerous because it has the right ingredients for enterprise adoption:

- Payments veterans.
- Regulatory and financial institution language.
- Custody and wallet infrastructure via Fireblocks/Zodia.
- Bank/liquidity/stablecoin partner strategy.
- Enterprise-first buyer framing.
- Funding from serious fintech and crypto investors.

The weak point is not ambition; it is execution scope. Building a global enterprise treasury network across fiat, stablecoins, custody, compliance, liquidity, ERP integrations, and regulation is extremely hard. That creates room for a focused product that wins one workflow before becoming a platform.

## Implication for our product

Do not copy Velocity head-on. They are building the "global enterprise treasury rail." We should start with a narrower wedge:

- Solana-native operating accounts.
- AI-assisted reconciliation and payables.
- Approval policies and spend intelligence.
- Specific customers with messy recurring finance workflows.
- Clear use cases where Bridge/Grid/Privy/Squads-style infrastructure can be composed quickly.

Velocity validates the market. It also shows that "stablecoin CFO stack" is becoming an enterprise category, not only a crypto-founder idea.
