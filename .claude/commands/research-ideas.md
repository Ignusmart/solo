You are helping Jobelo (Principal Engineer: Solidity/Web3 security, AI/agentic systems, full-stack TS/Python) find his next micro-SaaS product idea. He can build almost anything — the bottleneck is finding the RIGHT idea based on CURRENT market gaps.

## IMPORTANT CONTEXT: 13 iterations completed, 170+ ideas killed
This command has run 13 times. Every B2B problem domain, emerging AI category, and distribution channel (Chrome Web Store, VS Code, Slack/Teams) has been scanned. Zero ideas have scored 18/25 after adversarial review. Best surviving: DriftWatch at 17/25. Read the killed ideas file THOROUGHLY — do not revisit anything there.

## CONSTRAINTS (hard rules)
- NO Web3 security products (day job conflict at Webacy)
- NO LATAM-specific niches (global market, English-first)
- NO biotech/regulated industries
- NO consulting/freelancing/calls (async-only)
- Must be buildable solo in 1-4 weeks for MVP
- Must have clear monetization ($19-99/mo SaaS)
- Must target a gap where incumbents are weak, overpriced, or missing
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

## MANDATORY: READ KILLED IDEAS FIRST
Before doing ANY research, read this file completely:
- **research/strategy/06-KILLED-IDEAS.md** — 170+ killed ideas with reasons. Do NOT re-explore anything listed here.

## EXISTING RESEARCH (read before each iteration)

### Strategy docs (read once for context):
- research/strategy/00-SKILLS-PROFILE.md — Jobelo's skill stack
- research/strategy/01-IDEAS-RANKED.md — master ranked list of all ideas
- research/strategy/04-PRODUCT-IDEAS-DEEP-DIVE.md — deep dives on product ideas
- research/strategy/05-NO-CALLS-PLAYBOOK.md — async-only constraints
- research/strategy/06-KILLED-IDEAS.md — KILLED IDEAS REGISTRY (mandatory read)

### Iteration reports (read the LATEST 3 at minimum, then create the next one):
- research/reports/*-market-gap-iteration-*.md — all previous iteration findings (13 exist)
- research/reports/2026-04-04-idea-leaderboard.md — running leaderboard

### Deep review reports:
- research/reports/2026-04-05-scopeshield-deep-review.md
- research/reports/2026-04-05-postpilot-deep-review.md
- research/reports/2026-04-05-coursebot-deep-review.md
- research/reports/2026-04-05-ideas-4-6-deep-review.md

## LOOP EXECUTION MODEL

This command works with `/loop`. Each invocation is ONE iteration. **You have NO memory of previous runs** — the research files ARE your memory.

### Iteration lifecycle:
```
READ KILLED IDEAS → READ LAST 3 ITERATION REPORTS → READ LEADERBOARD → HUNT NEW SIGNALS → DEEP DIVE 2-3 IDEAS → ADVERSARIAL REVIEW → SCORE → UPDATE ALL FILES
```

### How to determine iteration number:
- Count existing `research/reports/*-market-gap-iteration-*.md` files
- Next iteration = max(existing) + 1

---

## EACH ITERATION

### Step 1: Read existing state
1. Read `research/strategy/06-KILLED-IDEAS.md` — the full kill list (MANDATORY, do not skip)
2. Read the LATEST 3 iteration reports — know what was recently covered
3. Read `research/reports/2026-04-04-idea-leaderboard.md` — current rankings
4. **Determine what angles have NOT been tried yet.** The killed file has a "Patterns That Kill Ideas" section — read it to avoid repeating failed strategies.

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
- Read 1-star and 2-star reviews — anger = opportunity
- Check for "alternatives to [expensive tool]" — high search volume = market pain

#### E) Explore a DIFFERENT vertical or angle each iteration
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
- What specifically is MISSING that no current tool does well?
- Why hasn't anyone built this yet? (If the answer isn't clear, the gap might not be real)

#### MVP and business model
- MVP scope (what ships in 1-2 weeks — specific features, not vague)
- Revenue model + realistic MRR ceiling (show the math: TAM x conversion x price)
- Why Jobelo's skills give a specific edge here
- Distribution plan: How do first 10 customers find this? First 100?
- Kill criteria: specific, measurable conditions to abandon this

### Step 4: ADVERSARIAL REVIEW (mandatory for every idea scoring 16+)

#### Competitor reality check
- Search for the exact product name + domain. Is it taken?
- Search Product Hunt for "[problem] tool" — launched in last 12 months?
- Search G2/Capterra — how many tools? What ratings?
- Search GitHub for open-source alternatives

#### The 5 kill tests
1. **ChatGPT test**: Can someone do this with ChatGPT/Claude for free? What's the workflow lock-in?
2. **Platform absorption test**: Will adjacent platforms add this as a feature? Check recent changelogs.
3. **Willingness to pay test**: Evidence of people ACTUALLY paying (not just complaining)?
4. **Churn test**: Daily-use (sticky) or fix-and-forget (churn)?
5. **Solo founder test**: Can one person build + maintain + support + market this?

If 2+ kill tests fail hard → KILL the idea.

### Step 5: Score each idea (1-5 scale)
- Market gap size | Build feasibility | Monetization clarity | Competition (5=empty) | Distribution ease
- Must score 18+ AFTER adversarial review to be considered viable

### Step 6: Write findings (non-negotiable — update ALL files)

#### A) Create iteration report:
- Write to `research/reports/YYYY-MM-DD-market-gap-iteration-N.md`
- Include ALL search queries, sources, links to evidence
- Include full adversarial review for any idea scoring 16+

#### B) Update leaderboard:
- Append new ideas with scores to `research/reports/2026-04-04-idea-leaderboard.md`
- Re-rank if any new idea scores higher than existing entries
- Never remove previous entries

#### C) Update killed ideas registry:
- Add any killed idea to `research/strategy/06-KILLED-IDEAS.md` with kill reason
- Update the stats section (total ideas, iterations, etc.)

---

## BAR FOR IDEAS
Be ruthlessly critical. 170+ ideas killed across 13 iterations. Top 6 scoring ideas ALL died under adversarial review. The question is NOT "does this sound like a good idea?" but:

1. "Can I find EVIDENCE of real people paying for workarounds to this problem?"
2. "Does this survive ALL 5 kill tests?"
3. "Does this have a clear path to $2K+ MRR within 6 months?"

An idea scoring 18+ AFTER adversarial review is worth building. Anything below is noise.
