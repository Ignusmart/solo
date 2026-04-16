# Iteration 20: Web3 Non-Security Tool/SaaS Exploration

**Date**: 2026-04-15
**Strategy**: First-ever systematic scan of Web3 non-security verticals. Explored 20+ sub-categories leveraging Jobelo's Solidity/EVM/DeFi expertise while respecting the Web3 security off-limits constraint.

---

## Search Strategy

Expanded into verticals never previously explored:
1. **DeFi yield/position tooling** — dashboards, alerts, backtesting, yield APIs
2. **DAO governance tooling** — voting, delegation, treasury management
3. **Web3 developer tools** — Foundry plugins, gas CI, ABI management, multi-chain deploy
4. **Pendle ecosystem tooling** — yield calculators, PT/YT strategy tools
5. **On-chain analytics (non-security)** — protocol revenue, whale tracking, token unlocks
6. **Web3 infrastructure** — RPC monitoring, webhooks, event streaming, transaction simulation
7. **Web3 AI agent infrastructure** — on-chain agent tooling, identity, payments
8. **Crypto finance (non-trading)** — tax reporting, payroll, airdrop tracking

## Sources Checked

- Google (20+ targeted searches across all categories)
- Alchemy dApp Store (ABI tools: 13 listed, webhooks: 7 listed, DAO tools: 29 listed)
- vaults.fyi (DeFi yield API — $399-999/mo, serves Etherscan/Kraken/Gauntlet)
- DeFi Monitor (health factor alerts — Aave, Spark, Morpho Blue, Compound, Uni V3)
- DeFiLlama (free yield/TVL/protocol data API)
- GitHub (foundry-gas-diff, foundry-storage-check — both free OSS)
- Product Hunt / HN / Reddit (no unmet demand signals found)
- CoinGlass, Nansen, Arkham (whale/funding rate/derivatives data)
- Token Terminal ($300+/mo protocol revenue analytics)
- Multiple competitor sites visited via WebFetch

---

## Results: 20+ Sub-Categories Scanned — All Saturated or Off-Limits

### Saturated (5+ competitors each)

| Category | Key Competitors | Kill Reason |
|----------|----------------|-------------|
| DeFi Portfolio Tracking | Zerion, Zapper, DeBank, DeFi Saver, APY.vision | 5+ major tools, free tiers |
| DAO Governance | Snapshot, Tally, Aragon | Mature platforms |
| Foundry Gas CI | foundry-gas-diff (free GH Action) | Free OSS, no pricing power |
| RPC Monitoring/Failover | Built into Alchemy, QuickNode, dRPC, Chainstack | Provider feature, not standalone product |
| DeFi Alerts | DeFi Monitor, Open DeFi Notification Protocol (30+ protocols) | Covered for major protocols |
| Transaction Simulation | Tenderly (dominant, VC-funded) | Enterprise tool, not micro-SaaS territory |
| Whale Tracking | Nansen ($9/mo), Arkham, CoinGlass, DexCheck | 7+ tools, Nansen at $9/mo sets floor |
| Web3 Webhooks | Alchemy, QuickNode, Moralis, Chainbase, GetBlock, Dispatch | 6+ providers |
| Multi-chain Deploy | thirdweb (2000+ chains), Remix, Foundry scripts | Well-served |
| Airdrop Tracking | Alpha Drops, Drops.bot, Earnifi, AirdropScan, AirdropAlert | 6+ tools |
| DeFi Yield API | vaults.fyi ($399+/mo), DeFiLlama (free) | Gap at $29-99/mo but requires massive data pipeline |
| ABI Tools | 13+ on Alchemy store, ContractABI, HashEx, Dune | Free tools dominate |
| Token Unlock Tracking | CoinMarketCap, CoinGecko, DeFiLlama, CoinGlass, Tokenomist, DropsTab | 7+ tools |
| Gas Calculators | RareSkills, free multi-chain calculators, hardhat-gas-reporter | Free tools |
| IL Calculators | DailyDeFi, CoinStats, Poolfish, Qalc.ai, open-source tools | 5+ free tools |
| DAO Treasury | Streamflow, Cashmere, Remox, HQ.xyz, Safe | Multiple tools |
| DeFi Tax | CoinTracker, Koinly, TokenTax, CoinTracking, CryptoTaxCalculator, Blockstats | 10+ tools |
| Web3 AI Agent Infra | 282 projects, $4.3B market, Coinbase Agentic Wallets | VC-funded gold rush (kill pattern #14) |
| Crypto Payroll | Request Finance, Superfluid | Covered |
| Protocol Revenue | TokenTerminal ($300+/mo), DeFiLlama (free) | Gap exists but massive build |

### Off-Limits (Web3 security conflict)

| Category | Why Off-Limits |
|----------|---------------|
| Smart Contract Monitoring | Explicitly listed in off-limits rule |
| Proxy Upgrade Monitoring | Smart contract monitoring variant |
| Contract ABI Change Detection | "APIDelta for contracts" — compelling concept but falls under smart contract monitoring |
| DeFi Security Alerts | Security product |

### Promising But Below Bar (18/30 — below 22 minimum)

**Idea A: DeFi Governance Watch** — Track governance proposals across Aave/Compound/Morpho/Pendle, alert users when parameter changes affect their positions.
- Gap: 3 (real — no tool connects "governance vote passed" → "your position is affected")
- Build: 3 (need to parse multiple governance APIs, 3-4 weeks)
- Money: 2 (intermittent use, low individual WTP, DeFi users resist subscriptions)
- Competition: 4 (no direct competitor doing position-specific governance alerts)
- Distribution: 3 (DeFi Twitter, Reddit r/defi, SEO possible)
- Automated marketing: 3 (crypto communities, keyword-targetable)
- **Total: 18/30** — Below 22 bar. Also borderline off-limits (monitoring/alerting for risk factors).

**Idea B: Pendle Yield Compass** — Third-party PT/YT yield comparison, strategy calculator, historical yield data for Pendle markets.
- Gap: 3 (no third-party tools — Pendle's own UI is the only option)
- Build: 4 (1-2 weeks with Pendle SDK, Jobelo has deep expertise)
- Money: 2 (tiny TAM — Pendle-only users, hard to justify $29/mo)
- Competition: 5 (zero competitors)
- Distribution: 2 (Pendle community only, can't SEO broadly)
- Automated marketing: 2 (niche audience, no broad keyword targeting)
- **Total: 18/30** — Below 22 bar. Zero competitors but TAM too small.

**Idea C: APIDelta Web3 Dev Vertical** — Not a new product. Position APIDelta to monitor Web3 SDK/library breaking changes (ethers.js→viem migration, OpenZeppelin upgrades, Foundry changelog, chain-specific SDK changes).
- This is a GTM strategy for APIDelta, not a new product to score.
- **Recommendation**: Add Web3 SDK monitoring as APIDelta use case. Zero incremental build.

---

## Key Insights

### Web3 mirrors the general SaaS saturation pattern
After scanning 20+ Web3 sub-categories, the same kill patterns from iterations 1-19 apply:
- **Every category has 5-30+ tools** (kill pattern #9)
- **Free tools set the floor** (DeFiLlama, Etherscan, CoinGecko — all free)
- **VC-funded players dominate infrastructure** (Tenderly, Nansen, Alchemy, The Graph)
- **New categories fill fast** (AI agents: 0 → 282 projects in ~12 months)
- **Platform absorption is real** (RPC providers absorbing monitoring, alerts, webhooks)

### The Web3 security constraint eliminates the best ideas
The most compelling concepts (contract ABI change detection, proxy upgrade monitoring, deployment changelog tracking) all fall under "smart contract monitoring" — explicitly off-limits. Jobelo's deepest edge (Solidity audit expertise) can't be productized without hitting the Webacy conflict.

### Non-security Web3 tools have a pricing problem
DeFi users expect tools to be free (DeFiLlama, Etherscan, CoinGecko set expectations). The B2B buyer (Web3 dev teams) pays for infrastructure (Alchemy, Tenderly, The Graph) but those are VC-backed with free tiers that crush micro-SaaS pricing.

---

## Conclusion

**8 consecutive zero-result iterations (13-20).** Web3 non-security tools follow the same saturation patterns as general SaaS. No new idea scored above 18/30, well below the 22/30 minimum bar.

The one actionable output: **position APIDelta for Web3 dev teams** as a market segment (monitor SDK/library changelogs). Zero new build required.

---

Running total: 20 iterations, 220+ ideas (20+ Web3-specific), APIDelta at 22/30 remains the only idea meeting the bar. **NO NEW IDEAS ABOVE BAR.**
