# Gmail AI Triage Sidebar -- Adversarial Kill Analysis

**Date**: 2026-04-05
**Verdict**: KILL. Google's native Gemini integration is a direct existential threat, and the market is crowded at every price point.

---

## Competitive Landscape (Exhaustive)

**Full email clients (not extensions):** Superhuman ($30/mo), Shortwave (free tier + $14/mo Pro), Spark Mail, Canary Mail. Shortwave explicitly markets itself as the Inbox by Google replacement and is actively funded.

**Chrome extensions already doing this:**
- **Simplehuman** ($7.49/mo) -- lightweight Superhuman alternative, keyboard shortcuts, split inbox, read receipts. 2MB, privacy-first, works in Gmail tab. Direct competitor to the proposed concept.
- **Email Prioritizer** -- AI-based urgency prediction, free on Chrome Web Store.
- **MailMaestro** -- AI drafts, summaries, prioritization inside Gmail.
- **Ovy, Remail, ChatGPT Writer, EzMail.AI, MailMood, Say Less** -- all ProductHunt-launched Gmail AI extensions (2025). Most are free or freemium. None have broken out.
- **HeyHelp** -- Gmail automation extension.
- **Inbox Reborn, Inboxy, Simplify Gmail** -- extensions replicating dead Inbox by Google features (bundles, snooze, highlights).

**Server-side filtering:** SaneBox ($7/mo Snack, $12/mo Lunch, $36/mo Dinner). 98.5% accuracy claimed, saves 3-4 hrs/week per reviews. Works across any email client, not just Gmail. At $7/mo for basic and $12/mo for multi-account, SaneBox directly undercuts the proposed $12/mo price with a more mature product and server-side approach that avoids extension fragility.

## The Google Kill Shot

In January 2026, Gmail launched its Gemini 3-powered overhaul:
- **AI Inbox**: non-chronological priority clustering, "Catch me up" summaries -- this IS the core feature of the proposed extension, now free and native.
- **AI Overviews**: thread summaries, natural-language inbox queries (free for basic, premium for advanced).
- **Suggested Replies**: context-aware one-click responses replacing Smart Reply -- this IS the quick-reply feature proposed.
- **Help Me Write**: free AI drafting for all users.
- **CC (Labs)**: experimental AI agent for daily inbox briefings.

These features are rolling out to all Gmail users by default. Users must opt OUT, not opt in.

## Kill Questions Answered

**Is Google's Gemini making third-party AI extensions redundant?** YES. The Jan 2026 launch covers prioritization, summaries, smart replies, and drafting -- all four pillars of the proposed extension. The remaining gap is narrow (custom labels, workflow automation) and shrinking.

**Is $12/mo defensible against SaneBox at $7/mo?** NO. SaneBox has years of training data, works server-side (no extension breakage), and their $7 plan already covers basic filtering. The proposed extension would need to justify a 70% premium over a battle-tested incumbent.

**Can extensions reliably access Gmail content?** RISKY. Google enforced full OAuth 2.0 as of March 2025. Extensions requesting Gmail read/write scopes face restricted scope verification, which is slow (weeks/months) and can be revoked. DOM-scraping approaches break on every Gmail UI update. Google controls the platform end-to-end.

**What is the churn pattern?** B2B SaaS monthly churn runs 2-5%. Email productivity tools likely trend higher because (a) the novelty effect fades fast, (b) Google keeps absorbing the value prop natively, and (c) email habits are sticky -- users revert to defaults. The zero-to-free ProductHunt launches flooding this space signal that retention is hard enough that developers cannot sustain paid models.

## Summary

The market is a graveyard of free/cheap Gmail AI extensions that never broke out, bracketed by Superhuman/Shortwave above and SaneBox below, with Google's free Gemini integration eating the entire middle. Do not build.
