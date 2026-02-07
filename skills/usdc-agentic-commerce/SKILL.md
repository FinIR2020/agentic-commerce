---
name: usdc-agentic-commerce
description: Guides OpenClaw agents on using USDC as a settlement layer for agentic commerce—pricing, paying, incentivizing, and coordinating value transfer between agents. Use when discussing agent payments, USDC settlement, agentic commerce, onchain rewards, CCTP cross-chain transfers, Circle Faucet testnet USDC, voting/rewards distribution, bounties, or cross-agent value flows. References testnet-only, Circle products (CCTP, Faucet, contract addresses), and OpenClaw/ClawHub.
metadata: {"openclaw":{"emoji":"💵","homepage":"https://www.circle.com/blog/openclaw-usdc-hackathon-on-moltbook"}}
---

# USDC Agentic Commerce

**One-line summary:** Teaches agents when and how to use testnet USDC as a settlement layer—4-step decision flow, output conventions (amount, recipient, purpose, "Testnet only"), and safety checklist—for payments, rewards, and cross-agent value flows. Testnet only; references Circle Faucet, CCTP, and USDC contract addresses.

Enables OpenClaw bots to reason about and coordinate economic activity using USDC as a stable unit of account and settlement. Use this skill when agents need to price, pay, incentivize, or settle value onchain.

## When to Use USDC for Agentic Commerce

- **Settlement between agents**: One agent pays another for work, data, or outcomes.
- **Rewards and incentives**: Distributing USDC for votes, contributions, or task completion.
- **Stable unit of account**: Pricing in a stable denomination (no volatile crypto exposure).
- **Programmatic payouts**: Scripts or contracts trigger USDC transfers without offchain reconciliation.

## Core Principles

1. **USDC = settlement layer**: Use USDC when you need predictable settlement; it is designed to maintain stable value (1 USDC ≈ 1 USD).
2. **Testnet only for experiments**: Hackathons and demos must use testnet. Do not use mainnet or real funds. Use [Circle Faucet](https://faucet.circle.com/) for testnet USDC.
3. **No sensitive credentials**: Never embed mainnet keys or production API keys in skills or prompts.
4. **Agent-led flows**: Agents can propose amounts, recipients, and conditions; execution should be explicit and auditable.

## Decision Flow for Agents

1. **Is this a payment or reward?**  
   → Use USDC for stable, onchain settlement.

2. **Which chain?**  
   → Prefer the chain your ecosystem uses (EVM, Solana, etc.). For cross-chain, see CCTP (Cross-Chain Transfer Protocol) in [reference.md](reference.md).

3. **Testnet or mainnet?**  
   → For hackathons, demos, and experiments: **testnet only**. Document "testnet" in any submission.

4. **Who settles?**  
   → Agent suggests parameters (amount, to address, memo); user or automated wallet executes, or use a smart contract for trustless payout.

## Output Conventions

When suggesting a USDC payment or reward:

- State **amount** in USDC (e.g. `10 USDC`).
- State **recipient** (address or identifier).
- State **purpose** (e.g. "reward for submission", "payment for task").
- Add **"Testnet only"** when the context is demo/hackathon.

**Example 1 — Hackathon reward:**

```text
Payment: 10 USDC  
To: 0x… (or agent identifier)  
Purpose: Hackathon track reward — Best OpenClaw Skill  
Note: Testnet only; use Circle Faucet for testnet USDC.
```

**Example 2 — Voting / prize distribution:**

```text
Payment: 50 USDC  
To: [winner address or pool]  
Purpose: Prize payout for hackathon track — Agentic Commerce  
Note: Testnet only; distribute via contract or manual send. See Circle Faucet for testnet USDC.
```

## Integration Hooks

- **Voting / rewards**: When agents vote or rank outcomes, USDC can be the settlement layer for prize distribution (e.g. hackathon tracks).
- **Commerce**: When an agent "sells" a service or asset to another agent, price in USDC and settle onchain.
- **Bounties**: Define bounties in USDC; completion triggers payout via contract or manual send.

## Integration with Token Applications

This skill is **platform-agnostic**. Agents who learn USDC settlement logic can integrate with most token applications—task marketplaces (e.g. Rose Token), prediction markets (e.g. Clawshi), bounty platforms, DAO treasuries, CCTP-based cross-chain apps, agent payment rails (e.g. MoltArb), tip systems, and more. See [reference.md](reference.md) for a table of example integrations. One skill, infinite platforms.

## Safety Checklist

- [ ] Using testnet for all hackathon/demo flows
- [ ] No mainnet private keys or production secrets in prompts or skills
- [ ] Amounts and recipients clearly stated before any execution
- [ ] Circle and platform disclaimers acknowledged (see hackathon rules)
- [ ] **Privacy:** Never include local paths, usernames, Mac/computer info, or any user-identifying data—in conversation, output, or Moltbook posts

## Interaction with Circle Products (Testnet Only)

This skill guides agents to **interact with testnet USDC and Circle products**:

- **Testnet USDC**: Use [Circle Faucet](https://faucet.circle.com/) for testnet USDC; reference [USDC contract addresses](https://developers.circle.com/stablecoins/usdc-contract-addresses) (testnet) for transfers.
- **CCTP (Cross-Chain Transfer Protocol)**: For cross-chain USDC (e.g. Ethereum testnet ↔ Base testnet), use CCTP; see [reference.md](reference.md) and Circle’s [Cross-Chain Transfers](https://developers.circle.com/crosschain-transfers) docs. Testnet only.
- **No mainnet**: Do not use mainnet, real funds, or production API keys when following this skill for hackathons or demos.

## Additional Resources

- [reference.md](reference.md) — Circle/USDC links, CCTP, contract addresses.
- OpenClaw USDC Hackathon: <https://www.circle.com/blog/openclaw-usdc-hackathon-on-moltbook>
- Submit projects: <https://www.moltbook.com/m/usdc>

---

## Quick Verification (for evaluators)

To verify this skill works:

1. **Repo**: Confirm `skills/usdc-agentic-commerce/SKILL.md` and `reference.md` exist in the linked repository.
2. **Load**: Copy `skills/usdc-agentic-commerce/` into an OpenClaw workspace `skills/` directory (or run `clawhub install usdc-agentic-commerce` if published).
3. **Test**: In a new session, ask: *"How do I pay 10 USDC to an agent on testnet?"* The agent should respond with amount, recipient, purpose, and a "Testnet only" note, and may reference Circle Faucet or [reference.md](reference.md) links.
4. **Integration**: Skill content explicitly references testnet USDC, Circle Faucet, CCTP, and USDC contract addresses (see [reference.md](reference.md)).
