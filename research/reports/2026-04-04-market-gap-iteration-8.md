# Iteration 8: Bottom-Up Signal Hunting

**Date**: 2026-04-04
**Approach**: Bottom-up signal hunting (specific complaints, real user pain) instead of top-down vertical scanning.
**Search queries executed**: 20+ across Reddit, HN, indie hackers, product comparisons, and competitive landscape checks.

---

## Critical Finding: ScopeShield Has New Direct Competitors

Before evaluating new ideas, the most important discovery from this iteration is that **ScopeShield's competitive landscape has changed since Iteration 2**:

### StopScopeCreep (stopscopecreep.com)
- **What it does**: Revision tracking, change requests with client approval in 60 seconds, shareable client link (no login), automatic reminders (Day 1, 7, 14), deliverable tracking.
- **Pricing**: Free (1 project), Pro (unlimited) -- pricing not publicly listed but appears to be $9-19/mo range.
- **Positioning**: "Stop doing free work." Exactly the same positioning ScopeShield would use.
- **SEO**: Strong content marketing with blog posts ranking for "scope creep freelancer," "scope creep statistics," "scope creep examples," etc.

### ClearTimeline (cleartimeline.com)
- **What it does**: Log agreements, track scope changes, get client sign-offs. "Gives you evidence" rather than enforcing pricing.
- **Positioning**: Professional project management framing. Client portal with documentation.
- **Status**: Appears newer, less established than StopScopeCreep.

### MicroGaps Analysis
- MicroGaps.com published a detailed gap analysis (2026-03-01) noting: "1.57 Billion Freelancers Send Proposals in Google Docs. Every Tool Charges Per Seat for Sales Teams."
- Plutio ($19/mo flat) and Bonsai are actively targeting the HoneyBook migration window.

### Impact on ScopeShield Score
- **Competition score must be downgraded from 3 to 2**. StopScopeCreep is a near-exact competitor. ClearTimeline is adjacent. Plutio and Bonsai cover the broader proposal-to-scope workflow.
- **Revised ScopeShield total: 18/25** (was 19).
- The HoneyBook migration window is real, but StopScopeCreep is already positioned to capture it.

---

## Search Queries & Sources

### Queries executed:
1. `"I would pay for" site:reddit.com SaaS tool 2025 2026` -- no results
2. `"why is there no" site:reddit.com SaaS tool app 2025 2026` -- generic results
3. `"someone please build" software tool SaaS 2025 2026` -- listicle results (Lovable, Elementor, BigIdeasDB)
4. `"shut up and take my money" site:reddit.com software tool app 2025` -- no results
5. `site:news.ycombinator.com "ask hn" what tool do you wish existed 2025 2026` -- found [HN thread](https://news.ycombinator.com/item?id=46345827) and [Oct 2025 wish thread](https://news.ycombinator.com/item?id=45500937)
6. `micro SaaS profitable solo founder under radar 2025 2026 reddit indie hackers` -- portfolio builders ($22-28K/mo), BigIdeasDB validation methodology
7. `reddit "paying for a tool" frustration terrible 2025 automation workflow` -- Retool 5x pricing jump, Zapier complexity complaints
8. `"AI wrapper" niche tool actually works profitable 2025 2026` -- generic "pick a niche" advice
9. `reddit "switched from" "nothing good" software 2025` -- no results
10. `niche data API product profitable micro SaaS 2025 2026` -- generic listicles
11. `stopscopecreep.com pricing features review freelancer 2026` -- **CRITICAL: direct ScopeShield competitor exists**
12. `cleartimeline.com freelancer scope tracking 2026` -- **second competitor found**
13. `"contract change order" freelancer software tool 2026 alternative honeybook` -- Plutio, Bonsai, Taskip, Dubsado all competing
14. `"AI agent" "monitoring" OR "observability" 2026` -- 15+ tools (Langfuse, LangSmith, Braintrust, AgentOps). Crowded with VC money.
15. `"prompt management" OR "prompt versioning" tool SaaS 2026` -- 5+ dedicated tools (Maxim AI, Langfuse, PromptLayer, MLflow). Filling in fast.
16. `"proposal software" freelancer "too expensive" 2025 2026` -- HoneyBook 89% price hike, Dubsado raised prices Dec 2025. Migration window confirmed.
17. `reddit freelancer "scope creep" tool software 2025 2026` -- 57% of agencies lose $1K-5K/mo. StopScopeCreep already has SEO presence.
18. `"AI code review" "too many false positives" 2026` -- CodeRabbit, Qodo, CodeAnt, Panto. 15+ tools. Pain is real but space crowded.
19. `"MCP server" marketplace paid premium 2026` -- Apify, MCP Market, Glama, Docfork. Monetization models emerging but still early.
20. `"smart contract" auditor assistant tool 2026` -- AuditBase, AI-augmented audits. Off-limits per constraints.

---

## Ideas Analyzed

### Idea 1: AuditScope -- Competitive Audit Scoping & Findings Dashboard for Security Researchers

**KILLED IMMEDIATELY**: Off-limits. Smart contract security is Jobelo's day job at Webacy. Even if it targets auditors rather than protocols, it's adjacent enough to conflict. Moving on.

---

### Idea 2: BriefForge -- AI Proposal Generator for Freelancers ($19/mo, flat-rate, no per-seat)

**Problem**: Freelancers send proposals in Google Docs because dedicated tools charge per-seat (Proposify $19/seat, Better Proposals $19/seat) or bundle into expensive all-in-one platforms (HoneyBook $39-129/mo, Bonsai $25-50/mo). The 89% HoneyBook price hike and Dec 2025 Dubsado increase created a migration wave.

**Signal source**: MicroGaps analysis (2026-03-01): "1.57 Billion Freelancers Send Proposals in Google Docs." Multiple "HoneyBook alternatives" articles from Jan-Mar 2026 confirm migration.

**Why current solutions fail**:
- Per-seat pricing punishes solo operators who collaborate with subcontractors
- All-in-one platforms (HoneyBook, Bonsai, Plutio) bundle too many features at higher prices
- Google Docs works but lacks e-signatures, analytics, and professional templates
- No tool does AI-generated proposals from a brief/intake form

**MVP scope (1-2 weeks)**:
- Paste client brief or fill intake form -> AI generates proposal with scope, timeline, pricing
- Professional template with e-signature
- Scope tracker (what was agreed)
- Change order generator when scope changes
- $19/mo flat, unlimited proposals, unlimited collaborators

**Revenue model**: $19/mo flat. MRR ceiling: $30-50K (1,500-2,500 paying freelancers).

**Why Jobelo's skills give an edge**: Full-stack TS, AI/LLM integration, async-only distribution. No blockchain needed.

**Kill criteria**: If Plutio or Bonsai add AI proposal generation in their current pricing tier. If StopScopeCreep expands into proposals.

**Score**:
| Gap | Build | Money | Comp | Dist | Total |
|-----|-------|-------|------|------|-------|
| 3   | 4     | 3     | 2    | 4    | **16** |

**Verdict**: The proposal space is already being served by Plutio ($19/mo flat), Proposal Air, and others. Adding AI generation is a feature, not a product. The per-seat complaint is already being addressed by Plutio's flat-rate model. **Does not beat ScopeShield.**

---

### Idea 3: PromptDiff -- Prompt Version Control for Small AI Teams

**Problem**: Teams building AI features treat prompts as hardcoded strings in code. No version history, no diff, no rollback, no way for non-engineers to iterate without triggering a deployment. This is painful when prompt changes affect output quality.

**Signal source**: DEV Community article "Keep Your Prompts Organized" (2026), Braintrust/Maxim/Langfuse all positioning around this pain. HN threads about developer tools wished for in 2026.

**Why current solutions fail**:
- Langfuse, LangSmith, Maxim, PromptLayer exist but are **enterprise-priced and complex**
- Most bundle observability + evaluation + prompt management together
- Small teams (2-5 devs) building AI features don't need full observability -- they just need prompt versioning
- No simple "Git for prompts" that's as easy as a shared spreadsheet but with version control

**MVP scope (2 weeks)**:
- Web UI: create/edit prompts with variables
- Version history with diff view
- API endpoint to fetch latest prompt version (or specific version)
- Environment support (dev/staging/prod)
- Rollback in one click
- Simple collaboration (share link, no per-seat)

**Revenue model**: Free (3 prompts), $19/mo (unlimited), $49/mo (team with RBAC). MRR ceiling: $20-40K.

**Why Jobelo's skills give an edge**: AI/agentic systems expertise means he understands the prompt engineering workflow deeply. Full-stack TS for fast build. API-first design from backend experience.

**Kill criteria**: If Langfuse (open source) ships a standalone prompt management UI that's easy to self-host. If Cursor/Copilot add prompt management. If the market converges on "prompts in code" as the right pattern (prompt-as-code movement).

**Score**:
| Gap | Build | Money | Comp | Dist | Total |
|-----|-------|-------|------|------|-------|
| 3   | 4     | 3     | 2    | 3    | **15** |

**Verdict**: The gap is real but narrowing fast. Langfuse is open source and already has prompt management. PromptLayer has been around since 2023. Maxim, Braintrust, and LangSmith all cover this. The "simple standalone" angle could work but distribution is hard in dev tools -- Cursor/IDEs absorb features. **Does not beat ScopeShield.**

---

### Idea 4: PayChaser -- Automated Invoice Follow-Up for Freelancers

**Problem**: 63% of freelancers wait 30+ days to get paid. 43% of invoices are paid outside agreed terms (28+ day average delay). Chasing payments is awkward and time-consuming.

**Signal source**: Indie Hackers post: "Chasing overdue invoices is awkward -- I built a small tool to automate reminders." Statistics from invoicing industry reports. Reddit freelancer communities.

**Why current solutions fail**:
- Chaser ($39-199/mo) is enterprise-focused, too expensive for freelancers
- Bonsai, FreshBooks, Wave have basic reminders but no escalation sequences
- No tool creates a "gentle to firm" escalation sequence with the right tone
- Most invoicing tools treat reminders as an afterthought feature
- The indie hacker who posted about building this got significant engagement

**MVP scope (1 week)**:
- Connect to Stripe/invoicing tool OR paste invoice details
- AI generates escalation sequence (friendly reminder -> firm follow-up -> final notice -> late fee warning)
- Scheduled sends at configurable intervals
- Payment tracking dashboard
- "Recovered $X" metric

**Revenue model**: $9/mo (5 active invoices), $19/mo (unlimited). MRR ceiling: $15-25K.

**Why Jobelo's skills give an edge**: Simple build, AI text generation, API integrations. Fast MVP.

**Kill criteria**: If FreshBooks/Wave add AI escalation sequences. If the price point is too low for meaningful revenue.

**Score**:
| Gap | Build | Money | Comp | Dist | Total |
|-----|-------|-------|------|------|-------|
| 2   | 5     | 2     | 2    | 3    | **14** |

**Verdict**: Chaser exists at the enterprise level. Every invoicing tool has basic reminders. The AI escalation angle is incremental, not transformative. Low price point ($9-19/mo) with high churn risk (freelancers cancel between projects). **Does not beat ScopeShield.**

---

## Summary Table

| Rank | Idea | Gap | Build | Money | Comp | Dist | Total |
|------|------|-----|-------|-------|------|------|-------|
| 1 | BriefForge (AI proposals) | 3 | 4 | 3 | 2 | 4 | **16** |
| 2 | PromptDiff (prompt versioning) | 3 | 4 | 3 | 2 | 3 | **15** |
| 3 | PayChaser (invoice follow-up) | 2 | 5 | 2 | 2 | 3 | **14** |

---

## The Honest Assessment: Can Anything Beat ScopeShield?

**No.** But ScopeShield itself is weaker than we thought.

### What bottom-up hunting revealed:
1. **ScopeShield's competition has increased.** StopScopeCreep is a near-exact competitor with strong SEO. ClearTimeline is adjacent. This drops ScopeShield from 19 to **18/25**.
2. **The freelancer tools space is more competitive than Iteration 2 assessed.** Plutio, Bonsai, Taskip, and Dubsado are all fighting for the HoneyBook migration wave. New startups (StopScopeCreep, ClearTimeline, Proposal Air) have entered.
3. **No bottom-up signal produced a score above 16/25.** The pain points are real but the solutions already exist or are emerging.
4. **AI agent observability and prompt management are crowded with VC money** (Langfuse, LangSmith, Braintrust, Maxim, AgentOps). Not micro-SaaS territory.
5. **Dev tools continue to be absorbed by IDEs and platforms** (Cursor, GitHub Copilot, Claude Code). Features, not products.

### Revised Top 3 after Iteration 8:
1. **ScopeShield** -- 18/25 (revised down from 19 due to StopScopeCreep/ClearTimeline)
2. **PostPilot** -- 18/25 (unchanged, tied for #1)
3. **BriefBot** -- 18/25 (unchanged, three-way tie)

### The real conclusion:
After 8 iterations, 24 ideas deep-dived, 90+ spaces dismissed, and 20+ bottom-up searches -- **no idea has scored above 19/25, and the leader just dropped to 18/25 due to new competitors.** The three-way tie at 18/25 (ScopeShield, PostPilot, BriefBot) suggests the answer isn't "which one to build" but "pick one and validate fast." ScopeShield still has the best ROI story ("recovered $X in unbilled work") but the competitive moat is thinner than assumed.

**Recommendation**: Validate all three with a 48-hour async survey (20 freelancers for ScopeShield, 20 content creators for PostPilot, 20 service businesses for BriefBot). Build whichever gets the strongest signal. Stop researching.

---

*Sources:*
- [StopScopeCreep](https://stopscopecreep.com/)
- [StopScopeCreep Pricing](https://stopscopecreep.com/pricing)
- [ClearTimeline](https://www.cleartimeline.com/problems/scope-creep)
- [MicroGaps: Proposal Software for Freelancers](https://www.microgaps.com/gaps/2026-03-01-proposal-software-freelancers)
- [57% of Agencies Lose $1K-$5K Monthly to Scope Creep](https://dev.to/valynx_saas/57-of-agencies-lose-1k-5k-monthly-to-scope-creep-heres-why-it-keeps-happening-39hf)
- [Scope Creep Statistics 2026](https://stopscopecreep.com/blog/scope-creep-statistics)
- [HoneyBook Alternatives 2026](https://www.hellobonsai.com/blog/honeybook-alternatives)
- [Best Proposal Software for Freelancers 2026](https://www.plutio.com/freelancer-magazine/best-proposal-software-for-freelancers)
- [Ask HN: What developer tool do you wish existed in 2026?](https://news.ycombinator.com/item?id=46345827)
- [BigIdeasDB: 50 Micro SaaS Ideas Validated from 238K+ Complaints](https://bigideasdb.com/micro-saas-ideas-2026)
- [30 Micro SaaS Ideas Reddit Is Begging You to Build](https://www.greensighter.com/blog/micro-saas-ideas)
- [Prompt Versioning Tools 2026](https://dev.to/debmckinney/keep-your-prompts-organized-best-versioning-tools-in-2026-4f95)
- [AI Agent Observability Tools 2026](https://arize.com/blog/best-ai-observability-tools-for-autonomous-agents-in-2026/)
- [Indie Hackers: Chasing Overdue Invoices](https://www.indiehackers.com/post/chasing-overdue-invoices-is-awkward-i-built-a-small-tool-to-automate-reminders-4f89bae266)
