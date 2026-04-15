You are helping Jobelo (Principal Engineer: Solidity/Web3 security, AI/agentic systems, full-stack TS/Python) find small, transactional utility tools that generate revenue through volume — NOT monthly subscriptions. Think Pieter Levels (PhotoAI, $100K+/mo), visa photo generators, background removers, PDF converters, AI headshot tools. He can build almost anything — the bottleneck is finding the RIGHT tool with proven demand and a clear monetization path.

## HOW THIS DIFFERS FROM /research-ideas

`/research-ideas` hunts for MRR subscription SaaS ($19-99/mo). This command hunts for **transactional utility tools** — small, focused tools where users pay per use, buy credits, or pay once. Different economics:

| Dimension | MRR SaaS | Utility Tool (this command) |
|-----------|----------|----------------------------|
| Revenue | $19-99/mo subscription | $1-15 per use, credit packs, one-time, or ads |
| Churn | The #1 killer | Irrelevant — no subscription to cancel |
| Stickiness | Must be daily-use | Doesn't need to be — solve once, get paid |
| Users | B2B buyers with budgets | Anyone with a credit card and a problem right now |
| Moat | Workflow lock-in, data | SEO, speed, UX, brand, volume |
| Build time | 1-4 weeks | 1-2 weeks (simpler scope) |
| Risk | Slow growth, churn death | Can die fast, but cheap to validate |
| Win condition | $2K+ MRR in 6 months | $1K+/mo revenue in 3 months |

## CONSTRAINTS (hard rules)
- NO Web3 **security** products (day job conflict at Webacy) — but Web3 broadly (trading, DeFi, infra, NFTs, on-chain analytics non-security) IS allowed
- NO LATAM-specific niches (global market, English-first)
- NO biotech/regulated industries
- NO consulting/freelancing/calls (async-only)
- Must be buildable solo in 1-2 weeks for MVP
- Must have clear monetization (pay-per-use, credits, one-time, or ad-supported with premium tier)
- Must target HIGH VOLUME use cases — the math only works at scale
- Can target consumers OR businesses — both are valid for utility tools

## KILL FILTERS (adapted for utility tools)

Before analyzing ANY idea, check against ALL of these. If it matches, skip immediately:

1. **Free and good enough = dead.** If a free tool does 90% of what yours would (e.g., free PDF merge, free image resize), there's no room. Your tool must do something the free version can't or won't.
2. **AI wrapper without unique output = dead.** "Upload X, get AI-generated Y" only works if the output quality is measurably better than ChatGPT/Claude doing it directly. The tool must add processing, formatting, compliance, or domain expertise that raw AI can't.
3. **Commoditized conversions = dead.** File format conversions (PDF→Word, PNG→SVG, etc.) are a race to zero. 50+ free tools exist. Only viable if you add domain-specific value ON TOP of the conversion.
4. **No search volume = no demand.** Utility tools live and die by SEO. If nobody is searching for the solution, you can't reach them. Check Google Trends and keyword volume BEFORE deep-diving.
5. **Platform gives it away free = dead.** If Apple/Google/Adobe/Canva include this as a built-in feature, don't compete.
6. **Regulatory/compliance tools need trust.** Visa photos, tax docs, legal forms — users will pay, but they need to trust accuracy. If getting it wrong has consequences, factor in the liability and support burden.
7. **One-and-done with zero virality = slow death.** If each user uses it once and never comes back AND never tells anyone, you need infinite ad spend. Best tools have natural word-of-mouth or repeat use cases.
8. **API costs eat margins.** If each use costs $0.05-0.50 in API calls (AI, cloud processing), your $3 price point might not survive. Calculate unit economics BEFORE building.

## CONTEXT BUDGET — CRITICAL FOR /loop RELIABILITY

This command runs inside `/loop`. Each iteration shares a single context window with the command prompt, file reads, web searches, and written output. **If you read too much, the iteration will fail or produce garbage.**

**Rules:**
- **DO NOT read full files when grep/glob suffices.** Use Grep to check if a tool idea is already killed instead of reading entire files.
- **Budget: ~60K tokens max for file reads per iteration.** The leaderboard + 1 iteration report + targeted greps should stay well under this.
- **Never read strategy docs or SaaS research reports unless specifically relevant.** This is a separate research track.

## KILLED IDEAS — CHECK BY GREP, NOT FULL READ

Killed tool ideas live in `research/strategy/07-KILLED-TOOL-IDEAS.md`. **Do NOT read this file in full** (it will grow over time).

Instead, before deep-diving any idea:
1. **Grep** the killed file for the tool name, category, and key terms
2. **Read only the "Patterns That Kill Tool Ideas" section** at the bottom of the file (last ~30 lines)
3. If grep finds a match, the idea is killed — skip it
4. Also grep `research/strategy/06-KILLED-IDEAS.md` — some SaaS-killed ideas might overlap

## EXISTING RESEARCH (reference — read selectively)

### Tool-specific files:
- `research/reports/tool-ideas-leaderboard.md` — running leaderboard for tool ideas (READ THIS every iteration)
- `research/reports/*-tool-ideas-iteration-*.md` — previous tool research iterations (read ONLY the latest 1)
- `research/strategy/07-KILLED-TOOL-IDEAS.md` — killed tool ideas registry (grep, don't full-read)

### Cross-reference (grep only, don't full-read):
- `research/strategy/06-KILLED-IDEAS.md` — SaaS killed ideas (some may overlap)
- `research/reports/2026-04-04-idea-leaderboard.md` — SaaS leaderboard (avoid duplicating)

## LOOP EXECUTION MODEL

This command works with `/loop`. Each invocation is ONE iteration. **You have NO memory of previous runs** — the research files ARE your memory.

### Iteration lifecycle:
```
GREP KILLED TOOLS → READ TOOL LEADERBOARD → READ LAST 1 REPORT → HUNT SIGNALS → DEEP DIVE 2-3 TOOLS → ADVERSARIAL REVIEW → SCORE → UPDATE ALL FILES
```

### How to determine iteration number:
- Count existing `research/reports/*-tool-ideas-iteration-*.md` files
- Next iteration = max(existing) + 1
- If none exist, this is iteration 1

### First iteration bootstrap:
If the leaderboard (`research/reports/tool-ideas-leaderboard.md`) doesn't exist, create it. If the killed file (`research/strategy/07-KILLED-TOOL-IDEAS.md`) doesn't exist, create it with an empty "Patterns That Kill Tool Ideas" section at the bottom.

---

## EACH ITERATION

### Step 1: Read existing state (KEEP IT LIGHT — context budget matters)
1. **Read the tool leaderboard** — `research/reports/tool-ideas-leaderboard.md` — current rankings
2. **Read ONLY the latest 1 tool iteration report** — the most recent `research/reports/*-tool-ideas-iteration-*.md` file. Do NOT read older reports.
3. **Grep the killed tool ideas file** — do NOT read `research/strategy/07-KILLED-TOOL-IDEAS.md` in full. Instead:
   - Use Grep to search for the "Patterns That Kill Tool Ideas" section and read only that
   - Before deep-diving any idea later in Step 3, grep the killed file for that tool's category/name
4. **Determine what tool categories have NOT been tried yet** based on the leaderboard + latest report.

### Step 2: Signal hunting — find tools people are ALREADY paying for

The strategy for utility tools is different from SaaS. You're looking for HIGH VOLUME, TRANSACTIONAL demand. Use these sources:

#### A) Revenue-proven tool hunting
- Search for solo founders making money from simple tools: "indie hacker revenue" + tool, "solo founder $X/mo"
- Study Pieter Levels' portfolio (PhotoAI, InteriorAI, AVA headshots) — what patterns make these work?
- Search for tools on platforms that show revenue: Gumroad top sellers, Lemon Squeezy trending, Paddle success stories
- Look at "micro tool" directories and aggregators

#### B) SEO demand validation (CRITICAL for utility tools)
- Use Google Trends to check search volume for "[thing] generator", "[thing] maker", "[thing] converter", "[thing] tool"
- Look for high-volume, low-competition keywords — these ARE the business opportunity
- Check "People also ask" and "Related searches" for tool-shaped queries
- Search: "[task] online free" — high volume here means people want it done, and "free" means current free tools might be inadequate

#### C) Social signal hunting
- site:reddit.com "is there a tool" OR "any tool that" OR "I need a tool" [task]
- site:reddit.com "I paid for" OR "worth paying for" [tool type]
- Twitter/X: "just used [tool type]" OR "this tool saved me" — real usage signals
- TikTok/YouTube: search for "[task] tutorial" — if people are watching tutorials, a tool could replace the manual process
- Product Hunt: recently launched SIMPLE tools (not complex SaaS) with high engagement

#### D) Existing tool gap analysis
- Find popular utility tools and check their reviews — what's missing?
- Look for tools with bad UX, slow processing, predatory pricing, or missing features
- Check App Store / Play Store for utility apps with high downloads but bad ratings
- Search "alternatives to [popular tool]" — what do people want that the incumbent doesn't do?

#### E) Category exploration (rotate each iteration)
Explore a DIFFERENT tool category each iteration. Examples:
- **Document tools**: resume builders, invoice generators, contract generators, receipt makers
- **Image tools**: headshot generators, background removers, passport photos, mockup generators, watermark removers
- **Video tools**: subtitle generators, thumbnail makers, clip extractors, video compressors
- **Data tools**: CSV cleaners, JSON formatters, data anonymizers, spreadsheet converters
- **Developer tools**: regex testers, API mock generators, SVG optimizers, favicon generators
- **Business tools**: email signature generators, business card makers, QR code generators, barcode creators
- **Personal tools**: AI avatar makers, baby name generators, meal planners, moving cost calculators
- **Compliance tools**: visa photo formatters, accessibility checkers, GDPR cookie generators, privacy policy generators
- **Content tools**: blog post formatters, social image resizers, Open Graph image generators, podcast transcribers
- **AI-powered tools**: AI headshots, AI interior design, AI logo makers, AI product photos

### Step 3: Deep analysis (2-3 tool ideas)
For each tool idea, validate with HARD DATA:

#### Demand validation
- **Search volume**: What are people searching for? Use Google Trends comparative data.
- **Who needs it**: Specific persona — "job applicant needs a passport photo", "realtor needs virtual staging"
- **Frequency**: One-time (passport photo) vs recurring (social media thumbnails) vs seasonal (tax forms)
- **Price sensitivity**: What are people currently paying? What would they pay for a better/faster version?
- **Evidence of payment**: Existing tools with pricing pages, App Store purchases, Gumroad sales

#### Competition analysis (MUST visit actual competitor sites — no armchair analysis)
- List ALL existing tools — web apps, mobile apps, desktop apps, browser extensions
- For each: pricing model, review count, rating, traffic estimate (SimilarWeb/SEMrush if possible)
- **VISIT the top 2 competitors' actual websites** (use WebFetch). Document:
  - Full product scope: every product/service they offer — competitors often do MUCH more than the one thing you're targeting. A "paystub generator" might actually be a full tax document platform with 30+ form types.
  - Pricing: all tiers, bundles, volume discounts
  - Content moat: blog posts, SEO landing pages, guides, templates — this is years of accumulated organic traffic you can't replicate in a week
  - Support infrastructure: live chat, email, phone, FAQ, knowledge base
  - Trust signals: reviews, testimonials, years in business, payment methods, refund policy
  - Mobile experience: responsive? native app?
- **Honest assessment**: Are existing tools actually "bad" or are you projecting? A site can look "dated" and still have excellent functionality, trust, and SEO authority that took years to build. Ugly ≠ bad product.
- What specifically is bad about existing options? (slow, ugly, expensive, inaccurate, limited) — back this up with evidence, not assumptions
- Is there an open-source version? If yes, why would someone pay for yours? (UX, speed, hosted, no-code)
- **Scope reality check**: If the top competitor has N features/products and you're building 1, you're not "differentiated" — you're incomplete. Acknowledge the real scope gap and assess whether your MVP can survive with just the core feature.

#### Unit economics (CRITICAL — utility tools live or die here)
- **Cost per use**: API costs (AI inference, cloud processing, storage) per transaction
- **Price per use**: What can you charge? ($1-5 for simple, $5-15 for complex, $15-50 for high-value)
- **Margin per use**: Price minus cost. Must be >60% for viability.
- **Volume needed**: To hit $1K/mo, how many transactions per day? Is that realistic for the search volume?
- **Revenue model options**: Pay-per-use vs credit packs vs freemium (3 free, then pay) vs one-time purchase

#### MVP scope
- What ships in 1 week? (specific features, specific pages)
- Tech: Next.js frontend + serverless API (or NestJS if complex). No need for full monorepo if simple enough.
- What's the SMALLEST thing that delivers value? One input → one output.
- Distribution plan: SEO landing pages, Product Hunt launch, social media, where the users already are

#### Kill criteria
- Specific, measurable conditions to abandon (e.g., "<50 uses in first 2 weeks after launch", "cost per use >$0.30 making margin impossible")

### Step 4: ADVERSARIAL REVIEW (mandatory for every idea scoring 16+)

#### Competitor reality check (MANDATORY — do not skip)
- Search for the exact tool name + domain. Taken?
- Search Product Hunt for "[task] tool" — launched in last 12 months?
- Search App Store / Play Store for similar utility apps
- Search GitHub for open-source alternatives
- Check if Canva, Adobe Express, or ChatGPT already does this well enough
- **If not already done in Step 3, VISIT the top 2 competitors' actual websites** (use WebFetch). This is non-negotiable. You cannot assess competition without seeing what they actually offer.
- **Platform vs tool assessment**: Is the competitor a simple single-purpose tool (like yours would be), or a full platform with dozens of products, content marketing, support team, and years of SEO authority? If the latter, acknowledge that "better UX on one feature" is NOT a viable differentiation strategy — you'd be bringing a knife to a gunfight.

#### The 5 kill tests (adapted for utility tools)
1. **Free tool test**: Is there a free version that's good enough? Not "does a free version exist" but "would a normal person find and use the free one instead?"
2. **ChatGPT/Claude test**: Can someone do this by pasting into ChatGPT? If yes, what specific value does a dedicated tool add? (Speed, formatting, compliance, batch processing, no prompt needed)
3. **Volume test**: Is there enough search volume / demand to hit $1K/mo at your price point? Show the math.
4. **Margin test**: After API/hosting costs, is there >60% margin per transaction? If AI-heavy, this is the most common killer.
5. **Solo maintainability test**: Can one person build, host, support, and market this without it becoming a full-time job?

If 2+ kill tests fail hard, KILL the idea.

### Step 5: Score each idea (1-5 scale)

| Criterion | What it measures |
|-----------|-----------------|
| Search volume / demand | Is anyone actively looking for this? (Google Trends, keyword data) |
| Build speed | Can MVP ship in 1 week? 2 weeks max? |
| Unit economics | Margin per use after API/hosting costs |
| Competition gap | Is there a real opening? (bad UX, overpriced, missing features) |
| SEO/distribution potential | Can you rank for relevant keywords? Organic growth path? |

- Score 1-5 each. Total /25.
- Must score **16+ AFTER adversarial review** to be considered viable (lower bar than SaaS — utility tools are cheaper to test)

### Step 6: Write findings (non-negotiable — update ALL files)

#### A) Create iteration report (KEEP CONCISE — max ~8K characters):
- Write to `research/reports/YYYY-MM-DD-tool-ideas-iteration-N.md`
- Include search queries and key links — but summarize findings, don't paste raw results
- Include adversarial review for any idea scoring 14+ — but keep it to bullet points
- **Why the size limit matters:** future iterations read this file. Bloated reports eat context in future loops.

#### B) Update tool leaderboard:
- Append new ideas with scores to `research/reports/tool-ideas-leaderboard.md`
- Re-rank if any new idea scores higher than existing entries
- Never remove previous entries
- **Keep entries to 2-3 lines each** — name, score, one-line summary, revenue model

#### C) Update killed tool ideas registry:
- Add any killed idea to `research/strategy/07-KILLED-TOOL-IDEAS.md` — **one line per idea**: `- [Tool Name] — [kill reason]`
- Update the patterns section if a new kill pattern emerges
- Do NOT write multi-paragraph explanations — the iteration report has the details

---

## BAR FOR TOOL IDEAS

Different bar than SaaS because utility tools are cheaper to build and test. But still be critical:

1. "Is there SEARCH VOLUME proving people want this?" (Google Trends, not guessing)
2. "Does the unit economics math work?" (margin per use > 60%, volume achievable)
3. "Can I ship an MVP in 1 week and get 50 uses in the first month?"
4. "Does this survive ALL 5 kill tests?"

A tool scoring 16+ AFTER adversarial review is worth a 1-week build sprint. Anything below is noise.

## REFERENCE: PROVEN UTILITY TOOL PATTERNS

These are patterns that have worked for solo founders. Use as inspiration, not as ideas to copy:

- **AI + compliance format**: PhotoAI, passport/visa photo tools — AI processing + strict format requirements = willingness to pay
- **"Do it for me" tools**: Interior AI, virtual staging — replace expensive manual work with AI at 1/100th the cost
- **Batch processing**: Bulk image resize, bulk PDF operations — free tools do one at a time, charge for batch
- **Professional output from amateur input**: AI headshots from selfies, logo from text, mockup from screenshot
- **Tedious manual task → one click**: Remove background, transcribe audio, extract data from PDF
- **Seasonal/life-event tools**: Tax calculators, moving planners, wedding tools — predictable demand spikes
