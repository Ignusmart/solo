# Integration Health Monitor — Kill Analysis

**Date**: 2026-04-05  
**Verdict**: KILL — This is a feature, not a product.

---

## What exists today

**Zapier already has this (enterprise-only):**
- **Alerts page** (GA on Enterprise plans): centralized error triage across all Zaps, priority-based.
- **Log streams** (alpha, Enterprise): real-time webhook notifications on Zap completion — lets you build external dashboards and alerting. Currently alpha/invite-only.
- **Auto-shutdown**: Zaps auto-turn-off at 95% error rate over 7 days, with email notifications.
- **Customizable error notifications**: per-step, configurable frequency.

**Make.com has built-in error handling:**
- Try/catch directives per module (Ignore, Stop, Rollback, Commit).
- Email notifications on unhandled errors and scenario disablement.
- Execution history with detailed logs.

**Workato and Tray.io** both ship comprehensive monitoring dashboards, real-time analytics, error alerting, and audit logs as core platform features.

## The cross-platform angle

The only defensible wedge would be **cross-platform visibility** — "single pane of glass for Zapier + Make + webhooks + custom APIs." But:

1. **Zapier's Log Streams and Make's execution logs are not designed to export to third parties.** You'd be screen-scraping or relying on alpha APIs that can break or get locked down.
2. **Hookdeck** already owns the webhook reliability/observability layer (ingestion, retry, monitoring) and is well-funded.
3. **The target buyer (ops manager at SMB with 10-20 automations) almost certainly uses ONE platform**, not multiple. Cross-platform monitoring solves a problem that barely exists at SMB scale.
4. **Datadog, Prismatic, and other observability tools** already serve the enterprise segment that actually runs multi-platform integrations.

## The kill question

**This is a feature, not a product.** Zapier is actively building exactly this (Alerts page, Log Streams) and gating it behind Enterprise pricing — which means they see it as an upsell lever, not something they'll leave unaddressed. Make.com has error handling built in. The moment you build a standalone monitor, you're competing with a roadmap item that the platform itself is shipping.

The only sliver of opportunity — cross-platform monitoring for SMBs — fails because SMBs don't run cross-platform automation stacks, and enterprises already have Datadog/Prismatic. There is no buyer in the middle who (a) runs multiple iPaaS platforms, (b) lacks observability tooling, and (c) will pay for a standalone product.

**Do not build.**

---

## Sources

- [Zapier Alerts (GA)](https://help.zapier.com/hc/en-us/articles/29206590194445-Alerts-is-now-generally-available)
- [Zapier Log Streams](https://help.zapier.com/hc/en-us/articles/43732241361421-Set-up-log-streams-to-monitor-Zap-activity)
- [Zapier Error Notifications](https://help.zapier.com/hc/en-us/articles/8496289225229-Manage-notifications-when-errors-occur-in-Zaps)
- [Make.com Error Handling](https://help.make.com/introduction-to-errors-and-warnings)
- [Hookdeck — Webhook Reliability Platform](https://hookdeck.com)
- [Prismatic — B2B Integration Monitoring](https://prismatic.io/platform/monitoring-management-tools/)
- [Workato vs Tray.io Comparison](https://www.taloflow.ai/guides/comparisons/trayio-vs-workato-dii)
- [Webhook Monitoring Guide (WebhookWatch)](https://www.webhookwatch.com/article/webhook-monitoring-tools)
