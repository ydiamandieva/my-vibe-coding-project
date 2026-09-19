# Living PRD

> Module 4 · Production Specs. Refactor for readability; extract a living PRD that stays true as the build evolves.

## Problem

_What user problem does this solve? Tie to the validated hypothesis._

Customer Success Managers and Account Managers can see that accounts are at risk, but risk dashboards stop at passive monitoring. The result: renewals arrive with no intervention taken, $1.1M ARR is at risk in the next renewal window, 30% of new accounts churn within 90 days, only 22% activate in week one, and adoption rarely spreads past the buyer (1.4 active seats per account).

Hypothesis under test (validated by this prototype): turning the dashboard from a passive risk summary into an actionable workflow — risk filters, account drill-down, explainable health scores, contextual account information, and recommended next steps — causes users to identify priority accounts faster, understand what is driving the risk, and take retention action earlier.

Success signal: users move from risk signal → account investigation → recommended action, with a measurable increase in action taken on high-risk accounts.

Kill switch (verbatim, shown in the product): "If users can identify and understand high-risk accounts but still do not take or initiate an action, the proposition is not solving a sufficiently valuable workflow problem and should not progress in its current form."

Mocked vs real: the hypothesis is tested against seeded data within a single browser session. No real customer behaviour has been measured yet.

## Users & jobs

- **Primary user:** Customer Success Managers and Account Managers accountable for customer health, renewals, and retention.
- **Job to be done:** When renewal risk is building in my book of accounts, I want to quickly see which accounts need attention, understand exactly why, and initiate the right intervention — so I can act weeks before renewal instead of reacting after churn.  Supporting user voices (shown on screen in the prototype as evidence attached to risk drivers):  "I signed up, poked around for ten minutes, and never figured out what it actually did for my team." — Ops lead, churned day 12 "We renewed once but couldn't point to a single number that changed because of it." — VP Product, did not renew "The value was probably in there somewhere, but I needed it to prove itself in week one, not month three." — Founder, churned day 63

## Scope

- **In:** - Prioritisation dashboard: metrics strip ($1.1M ARR at risk, 30% 90-day churn, 22% activation, 1.4 active seats/account), risk filters (severity, renewal window, ownership, search), and a sortable Priority Accounts queue.
- Account detail (drawer): explainable health score with weighted drivers, per-driver impact in points, evidence drill-down (source metric, current value, previous period, period, last updated, account activity), commercial context, timeline, and customer quotes tied to drivers.
- Recommended Action & Action Creation: recommended intervention with rationale, editable owner / due date / description, Create action and Dismiss recommendation, confirmation with View action.
- Action Detail & Outcome: status progression Not started → In progress → Completed, "What happened?" outcome capture (Customer contacted / Meeting scheduled / Risk reduced / No response / Other), supporting risk evidence.
- Hypothesis Monitor: full funnel Risk identified → Account investigated → Action initiated → Action completed, conversion and drop-off, kill-switch status, decision rule verbatim, and session behavioural evidence (investigated, actioned, dismissed accounts and time-ordered events).
- State handling: skeleton loading ("Updating account risk signals… Analysing product usage, renewal and account activity."), filter-empty state with Clear filters, no-critical-accounts state, and unavailable-telemetry error state ("Health score temporarily unavailable. - Product activity hasn't synced since 18 Sep, 14:20.") with Retry and View available evidence.
- **Out (explicitly):** - Authentication, user accounts, roles, multi-user collaboration.
- Persistence beyond the browser session; real backend, database, or API integrations.
- Real product-usage telemetry, CRM, or billing sync.
- Notifications, reminders, email/calendar scheduling of actions.
- Historical reporting, team analytics, or admin configuration.

## Requirements

| # | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| 1 | Surface the four headline risk metrics on the dashboard | Must | $1.1M ARR at risk, 30% 90-day churn, 22% activation rate, 1.4 active seats/account visible without scrolling on desktop |
| 2 | Filterable, sortable Priority Accounts queue | Must | Filters for risk level, renewal window, owner, and free-text search; high-risk high-value accounts visually obvious without relying on colour alone |

## Data & events

_What gets stored, what gets tracked._

Mocked vs real: all data below is seeded prototype data. There is no backend, no auth, and no live telemetry. State lives in sessionStorage only and resets with a new session. The "18 Sep, 14:20" sync timestamp on the Arcadia Systems error state is scripted, not observed.

Data entities:

Accounts (5 seeded): Northstar Labs (Critical, 21, $184k, renewal 14 days), Relay Collective (Critical, 27, $146k), Canopy Health (High, 39, $128k), Arcadia Systems (High, 46, $96k, stale telemetry), Meridian Works (Medium, 58, $72k). Each carries owner, stage, risk reason, engagement trend, active seats, last activity, four weighted health drivers with per-driver evidence, an optional customer quote, and a recommendation (title, why, owner, due, description).
Metrics (4 seeded): ARR at risk, 90-day churn, activation rate, active seats/account.
Telemetry status: per account; Arcadia Systems is seeded as stale with "Engagement trend" and "Adoption breadth" marked unavailable.

## Open questions

1. Real data sources. Which systems supply usage telemetry, renewal dates and ARR (product analytics, CRM, billing)? What sync latency is acceptable before a score must be marked unavailable?
2. Score model. Are the four drivers and weights correct for production, and who owns tuning them?
3. Owner assignment. Is the action owner always the account owner, or routed by play/segment?
4. After outcome capture. Does a completed action update the health score, create follow-ups, or feed a playbook library?
5. Kill-switch thresholds. What conversion rate from investigated → initiated validates the hypothesis, and over how many real users and weeks?
6. Scale. Behaviour with hundreds of accounts: grouping, pagination, team views, and cross-account prioritisation.
7. Persistence and audit. Retention of actions, outcomes and funnel data across sessions and users; visibility for managers.
