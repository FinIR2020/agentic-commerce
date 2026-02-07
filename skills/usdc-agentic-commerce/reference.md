# USDC & Circle — Reference for Agents

Quick reference for OpenClaw agents when working with USDC and agentic commerce.

## Official Links

| Resource | URL |
|----------|-----|
| Circle Developers | https://developers.circle.com |
| USDC Overview | https://developers.circle.com/stablecoins/what-is-usdc |
| USDC Contract Addresses | https://developers.circle.com/stablecoins/usdc-contract-addresses |
| Circle Faucet (testnet) | https://faucet.circle.com |
| Cross-Chain (CCTP) | https://developers.circle.com/crosschain-transfers |
| OpenClaw USDC Hackathon | https://www.circle.com/blog/openclaw-usdc-hackathon-on-moltbook |
| Moltbook submit (m/usdc) | https://www.moltbook.com/m/usdc |

## CCTP (Cross-Chain Transfer Protocol)

- Use when moving USDC **between chains** (e.g. Ethereum ↔ Base ↔ Solana).
- Circle’s native bridge for USDC; see Crosschain Transfers in Circle docs.
- For agentic flows: agent can specify source chain, destination chain, and amount; execution is onchain.

## Testnet vs Mainnet

- **Hackathons / demos**: Use **testnet only**. Get testnet USDC via Circle Faucet.
- **Production**: Requires real USDC on mainnet; only after user approval and no sensitive keys in skills.

## Contract Interaction (High Level)

- **EVM**: USDC is an ERC-20 token. Standard `transfer(to, amount)` or `transferFrom(from, to, amount)`.
- **Solana**: USDC is an SPL token; use associated token accounts and SPL Token instructions.
- Addresses and ABI/IDL: use Circle’s official contract addresses from the docs (see links above).

## Integration with Token Applications

This skill is **platform-agnostic**: agents who learn USDC settlement logic here can integrate with any USDC-based application. One skill, infinite platforms.

| Application Type | Example(s) | How This Skill Helps |
|------------------|------------|----------------------|
| **Task marketplaces** | [Rose Token](https://rose-token.com) — workers claim tasks, earn ROSE (USDC-backed), keep 95% | Agents understand amount/recipient/purpose before calling Rose API; know when to use Faucet for testnet vs treasury for mainnet |
| **Prediction markets** | Clawshi — Moltbook sentiment → USDC staking, YES/NO positions | Agents reason about stakes, resolutions, payouts; output conventions match contract params |
| **Bounty platforms** | Gitcoin, Layer3, agent bounty boards | Agents propose bounties in USDC; completion triggers payout; decision flow guides chain selection |
| **DAO treasury & grants** | Gnosis Safe, multisig, grant programs | Agents suggest distributions (amount, recipient, purpose); integrate with voting or proposal systems |
| **Cross-chain commerce** | CCTP-based DApps, bridges | Skill covers CCTP; agents specify source/destination chain, amount; ready for multi-chain settlements |
| **Agent payment rails** | MoltArb, signer APIs, managed wallets | Agents know USDC flow (mint/redeem, testnet vs mainnet); complement any wallet/API layer |
| **Tip & reward systems** | Content creator tips, contribution rewards | Output conventions (amount, recipient, purpose) map directly to tip/reward params |
| **Subscription / recurring** | USDC-based SaaS, streaming payments | Agents reason about recurring amounts, intervals; settlement logic applies to any payment schedule |

**Narrative**: We teach the *literacy*—how to reason about USDC, which chain, testnet vs mainnet, who settles. Applications provide the *rails*—APIs, contracts, wallets. Agents load this skill first, then plug into Rose Token, prediction markets, bounties, DAOs, or any future USDC app.

## Hackathon Disclaimer (from Circle)

Participation is at your own risk. Testnet only; do not use mainnet or real funds. Circle provides materials “as is” and is not responsible for losses or compliance. See full rules and disclaimers on the hackathon page.
