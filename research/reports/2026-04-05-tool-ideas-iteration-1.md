# Tool Ideas — Iteration 1 (2026-04-05)

## Signal Hunting Summary

Searched 25+ utility tool categories across image tools, document generators, developer tools, compliance tools, audio/voice tools, and AI-powered professional service replacements.

**Key market insight**: The AI boom has made utility tools trivial to build. Nearly EVERY obvious "X generator" category has 10-30+ competitors in 2026. Free tools dominate most categories. The Pieter Levels model (PhotoAI $138K/mo, InteriorAI $38-45K/mo) works because of 600K follower distribution — not replicable without existing audience.

### Categories Explored & Killed This Iteration
- Image generation (headshots, logos, tattoos, coloring pages, product photos)
- Image processing (restoration, background removal, upscaling, screenshot beautifiers)
- Document generators (contracts, receipts, invoices, proposals, resumes)
- Developer tools (diagrams, API docs, favicons, regex)
- Compliance tools (passport photos, brand guidelines)
- Content tools (podcast show notes, children's books, listing descriptions)
- Business tools (name generators, brand kits, email signatures)
- Audio/voice tools (voice clone, TTS)
- Floor plan generators, virtual staging, presentation makers

See killed file for full list with kill reasons.

---

## Deep Dives

### 1. ClipCast — Pay-per-Episode Podcast Clip Finder

**Concept**: Upload podcast audio → AI transcribes, finds top 3-5 viral-worthy clips (30-60s), generates show notes + chapter markers. Pay $3-5 per episode instead of $99/mo subscription.

**Demand**: 4M+ active podcasts, 500M+ listeners globally. Most indie podcasters can't justify $99/mo (Castmagic).

**Competition**: Castmagic ($99/mo), Descript ($24/mo), PodSqueeze, SwellAI, Opus Clip (video-focused). No good pay-per-episode option exists.

**Unit Economics**: Whisper API = $0.006/min. 1hr episode = $0.36. LLM analysis ~$0.10. Total cost ~$0.50/episode. At $4/episode, margin = 87%.

**Adversarial Review**:
- Free tool test: ChatGPT + manual transcript partially works but requires 30+ min manual effort. BORDERLINE.
- ChatGPT test: Can identify clips from text but can't process audio directly. Requires manual transcript upload. PASS.
- Volume test: Need 250 episodes/mo at $4 = $1K/mo. 0.006% of 4M podcasts. ACHIEVABLE.
- Margin test: 87%. PASS.
- Solo maintainability: Simple — Whisper API + LLM + basic UI. PASS.

**Score**: Search volume 3 | Build speed 4 | Unit economics 4 | Competition gap 3 | SEO/distribution 3 | **Total: 17/25 → revised to 15/25 after adversarial** (ChatGPT overlap risk)

**Kill criteria**: <50 episodes processed in first month after launch.

---

### 2. FoodGlow — Pay-per-Photo Restaurant Photo Enhancer

**Concept**: Upload food photos → AI enhances lighting, color, composition. Specifically optimized for food photography (not generic). $2-3 per photo. Replaces $2,500-7,500 traditional food photography sessions.

**Demand**: 1M+ restaurants in US alone. Traditional food photography = $25-200/dish. Food delivery apps (DoorDash, UberEats) require good photos.

**Competition**: FoodShot AI ($15/mo, 25 images), MenuPhotoAI ($39/mo). Both subscription-based. No good pay-per-photo for small restaurants that need 5-10 photos occasionally.

**Unit Economics**: Image processing ~$0.05-0.20/image. At $2/photo, margin = 75-90%.

**Adversarial Review**:
- Free tool test: Snapseed (free) auto-enhance works for basics. Not food-specific. BORDERLINE.
- ChatGPT test: Can't process images for editing. PASS.
- Volume test: Need 500 photos/mo at $2 = $1K/mo. With 1M+ restaurants, very achievable.
- Margin test: 75-90%. PASS.
- Solo maintainability: Needs image processing pipeline. Medium complexity. PASS.

**Score**: Search volume 3 | Build speed 3 | Unit economics 3 | Competition gap 3 | SEO/distribution 3 | **Total: 15/25 → 14/25 after adversarial** (uncertain search volume, existing competitors)

**Kill criteria**: <100 photos processed in first 2 weeks.

---

### 3. ProposalDrop — Pay-per-Proposal PDF Generator

**Concept**: Input project scope + pricing → professional PDF proposal with cover page, scope, timeline, pricing table, T&Cs. $3-5 per proposal. Targets freelancers who send 2-5 proposals/month and can't justify $29/mo (Proposify).

**Demand**: "Proposal template" is high search volume. Millions of freelancers globally.

**Competition**: Proposify ($29/mo), PandaDoc ($19/mo), SendAndSign ($5/proposal), Bookipi (FREE), SoloTools (3 free/mo).

**Unit Economics**: Text generation ~$0.01-0.05/proposal. PDF gen = free. Margin >95%.

**Adversarial Review**:
- Free tool test: Bookipi is free and generates proposals. **HARD FAIL.**
- ChatGPT test: Generates text but not formatted PDF. PASS.
- Volume test: Need 250/mo at $4. Achievable but Bookipi (free) siphons demand.
- Margin test: >95%. STRONG PASS.
- Solo maintainability: Simple app. PASS.

**Score**: Search volume 4 | Build speed 4 | Unit economics 5 | Competition gap 2 | SEO/distribution 3 | **Total: 18/25 → 14/25 after adversarial** (Bookipi free is a killer)

**Kill criteria**: <30 proposals generated in first month.

---

## Key Patterns Discovered

1. **Every "X generator" category has 10-30+ competitors** — the AI wave made these trivially buildable.
2. **Free tools dominate most categories** — platforms (Canva, Google, Adobe) give away what indie devs charge for.
3. **The Pieter Levels model requires distribution** — without 600K followers, you need SEO dominance.
4. **Pay-per-use pricing is rare** — most competitors use subscriptions. This IS a gap in some categories.
5. **Image generation tools are the most saturated** — headshots, logos, backgrounds, etc.
6. **The "cheaper alternative to expensive tool" play is viable** — $1 passport photos vs $14 PhotoAiD proves this.

## Next Iteration Should Explore
- Non-AI utility tools (data processing, file operations, calculators)
- B2B-specific tools (not consumer)
- Seasonal/event-driven tools (wedding, tax, moving)
- Tools that combine multiple APIs (domain + trademark + social handle checks)
- Physical product adjacent tools (shipping label generators, barcode tools)
