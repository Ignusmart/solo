# Killed Ideas Registry

> **Purpose**: Permanent record of ideas that have been researched and rejected. Any future research session MUST check this file first to avoid re-exploring dead ideas.
>
> **Last updated**: 2026-04-05 (after 13 discovery iterations + deep adversarial reviews)

---

## How to read this file

- **Surface kill**: Dismissed during initial vertical scanning (competitor count, saturation)
- **Deep kill**: Survived initial scoring but killed under adversarial deep-dive with real competitor/market evidence
- Every idea has a one-line kill reason so you can quickly skip it

---

## Deep-Killed Ideas (Top 6 — survived initial scoring, killed under scrutiny)

These were the highest-scoring ideas from 9 iterations of research. All were killed during adversarial deep review on 2026-04-05.

| Idea | Original Score | Revised Score | Kill Reason | Report |
|------|:-:|:-:|-------------|--------|
| **ScopeShield** — AI scope & revenue guard for freelancers | 18/25 | 12/25 | Name taken (scopeshield.cloud). 4+ competitors exist but NONE show PMF = market rejects category. $29/mo > full CRMs (Bonsai $17, Plutio $19). AI moat is a single GPT prompt. Contracts are the real solution, not software. | `reports/2026-04-05-scopeshield-deep-review.md` |
| **PostPilot** — text-first blog-to-social repurposer | 18/25 | KILL | Missinglettr does this at $15/mo. Planable does it free. ChatGPT Plus ($20/mo) does this + everything. 77% annual churn for budget AI tools. Repurposing is becoming a built-in feature everywhere. | `reports/2026-04-05-postpilot-deep-review.md` |
| **CourseBot** — AI student support for course creators | 17/25 | 10/25 | Platform absorption already happened: Thinkific "Thinker" (Feb 2026), Kajabi Creator.io, Heights AI chat. Chatbase/Wonderchat serve same purpose. Student support isn't a top-5 creator pain point. | `reports/2026-04-05-coursebot-deep-review.md` |
| **LessonLoop** — AI course completion nudges | 17/25 | KILL | Empty niche is empty for a reason (Nudge Coach shut down). Platforms absorbing nudge features. ROI is 3-step indirect. 3-4 week build minimum for multi-platform integration. | `reports/2026-04-05-ideas-4-6-deep-review.md` |
| **CodeOnboard** — AI codebase explorer for onboarding | 17/25 | KILL | $900M+ in competitor funding. 1M-token context windows make "chat with codebase" commodity. Greptile was literally "Onboard AI" and pivoted away. | `reports/2026-04-05-ideas-4-6-deep-review.md` |
| **AIComply Lite** — EU AI Act compliance tracker | 16/25 | KILL | "AIComply" name taken (2 products). 13+ competitors. Built in 72 hours by someone publicly. Deadline-driven churn. Requires EU legal expertise. | `reports/2026-04-05-ideas-4-6-deep-review.md` |

---

## Surface-Killed Ideas (from 9 iterations of vertical scanning)

### Developer Tools (Iteration 1)
| Idea | Kill Reason |
|------|-------------|
| DocDrift — stale doc detector | 5+ new competitors since discovery (Doctective, Rasepi, Mintlify). Score dropped 17 -> 16. |
| HookRelay — webhook dev workspace | Hookdeck well-funded, expanding down-market |
| Changelog generators | 12+ tools, trending to bundled suites |
| Env/secrets management | Doppler, Infisical, dotenvx, Keyway. Well-served |
| Feature flags | ConfigCat, Flipt, PostHog, Rollgate, Unleash. Crowded |
| Cron job monitoring | CronMonitor, Dead Man's Snitch, Better Stack. Saturated |
| Uptime/status pages | 20+ competitors |
| AI PR descriptions | 5+ free GitHub Actions. No pricing power |
| AI commit messages | Built into every AI IDE. Feature, not product |
| Error tracking | GlitchTip, SigNoz, PostHog, Better Stack. Well-funded |
| Incident/runbook automation | Enterprise-only (Rootly, FireHydrant) |
| Contract testing | PactFlow dominates. Enterprise sales cycle |
| Infrastructure drift | DriftHound (OSS), Spacelift. Enterprise IaC territory |
| AI code migration | Moderne ($70M+). Enterprise problem |
| Webhook testing (standalone) | ngrok, Webhook.site, Hookdeck cover pieces |
| API diff tools | oasdiff is free/OSS. Niche too small |
| Regex builders | 10+ free AI tools. No pricing power |
| Technical debt trackers | SonarQube, CodeScene, Stepsize. Well-covered |

### Creator Economy / E-commerce / Solopreneur (Iteration 2)
| Idea | Kill Reason |
|------|-------------|
| BriefBot — AI conversational client intake | Demolished: Perspective AI (exact match), Dashform $19/mo, CrispForms (free). 5+ competitors. Score 18 -> 14 |
| AI review response (local biz) | ReplyChampion $10/mo, ReviewScout $4.99/mo. Race to bottom |
| Content repurposing (video-first) | 15+ tools: Opus Clip, Repurpose.io, Minvo, PostOnce |
| E-commerce multi-channel listing | OneCart, Sellbrite, ChannelAdvisor. Enterprise APIs expensive |
| Etsy seller tools | EverBee, Alura, eRank, Marmalead. Well-served $5-30/mo |
| Testimonial/social proof widgets | Senja, Testimonial.to, Famewall, LaunchWall, 10+ more |
| Email marketing | MailerLite (free), Moosend $9/mo, Flodesk $19/mo. Extremely crowded |
| AI meeting notes | Otter.ai, Fireflies, tl;dv, Granola. Well-funded |
| E-commerce analytics dashboards | Triple Whale, Lifetimely, Boardroom, Looker Studio (free) |

### Compliance / HR / API-First (Iteration 3)
| Idea | Kill Reason |
|------|-------------|
| DeadlineGuard — contract deadline tracker | ExpiryEdge + Termedora adjacent. Market filling in |
| HireKit — hiring scorecards | Seasonal hiring = 15-25% monthly churn |
| DocuParse API — vertical doc extraction | Hardest build (3-4 weeks), accuracy make-or-break, LLM cost pressure |
| HR compliance (SOC 2, ISO, GDPR) | Vanta, Sprinto, Drata. VC-funded enterprise tools |
| Employee handbook generators | AirMason, Waybook, HandbookHub. Crowded free + paid |
| Full ATS / applicant tracking | 24+ platforms including free options |
| Policy management platforms | Xoralia, ComplianceBridge, StandardFusion. SMB filling in |
| Background check APIs | Checkr, GoodHire, Accurate. Mature, regulated |
| PDF/invoice data extraction APIs | AWS Textract, Google Doc AI, Mindee, Klippa, Veryfi. 15+ providers |
| API monetization/billing | Zuplo, Moesif, Kong Konnect. Well-served |
| Employee onboarding platforms | Gusto, BambooHR, Zoho People (free), CharlieHR |
| Full contract management (CLM) | PandaDoc, Juro, ContractSafe. Mid-market filling in |

### Education / Content Management / Real Estate (Iteration 4)
| Idea | Kill Reason |
|------|-------------|
| TenantReady — AI landlord tool | TurboTenant (free), TenantCloud (free). Score 11/25 — lowest ever |
| Headless CMS for small teams | 15+ options (Strapi, Sanity, Payload, Prismic...) |
| Content calendar / editorial workflow | 20+ tools (CoSchedule, Planable, Buffer...) |
| Knowledge base software | KnowledgeOwl, BookStack, GitBook, Slite. Well-served |
| Real estate CRM / lead management | 15+ platforms (Follow Up Boss, Lone Wolf, kvCORE...) |
| Small landlord property management | Free tools dominate (TurboTenant, Stessa, Baselane) |
| Real estate showing scheduling | Tenant Turner, ShowMojo. Mature |
| Real estate open house apps | Showable, Open Home Pro. Niche, already served |
| SEO content brief generators | Frase, NeuronWriter, Surfer SEO, Outranking. 10+ tools |
| Course creator communities | Circle, Skool, Mighty Networks, Heartbeat. Crowded |
| Online quiz/assessment builders | 15+ tools (Meiro, LeadQuizzes, OpinionStage...) |
| AI tutoring platforms | Khanmigo, AI Tutor, Strater AI. Well-funded. Not micro-SaaS |
| Course creation platforms | 15+ platforms. Don't compete with platforms |

### Email / Customer Support / QA-Testing (Iteration 5)
| Idea | Kill Reason |
|------|-------------|
| HelpdeskLite — AI micro help desk | 61 free shared inbox tools. Freshdesk free tier |
| InboxPulse — email deliverability monitor | GlockApps covers this. Intermittent pain = churn |
| ReviewDrop — visual website feedback | 6+ competitors including free. Most crowded niche |
| Email deliverability tools | 15+ tools. GlockApps, ZeroBounce, Mailtrap, Google Postmaster (free) |
| Email warm-up tools | 11+ tools. Race to the bottom |
| Cold email platforms | Instantly, SalesHandy, SmartLead, Lemlist. VC-funded |
| Email signature management | 10+ tools at $5-11/mo |
| Email inbox placement testing | 10+ options. Saturated |
| Email domain reputation monitoring | Google Postmaster (free), Microsoft SNDS (free) |
| Shared inbox tools | 61 free tools on G2 |
| Help desk / ticketing | 25+ tools. Problem is complexity, not missing tools |
| Intercom alternatives | 16+ affordable alternatives. Gap filled 3 years ago |
| Visual regression testing | BackstopJS, Playwright, Percy (free). OSS dominates |
| Bug tracking / reporting | Linear, Gleap, Marker.io, SnapFeed, BugSmash (free). 6+ tools |
| Customer feedback tools | 22+ tools. Market consolidating |
| Test automation for indie devs | Playwright (free), Cypress (free). Gap is education, not tooling |

### Fitness / Events / Supply Chain (Iteration 6)
| Idea | Kill Reason |
|------|-------------|
| StockSnap — spreadsheet-to-inventory | 20+ free inventory tools. Zoho free tier |
| SessionPack — credit-based coach booking | CoachIQ owns this niche |
| GigTix — micro-event ticketing | Luma (free), TixFox ($0.39/ticket). Dead on arrival |
| Gym management software | 19+ tools ($59-299/mo). Every segment served |
| Personal trainer platforms | 15+ tools (Trainerize, TrueCoach, Everfit...) |
| Fitness challenge delivery | CommuniPass dominates |
| Event management platforms | 30+ tools. $15.2B market |
| Event ticketing (Eventbrite alts) | 12+ alternatives. Gap filled years ago |
| Virtual event platforms | Airmeet, Contrast, Livestorm. Every price point covered |
| Supply chain visibility | Enterprise-only. Not micro-SaaS |
| Warehouse management (small biz) | 14+ free options |
| Food truck/restaurant operations | Square (free), Toast, Revel. POS-first model = free software |
| Small manufacturer MRP | Gap is real but 3-6 month build. Not feasible |

### Food / Documentation / Privacy Wildcards (Iteration 7)
| Idea | Kill Reason |
|------|-------------|
| DocPulse — doc health monitor | 5 new competitors since Iter 1. More competitive, not less |
| MenuMath — restaurant menu profitability | Offline-first buyers. Eatos + free templates cover it |
| Ghost kitchen management | Otter, Deliverect, Cuboh. POS-first model |
| Restaurant food costing | 10+ tools on Capterra including free |
| Restaurant menu engineering | Eatos ($49-199/mo, AI-powered, POS-integrated) |
| Changelog tools | 12+ tools. Trend toward bundling |
| SOP/playbook documentation | 9+ dedicated tools (Waybook, Trainual, Scribe...) |
| Cookie consent management | 8+ tools. CookieYes, Enzuzo, Termly all have free tiers |
| Privacy policy generators | 10+ free generators. No pricing power |
| GDPR compliance (general) | SMB tier served by free plans |
| Async standup tools | 5+ dedicated tools (Geekbot, DailyBot, Standuply...) |
| AI automation (no-code) | Zapier, Make, n8n dominate |

### Bottom-Up Signal Hunting (Iteration 8)
| Idea | Kill Reason |
|------|-------------|
| BriefForge — AI proposal generator | Plutio already solves flat-rate proposals. AI is feature, not product |
| PromptDiff — prompt version control | Langfuse (OSS), PromptLayer, LangSmith all cover this |
| PayChaser — automated invoice follow-up | Chaser exists ($39-199/mo). Every invoicing tool has reminders |
| AI agent observability | 15+ tools including VC-funded. Not micro-SaaS |
| Prompt management (full) | 5+ dedicated tools. Filling in fast |
| AI code review tools | CodeRabbit, Qodo, CodeAnt. 15+ tools. VC-funded |
| Waitlist/pre-launch tools | 7+ tools at $0-19/mo |
| Invoice payment chasing | Chaser, FreshBooks, Wave all cover this |

### Agency / Trades / Pricing (Iteration 9)
| Idea | Kill Reason |
|------|-------------|
| TradeQuote — AI quote generator for trades | ServiceM8 AI, QuoteIQ, CrewRoute. Trades are offline-first |
| RegAlert — regulatory change notifications | Content curation, not software. Needs regulatory expertise |
| Agency white-label reporting | 11+ tools (Swydo, Reporting Ninja, AgencyAnalytics, DashThis...) |
| Agency client onboarding | 16+ tools. Leadsie owns ad-account-access niche |
| Cleaning/landscaping software | ZenMaid, Yardbook, Connecteam (free). Well-served |
| Field service management | 20+ tools. Jobber, ServiceBridge, Connecteam (free) |
| Dynamic pricing (small biz) | Prisync, Price2Spy, Pricefy. Mature market |
| AI pricing (Shopify) | Price Perfect + multiple Shopify-native solutions |
| Price monitoring tools | 10+ tools from free to $99/mo |

### Multi-Source Signal Hunting (Iteration 10)
| Idea | Kill Reason |
|------|-------------|
| CommCalc — micro-team sales commission calculator | Commissionly + Sales Cookie already serve. 23+ tools in category. Spreadsheets "good enough" for <15 reps. ChatGPT can build a commission sheet. |
| DepWatch — combined status + changelog + impact dashboard | Combination product. IsDown adds changelog tab = killed. Feature, not product. |
| Procurement software (SMB) | 15+ affordable tools. Zapro, ProcureDesk, Kissflow. $8.2B market well-served. |
| Internal tool builders | Budibase, Appsmith, ToolJet all OSS/free. Retool alternatives abundant. |
| Data pipeline/ETL (small teams) | Airbyte (OSS), Weld, Stitch, Hevo. Well-served from free to $299/mo. |
| B2B notification infrastructure | Novu, SuprSend, Knock, Courier. Well-funded dedicated platforms. |
| SOC 2 evidence automation | Vanta, Drata, Sprinto, Delve, Comp AI, Screenata. $1.3B market. |
| Status page aggregation | IsDown ($37/mo), StatusGator, IncidentHub. 3+ direct competitors. |
| Calculation form builders | Cognito Forms, Paperform, Formstack, Logiforms. Well-served. |
| Employee offboarding/deprovisioning | Josys, Auvik, Torii, Stitchflow, Nudge Security. Covered. |
| SaaS pricing A/B testing | Optimizely, VWO, Statsig (free tier), Convert, AB Tasty. 15+ tools. |
| Client portals (agency/freelancer) | SuperOkay, Taskip ($12/mo), SuiteDash, Zite (free). 16+ tools. |
| Webhook delivery infrastructure | Hookdeck (well-funded), Svix ($490/mo), GetHook. Mature space. |
| SaaS access review/permissions | ConductorOne, Lumos, BetterCloud, Wing Security, AccessOwl. 9+ tools. |
| Virtual data rooms | 20+ providers from free (Peony) to $200K+/yr. |
| Sales commission tracking | QuotaPath ($25/user/mo), Commissionly, Spiff, CaptivateIQ. 23+ platforms. |
| Deal desk workflow | DealHub, PandaDoc, IdeaPlan. 8+ tools. Mostly mid-market+. |
| SSL certificate monitoring | TrackSSL (free), LetsMonitor (free), UptimeRobot, StatusCake. 12+ tools. |
| SBOM/license compliance | Syft (OSS), Snyk, Aikido, Anchore. OSS dominates. |
| RFP/proposal response | 30+ tools on GetApp. DeepRFP, AutoRFP.ai, Arphie, Responsive. |
| Incident postmortem automation | incident.io, Rootly, Datadog, PagerDuty. Enterprise-focused. |
| Customer onboarding tracking | Rocketlane, GUIDEcx, Zite, Dock. 16+ tools. |
| API changelog (internal/provider) | Theneo, Stoplight, ReadMe. API docs tools adding this natively. |
| DevRel community metrics | Advocu, Common Room, Orbit (Postman). Covered. |
| Customer health scoring | Custify, Churn Assassin, ChurnZero, Gainsight. 10+ tools. |
| Dependency update bots | Dependabot (free, GitHub-native), Renovate (free). No gap. |

### Hyper-Vertical & Orphaned Customer Signal Hunting (Iteration 11)
| Idea | Kill Reason |
|------|-------------|
| Freight Broker Micro-TMS — targeting LoadPilot's orphaned customers | AscendTMS free tier is official migration path. LoadPartner (OSS) targets same niche. Domain expertise barrier. Score 13/25. |
| Dunning/Failed Payment Recovery for Indie SaaS | Weekend project (Stripe webhook + 3 emails). 8+ competitors (Churnkey, Churnbuster, Butter, Stunning). Stripe commoditizing. |
| Self-Storage Operator Wedge Tool | Cubby raised $63M (Goldman Sachs). 8+ competitors (Prorize, Veritec, RevMan AI, Storeganise, Hummingbird, Monument, Stora). Storable controls SiteLink API. |
| SMB Google Review Request ($15-29/mo) | 276+ tools on GetApp. 10+ at exact price point (Reputigo free, HiFiveStar free, EmbedReviews $29). Trivially replicable. Thin margins with Twilio SMS costs. |
| Integration Health Monitor (cross-platform sync watchdog) | Feature, not product. Zapier shipping Alerts (GA on Enterprise) + Log Streams. Make.com has built-in error handling. No buyer segment in the middle. |
| Self-storage rate management | Prorize (20 years, 8K stores), Veritec (8K stores), RevMan AI. Mature incumbents. |
| Print shop management | Printavo ($49-149/mo), ShopVOX ($99/mo+$19/user). Incumbents adequate. |
| Pest control software | PestPac, Pocomos, FieldRoutes, HouseCall Pro, GorillaDesk. Dozens of tools. |
| Accounting firm doc collection | Content Snare ($28-74/mo), SafeSend ($500+/yr), Canopy, SmartVault, ClientHub. Served. |
| Insurance agency operations | Applied Epic, HawkSoft, EZLynx, AgencyZoom. Many incumbents. |
| Localization/translation PM | Phrase, Smartcat, XTM, memoQ, Trados. Mature $75B industry. |
| Feature voting at indie scale | Nolt ($29/mo), Fider (free OSS), Upvoty, Sleekplan, Canny. Well-served. |

### AI-Adoption Aftermath & Emerging Categories (Iteration 12)
| Idea | Kill Reason |
|------|-------------|
| Vibe Code Health Scanner — AI-generated code security audit | 8+ dedicated tools (Vibe App Scanner, VibeSecurity, VibeWrench, VibeSafe, etc.). $88M+ VC (Escape.tech $18M, Qodo $70M). Platforms bundling security (Lovable+Aikido, Cursor, GitHub Copilot). Window closed. |
| LLM Cost Dashboard — "Plausible for AI Spend" | CostLayer ($9/mo) does exactly this with no code changes. StackSpend also. 10+ tools. Cloud cost tools (CloudZero, Vantage) absorbing. Token prices dropping 67-97% YoY. |
| Accessibility Compliance Tool (EAA + ADA) | 50+ tools on G2. axe-core (OSS) commoditizes scanning. accessiBe/UserWay own SMB at $49/mo. EAA demand absorbed (deadline June 2025). Fix-once = high churn. |
| MCP server security middleware | MCP infrastructure previously killed. Protocol absorbing security standards. Too early for revenue. |
| SMB AI governance / policy-in-a-box | Adjacent to AIComply Lite (killed). "Policy generator" is AI wrapper. Requires compliance expertise. |
| Shadow AI detection (browser extension) | Requires MDM/centralized deployment. DLP tools exist (Nightfall, etc.). Too enterprise. |
| US multi-state privacy compliance tracker | Osano, OneTrust, TrustArc, Enzuzo cover this. Free tiers available. |
| AI content fact-checking tool | Best accuracy 82%, too unreliable for B2B. Liability risk. Early. |
| Meeting action-item enforcement | Overlaps PM tools (Asana, Linear, Monday). Meeting-focused conflicts with async-only constraint. |

### Distribution-First Marketplace Scanning (Iteration 13)
| Idea | Kill Reason |
|------|-------------|
| AI Meeting Prep Chrome Extension | 8-12 competitors (Briefcase, Wudpecker, Read.ai, Fellow, Fireflies). Sales platforms absorbing (Apollo, ZoomInfo, Gong). LinkedIn scraping = legal risk. ChatGPT does 80% in 60 seconds. Weekly use, not daily. |
| VS Code Database GUI Extension | DBCode already captured this ($3/mo, 50+ databases, 150K installs, April 2026). VS Code has NO native payment infrastructure. Dev WTP near zero for extensions. |
| AI Gmail Triage Sidebar Extension | Google's Gemini 3 absorbed this natively (Jan 2026): AI Inbox, AI Overviews, Suggested Replies — all free. SaneBox at $7/mo. Simplehuman at $7.49/mo. Platform risk severe (OAuth, DOM changes). |
| LinkedIn Inbox CRM extension | LinkedIn actively fights extensions (sued HiQ Labs). DMCA takedowns. Legal/technical minefield. |
| Slack feedback triage bot | Narrow buyer pool. Slack AI absorbing. Platform dependency. |
| Slack approval workflows | Approveit/Wrangle exist. Slack Workflow Builder improving. |
| VS Code AI Prompt Management | Speculative, no proven demand signal. |
| VS Code API Testing (better Thunder Client) | Thunder Client 7M+ installs. DBCode precedent: $3/mo ceiling for VS Code. |

| Scheduled report/PDF automation | Looker Studio (free), Reporting Ninja, Kaelio. Well-served. |
| Usage-based billing/metering | OpenMeter, Orb, Lago, Metronome, Stripe Billing. Well-funded. |
| Technical SEO monitoring | Ahrefs, Semrush, Screaming Frog, Sitebulb, DebugBear. 11+ tools. |
| MSP/PSA tools | ConnectWise, Syncro, ITFlow (free OSS). 13+ tools. |
| Customer expansion/upsell tracking | Gainsight ($2,500/mo), Journeyz. Enterprise-focused. |
| Security questionnaire automation | Conveyor, Breeze, 1up, Vanta, Tribble. 13+ tools. |

---

## Previously Killed (from prior research, before iterations)

| Idea | Kill Reason |
|------|-------------|
| SaaS spend tracker | Market rejected this repeatedly. 8-15% monthly churn. Spreadsheet is real competitor |
| MCP infrastructure tooling | Crowded or no proven demand |
| AI lab notebook | Regulated, slow adoption, labs behind on tech |
| Traditional freelancing (Upwork) | Race to bottom, requires calls |
| Bug bounties as primary income | Payout variance too high. First-reporter-wins economics |
| YouTube/streaming | Requires video production. Different skillset |
| Agency model | Requires hiring, managing people, client calls |
| Open source as primary income | GitHub Sponsors median ~$0 |

---

## Patterns That Kill Ideas (learned from 10 iterations)

Use these as pre-filters for future research:

1. **AI wrapper = dead on arrival.** If the core value is "GPT + nice UI for [task]," ChatGPT ($20/mo) kills it. The output must involve workflow, data, or process — not just text generation.
2. **Freelancer/creator tools churn catastrophically.** Budget AI tools see 77% annual churn (ChartMogul). Don't build tools for buyers who resist paying.
3. **Platform absorption is faster than you think.** Teachable, Thinkific, Kajabi, Cursor, GitHub Copilot — all adding AI features quarterly. If your value prop can be a checkbox feature, it will be.
4. **"No competitors" often means no market.** Empty niches stay empty because the market rejected the category (see: Nudge Coach shutting down, scope-creep tools with zero reviews).
5. **Check the name before falling in love.** ScopeShield and AIComply were both already taken.
6. **Free tools set the floor.** If Zoho/Google/Freshdesk/TurboTenant offer a free tier, your $19/mo needs 10x more value, not 2x.
7. **Intermittent pain = high churn.** If the problem is episodic (scope creep, email deliverability issues), users subscribe when hurting and cancel when resolved.
8. **B2B with budget > solopreneurs who resist paying.** Target buyers with company credit cards, not individuals counting every $19.
9. **Every category-level gap is filled (as of April 2026).** After 11 iterations and 150+ ideas, every B2B software category has 5-30+ tools. The remaining opportunities are hyper-vertical workflow tools, timing-window exploits, or early-stage categories where 1-2 weak competitors haven't achieved PMF.
10. **Hyper-vertical > horizontal.** Solo founders reaching $5K+ MRR (CottageKeeper, GmailSnippets, EZ Fulfill) solve one specific workflow pain for one specific buyer in one specific industry. Category-level micro-SaaS is essentially impossible to enter fresh in 2026.
11. **"Pricing gap" is a trap.** When expensive tools ($300+/mo) serve mid-market, the $15-49/mo tier below attracts dozens of micro-SaaS competitors, not zero. The gap fills faster than you can build (see: 276+ review management tools, 10+ at $15-29/mo).
12. **"Orphaned customer" windows close instantly.** When a product shuts down, it funnels users to a successor (LoadPilot → AscendTMS). By the time you build, the window is closed.
13. **Monopoly anger ≠ solo founder opportunity.** Angry customer bases attract funded competitors ($63M Cubby vs Storable), not micro-SaaS. Monopoly disruption requires capital.
14. **New categories fill in 6-12 months, not 2-3 years.** AI-enabled development compresses the competition cycle. Vibe code security went from zero to 8+ tools + $88M VC in under a year. By the time you identify an emerging category, it's already crowded.
15. **Distribution > problem novelty.** 70% of micro-SaaS never breaks $500/mo. Solo founders hitting $50K+ MRR win on distribution channels (Chrome Web Store, Shopify, SEO), not on finding unserved problems.
16. **Platform-dependent distribution = borrowed audience.** If the platform controls your distribution AND your feature set AND your API access, you're building a feature they'll absorb or block. Extensions survive only when the platform is a "dumb pipe" (GMass uses Gmail for sending, not product features).

---

### Iteration 14 Kills (developer workflow niches)
- Dead Code Detection SaaS — episodic use (churn), Knip 4.9M downloads/week (free), CodeScene exists at price point
- Tech Debt Tracking — SonarQube/CodeScene saturated, 7% adoption = category rejection
- Release Notes Automation — already killed (changelog generators, 12+ tools)
- On-Call Management — PagerDuty dominates, saturated
- Database Migration — saturated, high-touch sales needed
- Staging Environment — bundled into platforms (Vercel, Northflank)
- Freight Broker Micro-TMS — offline buyers, high-touch sales required, killed from /implement

### Iteration 15 Kills (non-dev B2B + compliance)
- Cookie consent tools — free tiers everywhere (CookieYes, Termly, Enzuzo), race to bottom
- Vendor risk assessment (SMB) — all enterprise-priced ($10K+/yr), thin SMB TAM
- Data retention policy automation — feature not product, inside larger compliance platforms
- DORA/NIS2 compliance (SME) — EU-centric, requires regulatory expertise, local-language tools
- International tax compliance SaaS — Paddle, Stripe Tax, Avalara dominate, liability risk
- SaaS compliance pre-flight/readiness — episodic (pre-audit only), Vanta/Sprinto upsell path
- Software license compliance tracking (SMB) — overlaps expense tracking, thin standalone value

### Iteration 16 Kills (revenue-reverse adjacent gaps)
- PDF generation API (Bannerbear adjacent) — PDFShift, PDFMonkey, DocSpring exist
- Vertical privacy analytics — Plausible, Fathom, Simple Analytics saturate the space
- Screenshot-to-docs automation — AI wrapper risk, too niche
- OTA updates for React Native — Expo dominates ecosystem
- AI business generators (FounderPal adjacent) — AI wrapper kill filter, ChatGPT substitute

## Stats (16 iterations)

- **Total ideas considered**: 190+
- **Total verticals scanned**: 58+
- **Distribution channels scanned**: 4 (Chrome Web Store, VS Code, Slack, Teams)
- **Ideas deep-dived**: 43+
- **Ideas surviving above bar**: DriftWatch at 22/30 (new scoring), API Rate Limit Aggregator at 24/30 (recommended as DriftWatch feature)
- **Best surviving idea**: DriftWatch (API dependency change monitoring) — BEING BUILT, 6/10 MVP

---

*This file is the canonical kill list. Check it before exploring any new idea.*
