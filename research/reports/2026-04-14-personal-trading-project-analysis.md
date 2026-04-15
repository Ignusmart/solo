# Personal Trading/Income Project — Deep Research Analysis

**Date**: 2026-04-14
**Context**: Jobelo wants a personal (non-product) crypto trading/income system that genuinely makes money. Constraints: $1–5k starting capital (scalable to ~$25k), solo build, leverage his smart-contract audit expertise.
**Status**: Research complete → Recommendation delivered

## Methodology

Three parallel research agents, each with distinct focus and non-overlapping scope, using WebSearch + WebFetch against live 2026 data sources (EigenPhi, Dune, DeFiLlama, CoinGlass, GitHub, academic papers, trader post-mortems):

1. **MEV & liquidation competition landscape** — who's profiting, who's saturated, which niches are under-contested
2. **Non-MEV income strategies** — funding arb, airdrops, sniping, yield, stat arb, market making
3. **Build reality** — open-source tooling, dev time, infra cost, historical solo-builder success rates

---

## Honest Top-Level Finding

**Across 15+ strategies researched, the solo-builder success rate is <20%. 60–80% of similar GitHub repos are abandoned within 12 months.** Retail MEV bots consistently lose money against professional operators with sub-10ms RPC latency.

This isn't a reason to skip — but any "expected earnings" figures below are conditional on you being in the 20% that ship and iterate.

---

## Candidate Matrix

| Strategy | Realistic $/mo ($5k cap) | Time-to-Profit | 3-mo Infra Cost | Solo Success Rate | Auditor Edge | Verdict |
|---|---|---|---|---|---|---|
| **Pendle PT/YT arb** | $500–$1,600 | 45–75 days | ~$200–$500 | Higher (new niche) | **Very high** | ⭐ **TOP** |
| **Liquidations — small protocols** (Silo, Fluid, Gearbox, Morpho Blue per-market) | $500–$2,000 | 30–45 days | $700–$2,500 | <15% | **Very high** | ⭐ **TOP** |
| **Stablecoin depeg arb** | $0–$3,000 (episodic) | opportunity-dependent | ~$300 | N/A (event-driven) | **Very high** | Secondary |
| **Oracle-lag arb on zkSync Era** | $500–$3,750 | 45–60 days | ~$500 | Unknown | Moderate | Worth exploring |
| **Funding rate arb** | $250–$750 net | 15–30 days | ~$300 | Medium | Low (4/10) | Edge compressed — already scaffolded |
| **Liquidations — Aave/Compound majors** | $0–$1,200 | 60–90 days | $2,000+ | <10% | High | **Skip** (saturated) |
| **Solana memecoin sniping** | $500–$2,000 | 10–20 days | $600–$2,400 | ~10% | High (honeypot filter) | **Skip** (gambling, not engineering) |
| **DEX-DEX atomic arb (L1)** | $0 | N/A | $3,000+ | <5% | Low | **DEAD** for solo |
| **JIT liquidity** | $0 | N/A | $5M+ capital | ~0% | Low | **DEAD** for solo |
| **Airdrop farming (50+ wallets)** | $30–$300 (lottery) | 3–9 months | $1,000–$3,600 | ~5% net positive | Low | **Skip** (85% sybil-filtered) |
| **Stat arb / CEX mean reversion** | $0–$150 | N/A | ~$300 | <5% | None | **DEAD** (edge gone) |
| **Leveraged yield loops (sUSDe/Aave)** | $30–$170 | 1 week | ~$100 | Variable | Moderate | **Trap** ($4.2B systemic risk, unpriced) |
| **HLP vault passive** | <$10 | instant | $0 | N/A | None | Too diluted — Skip |

---

## Key Insights (non-obvious)

1. **Your audit edge is largest in Pendle, liquidations, and depeg arb — NOT in MEV searching or sniping.** MEV/sniping are latency races; your reading speed on contracts doesn't compensate. Pendle PT/YT, lending protocol liquidation math, and stablecoin redemption mechanics are *interpretation* games where you have a real advantage.

2. **Ethereum L1 is dead for solo builders across every strategy.** 90%+ of MEV value now captured by private builders + validators. Don't touch mainnet as a solo entrant in 2026. Base, Arbitrum, zkSync, and Solana are the only viable playing fields.

3. **Capital requirements are uniformly higher than marketing suggests.** Real minimums:
   - Liquidations (small): $5–10k working capital + $2k infra buffer
   - Pendle PT/YT: $5–15k
   - Funding arb: $5k to overcome fees ($1k won't work)
   - Sniping: $1–5k but ~90% of snipers lose money

4. **The funding arb we already scaffolded is valid but modest.** At $5k capital, realistic net $250–$750/mo. Edge is compressing vs 2023–2024. It's a baseline income strategy, not a wealth-builder.

5. **Pendle PT/YT arbitrage is the most under-contested niche that fits your exact skill profile.** Pendle's SY (Standardized Yield) contracts + underlying yield-source contracts are non-trivial to read correctly. Most quant-oriented traders can't audit the yield math; most auditors don't trade. Few builders occupy this intersection.

6. **Liquidation bots on small protocols work but infrastructure cost is real.** $700–$2,500 in RPC + gas losses during the first 3 months of tuning. Payback period 3–6 months. Competition on Aave/Compound is lost; competition on Morpho Blue *per-market*, Silo, Gearbox, Fluid is winnable.

7. **Surprising dead strategies**: JIT liquidity (top 25 wallets own $740B of $760B flow), stat arb (edge completely competed away), airdrop farming (85% sybil-filtered, 88% of tokens collapse 60%+ post-TGE).

---

## Tension: Capital Gap

Your stated capital is $1–5k. Research shows:
- **$1–3k**: none of the strategies reliably net-positive after infra + fees
- **$5–10k**: Pendle + small-protocol liquidations become viable
- **$15–25k**: Funding arb + liquidations + Pendle all become meaningful

**Implication**: to avoid building infra that can't pay for itself, either commit to scaling capital to $5–10k range before going live, or deliberately build at near-zero infra cost (self-hosted VPS, free-tier everything) until Phase 2.

---

## Recommendation

### Primary target: **Pendle PT/YT arbitrage bot**

**Why this, and not the others:**

- **Skill fit is maximal.** Reading SY contracts, understanding PT burn mechanics, auditing the underlying yield sources (Lido, Aave positions, Ethena, Kamino) — this is *literally* your day job applied to trading decisions instead of security findings.
- **Under-contested.** Agent 1 confirmed: "Few builders have this expertise; edge exists." Most yield traders are not auditors; most auditors don't trade. This intersection is thin.
- **Low infrastructure cost.** Doesn't need archive nodes or sub-10ms RPC. Standard Alchemy/Helius free-to-paid tier works. ~$50–$200/month infra.
- **Capital-scalable.** Works at $5k; scales cleanly to $25k+.
- **Real edge decay is slow.** Not latency-arbitrage — it's *interpretation* arbitrage. Your edge persists as long as Pendle has new pools launching faster than the market prices them.
- **Time-to-profit realistic.** 45–75 days, which aligns with "ship something real in 2–3 months."

**Realistic earnings**: $500–$1,600/month at $5–10k capital, higher upside during yield-market volatility.

### Secondary (layer on after Pendle works): **Liquidation bot on Morpho Blue + Silo**

**Why:**
- Your audit brain reads lending contracts precisely — oracle timing, LTV quirks, incentive math
- Morpho Blue's per-market design means *each market* is essentially its own liquidation game with its own competition level — you can hunt for underserved ones
- Silo on Arbitrum + Morpho Blue on Base have lighter competition than Aave/Compound
- Can reuse the funding-arb scaffold's Python async patterns + Postgres persistence

**Realistic earnings**: $500–$2,000/month once tuned. Higher variance than Pendle.

### Tertiary (opportunistic, ready-to-fire): **Stablecoin depeg arb trigger**

**Why:**
- Zero baseline cost; just a monitoring bot that alerts you + auto-executes when any tracked stablecoin deviates >X%
- Auditor edge is maximal — you know which stablecoins have arbitrage-friendly redemption flows vs. restrictive ones
- Episodic income ($0 in quiet months, $500–$3k in event months)
- Minimal build time (1 week on top of existing monitor scaffold)

### What NOT to build (even though they were on the table)

| Rejected | Reason |
|---|---|
| Solana memecoin sniping | Gambling with a filter, not engineering. 10% win rate. Below your dignity and misuses your skills. |
| Ethereum L1 MEV/arb | 90% of value captured by builders. Dead for solo. |
| JIT liquidity | Capital requirement $5M+. Institutional only. |
| Leveraged yield loops | Systemic risk ($4.2B sUSDe bomb) unpriced. You'd be picking up pennies in front of a steamroller. |
| Airdrop farming | 85% sybil-filtered. 88% of tokens collapse post-TGE. Lottery with negative EV at sub-50-wallet scale. |
| Stat arb / CEX market making | Edge completely competed away. Need $50k+ and institutional latency. |

---

## Implementation Plan Sketch (Pendle-primary)

### Phase 0 (this week): Research Pendle landscape specifically
- Map all active Pendle pools by chain (Ethereum, Arbitrum, Base, BNB, Sonic)
- Identify pools where SY underlying is non-trivial (multi-step yield sources)
- Track PT/YT spread vs. theoretical fair value using public data
- Build a static dashboard (reuse `projects/trading/` scaffold)

### Phase 1 (weeks 2–4): Pricing model
- Build a PT fair-value calculator accounting for underlying yield, decay to maturity, liquidity discount, protocol risk
- Compare model price vs. market price for all pools
- Identify recurring mispricings (which pools? how long do they persist?)

### Phase 2 (weeks 5–6): Execution bot
- Trading against Pendle via their Router / SDK
- Start with $5k capital on 2–3 identified pools
- Size per trade: 10% max per pool

### Phase 3 (ongoing): Expand coverage + add liquidation bot as second strategy

---

## Honest Risks (stated plainly)

1. **Solo crypto bot failure rate is 60–80% within 12 months.** You might be in the majority who don't ship iteratively enough to find real edge.
2. **Pendle protocol risk.** Smart contract exploit or governance failure could wipe positions. Size accordingly.
3. **Yield market collapse.** If broader DeFi yields compress (ETH staking goes to 2%, LST spreads collapse), Pendle mispricings shrink proportionally.
4. **Opportunity cost.** Hours spent here are hours not spent on ScanAble/APIDelta flywheel (per your portfolio strategy). Be honest about which you actually prioritize.
5. **Competitive audits on Code4rena/Sherlock remain higher $/hour** than any bot at your capital range. If pure income is the goal, more audits = more money. Trading bots win only if you value the scalable/passive-ish nature.

---

## Sources

- arxiv.org/html/2507.13023v1 — MEV Searchability & Profitability
- medium.com/dragonfly-research — Liquidator Bot Landscape
- eigenphi.io — Live MEV data
- writings.flashbots.net — MEV and Limits of Scaling
- arxiv.org/html/2406.02172v1 — L2 Arbitrage Dynamics
- coinglass.com/FrArbitrage — Funding rate scanner
- docs.morpho.org/learn/concepts/liquidation — Morpho Blue mechanics
- pawelurbanek.com/rust-mev-bot — Solo MEV failure case study (~$750/mo infra, lost capital)
- github.com/solendprotocol/liquidator, jito-labs/mev-bot, solidquant/mev-templates — Reference implementations
- bydfi.com/pendle-yield-tokenization-deep-dive — Pendle mechanics
- hummingbot.org/release-notes/1.27.0/ — Funding rate strategy
- rockawayx.com/defi-vaults-explained-2026-guide — Systemic leverage risk
- nansen.ai/articles/linea-airdrop-sybil-detection — 85% sybil filter rate
- SEC/CFTC joint guidance, March 17 2026 — 16 digital commodities classified, leverage allowed

---

## Next Step

Decide: **(a) commit to Pendle-first build**, or **(b) continue audits as primary + trading as side-R&D**, or **(c) scale capital first to $10–25k before committing**. Then we scaffold the Pendle research phase in `projects/trading/pendle/`.
