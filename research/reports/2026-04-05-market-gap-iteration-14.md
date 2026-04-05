# Iteration 14: Fresh Angles with Updated Distribution Scoring

**Date**: 2026-04-05
**Strategy**: Searched unexplored developer niches with new scoring system (6 dimensions, max 30, distribution weighted 2x). Updated constraints: no high-touch sales, automated marketing only.

---

## Search Coverage

### Verticals scanned (all new):
- Dead code detection, tech debt tracking, release notes automation, incident postmortems, on-call rotation, database migration, API rate limit monitoring, staging environment management, PR review bottleneck

### Pre-filtered (already killed):
- Cron monitoring, uptime, status pages, error tracking, webhooks, changelogs, API docs, feature flags, env vars, SSL monitoring, AI code review (15+ tools)

---

## Ideas Deep-Dived

### 1. Dead Code Detection SaaS — KILL
- **Gap**: No mid-market SaaS ($20-100/mo). CodeScene at €18/author/mo is the only transparent pricing.
- **Problem**: Knip (JS/TS) has 4.9M weekly npm downloads — free. Python detection is harder (dynamic dispatch) but niche.
- **Kill reason**: Episodic use (run once, clean up, cancel = high churn). Free OSS covers main languages. Platform absorption risk from GitHub/Cursor adding dead code analysis.
- **Score**: Not scored — fails churn test

### 2. API Rate Limit Aggregator — PROMISING (24/30)
- **Gap**: No dedicated SaaS monitors rate limit consumption across third-party APIs from a single dashboard.
- **Current state**: Devs check each API dashboard separately, parse headers manually, build custom logging.
- **Buyer**: Engineering leads at SaaS companies using 5-10+ third-party APIs.
- **Distribution**: SEO "API rate limit monitoring", Google ads, dev communities, Product Hunt.
- **Concern**: Could be a FEATURE of DriftWatch rather than a standalone product. DriftWatch already monitors third-party APIs — adding rate limit monitoring is a natural extension.
- **Score**: 24/30 (gap:3, build:5, money:3, comp:5, dist:4, marketing:4)

### 3. DriftWatch re-scored under new system — 22/30 (MEETS BAR)
- Scores: gap:3, build:4, money:4, comp:3, dist:4, marketing:4
- Already 6/10 MVP complete. Best surviving idea across 14 iterations.

---

## Key Insight: API Rate Limit Monitoring as DriftWatch Feature

Rather than a standalone product, API rate limit monitoring could strengthen DriftWatch's value prop:
- **Current**: DriftWatch monitors changelogs + classifies breaking changes
- **Extended**: DriftWatch monitors changelogs + rate limits + deprecation timelines = "complete third-party API health dashboard"
- This increases stickiness (daily use for rate limits vs. episodic for changelogs)

---

## Ideas Killed This Iteration
- Dead Code Detection SaaS — episodic use, free OSS (Knip), platform absorption
- Tech Debt Tracking — SonarQube/CodeScene saturated, only 7% tool adoption suggests category rejection
- Release Notes Automation — already killed (changelog generators, 12+ tools)
- PR Review Bottleneck / AI Code Review — already killed (15+ tools, VC-funded)
- On-Call Management — PagerDuty dominates, saturated
- Database Migration — saturated, high-touch sales needed
- Staging Environment — bundled into platforms (Vercel, Northflank)

---

## Running Total
- 14 iterations, 178+ ideas considered
- 1 idea meets new 22/30 bar: DriftWatch (22/30)
- 1 adjacent idea worth considering as DriftWatch feature: API Rate Limit Monitoring (24/30 standalone)
