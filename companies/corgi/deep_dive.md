# Corgi - Deep Dive

Date: 2026-05-08

## Executive summary

Corgi is an AI-native full-stack insurance company, currently focused on insurance for technology startups. It is not just a broker comparison site. Corgi's public materials say the group includes licensed insurance producers, affiliated licensed carriers, and affiliated claims administration operations. Its website footer clarifies that at least some coverage is underwritten by Technology Risk Retention Group, Inc. (TRRG), while Corgi Insurance Services, Inc. is a licensed insurance producer and program administrator, not the insurer for those policies.

That nuance matters: Corgi's marketing says "we own our carrier" and "we create and sell our own policies," but the legal substrate is a group/program structure where different products may be underwritten by affiliated carriers or third-party carrier partners depending on product, jurisdiction, and risk profile.

The market bet is simple: insurance is huge, manual, document-heavy, regulated, and slow. Corgi uses AI and full-stack control to make quote, underwriting, policy issuance, claims, and upgrades happen much faster.

## What Corgi sells

Corgi sells startup business insurance packages by company stage:

- Pre-seed & seed: CGL, D&O, Tech E&O, Cyber.
- Series A: CGL, D&O, Tech E&O, Cyber, Media, EPLI.
- Growth stage: CGL, D&O, Tech E&O, Cyber, Media, EPLI, Fiduciary.
- Custom: modular selection including HNOA and other specialized lines.

Additional coverage categories visible on the homepage:

- Commercial Umbrella.
- Workers' Compensation.
- Contractors Professional.
- Business Owners Policy.
- Real Estate E&O.
- Lawyer E&O.
- Miscellaneous E&O.
- Medical Malpractice.
- Representations & Warranties.
- Non-Profit D&O.
- K&R.
- Crime Insurance.

Public copy separates some products into "instant quote" and others into "1-14 days turnaround." That is important: Corgi is not instant for everything.

Sources: [homepage](https://www.corgi.insure/), [customers page](https://www.corgi.insure/customers).

## Founders and team

Corgi was founded in 2024 by Nico Laqua and Emily Yuan. YC lists Corgi as Summer 2024, active, San Francisco, fintech/insurance/AI, with team size 70. YC says Laqua is founder and CEO/CTO and previously founded Basket, a gaming publisher with 200M+ monthly active users. Yuan is co-founder and COO.

Sources: [YC profile](https://www.ycombinator.com/companies/corgi-insurance), [Series B release](https://www.corgi.insure/press-releases/series-b).

## Funding and valuation

Corgi announced:

- $108M across seed + Series A in January 2026 after receiving regulatory approval to launch.
- $160M Series B in May 2026 at a $1.3B valuation.
- Total raised over $268M.

Series B was led by TCV. Other named investors include Oliver Jung, Leblon Capital, Kindred Ventures, Repeat VC, Zone 2 Ventures, Audeo Ventures, Quadri Ventures, First Order Fund, Vocal Ventures, Maiora Ventures, Nordstar, Seven Stars Ventures, Hexa Capital, Alpha Square Group, GSBackers, OurCrowd, Alumni Ventures, Global Growth Fund, and others. Earlier investors included Y Combinator, Kindred Ventures, Contrary, Oliver Jung, Glade Brook Capital Partners, Seven Stars, Leblon Capital, Fellows Fund, Alumni Ventures, Quadri Ventures, Vocal Ventures, Phosphor Capital, and SV Angel.

The January 2026 release stated ARR surpassed $40M since regulatory approval in July 2025. That is company-reported and should be treated as a marketing/press claim unless verified by financials.

Sources: [Series B release](https://www.corgi.insure/press-releases/series-b), [PRNewswire Jan 2026 release](https://www.prnewswire.com/news-releases/corgi-insurance-raises-108-million-receives-regulatory-approval-to-launch-the-first-full-stack-insurance-carrier-for-startups-302657727.html).

## Regulatory structure

Corgi is vertically integrated but not a single simple legal box.

Public disclaimers say:

- The Corgi group includes licensed insurance producers, affiliated licensed insurance carriers, and affiliated claims administration operations.
- Corgi owns and controls multiple licensed risk-bearing insurance entities domiciled in various U.S. states.
- Insurance products may be underwritten by affiliated carrier entities or third-party carrier partners.
- Producer entities distribute insurance and act as authorized agents; they do not underwrite risk themselves.
- Claims may be administered by affiliated claims operations or third-party administrators.
- Producer licenses are listed in 45 U.S. jurisdictions.

The site footer says coverage is underwritten by Technology Risk Retention Group, Inc. (TRRG), a risk retention group organized under the Liability Risk Retention Act, and warns that state insurance insolvency guaranty funds are not available for policies issued by a risk retention group. Corgi Insurance Services, Inc. is listed as a licensed producer and program administrator, not the insurer.

Sources: [Disclaimers & Licensing](https://www.corgi.insure/disclaimers), [producer licenses](https://www.corgi.insure/broker-licenses).

## AI usage

Corgi's own disclaimer is the best public description of AI usage. It says Corgi uses AI, machine learning, algorithms, and automated tools across marketing, quoting, underwriting, pricing, policy issuance, claims processing, fraud detection, and customer service. It says material coverage and claims decisions remain subject to human oversight and automated tools are tested/monitored for fairness, accuracy, and non-discrimination.

This is stronger than vague "AI-powered" marketing because it names operational surfaces. But it still does not disclose model architecture, vendors, evaluation methodology, data sources, or automation rate.

Source: [Disclaimers & Licensing](https://www.corgi.insure/disclaimers).

## Customers and demand

Named customers/testimonials include Intryc, Bland, Origami, AthenaHQ, Eragon, Series, Sorcerer, Hallway, Pax, Imagine AI, Finni Health, and Artisan. Case studies show the wedge is not abstract "insurance optimization"; it is concrete:

- Enterprise customer asks startup for proof of insurance.
- Founder needs a policy/certificate quickly to close the deal.
- Traditional broker flow is slow and confusing.
- Corgi quotes/binds fast and creates documents/Slack support.

Sources: [Customers](https://www.corgi.insure/customers), [Intryc case study](https://www.corgi.insure/customers/intryc), [Eragon case study](https://www.corgi.insure/customers/eragon), [Imagine AI case study](https://www.corgi.insure/customers/imagine-ai).

## ETF / financial products side quest

Corgi also has Corgi Strategies, LLC, which launched Founder-Led ETFs. SEC filings say Corgi Strategies is a Delaware LLC registered as an SEC investment adviser and adviser to Corgi ETF Trust I. FDRS launched as the Founder-Led ETF, and FDRX as the 2x Daily ETF. The About page shows ETF tickers and values.

This is unusual for an insurance startup. It suggests the founders are not only building startup insurance; they are building a broader "AI financial infrastructure" company, with insurance as the first or main operating wedge and ETFs as another financial product line.

Sources: [SEC filing](https://www.sec.gov/Archives/edgar/data/2078265/000207826526000003/corgietftrust1_fdrsfdrx497.htm), [Nasdaq/PRNewswire ETF release](https://www.prnewswire.com/news-releases/corgi-an-ai-startup-lists-fdrs-on-nasdaq-302651983.html), [About](https://www.corgi.insure/about).

## Competitive positioning

Corgi compares itself against legacy brokers, Embroker, Vouch, and traditional insurance carriers. The pitch:

- Faster quote/bind.
- Direct carrier/program structure instead of broker middlemen.
- Startup-specific policy packages.
- AI-enhanced underwriting/policy/claims ops.
- Same-day documents.
- Slack/white-glove support.

The strongest wedge is distribution + speed, not only underwriting math. Startups buy insurance at moments of urgency: fundraising, hiring, office lease, enterprise contract, SOC 2, security review, board formation. Corgi meets them at that point and makes the transaction feel like modern software.

## What is actually impressive

- They picked a real pain: founders hate insurance until a customer/investor forces it.
- They own more of the stack than a broker.
- They have regulatory/producer coverage across many jurisdictions.
- They compress quote/bind/document workflows into minutes for common lines.
- They use founder/YC distribution extremely well.
- They are expanding aggressively into new verticals, including trucking per Series B release.
- They turned insurance into a culturally visible startup brand, which is rare.

## Biggest unresolved questions

- How much of ARR is earned premium vs commission/fee revenue vs run-rate gross written premium?
- What is the loss ratio?
- What is the risk retention structure?
- How much risk is actually retained by Corgi-affiliated carriers vs ceded/reinsured?
- Which products are truly underwritten by Corgi-controlled carriers?
- What percentage of quotes/binds are fully automated?
- What percentage of claims are handled internally?
- What is AI doing in underwriting beyond workflow acceleration?
- How durable is startup insurance as a niche once incumbents copy instant quote UX?

## Strategic lesson

Corgi is a better example of AI-native vertical infrastructure than most AI app companies. The lesson is: own the regulated workflow, compress the slow path, and use AI as an operating advantage inside the system, not as the product headline alone.
