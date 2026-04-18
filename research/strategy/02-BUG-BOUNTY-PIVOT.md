# Bug Bounty: Why It's Hard and What to Do Instead

## 2026-04-18 Reality Check (supersedes original framing)

The "pivot to competitive audits" below was the right *direction* but has not produced revenue. Data from `projects/bounty/claude-bug-bounty/BOUNTIES.md`:
- **~170 projects audited, $0 paid** as of 2026-04-18
- **~130 EXHAUSTED** (0 submittable findings, most due to 5-20 prior audits + Certora FV)
- **7 submitted + rejected** (alchemix N/A, 40acres out-of-scope, trustee-plus N/A, iotex Informative, dexalot-omnivault not-reachable, firedancer not-reachable, termmax DUP)
- **6 pending**: ssvnetwork ESCALATED 2026-04-17 (strongest), glow-finance Critical, dexalot Critical, chainlink-c4 QA, intuition-c4 Medium, layer-zero Medium
- **~20 BLOCKED** on platform rep tiers (multipli, gmx-immunefi hold confirmed Mediums)

Root cause is **target saturation**, not harness failure. The time-allocation table below is therefore on hold — do not treat "60% competitive audits" as a live recommendation until at least one submission pays. See also: `memory/project_bounty_roi_warning.md`.

---

## Current Situation (original)
- You started a bounty project (~/Repos/bounty with 8+ protocol repos)
- Finding it hard to get payouts
- This is normal. Here's why and what to do about it.

## Why Bug Bounties Are Hard for Income

1. **First-reporter-wins**: Even if you find the same bug, only one person gets paid
2. **Severity disputes**: Projects downgrade findings to pay less
3. **Time investment is unpredictable**: 40 hours on one protocol can yield $0
4. **Top auditors dominate**: They have tooling, reputation, and speed advantages
5. **Payout delays**: Some platforms take months to process

## The Pivot: Competitive Audits Instead

Competitive audits (Code4rena, Sherlock, Hats Finance) are structurally better:

| Factor | Bug Bounties | Competitive Audits |
|--------|-------------|-------------------|
| **Payment** | First reporter only | All unique valid findings paid |
| **Timeline** | Open-ended | Fixed contest period (1-4 weeks) |
| **Payouts** | Unpredictable | Pool-based, more predictable |
| **Competition** | Against all hunters forever | Against contest participants only |
| **Reputation** | Hard to build | Leaderboard visibility |

### Platforms to Focus On

1. **Code4rena** - Largest, best payouts, most contests
   - URL: code4rena.com
   - Focus: EVM protocols
   - Avg payout for medium findings: $500-5000

2. **Sherlock** - Higher quality, curated contests
   - URL: sherlock.xyz
   - Focus: DeFi protocols
   - Requires stake but higher per-finding payouts

3. **Hats Finance** - Newer, less competition
   - URL: hats.finance
   - Focus: Various Web3 protocols
   - Good for building initial reputation

## Your Competitive Advantage for Audits

Based on your bounty folder:
- You've studied Lido (CSM, dual governance, stonks) - governance + staking protocols
- You've studied Spark (ALM controller, gov relay, rewards, vaults) - DeFi vaults
- You've studied CapyFi and Veda boring vault - vault strategies
- You know Foundry deeply (all projects use it)

**Focus your audits on**: Governance mechanisms, staking protocols, vault strategies, and cross-chain messaging. These are your strongest domains.

## Hybrid Strategy

Don't fully abandon bounties, but shift your time allocation:

| Activity | Time Allocation | Expected Monthly |
|----------|----------------|-----------------|
| Competitive audits | 60% | $2K-10K (variable) |
| Building a product (Tier 1 ideas) | 30% | $0 initially, compounds |
| Bug bounties (only protocols you already know) | 10% | $0-5K (bonus) |

## Action Items

- [ ] Sign up for Code4rena if not already
- [ ] Sign up for Sherlock
- [ ] Check upcoming contests that match your domain expertise
- [ ] Set up alerts for new contests in governance/staking/vault categories
- [ ] Keep the bounty repos as study material for audit contests
