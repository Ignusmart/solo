# Slack & Teams Marketplace Gap Analysis

> **Date**: 2026-04-05
> **Purpose**: Identify micro-SaaS opportunities in Slack App Directory and Microsoft Teams Apps marketplace
> **Market size**: Slack 750K+ orgs, Teams 320M+ MAU

---

## 1. Who's Making Money in Slack Apps?

| App | Revenue | Model | Team Size |
|-----|---------|-------|-----------|
| **Polly** (polls/surveys) | ~$9.7M ARR (2024) | Per-user/mo, freemium | Funded startup |
| **Standuply** (async standups) | $25K/mo within 8 months, bootstrapped | Per-user tiers + usage limits | 4-person team (Siberia) |
| **Geekbot** (async standups) | Undisclosed, 200K+ users (GitLab, Netflix, Shopify) | $2.50-3/user/mo | Small team |
| **DailyBot** | Undisclosed, growing | Per-user tiers | Small team |
| **Abot** (anonymous messages) | $50K total profit, ~$1.5K MRR on autopilot | Flat tiers, no free plan | **Solo founder** (Rails) |

**Key takeaway**: Solo-founder Slack apps can reach $1-5K MRR on autopilot. Funded Slack apps reach $5-25K+ MRR. The Slack App Directory itself is a meaningful acquisition channel (Standuply got 750 signups in 2 weeks from a featured listing).

---

## 2. Typical Slack App Pricing

- **Per-user/month** is the dominant model: $1-5/user/mo for utilities, $3-8/user/mo for workflow tools
- **Per-workspace flat rate** works for simpler bots: $10-49/mo for SMB tiers
- **Freemium with usage limits** is the proven growth lever (Standuply's revenue jumped when they added limits)
- Annual billing discount of 15-20% is standard

---

## 3. Workflow Gaps Analyzed

### A. Async Standups (Geekbot/DailyBot territory)
**Gap**: Pricing. Geekbot is $3/user/mo with no free tier. Small teams (5-10 people) pay $15-30/mo for a bot that sends 3 questions daily.
**Real gap**: None meaningful. This is a solved, saturated category. Geekbot, DailyBot, Standuply, Sup Bot, Standup Alice all compete. Slack's own Workflow Builder can replicate basic standups for free.
**Verdict**: SKIP. Commoditized.

### B. Incident Management for SMBs
**Gap**: PagerDuty ($21-49/user/mo) and OpsGenie (dead -- Atlassian ending sales, shutdown April 2027) leave a hole for teams of 5-20 engineers who need on-call + incident channels without enterprise pricing.
**Existing alternatives**: incident.io (Slack-native, but enterprise-priced), Rootly (same), Better Stack (free tier exists but limited), AlertOps ($5/user/mo entry), Spike.sh ($7/user/mo).
**Buyer**: Engineering leads at seed/Series A startups, 5-20 engineers.
**Verdict**: Crowded even at SMB tier. Spike.sh and Better Stack already serve this. SKIP.

### C. Knowledge Management / Search Across Channels
**Gap**: Slack's native search is weak for institutional knowledge. "Same questions answered repeatedly" is a universal complaint. Slack AI (bundled in Business+ at $15/user/mo) added enterprise search in 2025, but it requires the expensive tier.
**Existing**: Guru ($10/user/mo), Question Base, eesel AI. All are well-funded.
**Buyer**: Ops/HR/engineering managers at 50-500 person companies.
**Verdict**: Slack itself is absorbing this with AI features. Third-party funded players already here. Platform risk is extreme -- Slack can kill you overnight. SKIP.

### D. Approval Workflows
**Gap**: Multi-step approvals (PTO, expense, discount, access requests) that live entirely in Slack. Slack Workflow Builder added branching but remains primitive for real approval chains (no escalation, SLA tracking, audit trails).
**Existing**: Approveit, Wrangle, LedgerUp. All small, none dominant.
**Buyer**: Ops managers at 20-200 person companies without full HRIS/ERP.
**Pricing**: $3-5/user/mo or $49-99/workspace/mo flat.
**Verdict**: INTERESTING. Small competitors, none with clear PMF. But the market may be small (companies needing approvals but not big enough for Jira Service Management or ServiceNow). MAYBE.

### E. Time Tracking in Slack
**Gap**: No dominant Slack-native time tracker. Most integrate (Toggl, Harvest, Clockify) but require leaving Slack.
**Existing**: Harvest, Toggl Track, Clockify all have Slack integrations. Timebot exists but is small.
**Buyer**: Agency owners, freelancer teams, consultancies.
**Verdict**: Slack integration is a feature of existing time trackers, not a standalone product. SKIP.

### F. Customer Feedback from Internal Channels
**Gap**: Sales/support teams share customer feedback in Slack channels (#product-feedback, #bugs) but there's no structured way to extract, tag, deduplicate, and route this to product teams.
**Existing**: Productboard ($20/maker/mo, has Slack integration), Canny (has Slack integration), Zonka Feedback. But these are feedback platforms with Slack as a side channel, not Slack-first tools.
**Buyer**: Product managers at B2B SaaS companies (50-500 employees).
**Pricing**: $49-99/mo flat or $5-10/user/mo for product team seats.
**Verdict**: INTERESTING. The "Slack-first feedback triage" angle is underserved. Productboard/Canny require context-switching. A bot that watches designated channels, uses AI to extract/tag/deduplicate feedback, and pushes structured entries to a simple dashboard could work. Risk: narrow buyer pool, Slack AI could absorb this.

### G. AI-Powered Channel Summaries
**Gap**: Slack bundled AI summaries/recaps into all paid plans in 2025. Daily digests, thread summaries, huddle transcriptions are now native.
**Verdict**: COMMODITIZED. Slack absorbed this entirely. Third-party summary tools are dead. SKIP.

---

## 4. Microsoft Teams: The Underserved Platform

Teams has 320M+ MAU but a weaker third-party ecosystem (1,400 apps vs Slack's 2,600+). Key observations:

- **Frontline/deskless workers** are the biggest underserved segment. Teams is pushing hard here with Frontline Hub but third-party tooling is thin.
- **Teams AI library** is now GA for JS/C# (Python preview), with MCP and A2A support -- the developer experience is catching up.
- **Classic app deprecation** (Sept 2025 - Nov 2026) means some established apps need migration, creating brief windows of disruption.
- **Dual-platform strategy** (Slack + Teams) is the smart play. Polly, Geekbot, and Standuply all serve both. Building for Teams alone is risky (Microsoft could absorb features), but Teams support doubles your TAM.

**Teams-specific gaps**: Approval workflows and async standups are more underserved on Teams than Slack. The Teams app store has fewer options in these categories.

---

## 5. Solo-Founder Feasibility

Proven patterns from profitable solo/small-team Slack apps:

| Factor | Evidence |
|--------|----------|
| **Revenue ceiling** | $1-5K MRR solo (Abot), $10-25K MRR small team (Standuply) |
| **Growth channel** | Slack App Directory listing + Product Hunt launches (Standuply launched on PH 8 times) |
| **Tech stack** | Rails, Node.js, or Python. Slack's Bolt SDK simplifies development. |
| **Time to MVP** | 2-4 weeks for a focused bot |
| **Maintenance** | Can run on autopilot once stable (Abot example) |
| **Platform risk** | HIGH. Slack controls distribution, review, API access. One policy change can kill you. |
| **Paid marketing** | Does NOT work (Abot founder paid agency, got nothing). Organic/directory/PH is the path. |

---

## 6. Two Gaps Worth Further Investigation

### Gap 1: Slack-First Feedback Triage Bot
**Workflow**: Bot watches #feedback/#bugs channels, AI extracts structured feedback items (feature request vs bug vs complaint), deduplicates, tags by product area, pushes to a lightweight dashboard with voting/prioritization.
**Buyer**: Product managers at B2B SaaS (50-500 employees) who already use Slack as their feedback dumping ground.
**Existing**: Productboard/Canny are feedback platforms that happen to have Slack integrations. No one is Slack-first.
**Pricing**: $49/mo (up to 3 watchers) / $99/mo (unlimited channels) -- workspace-based, not per-user.
**Risks**: Narrow buyer pool. Slack AI could add "extract action items from channel" natively. Productboard could deepen their Slack integration.

### Gap 2: Lightweight Approval Workflows (Slack + Teams)
**Workflow**: Bot enables multi-step approval chains (PTO, expense, access, discount) with escalation, SLA reminders, and audit log. No code needed -- configure via slash commands or simple web UI.
**Buyer**: Ops/office managers at 20-200 person companies without HRIS/ERP.
**Existing**: Approveit, Wrangle exist but are small with mediocre reviews. Slack Workflow Builder is too primitive for real chains.
**Pricing**: $3/user/mo or $49-149/workspace/mo flat.
**Risks**: Slack improving Workflow Builder could absorb this. Market size unclear -- companies needing approvals but not big enough for ServiceNow may be a thin slice.

---

## 7. Overall Assessment

The Slack/Teams marketplace is a **distribution channel**, not a market. The channel is powerful (750K+ orgs see your listing) but platform risk is extreme. The best micro-SaaS Slack apps share these traits:

1. **Solve a workflow Slack can't absorb** (not AI summaries, not basic polls)
2. **Cross-platform** (Slack + Teams doubles TAM, reduces single-platform risk)
3. **Workspace-based pricing** over per-user (simpler sale, less friction)
4. **Can run on autopilot** after initial development (Abot model)
5. **Niche enough** that Slack/Microsoft won't build it natively

Neither gap above is a strong enough signal for immediate build. The feedback triage bot is the more defensible of the two but needs validation that product managers would pay $49-99/mo for it vs. just using a shared spreadsheet or existing Productboard integration.

**Recommendation**: Park these as Tier 3 ideas. The Slack/Teams ecosystem is better as a distribution channel for a product that has standalone value, not as the entire product thesis.

---

## Sources

- [Business of Apps - Slack Statistics 2026](https://www.businessofapps.com/data/slack-statistics/)
- [Abot: $50K Profit from Solo Slack Bot](https://www.indiehackers.com/post/how-ive-made-50-000-profit-from-a-side-project-anonymous-slack-bot-4918f94294)
- [Standuply: Zero to $25K/mo](https://medium.com/slack-developer-blog/from-zero-to-25-000-mo-bf7caddea44d)
- [Geekbot Pricing & Reviews - Capterra](https://www.capterra.com/p/148076/geekbot/)
- [Slack AI Enterprise Search](https://slack.com/blog/productivity/ai-enterprise-search-top-features-and-tools-in-2025)
- [Slack Hidden Knowledge Crisis](https://slack.com/blog/productivity/the-hidden-knowledge-crisis)
- [PagerDuty Alternatives 2026 - Better Stack](https://betterstack.com/community/comparisons/pagerduty-alternatives/)
- [OpsGenie Shutdown Notice](https://www.xurrent.com/blog/pagerduty-alternatives)
- [Slack Approval Workflows - ClearFeed](https://clearfeed.ai/blogs/slack-approval-workflow-guide)
- [Teams Statistics 2026 - DemandSage](https://www.demandsage.com/microsoft-teams-statistics/)
- [Teams Third-Party Agent Support - Petri](https://petri.com/microsoft-teams-agents-third-party-apps/)
- [Micro SaaS Slack Plugin Ideas](https://microsaasbytes.com/slack-plugin-ideas)
- [Slack AI Daily Recaps - eesel AI](https://www.eesel.ai/blog/slack-ai-daily-recaps)
- [SQ Magazine - Slack Statistics 2026](https://sqmagazine.co.uk/slack-statistics/)
