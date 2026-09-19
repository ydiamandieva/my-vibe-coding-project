# Living PRD

> Module 4 · Production Specs. Refactor for readability; extract a living PRD that stays true as the build evolves.

## Problem

Customer Success Managers and Account Managers can see that accounts are at risk, but risk dashboards stop at passive monitoring. The result: renewals arrive with no intervention taken, $1.1M ARR is at risk in the next renewal window, 30% of new accounts churn within 90 days, only 22% activate in week one, and adoption rarely spreads past the buyer (1.4 active seats per account).

Hypothesis under test (validated by this prototype): turning the dashboard from a passive risk summary into an actionable workflow — risk filters, account drill-down, explainable health scores, contextual account information, and recommended next steps — causes users to identify priority accounts faster, understand what is driving the risk, and take retention action earlier.

Success signal: users move from risk signal → account investigation → recommended action, with a measurable increase in action taken on high-risk accounts.

Kill switch (verbatim, shown in the product): "If users can identify and understand high-risk accounts but still do not take or initiate an action, the proposition is not solving a sufficiently valuable workflow problem and should not progress in its current form."

Mocked vs real: the hypothesis is tested against seeded data within a single browser session. No real customer behaviour has been measured yet.

## Users & jobs

**Primary user:** Customer Success Managers and Account Managers accountable for customer health, renewals, and retention.

**Job to be done:** When renewal risk is building in my book of accounts, I want to quickly see which accounts need attention, understand exactly why, and initiate the right intervention — so I can act weeks before renewal instead of reacting after churn.  Supporting user voices (shown on screen in the prototype as evidence attached to risk drivers):  "I signed up, poked around for ten minutes, and never figured out what it actually did for my team." — Ops lead, churned day 12 "We renewed once but couldn't point to a single number that changed because of it." — VP Product, did not renew "The value was probably in there somewhere, but I needed it to prove itself in week one, not month three." — Founder, churned day 63

## Scope

**In:** 
- Prioritisation dashboard: metrics strip ($1.1M ARR at risk, 30% 90-day churn, 22% activation, 1.4 active seats/account), risk filters (severity, renewal window, ownership, search), and a sortable Priority Accounts queue.
- Account detail (drawer): explainable health score with weighted drivers, per-driver impact in points, evidence drill-down (source metric, current value, previous period, period, last updated, account activity), commercial context, timeline, and customer quotes tied to drivers.
- Recommended Action & Action Creation: recommended intervention with rationale, editable owner / due date / description, Create action and Dismiss recommendation, confirmation with View action.
- Action Detail & Outcome: status progression Not started → In progress → Completed, "What happened?" outcome capture (Customer contacted / Meeting scheduled / Risk reduced / No response / Other), supporting risk evidence.
- Hypothesis Monitor: full funnel Risk identified → Account investigated → Action initiated → Action completed, conversion and drop-off, kill-switch status, decision rule verbatim, and session behavioural evidence (investigated, actioned, dismissed accounts and time-ordered events).
- State handling: skeleton loading ("Updating account risk signals… Analysing product usage, renewal and account activity."), filter-empty state with Clear filters, no-critical-accounts state, and unavailable-telemetry error state ("Health score temporarily unavailable. - Product activity hasn't synced since 18 Sep, 14:20.") with Retry and View available evidence.

**Out (explicitly):** 
- Authentication, user accounts, roles, multi-user collaboration.
- Persistence beyond the browser session; real backend, database, or API integrations.
- Real product-usage telemetry, CRM, or billing sync.
- Notifications, reminders, email/calendar scheduling of actions.
- Historical reporting, team analytics, or admin configuration.

## Requirements

| # | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| 1 | Surface the four headline risk metrics on the dashboard | Must | $1.1M ARR at risk, 30% 90-day churn, 22% activation rate, 1.4 active seats/account visible without scrolling on desktop |
| 2 | Filterable, sortable Priority Accounts queue | Must | Filters for risk level, renewal window, owner, and free-text search; high-risk high-value accounts visually obvious without relying on colour alone |
| 3 | Account detail with explainable health score | Must | Health score broken into weighted drivers; each driver shows its point impact and expands to evidence (source metric, current value, previous value/trend, period, last updated, related activity) |
| 4 | Contextual account information | Should | Commercial details, lifecycle timeline, stakeholders, product activity and recent signals alongside the score |
| 5 | Customer voice as evidence | Should | The three churn quotes rendered with exact attribution, connected to relevant risk drivers |
| 6 | Recommended action per account	| Must |	Ranked recommendation with rationale tied to the account's risk drivers (e.g. Northstar Labs: "Re-engage the account champion before renewal" with the 31% / 1-of-18-seats / 14-days rationale) |
| 7	| Action creation	| Must |	Owner, due date and description editable; Create action assigns and confirms ("Action created — …assigned to Maya Chen") with a View action path; Dismiss returns without changing funnel counts |
| 8	| Action tracking and outcome capture	| Must |	Status Not started → In progress → Completed; on completion, outcome prompt with the five defined options; outcome recorded per account |
| 9	| Observable experiment funnel	| Must |	Monitor always accessible; shows identified → investigated → initiated → completed counts, step conversion and drop-off, kill-switch status, the decision rule verbatim, and behavioural evidence (investigated / actioned / dismissed / events) |
| 10 | Loading state without losing context	| Must	| Skeleton rows for the account list during recalculation; existing dashboard information retained; copy "Updating account risk signals… Analysing product usage, renewal and account activity."; no full-page spinner |
| 11 | Empty states	| Must |	Zero filter results: "No accounts match these filters. Try changing the risk level, renewal window or search criteria." + Clear filters CTA restoring the full list. No critical/high accounts: "No critical accounts need attention right now. We'll surface accounts here when their risk signals cross the attention threshold." |
| 12 | Unreliable-data state	| Must | On fetch failure or stale telemetry: "Health score temporarily unavailable. Product activity hasn't synced since 18 Sep, 14:20." Never present a stale score as current fact. Retry triggers loading then restores score or re-shows the error; View available evidence keeps reliable evidence visible and labels unavailable signals |
| 13 | Session continuity	| Should	| Filters, investigated accounts, actions, outcomes and funnel events survive page reload within the browser session |

## Data & events
**Mocked vs real: all data below is seeded prototype data. There is no backend, no auth, and no live telemetry. State lives in sessionStorage only and resets with a new session. The "18 Sep, 14:20" sync timestamp on the Arcadia Systems error state is scripted, not observed.**

Data entities:

**Accounts (5 seeded)**: Northstar Labs (Critical, 21, $184k, renewal 14 days), Relay Collective (Critical, 27, $146k), Canopy Health (High, 39, $128k), Arcadia Systems (High, 46, $96k, stale telemetry), Meridian Works (Medium, 58, $72k). Each carries owner, stage, risk reason, engagement trend, active seats, last activity, four weighted health drivers with per-driver evidence, an optional customer quote, and a recommendation (title, why, owner, due, description).
**Metrics (4 seeded)**: ARR at risk, 90-day churn, activation rate, active seats/account.
**Telemetry status**: per account; Arcadia Systems is seeded as stale with "Engagement trend" and "Adoption breadth" marked unavailable.

Events logged to the session store (power the Hypothesis Monitor):

| Event | Fired when | 
|---|---|
| Account investigated | Account drawer opened | 
| Action initiated	| Create action confirmed |
| Recommendation dismissed	| Dismiss recommendation |
| Action status changed	| Not started → In progress → Completed | 
| Action completed / outcome captured	| Outcome option selected |

Funnel counts: identified (accounts in queue) → investigated → action initiated → action completed, with conversion and drop-off derived from the event log.

## Open questions

1. Real data sources. Which systems supply usage telemetry, renewal dates and ARR (product analytics, CRM, billing)? What sync latency is acceptable before a score must be marked unavailable?
2. Score model. Are the four drivers and weights correct for production, and who owns tuning them?
3. Owner assignment. Is the action owner always the account owner, or routed by play/segment?
4. After outcome capture. Does a completed action update the health score, create follow-ups, or feed a playbook library?
5. Kill-switch thresholds. What conversion rate from investigated → initiated validates the hypothesis, and over how many real users and weeks?
6. Scale. Behaviour with hundreds of accounts: grouping, pagination, team views, and cross-account prioritisation.
7. Persistence and audit. Retention of actions, outcomes and funnel data across sessions and users; visibility for managers.
