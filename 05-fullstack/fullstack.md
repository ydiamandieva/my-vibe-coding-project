# Full-Stack: Data, Access Rules, Edge Cases, Deploy

> Module 5 · Full-Stack. Add data schemas, access rules, and edge cases; stress-test and deploy.

## Deployed link

_The working, shareable link that survives real users._

_____

## Data schema

| Entity | Key fields | Notes |
|---|---|---|
| accounts | id (text, e.g. "northstar"), name, risk (Critical/High/Medium), score, arr, renewal, days, owner, stage, reason, trend, active_seats, last_active, action / action_detail (latest action summary), quote_text / quote_by, telemetry_status / telemetry_since / telemetry_unavailable, account_owner_id (nullable link to a user — demo accounts have none), sort_order. | Shared reference data; seeded with the 5 demo accounts; updated_at auto-maintained by trigger. |
| account_health_drivers | accounts, label, score, impact, note, sort_order, plus evidence fields (evidence_source, evidence_current, evidence_previous, evidence_period, evidence_updated, evidence_activity). | 4 per account (20 rows); a missing evidence row is what renders "evidence not available". |

## Access rules

_Who can see / do what? Where are the auth boundaries?_

Auth boundary: everything sits behind login (email/password with email confirmation, or Google). The /workspace route redirects signed-out visitors to /auth, and every server function rejects calls without a valid session. There is no anonymous access to any table.

Shared team data — read-only for everyone signed in:

- accounts, account_health_drivers, account_recommendations, headline_metrics: any signed-in user can read; nobody can insert, update or delete through the app (only privileged backend access can).

Private per-user data — you only see and change your own:

- retention_actions, investigations, hypothesis_events, recommendation_dismissals, profiles: read, create and update are restricted to rows where user_id matches your authenticated session. The user_id is always stamped from the verified session on the server — the browser can't supply or override it, so nobody can create or edit records in someone else's name.
- invites: you can read, create and update only invites you sent (sender_id = you); the dashboard invite numbers count only your own.

Enforcement: all of the above is enforced by row-level security in the database itself, not just in the UI — so even a hand-crafted request can't cross these boundaries.

## Edge cases hardened

| Case | Before | After |
|---|---|---|
| Empty / first-run state | Empty workspace -  The account list rendered blank with no explanation; a new user couldn't tell if it was loading, broken, or just empty. | Adedicated empty state explains there are no accounts yet and offers a Get started button; a separate "No accounts match these filters" state with Clear filters covers the filter-hides-everything case, so the two kinds of "empty" are never confused. |
| Bad / malicious input | Forged ownership - user_id came from the browser, so anyone could send a hand-crafted request writing records in someone else's name. | The server ignores any supplied user_id and stamps it from the verified login session — forging it is impossible even with a modified request. |
| Failure / offline | Load failure - If the workspace data failed to load, the screen sat on a broken or blank state with no way forward. | An inline error message explains what went wrong and a Retry button reloads the data without losing your place. |

## Stress test results

_What you threw at it, and what held / broke._

_____
