# Private Transactions on Solana for Stablecoin Business Payments

Date: 2026-05-07

## Executive Summary

There is no single Solana switch that makes an arbitrary transaction private. A normal Solana transaction exposes the program, account addresses, signers, and instruction data needed for execution. Solana's docs describe transactions as signed messages containing instructions, account addresses, and a recent blockhash, and those messages are processed by the network as-is.

For an Altitude-style stablecoin business OS, privacy has to be designed at the payment architecture layer. The main options are:

1. Token-2022 Confidential Transfers: native encrypted token amounts, but not sender/recipient privacy, and currently unavailable on mainnet/devnet because the ZK ElGamal program is disabled during audit.
2. Shielded pools / zk private payment protocols: hide sender-recipient links and sometimes amounts by depositing into a pool and withdrawing/transferring with ZK proofs. This is the closest model to "business payments private on-chain", but protocol maturity varies heavily.
3. Stealth addresses: generate a fresh recipient address per payment. This hides recipient identity from casual observers, but amount and source funding flows are still visible unless combined with relayers or shielded pools.
4. TEE / private execution environments such as MagicBlock Private Ephemeral Rollups: run sensitive state and logic inside hardware-encrypted execution, with Solana settlement. Promising for compliant enterprise workflows, but introduces TEE/operator trust assumptions.
5. Confidential compute / MPC such as Arcium: useful for private business logic, matching, risk scoring, or encrypted inputs/outputs, but not a drop-in private USDC transfer rail.
6. Jito / private transaction submission: hides transactions from some public routing paths before landing and helps MEV/front-running, but once landed the transaction is public. This is not business-payment privacy.
7. Off-chain/internal ledger with on-chain net settlement: practical for a business OS if users accept custody or controlled accounts. Public chain only sees aggregate settlements, while invoices/payroll/vendor details stay in your database. This is operationally strong but changes the custody, compliance, and trust model.

Best near-term architecture: use normal USDC/SPL settlement plus strong operational privacy now; integrate a pluggable privacy rail later. If you need product-ready privacy today, the realistic candidates are shielded-pool integrations, stealth-address flows, or a TEE-based rail. Token-2022 Confidential Transfers are strategically important but not currently usable on mainnet as of this research.

## What "Private" Can Mean

### Pre-confirmation privacy

The transaction is hidden from regular RPC paths or MEV searchers before it lands. Jito's block engine can forward transactions directly to validators with MEV protection and supports bundles, revert protection, and sandwich-mitigation patterns. This helps with trading execution, not with hiding business activity after settlement.

### On-chain data privacy

The public ledger cannot reveal one or more of:

- amount
- sender
- recipient
- business purpose or memo
- balance
- graph relationship between wallets

This is the layer your use case needs.

### Operational privacy

Even if the blockchain is public, you prevent observers from learning business context by using fresh addresses, internal ledgers, batching, net settlement, delayed settlement, custodial omnibus wallets, and carefully controlled metadata.

## Option Matrix

| Option | Hides amount | Hides sender/recipient link | Supports existing USDC? | Production readiness | Fit for stablecoin business OS |
|---|---:|---:|---:|---|---|
| Jito/private RPC submission | No | No | Yes | High | Use for MEV/landing only |
| Token-2022 Confidential Transfers | Yes | No | Usually no, requires Token-2022 mint with extension | Blocked today on mainnet/devnet per Solana docs | Good later for amount privacy |
| Shielded pool / zk private payment rail | Often yes | Yes | Depends on protocol bridge/pool support | Mixed | Best conceptual fit |
| Stealth addresses | No by itself | Partially, recipient unlinkability | Yes for basic transfers | Emerging | Good lightweight privacy layer |
| TEE private rollup/payment rail | Yes, if designed that way | Yes, if designed that way | Potentially | Emerging | Strong enterprise/compliance fit |
| Arcium/MPC confidential compute | Private inputs/outputs | Not transfer privacy by itself | N/A | Emerging | Useful for private workflows around payments |
| Off-chain ledger + net settlement | Yes from public chain | Yes from public chain | Yes | High if you can manage custody/compliance | Most practical MVP path |
| Mixer-style third-party sites | Maybe | Maybe | Varies | Very risky | Avoid unless audited, reputable, compliant |

## Detailed Options

### 1. Native Token-2022 Confidential Transfers

Solana's Token-2022 Confidential Transfer extension lets token accounts transfer without revealing transfer amounts. The public chain still sees token account addresses. Solana's current docs explicitly say only transfer amounts and balances are private; token account addresses remain public.

Important blocker: Solana's docs currently say the ZK ElGamal program is temporarily disabled on mainnet and devnet during security audit, so confidential transfers are currently unavailable and examples will not run. Treat this as a future rail, not an MVP dependency.

Stablecoin implications:

- It works for mints created with the confidential transfer extension.
- You cannot simply make ordinary SPL USDC private unless the issuer/mint and wallet/account ecosystem support the extension.
- It can include an auditor public key, which is useful for regulated business payments.
- It does not hide counterparties, invoice relationships, token account addresses, or timing patterns.

Use when:

- You issue your own stable-value token or work with an issuer that supports Token-2022 confidential transfer.
- Your primary concern is amounts and balances, not counterparty graph privacy.

Do not use as sole solution when:

- You need payroll/vendor identities hidden.
- You need existing USDC transfers private today.

### 2. ZK Shielded Pools / Private Payment Protocols

Model: users deposit SOL/SPL tokens into a shared pool, receive shielded notes or private balances, and later transfer or withdraw using ZK proofs. This breaks the direct source-destination link and can hide amounts, depending on design.

Elusiv is the historical Solana example. QuickNode's guide describes Elusiv as a Solana ZK privacy protocol with a shared pool, private transfers, viewing keys, and a relayer/warden component. However, the same guide marks Elusiv as legacy and notes Elusiv announced sunsetting on February 29, 2024. So Elusiv is useful as a pattern, not a vendor to build on.

Current/emerging projects found during research include Cloak, Penta, ZKnon, Zecra, Solanon, zkVoid, ExePay, and similar "Solana privacy mixer/private payments" sites. Maturity varies substantially; many have marketing pages but limited visible audits, usage, or docs. For business payments, only consider protocols with:

- public source code
- reproducible circuits/provers
- independent audits
- clear relayer/compliance model
- viewing keys or audit disclosure
- stablecoin liquidity and withdrawal depth
- sanctions/abuse controls suitable for your users

Use when:

- You need strongest on-chain privacy for sender, receiver, and amount.
- You can accept protocol integration risk and potential regulatory scrutiny.

Risks:

- Shared pools can attract compliance attention.
- Poor anonymity sets create false privacy.
- Deposits and withdrawals are still visible; timing and amount correlation attacks matter.
- Relayers can become metadata chokepoints.

### 3. Stealth Addresses

Model: a recipient publishes a meta-address. The sender derives a unique one-time address for every payment. Observers see funds going to fresh addresses, not obviously to the recipient's known business wallet.

Cloak's docs describe this pattern as ECDH-derived one-time addresses on Solana. On-chain, each payment goes to a fresh address that appears unrelated to other recipient addresses.

This is useful but incomplete:

- It hides recipient wallet identity better than sending to a known address.
- It does not hide amount.
- It does not hide the sender's funding wallet unless a relayer, custody layer, or shielded source is also used.
- The recipient must scan announcements or use an indexer/viewing key system.
- Spending from stealth addresses can re-link funds if consolidated carelessly.

Use when:

- You want a practical privacy upgrade for invoices and vendor payments.
- You can tolerate public amounts.
- You combine it with batching, relayers, and careful withdrawal/consolidation.

### 4. TEE / Private Ephemeral Rollups

MagicBlock's Private Ephemeral Rollup model uses Intel TDX TEEs plus Solana-native ephemeral rollups to run sensitive logic in a hardware-protected environment. MagicBlock docs describe PER as enabling confidential state, scalability, composability, and compliance. Their docs also list Private Payments API endpoints such as deposit, transfer, withdraw, private balance, and swap.

This is a strong candidate for enterprise payments because it can support:

- confidential balances
- private transfers
- permissioned access
- audit/compliance controls
- fast UX
- selective disclosure

Tradeoffs:

- You trust TEE security, attestation, and operator infrastructure.
- This is newer infrastructure than plain Solana programs.
- Final settlement visibility depends on how the rollup commits state back to Solana and how assets are escrowed/delegated.

Use when:

- You want "business privacy with compliance", not pure cypherpunk anonymity.
- You need invoices, payroll, vendor payments, treasury workflows, and audit access.

### 5. Confidential Compute / MPC

Arcium is not a direct private transfer mechanism, but it is relevant if your product needs private business logic. Arcium docs describe encrypted inputs and outputs, including `Enc<Shared, T>` and `Enc<Mxe, T>`, where plaintext visibility is restricted to client+MXE or MXE only.

Use cases around payments:

- private credit/risk scoring before payment
- private invoice matching
- confidential payroll computation
- confidential treasury policy evaluation
- private stablecoin routing decisions

This can complement a payment rail, but it does not by itself hide a normal SPL token transfer on-chain.

### 6. Jito / Private Submission / Bundles

Jito's low-latency transaction send forwards transactions directly to validators and provides MEV protection. Bundles can contain up to five transactions, execute sequentially and atomically, and support revert protection. Jito also documents `jitodontfront` sandwich-mitigation patterns.

Use this for:

- private pre-confirmation routing
- reducing sandwich/front-run risk for swaps
- atomic multi-step settlement
- better landing probability

Do not confuse it with:

- amount privacy
- counterparty privacy
- balance privacy
- hiding instructions after confirmation

Once a Jito-submitted transaction lands, it is still a normal Solana transaction visible to explorers and indexers.

### 7. Off-chain Ledger + On-chain Net Settlement

For an Altitude-like business OS, this may be the most practical MVP:

- Customers deposit USDC into organization vaults or controlled subaccounts.
- Your app maintains invoices, payroll, vendor bills, approvals, and internal balances off-chain.
- You batch and net actual on-chain settlement.
- Public chain sees fewer aggregate movements, not every business event.
- You provide per-organization audit exports and internal controls.

Variants:

- non-custodial smart account/vault per organization
- custodial omnibus ledger
- MPC-controlled treasury wallets
- stablecoin payment processor model
- hybrid: on-chain for external settlement, off-chain for internal business activity

This does not provide cryptographic on-chain privacy, but it is often what businesses actually need: competitors, employees, and vendors cannot trivially inspect operational details.

Tradeoffs:

- Custody, money transmission, KYC/AML, and accounting obligations become central.
- Users must trust your accounting system unless you build proofs/reserves/audit trails.
- You need strong security controls and role-based approvals.

## Recommended Architecture for Your Product

### MVP

Build a private-by-design stablecoin operations layer:

- no public memos containing invoice/vendor/customer data
- fresh addresses or vault subaccounts per organization and purpose
- batched vendor payouts and payroll
- optional delayed settlement windows
- internal ledger for invoice/payment state
- Jito/private submission for swaps and urgent settlement
- compliance-grade audit exports for the organization owner

### Next

Add a pluggable privacy rail abstraction:

```text
PaymentIntent
  -> public USDC transfer
  -> stealth address transfer
  -> shielded pool transfer
  -> TEE/private rollup transfer
  -> future Token-2022 confidential transfer
```

Expose privacy levels clearly:

- Public: normal USDC transfer.
- Discreet: fresh address, no memo, batched settlement.
- Shielded: private pool or TEE rail.
- Confidential amount: Token-2022 confidential transfer when available.

### Longer Term

If Token-2022 Confidential Transfers become available and stablecoin issuers support them, integrate them for amount privacy. Pair with stealth addresses or a shielded/TEE layer if you need counterparty privacy.

## What I Would Avoid

- Relying on Jito/private RPC as the privacy solution.
- Using unaudited mixer websites for business payments.
- Putting invoice numbers, customer names, payroll metadata, or vendor references in Solana memos.
- Claiming "no one can know what we are doing" unless the design has been threat-modeled against chain analysis, RPC logs, relayers, timing correlation, exchange deposits/withdrawals, and app telemetry.
- Building on Token-2022 Confidential Transfers as an immediate mainnet launch dependency while the ZK ElGamal program remains disabled.

## Source Notes

- Solana transactions: https://solana.com/docs/core/transactions
- Solana Confidential Transfer docs: https://solana.com/docs/tokens/extensions/confidential-transfer
- Solana Token Extensions page: https://solana.com/solutions/token-extensions
- Jito Low Latency Transaction Send: https://docs.jito.wtf/lowlatencytxnsend/
- MagicBlock PER docs: https://docs.magicblock.gg/pages/tools/tee/introduction
- MagicBlock PER quickstart/API navigation: https://docs.magicblock.gg/pages/private-ephemeral-rollups-pers/how-to-guide/quickstart
- QuickNode legacy Elusiv guide: https://www.quicknode.com/guides/solana-development/legacy/privacy-with-elusiv
- Cloak stealth address docs: https://www.cloaksdk.com/docs/concepts/stealth-addresses
- Arcium encrypted input/output docs: https://docs.arcium.com/developers/arcis/input-output
