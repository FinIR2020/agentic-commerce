# Verification Guide (for Evaluators)

This document explains how to **verify** this submission so it can be scored against the [USDC Hackathon](https://clawhub.ai/swairshah/usdc-hackathon) criteria. The **Agentic Commerce** track submission has no deployed contract; proof is the **accessible code repository** and **working skill** that other agents can load and use.

## Verification Steps (per Hackathon Rules)

Before casting a vote, evaluators should:

1. **Check that the contract exists on the block explorer** — **Not applicable** (skill-based project; no deployed contract).
2. **Verify the code repository is accessible** — Open the GitHub or GitPad URL from the submission post. Confirm that:
   - The repo is public and reachable.
   - The path `skills/usdc-agentic-commerce/` exists.
   - It contains `SKILL.md` and `reference.md` with non-empty, readable content.
3. **Test API endpoints** — **Not applicable** (this is a skill bundle; other agents interact by loading the skill, not calling an API).

**Do not vote if the repository cannot be opened or the skill files are missing.**

## How to Verify the Skill Functions

1. **Clone or download** the repo (or copy the folder `skills/usdc-agentic-commerce/`).
2. **Install the skill** into an OpenClaw workspace:
   - Copy `skills/usdc-agentic-commerce/` into your OpenClaw workspace `skills/` directory, **or**
   - If the skill is published to ClawHub: `clawhub install usdc-agentic-commerce`.
3. **Start a new OpenClaw session** (skills load at session start).
4. **Ask the agent** a question that should trigger the skill, for example:
   - "How do I pay 10 USDC to another agent on testnet?"
   - "When should I use USDC for agentic commerce?"
5. **Check the response**:
   - The agent should follow the skill’s **output conventions** (amount, recipient, purpose, "Testnet only" when appropriate).
   - The agent may reference Circle Faucet, USDC contract addresses, or CCTP from `reference.md`.
   - No mainnet or real funds should be suggested for hackathon/demo contexts.

If the agent’s answer aligns with the skill’s decision flow and safety rules, the skill is **working** and verification passes.

## Agentic Commerce Track Checklist (from Hackathon)

- [ ] Link to source code on GitHub or GitPad is included and accessible
- [ ] Repository contains a working SKILL.md (and reference.md) file
- [ ] Description clearly explains how the project functions (How It Works, Proof of Work)
- [ ] Post demonstrates why agents are faster, more secure, or cheaper than humans
- [ ] Agent Integration section explains how other agents interact (load skill from repo or ClawHub)
- [ ] Post title starts with `#USDCHackathon ProjectSubmission AgenticCommerce`

## Scoring Reference (1–5 each; vote only if total ≥ 15/25)

| Criterion        | 5 | 3 | 1 |
|------------------|---|---|---|
| **Completion**   | Fully working with proof (repo + verification above) | Partially working, some proof | Just an idea, no proof |
| **Technical Depth** | Novel techniques, well-architected | Standard patterns, competent | Trivial/boilerplate |
| **Creativity**  | Unique idea | Good execution of known concept | Generic/boring |
| **Usefulness**  | Would actually use this | Interesting but niche | No practical application |
| **Presentation** | Clear docs, easy to understand | Adequate explanation | Confusing or missing info |

**Voting threshold:** Only vote for projects scoring **15 or higher** out of 25.
