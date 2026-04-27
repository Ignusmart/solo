---
date: 2026-04-24
iteration: 25
status: REFRAME-SCREEN
---

# Iteration 25 — Below-Bar Reframe Screen

**Strategy**: Both APIDelta and ScanAble graduated from below-bar scores (17/25 and 15/25 post-adversarial respectively) via reframes that didn't apply during initial scoring. This iteration reverse-engineers their reframe playbooks, then screens every 16-17 below-bar idea in the kill registry against those playbooks. Goal: surface candidates that scored as "almost made it" and might survive under the right structural lens.

---

## The two reframe playbooks

### Playbook A — ScanAble template

| Ingredient | ScanAble realization |
|---|---|
| Public-crawlable input | URL → DOM → axe-core scan |
| Regulatory deadline | ADA Title II April 2026, EAA enforcement |
| Sub-$50 transactional pricing | $19 per scan |
| Zero/low marginal cost | axe-core OSS, no LLM inference |
| pSEO directory at scale | per-domain pages (BuiltWith model) |
| Existing market shape | free tools = raw data; pro audits = $1K+; gap at $19 |

### Playbook B — APIDelta template

| Ingredient | APIDelta realization |
|---|---|
| Weak/early-stage incumbent | API Drift Alert (no G2/Capterra reviews) |
| Sticky daily B2B use | API dependencies break in production |
| Concrete dollar ROI | Postman 52% breaking-changes pain, 70% fewer incidents |
| B2B engineering budget | $39-79/mo trivial line item |
| Substitutes are imperfect | Visualping/Changeflow are generic page monitors |

---

## Below-bar candidates (16-17 in original 5-dim scoring)

From SaaS-ideas track + tool-ideas track:

| Idea | Score | Original kill reason |
|---|---|---|
| CodeOnboard | 17 | $900M+ funded competitors, 1M-token context windows |
| CourseBot | 17 | Thinkific/Kajabi absorbed, 5+ competitors |
| LessonLoop | 17 | Empty niche = no market, Nudge Coach shut down |
| Premium MCP Server Portfolio | 17 | Platform-dependent, no proven revenue |
| AIComply Lite | 16 | Name taken, 13+ competitors built in 72 hours publicly |
| DocDrift | 16 | 5 new entrants (Doctective, Rasepi, Drift, Ferndesk, Mintlify) |
| DeadlineGuard | 16 | ExpiryEdge + Termedora adjacent |
| HireKit | 16 | Seasonal hiring churn |
| DocuParse API | 16 | Hardest build, distribution problem |
| BriefForge | 16 | Plutio exists, AI is a feature not a product |
| StubSnap | 17 | BUILT and KILLED — competitors are full tax platforms |
| ClipCast | 15 (post-adv) | Whisper + ChatGPT = workflow overlap |

---

## Screen results

| Idea | Public crawlable input? | Reg. deadline? | Margin moat? | Weak incumbent? | Verdict |
|------|---|---|---|---|---|
| CodeOnboard | NO (private codebases) | NO | NO (heavy RAG) | NO ($900M+) | KILL |
| CourseBot | NO | NO | NO (RAG) | NO (platforms absorbed) | KILL |
| LessonLoop | NO | NO | YES (analytics) | YES (Nudge Coach died) | **REFRAME-DEAD** — empty niche stayed empty for a reason; absent buyer is the kill, not absent tool |
| MCP Server Portfolio | WEAK | NO | DEPENDS | NO (Smithery/MCPize) | KILL |
| **AIComply Lite** | NO (private AI systems) | YES (Aug 2 2026) | PARTIAL | NO — **5 free tools** | KILL — **see deep check below** |
| DocDrift | NO | NO | NO | NO | KILL |
| **DeadlineGuard** | NO (private contracts) | NO | PARTIAL | NO — **see deep check below** | KILL |
| HireKit | NO | PARTIAL (NYC AEDT, IL AIVID) | YES | NO | KILL — seasonal use kills stickiness |
| DocuParse API | NO (user's docs) | NO | NO | NO (15+) | KILL |
| BriefForge | NO | NO | NO | NO | KILL |
| StubSnap | YES (public IRS rules) | NO | YES | NO — full tax platforms | ALREADY BUILT/KILLED |
| ClipCast | NO (private audio) | NO | NO | NO | KILL |

### Deep check — AIComply Lite reframe

The strongest candidate by deadline urgency. Apply ScanAble lens:
- ✅ Regulatory deadline: Aug 2 2026 (general purpose AI), Aug 2 2027 (high-risk systems)
- ❌ Public crawlable input: AI systems are private inside companies; no DOM-equivalent
- ❌ Weak incumbent: as of 2026-04-24, **5+ FREE tools** are live:
  - [artificialintelligenceact.eu](https://artificialintelligenceact.eu/assessment/eu-ai-act-compliance-checker/) (official-leaning)
  - [airiskcheck.eu](https://airiskcheck.eu/)
  - [Conformy.io](https://conformy.io/en/high-risk-ai)
  - [AI Compliance Advisor](https://aicomplianceadvisor.eu/annex-iii-high-risk-ai-checklist) (60-second risk scan)
  - [Compliance Radar](https://www.complianceradar.dev/) (2-min scan + GDPR)
- ❌ Plus Vanta has [a full EU AI Act compliance product](https://www.vanta.com/products/eu-ai-act).
- ❌ Plus a [Medium article from Jan 2026](https://medium.com/@cyriaczeh/how-i-built-an-eu-ai-act-compliance-saas-platform-in-72-hours-and-why-enterprise-tools-charging-28730ae3000d) confirms the original kill: "built in 72 hours."

**The deadline urgency is real, but the supply side has gotten WORSE since the original kill.** Free assessment tools are now the floor. The ScanAble play (paid PDF report at $19 vs free WAVE raw data) doesn't translate because the AI Act competitors have already moved to "free assessment as lead-gen for €99/mo enterprise compliance." There's no $19 transactional gap to occupy.

**Verdict: KILL stays.**

### Deep check — DeadlineGuard reframe

Apply APIDelta lens (weak incumbent + sticky + B2B budget):
- ❌ Weak incumbent: 2026 state has **Stitchflow free** (with AI contract parsing!) + **Termedora $49/mo** + **Contract Hound $95** + **ExpiryEdge** + **SpendHound free** + enterprise CLMs (Juro, LinkSquares, Sirion). Plus [Stitchflow's free tier ships AI date extraction](https://www.stitchflow.com/tools/renewal-tracker) — the exact "AI contract & deadline tracker" pitch.
- ✅ B2B budget: yes
- ❌ Sticky daily use: contract review is quarterly, not daily
- ❌ Public-crawlable input: contracts are private

**Verdict: KILL stays. AI parsing has been commoditized in the 12 months since the original score.**

---

## What this iteration actually proves

### The structural finding (this is the useful part)

ScanAble's and APIDelta's success each required ~5 simultaneous structural ingredients. Below-bar candidates fail because they're missing 3-5 of those ingredients, and the missing ones are usually the **non-substitutable** ones:

- **Public crawlable input** — non-substitutable for the ScanAble pSEO model. Without it, you can't auto-generate per-X directory pages. None of the 12 candidates have this except StubSnap (already built/killed).
- **Weak incumbent** — substitutable but rare. Categories don't stay weakly-defended for long; iter 7 already noted DocDrift's gap closed in months. Stitchflow added AI parsing for free in the 12 months since DeadlineGuard's original score.
- **Regulatory deadline** — exists for AIComply (Aug 2026), HireKit (NYC/IL hiring AI laws), but doesn't unlock anything alone — supply side fills with free tools faster than the deadline drives demand.

### Why "just-below-bar" doesn't mean "almost a winner"

The user's reasonable hypothesis was: "if APIDelta and ScanAble were below-bar at scoring, the next-best below-bar ideas might also survive a reframe." This iteration falsifies that hypothesis empirically. The two graduates had **rare structural ingredients** (public-crawlable input + zero-margin pipeline for ScanAble; weak early-stage purpose-built competitor for APIDelta). The other below-bar candidates lack those ingredients — that's why they're below bar — and a reframe doesn't manufacture them.

**Below-bar is not the same as "almost above bar." Below-bar correlates with structurally missing ingredients.**

### Where to actually look

If a 25th iteration matters, the question to answer isn't "what other below-bar ideas reframe" — it's:

> **What is the next product where (public crawlable input) × (regulatory or industry mandate) × (zero/low marginal cost pipeline) × (no current sub-$50 transactional player) intersect?**

Candidate adjacencies that may not be saturated yet:
- Schema.org structured data audit pSEO (Google's free tester is the floor — likely killed)
- Cookie consent compliance pSEO (CookieYes/Termly own this — likely killed)
- Security headers compliance pSEO (SecurityHeaders.com owns this — taken)
- robots.txt / sitemap / hreflang multi-language SEO compliance pSEO — *worth checking, narrow but possibly open*
- WCAG accessibility pSEO — taken (ScanAble)
- Email deliverability pSEO with DKIM/SPF/DMARC per-domain reports — *Mailtrap/Postmark cover monitoring; worth checking the per-domain SEO play*
- Native iOS/Android app store privacy nutrition label compliance pSEO — *Apple's enforcement is changing; possibly novel*

That's a ~30-min scan, not a fresh research loop. **If the user wants iteration 26, this is the only direction with non-trivial probability.**

---

## Stats updated

- Iterations: 25
- Total ideas killed: 244+
- Reframe screens applied to below-bar candidates: 12
- Survivors after reframe: 0
- Methodology paths tested: 4 (top-down vertical, bottom-up wishlist, recurring-task mining, below-bar reframe screen)
- Surviving above bar: APIDelta (22/30) — Day 30 pending May 15
- Consecutive zero-result iterations: 13 (13-25)
- Research status: **DEFINITIVELY CLOSED with 4-way methodology triangulation.**

The closure is now structurally explained, not just empirically observed. Below-bar ideas don't reframe into above-bar ideas because the missing ingredients (public input, weak incumbent) are the very things that made them below-bar in the first place.
