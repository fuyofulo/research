# Provenance: Private Transactions on Solana

Date: 2026-05-07

## High-confidence Sources

1. Solana Core Transactions
   - URL: https://solana.com/docs/core/transactions
   - Used for: baseline that normal Solana transactions contain instructions, account addresses/signatures, and are public after landing.

2. Solana Confidential Transfer Extension
   - URL: https://solana.com/docs/tokens/extensions/confidential-transfer
   - Used for: current availability blocker; what Token-2022 confidential transfers hide and do not hide; basic flow.
   - Key finding: ZK ElGamal program temporarily disabled on mainnet/devnet; only amounts/balances are private, token account addresses remain public.

3. Solana Token Extensions
   - URL: https://solana.com/solutions/token-extensions
   - Used for: institutional/token-extension context and caveats such as extension readiness and auditor model.

4. Jito Low Latency Transaction Send
   - URL: https://docs.jito.wtf/lowlatencytxnsend/
   - Used for: pre-confirmation/private routing, direct validator forwarding, bundles, MEV protection, sandwich mitigation.
   - Key finding: useful for landing/MEV; not post-confirmation data privacy.

5. MagicBlock Private Ephemeral Rollups
   - URLs:
     - https://docs.magicblock.gg/pages/tools/tee/introduction
     - https://docs.magicblock.gg/pages/private-ephemeral-rollups-pers/how-to-guide/quickstart
   - Used for: TEE/private rollup privacy model and private payments API surface.

6. QuickNode Legacy Elusiv Guide
   - URL: https://www.quicknode.com/guides/solana-development/legacy/privacy-with-elusiv
   - Used for: historical shared-pool ZK privacy architecture and warning that Elusiv is sunset/legacy.

7. Cloak Stealth Address Docs
   - URL: https://www.cloaksdk.com/docs/concepts/stealth-addresses
   - Used for: stealth-address model and limitations.

8. Arcium Encrypted Inputs/Outputs
   - URL: https://docs.arcium.com/developers/arcis/input-output
   - Used for: encrypted input/output and MPC/confidential-compute applicability.

## Lower-confidence / Needs Diligence

The research also surfaced many Solana privacy or mixer-style projects, including ExePay, Finqora, Solnexis, Cipher, Sentinel, Aegiz, ZKnon, zkVoid, Solanon, Penta, Zecra, Cloak, and others. I did not treat these marketing pages as proof of production readiness. Before using any of them, verify:

- public source code
- deployed program IDs
- audits
- TVL/liquidity/anonymity set
- circuit/prover implementation
- relayer trust model
- sanctions/compliance posture
- stablecoin support
- active maintenance

## Research Queries

- Solana private transactions confidential transfers Token-2022 ElGamal zero knowledge docs
- Solana privacy private transactions shielded pools Light Protocol Elusiv Arcium Helius Shredstream Jito private mempool
- Solana Token-2022 Confidential Transfers official documentation
- Solana MEV private transaction Jito bundle documentation sendTransaction
- Elusiv Solana private transactions docs
- MagicBlock private ephemeral rollups TEE Solana docs
- Arcium Solana confidential computing encrypted transaction private payments
- Solana stealth addresses private payments standard
