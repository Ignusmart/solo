You are helping Jobelo (Principal Engineer: Solidity/Web3 security, AI/agentic systems, full-stack TS/Python) find his next micro-SaaS product idea. He can build almost anything — the bottleneck is finding the RIGHT idea based on CURRENT market gaps.

## IMPORTANT CONTEXT: 16 iterations completed, 190+ ideas killed
This command has run 16 times. Every B2B problem domain, emerging AI category, and distribution channel (Chrome Web Store, VS Code, Slack/Teams) has been scanned. APIDelta at 22/30 (new scoring) is the only survivor above bar. Research exhausted — recommend focusing on tool ideas or building. Read the killed ideas file THOROUGHLY — do not revisit anything there.

## CONSTRAINTS (hard rules)
- NO Web3 **security** products (day job conflict at Webacy) — but Web3 broadly (trading, DeFi, infra, NFTs, on-chain analytics non-security) IS allowed
- NO LATAM-specific niches (global market, English-first)
- NO biotech/regulated industries
- NO consulting/freelancing/calls (async-only)
- **NO high-touch sales verticals** — the buyer must be reachable via automated channels (SEO, paid ads, content marketing, Product Hunt, dev communities, marketplaces). If the buyer is offline-first, requires demos, cold calls, or relationship selling → KILL.
- Must be buildable solo in 1-4 weeks for MVP
- Must have clear monetization ($19-99/mo SaaS)
- Must target a gap where incumbents are weak, overpriced, or missing
- **Distribution must be automatable** — Jobelo is a software engineer, not a biz dev person. Customer acquisition should work through: paid ads (Google/Facebook), SEO/content, Product Hunt/HN launches, dev tool marketplaces, Chrome Web Store, or viral/PLG loops. NOT through: sales calls, conferences, cold outreach, partnerships, or enterprise procurement.
- PRIMARY FOCUS: micro-SaaS opportunities (but flag non-SaaS gems if found)

## KILL FILTERS (learned from 13 iterations + deep reviews)
Before analyzing ANY idea, check it against ALL of these. If it matches, skip immediately:

1. **AI wrapper = dead.** If core value is "GPT + nice UI for [task]," ChatGPT ($20/mo) kills it. Must involve workflow, data, or process lock-in — not just text generation.
2. **Freelancer/creator tools churn catastrophically.** Budget AI tools see 77% annual churn. Don't build for buyers who resist paying unless the lock-in is extreme.
3. **Platform absorption is faster than you think.** If your value prop can be a checkbox feature on Teachable/Thinkific/Cursor/GitHub Copilot/Shopify, it will be within 12 months.
4. **"No competitors" often means no market.** Empty niches stay empty because the market rejected the category.
5. **Check the name before scoring.** If the name/domain is taken, note it.
6. **Free tools set the floor.** If Zoho/Google/Freshdesk/etc offer a free tier, your $19/mo needs 10x more value.
7. **Intermittent pain = high churn.** If the problem is episodic, users subscribe when hurting and cancel when resolved.
8. **B2B with budget > solopreneurs.** Target buyers with company credit cards, not individuals counting every $19.
9. **Every category-level gap is filled.** After 13 iterations and 170+ ideas, every B2B software category has 5-30+ tools.
10. **Hyper-vertical > horizontal.** Solo founders reaching $5K+ MRR solve one specific workflow pain for one specific buyer in one specific industry.
11. **"Pricing gap" is a trap.** When expensive tools ($300+/mo) serve mid-market, the $15-49/mo tier below already has dozens of micro-SaaS competitors.
12. **"Orphaned customer" windows close instantly.** When a product shuts down, it funnels users to a successor. By the time you build, the window is closed.
13. **Monopoly anger ≠ solo founder opportunity.** Angry customer bases attract funded competitors, not micro-SaaS.
14. **New categories fill in 6-12 months.** AI-enabled dev compresses competition cycles. By the time you identify an emerging category, it's already crowded.
15. **Distribution > problem novelty.** 70% of micro-SaaS never breaks $500/mo. Winners win on distribution channels, not finding unserved problems.
16. **Platform-dependent distribution = borrowed audience.** If the platform controls your distribution AND your feature set AND your API access, you're building a feature they'll absorb or block.
17. **Offline-first buyers = distribution death.** If the target buyer doesn't Google for solutions, read Product Hunt, or click Facebook/Google ads — you can't reach them without sales calls, conferences, or door-to-door. Examples: freight brokers, dentists, restaurants, construction, trades. These markets require BD, not engineering.
18. **High-touch sales = solo founder trap.** If converting a lead requires a demo call, custom onboarding, or multi-stakeholder approval → the CAC will eat you alive as a solo builder. The product must sell itself: landing page → signup → value in <5 minutes.

## CONTEXT BUDGET — CRITICAL FOR /loop RELIABILITY

This command runs inside `/loop`. Each iteration shares a single context window with the command prompt, file reads, web searches, and written output. **If you read too much, the iteration will fail or produce garbage.**

**Rules:**
- **DO NOT read full files when grep/glob suffices.** Use Grep to check if a vertical or idea name is already killed instead of reading the entire killed-ideas file.
- **Budget: ~60K tokens max for file reads per iteration.** The leaderboard + 1 iteration report + targeted greps should stay well under this.
- **Never read deep-review reports or strategy docs (00-05) unless you have a specific reason.** They are reference material, not per-iteration reads.

## KILLED IDEAS — CHECK BY GREP, NOT FULL READ

170+ killed ideas live in `research/strategy/06-KILLED-IDEAS.md`. **Do NOT read this file in full.**

Instead, before deep-diving any idea:
1. **Grep** the killed file for the idea name, vertical, and key terms (e.g., `grep -i "freight\|logistics\|shipping"`)
2. **Read only the "Patterns That Kill Ideas" section** at the bottom of the file (last ~30 lines) — this tells you what angles are exhausted
3. If grep finds a match → the idea is killed, skip it

## EXISTING RESEARCH (reference — read selectively, not exhaustively)

### Strategy docs (DO NOT read every iteration — reference only when needed):
- research/strategy/00-SKILLS-PROFILE.md — Jobelo's skill stack
- research/strategy/01-IDEAS-RANKED.md — master ranked list of all ideas
- research/strategy/04-PRODUCT-IDEAS-DEEP-DIVE.md — deep dives on product ideas
- research/strategy/05-NO-CALLS-PLAYBOOK.md — async-only constraints
- research/strategy/06-KILLED-IDEAS.md — KILLED IDEAS REGISTRY (grep, don't full-read)

### Iteration reports (read ONLY the latest 1 + leaderboard):
- research/reports/*-market-gap-iteration-*.md — previous iteration findings
- research/reports/2026-04-04-idea-leaderboard.md — running leaderboard (READ THIS — it's the summary)

### Deep review reports (DO NOT read unless specifically relevant):
- research/reports/2026-04-05-scopeshield-deep-review.md
- research/reports/2026-04-05-postpilot-deep-review.md
- research/reports/2026-04-05-coursebot-deep-review.md
- research/reports/2026-04-05-ideas-4-6-deep-review.md

## LOOP EXECUTION MODEL

This command works with `/loop`. Each invocation is ONE iteration. **You have NO memory of previous runs** — the research files ARE your memory.

### Iteration lifecycle:
```
GREP KILLED IDEAS (targeted) → READ LEADERBOARD → READ LAST 1 REPORT → HUNT NEW SIGNALS → DEEP DIVE 2-3 IDEAS → ADVERSARIAL REVIEW → SCORE → UPDATE ALL FILES
```

### How to determine iteration number:
- Count existing `research/reports/*-market-gap-iteration-*.md` files
- Next iteration = max(existing) + 1

---

## EACH ITERATION

### Step 1: Read existing state (KEEP IT LIGHT — context budget matters)
1. **Read the leaderboard** — `research/reports/2026-04-04-idea-leaderboard.md` — current rankings and what's been explored
2. **Read ONLY the latest 1 iteration report** — the most recent `research/reports/*-market-gap-iteration-*.md` file. Do NOT read older reports.
3. **Grep the killed ideas file** — do NOT read `research/strategy/06-KILLED-IDEAS.md` in full. Instead:
   - Use Grep to search for the "Patterns That Kill Ideas" section (last ~30 lines of the file) and read only that
   - Before deep-diving any idea later in Step 3, grep the killed file for that idea's vertical/name
4. **Determine what angles have NOT been tried yet** based on the leaderboard + latest report + kill patterns.

### Step 2: Market gap discovery — multi-source signal hunting
Use ALL of these sources. Do not rely on web search alone. The goal is to find REAL unmet demand, not hypothetical gaps.

#### A) Product Hunt mining
- Search for recently launched products (last 3-6 months) with HIGH upvotes but NEGATIVE comments
- Products that launched and FAILED (few upvotes, dead websites) — problem might be real but execution wrong
- Search: site:producthunt.com "[vertical] tool" OR "[vertical] software"

#### B) Reddit / HN / Twitter signal hunting
- site:reddit.com "I'd pay for" OR "I wish there was" OR "why doesn't X exist" [vertical]
- site:reddit.com "switched from" AND "nothing good" OR "all suck" [vertical]
- site:news.ycombinator.com "ask hn" tool OR software [vertical]
- Look for threads with 50+ upvotes — that's real demand signal

#### C) Market research and trend analysis
- "micro SaaS low competition 2026", "underserved B2B SaaS niches 2026"
- "boring SaaS that prints money", "unsexy SaaS profitable solo founder"
- "[vertical] software pain points 2026", "overpriced [vertical] tools"
- Search Indie Hackers for profitable products — study adjacent gaps they DON'T cover

#### D) Competitor gap analysis
- Search G2, Capterra, TrustRadius for existing tools in any promising space
- **Phrase-mine 1-2 star reviews** for: `"doesn't have"`, `"wish it could"`, `"missing"`, `"switched away from"`, `"had to use a workaround"`. These tell you exactly what the next product should ship — not generic complaints, but the precise feature gap.
- Check for "alternatives to [expensive tool]" — high search volume = market pain

#### E) Upwork / Fiverr task mining (paying humans to do this manually)
- Search Upwork for active jobs in the vertical — filter by hourly + repeat clients
- Tasks posted weekly with $30-100/hr budgets are SaaS-replaceable
- "People pay humans every week to do this" is a stronger demand signal than "people complain about this on Reddit." Look for repeated, predictable tasks — those are workflow gaps.

#### F) Explore a DIFFERENT vertical or angle each iteration
- **DO NOT repeat verticals from previous iterations** — check the killed file
- Prioritize B2B with real budgets over solopreneur/creator tools
- Consider non-obvious angles: developer workflows, back-office operations, compliance timing windows, marketplace gaps

### Step 3: Deep market gap analysis (2-3 ideas)
For each idea, go DEEP — don't just describe it, PROVE the gap exists:

#### Problem validation
- Problem + who has it (specific buyer persona with job title, company size, budget authority)
- **Evidence the problem exists**: specific Reddit threads, HN posts, G2 reviews, tweets, Product Hunt comments
- **Evidence people are paying for workarounds**: spreadsheets, VAs, Zapier duct-tape, overpaying for enterprise tools
- Frequency: Daily = sticky. Monthly = churn risk. Yearly = dead.

#### Solution gap analysis
- List ALL existing solutions (G2, Capterra, Product Hunt, GitHub). Be exhaustive.
- For each: pricing, bad reviews, shortcomings
- **VISIT the top 2 competitors' websites** (use WebFetch) — see their full feature set, pricing pages, support options, and content. Do NOT guess what they offer from a G2 listing. Competitors are almost always more capable than they look from the outside.
- What specifically is MISSING that no current tool does well?
- Why hasn't anyone built this yet? (If the answer isn't clear, the gap might not be real)
- **Scope honesty**: If the top competitor offers 10+ features/products and you're planning to build 1, acknowledge that you're entering at a massive feature disadvantage. Is the one thing you do really enough to win users away?

#### MVP and business model
- MVP scope (what ships in 1-2 weeks — specific features, not vague)
- Revenue model + realistic MRR ceiling (show the math: TAM x conversion x price)
- Why Jobelo's skills give a specific edge here
- Distribution plan: Pick **ONE primary channel** and write a 90-day execution plan. Specific weekly actions (e.g., "Reddit: 3 posts/week in r/X + r/Y, comment on 5 threads/day"), not "SEO + ads + Product Hunt." Multi-channel launches fail — channel-hopping founders learn nothing from any of them. If you can't commit to one channel for 90 days, the idea isn't ready.
- Kill criteria: specific, measurable conditions to abandon this

### Step 4: ADVERSARIAL REVIEW (mandatory for every idea scoring 16+)

#### Competitor reality check (MANDATORY — do not skip)
- Search for the exact product name + domain. Is it taken?
- Search Product Hunt for "[problem] tool" — launched in last 12 months?
- Search G2/Capterra — how many tools? What ratings?
- Search GitHub for open-source alternatives
- **VISIT the top 2 competitors' actual websites** (use WebFetch). Document:
  - Full product scope: every product/feature they list (not just the one you're targeting)
  - Pricing: all tiers, what's included, upsells
  - Content/SEO: blog, guides, templates, landing pages — this is their real moat
  - Support: live chat, email, phone, knowledge base, community
  - Trust signals: reviews, testimonials, case studies, certifications, payment methods
  - Integrations and ecosystem: what else do they connect to?
- **Assess honestly**: Is the competitor a simple tool you can out-execute, or a full platform with years of content, features, and trust? If the latter, your "better UX" angle is naive — you're competing with a product ecosystem, not just a UI.
- **Scope reality check**: Based on what the competitor actually offers, what is the REAL MVP scope to be competitive? If the competitor has 30+ features and yours has 1, you're not "differentiated" — you're incomplete.

#### The 7 kill tests
1. **ChatGPT test**: Can someone do this with ChatGPT/Claude for free? What's the workflow lock-in?
2. **Platform absorption test**: Will adjacent platforms add this as a feature? Check recent changelogs.
3. **Willingness to pay test**: Evidence of people ACTUALLY paying (not just complaining)?
4. **Churn test**: Daily-use (sticky) or fix-and-forget (churn)?
5. **Solo founder test**: Can one person build + maintain + support + market this?
6. **Automated distribution test**: Can customers be acquired via SEO, Google/Facebook ads, Product Hunt, dev communities, or PLG without sales calls? If the buyer doesn't Google their problem or hang out in online communities → KILL.
7. **Self-serve conversion test**: Can a stranger land on the page, understand the value, sign up, and get value in <5 minutes without talking to anyone? If a demo call or custom onboarding is needed → KILL.
8. **Free-tier mask test**: If you launched with a free tier, would the likely outcome be 100+ signups but <10% paid conversion? If yes, the free tier is masking the fact that nobody would actually pay. Either go paid-only (or paid-trial) or no launch. Reference failure mode: 7 months of building, 100+ signups, 8-9 paid, killed.

If 2+ kill tests fail hard → KILL the idea. **Tests 6, 7, and 8 are mandatory passes** — any idea that fails any of them is auto-killed regardless of other scores.

#### Pre-Build Validation Gate (mandatory for any idea scoring 22+)

Before an idea graduates from research → /implement, the iteration report MUST answer all three:

1. **Who are the 10 DM targets?** Specific named accounts, not personas. "DevOps engineers" fails. "10 named companies actively hiring [job title] on LinkedIn this month" passes. Provide the list (or a concrete way to generate it).
2. **Where do they hang out?** A specific subreddit, Discord/Slack, LinkedIn group, GitHub org, newsletter, or community list — not "developer communities." If you can't name the place, you can't reach the buyer.
3. **What does the cold-DM script ask?** A 3-line message ending with: "Would you pay $X/month for [specific outcome]?" The 3-of-10 yes bar applies *before any code is written*.

If any of the three is missing or vague, the idea is **RETURNED** (not killed, not promoted) — back to research with a note about what's unanswered. Validation precedes building. T3's failure was 7 months of code with no DM evidence; don't repeat it.

### Step 5: Score each idea (1-5 scale, 6 dimensions now — max 30)

| Dimension | 1 (worst) | 5 (best) |
|-----------|-----------|----------|
| Market gap size | No evidence of pain | Paying for workarounds |
| Build feasibility | Needs team, 6+ months | Solo, 1-2 weeks |
| Monetization clarity | Vague, freemium trap | Clear tiers, proven WTP |
| Competition | 30+ tools, funded players | 0-2 weak incumbents |
| Distribution ease | Requires sales team, cold calls | SEO/ads/PH/PLG, self-serve signup |
| Automated marketing fit | Offline buyers, conferences | Google-able problem, dev communities, paid ads work |

**Distribution ease + Automated marketing fit are weighted 2x** — a great product with no automated path to customers is worthless for a solo engineer.

**Minimum viable score: 22/30** AFTER adversarial review. Any idea scoring <3 on either distribution dimension → auto-KILL regardless of total score.

### Step 6: Write findings (non-negotiable — update ALL files)

#### A) Create iteration report (KEEP CONCISE — max ~8K characters):
- Write to `research/reports/YYYY-MM-DD-market-gap-iteration-N.md`
- Include search queries and key links — but summarize findings, don't paste raw results
- Include adversarial review for any idea scoring 16+ — but keep it to bullet points, not essays
- **Why the size limit matters:** future iterations read this file. Bloated reports eat context in future loops.

#### B) Update leaderboard:
- Append new ideas with scores to `research/reports/2026-04-04-idea-leaderboard.md`
- Re-rank if any new idea scores higher than existing entries
- Never remove previous entries
- **Keep entries to 2-3 lines each** — name, score, one-line summary. Full analysis lives in the iteration report.

#### C) Update killed ideas registry:
- Add any killed idea to `research/strategy/06-KILLED-IDEAS.md` — **one line per idea**: `- [Idea Name] — [kill reason]`
- Update the stats section (total ideas, iterations, etc.)
- Do NOT write multi-paragraph explanations in the killed file — the iteration report has the details

---

## BAR FOR IDEAS
Be ruthlessly critical. 170+ ideas killed across 13 iterations; top 6 scoring ideas ALL died under adversarial review. An idea graduates only if:

1. EVIDENCE of real people paying for workarounds (Reddit / G2 / Upwork — not just "people complain")
2. Survives all 8 kill tests (with tests 6, 7, 8 as mandatory passes)
3. Clears the Pre-Build Validation Gate (10 named DM targets + community + script)
4. Score ≥22/30 AFTER adversarial review

Anything below is noise.
