# SaaS Spend Tracker — Implementation Plan

## Context

Small teams (1-20 people) have no affordable tool to track SaaS spending. Enterprise tools start at $300/mo (Cledara). Current solution: spreadsheets or nothing. This product fills the $19-49/mo whitespace with an AI-powered web dashboard.

Born from real pain: manually tallying $25K+/mo across 23+ services from Slack messages at Webacy.

---

## Data Ingestion Strategy (Layered with Fallbacks)

The core technical challenge. Three layers, each adding automation:

### Layer 1 — MVP: Manual + CSV Upload + Email Forwarding

**Manual Entry** (always available, zero cost):
- Form: vendor name (autocomplete from 200+ pre-seeded vendors), amount, currency, billing cycle, category
- Fallback for everything — if AI parsing fails, user enters manually

**CSV/Invoice Upload** (~$0.005/invoice via Claude):
- Accept PDF, CSV bank statements, PNG/JPG receipt screenshots
- Upload → Supabase Storage (encrypted) → Claude API (tool_use for structured output) → user confirms → save
- Batch CSV support: send all transaction descriptions in one Claude call, classify which are SaaS

**Email Forwarding** (~$5-10/mo via Mailgun):
- Each workspace gets: `{workspace-slug}@receipts.spendtrack.dev`
- User sets Gmail/Outlook filter to forward billing emails there
- Mailgun inbound webhook → Claude parses body + attachments → review queue
- **No Gmail OAuth needed** — user controls forwarding rules, we never access their inbox

### Layer 2 — V2 (after $2K+ MRR): Plaid Bank Connection
- Auto-import transactions, AI classifies recurring SaaS charges
- $1.50/user/mo — only viable once revenue covers cost

### Layer 3 — V3: Direct API Integrations (AWS, Stripe, GitHub billing)
- Only for the top 5-10 most common services
- Deferred — maintenance burden too high for solo dev at MVP

### Fallback Chain
Every AI parse → confidence check → if low confidence, user reviews manually → nothing saves without confirmation. Bad data never enters the dashboard.

### Approaches Avoided
- Gmail OAuth: restricted scope, Google security audit takes weeks, privacy nightmare
- Browser extension: fragile, breaks on every UI change
- Stripe Connect: only shows outgoing charges, not purchases
- Direct SaaS API integrations at scale: maintenance nightmare

---

## Architecture

```
Browser (Next.js App Router)
    │
    v
Next.js API Routes
    │
    ├── Supabase (PostgreSQL + Auth + Storage)
    │     - RLS on all tables
    │     - Encrypted storage for uploads
    │     - Edge Functions for webhooks
    │
    ├── Claude API (receipt/invoice parsing via tool_use)
    │
    ├── Mailgun (inbound email receiving)
    │
    └── Stripe (billing)
```

**Stack**: Next.js (App Router), TypeScript, Tailwind, shadcn/ui, Supabase, Prisma, Claude API, Mailgun, Stripe, Recharts

**Why Next.js + Supabase (not NestJS like Plata)**: API routes eliminate separate backend. Supabase eliminates DevOps. One deploy target (Vercel). Fewer moving parts for solo dev.

---

## Security

- **Supabase**: SOC 2 Type II, AES-256 at rest, TLS 1.3 in transit
- **Row-Level Security**: every table — users only see their workspace's data, enforced at DB level
- **Sensitive field encryption**: email bodies encrypted with AES-256-GCM before DB insert (per-workspace key)
- **File uploads**: private Supabase Storage buckets, signed URLs only
- **Audit logging**: DB triggers log who did what, when, to which record
- **Email retention**: raw email bodies auto-deleted after 7 days, only extracted fields kept
- **No PCI scope**: never touch card numbers. Plaid (V2) handles bank credentials. Stripe handles payments.
- **GDPR**: workspace deletion cascades all data. Export endpoint returns all user data as JSON.

---

## Pricing

| Feature | Free | Pro ($19/mo) | Team ($49/mo) |
|---------|------|-------------|---------------|
| Manual entry | Yes | Yes | Yes |
| Subscription limit | 15 | Unlimited | Unlimited |
| Dashboard & charts | Basic | Full | Full |
| CSV/invoice upload | 3/month | Unlimited | Unlimited |
| AI parsing | 3/month | Unlimited | Unlimited |
| Email forwarding inbox | No | Yes | Yes |
| Renewal reminders | No | Yes | Yes |
| Export CSV | No | Yes | Yes |
| Team members | 1 | 1 | Up to 20 |
| Shared dashboard | No | No | Yes |
| Audit log | No | No | Yes |

---

## MVP Dashboard Features

**Summary cards**: Total monthly spend, MoM change, active subscription count, next renewal

**Subscription table**: Sortable/filterable list with vendor logo, amount, cycle, category, renewal date, status. Quick edit/cancel/delete.

**Charts**: Spending by category (donut), monthly spend timeline (bar chart, 12 months)

**Renewal calendar**: Upcoming renewals in next 30 days

**Ingestion queue**: Pending AI-parsed items awaiting confirmation. Upload button. Forwarding email address with setup instructions.

---

## Database Schema (Key Tables)

- `workspaces` — multi-tenant unit, billing plan, Stripe IDs, unique forwarding email
- `workspace_members` — user ↔ workspace with roles (owner/admin/member)
- `subscriptions` — core entity: vendor, amount (cents), currency, cycle, category, plan, seats, status, source, confidence score
- `subscription_events` — price/plan change history
- `invoices` — individual charges linked to subscriptions
- `uploads` — file metadata, processing status, parsed data (JSONB)
- `inbound_emails` — encrypted body, processing status, parsed data
- `vendors` — pre-seeded directory (200+ SaaS tools with logos, categories, aliases)
- `usage_counters` — per-workspace feature usage for tier gating
- `audit_logs` — who did what, when

All money stored as integer cents. UUID primary keys. RLS on every table.

---

## Project Structure

```
saas-costs-tracker/
├── src/app/
│   ├── (auth)/                 # login, signup
│   ├── (dashboard)/            # authenticated routes
│   │   ├── page.tsx            # main dashboard
│   │   ├── subscriptions/      # CRUD
│   │   ├── upload/             # file upload + AI parsing
│   │   ├── inbox/              # email review queue
│   │   ├── settings/
│   │   └── billing/
│   └── api/webhooks/           # Stripe, Mailgun
├── src/lib/
│   ├── supabase/               # client helpers
│   ├── claude/                 # AI parsing pipeline
│   ├── stripe/                 # billing
│   ├── mailgun/                # email processing
│   ├── encryption/             # AES-256-GCM
│   └── vendors/                # matching & autocomplete
├── supabase/
│   ├── migrations/
│   ├── functions/              # Edge Functions
│   └── seed.sql                # vendor directory
└── package.json
```

---

## Timeline (4 Weeks to MVP)

**Week 1 — Foundation**: Next.js + Supabase + Auth + DB schema + RLS + Stripe billing + vendor seed data. Deliverable: user can sign up, see empty dashboard, upgrade to paid.

**Week 2 — Manual Entry + Dashboard**: Subscription CRUD with vendor autocomplete. Dashboard: summary cards, subscription table, category chart, spend timeline, renewal calendar. Deliverable: fully functional manual tracker.

**Week 3 — AI Pipeline + Upload**: File upload (PDF/CSV/image) → Claude parsing → confidence scoring → review queue → confirm → save. Deliverable: user uploads bank statement, AI extracts subscriptions.

**Week 4 — Email Forwarding + Polish**: Mailgun inbound setup, email parsing pipeline, review queue for email items, usage counters + tier gating, onboarding flow, error handling, responsive design. Deliverable: complete MVP, ship to production.

**Week 5-6 — Launch**: Landing page, Product Hunt, build-in-public, bug fixes, renewal reminders.

---

## Infrastructure Cost (MVP)

| Component | Service | Cost |
|-----------|---------|------|
| Frontend + API | Vercel Pro | $20/mo |
| Database + Auth + Storage | Supabase Pro | $25/mo |
| Email receiving | Mailgun | Free tier (MVP scale) |
| AI parsing | Claude API | ~$5-10/mo |
| Domain | spendtrack.dev | $12/yr |
| **Total** | | **~$50-60/mo** |

---

## Risks & Mitigations

| Risk | Mitigation |
|------|-----------|
| Claude parsing accuracy too low | Tool_use forces structured output. User always confirms. Confidence scoring flags uncertain results. |
| No one pays $19/mo | Free tier validates demand. If engaged but don't convert, test $9/mo. If no engagement, kill by week 6. |
| Supabase RLS misconfiguration | Write RLS tests. Every table gets policy before any data inserted. Security audit before launch. |
| GDPR/privacy complaints | Encrypt email bodies. Auto-delete after 7 days. Clear privacy policy. |
| Scope creep | 4-week timeline is the forcing function. No Plaid, no integrations, no mobile until validated. |

---

## Verification

1. **Auth**: Sign up with magic link and Google OAuth → lands on empty dashboard
2. **Manual entry**: Add a subscription → appears in table and charts update
3. **Upload**: Upload a real bank statement CSV → Claude extracts SaaS charges → review and confirm → subscriptions created
4. **Email**: Forward a real billing email to workspace address → appears in inbox queue → confirm → subscription created
5. **Billing**: Upgrade to Pro → limits removed → downgrade → limits enforced
6. **Security**: Try accessing another workspace's data via API → RLS blocks it
7. **Team**: Invite a member → they see shared subscriptions (Team tier)

---

## Critical Files

- `/Users/jobeloquintero/Repos/solo/saas-costs-tracker/` — project directory
- `/Users/jobeloquintero/Repos/solo/costs-tracker/apps/api/prisma/schema.prisma` — reference for DB patterns (integer money, UUIDs, usage counters)
- `/Users/jobeloquintero/Repos/solo/research/reports/2026-04-04-saas-spend-tracker.md` — opportunity research
