# Engineering Handoff Note

> Module 4 · Production Specs. Open the black box, make the build legible to an engineer.

## What this is

_One paragraph an engineer can read in 60 seconds._

60-second summary

The Retention Engine is a clickable prototype that tests whether turning a passive risk dashboard into an actionable retention workflow helps CSMs and AMs identify at-risk accounts faster, understand the drivers, and take earlier action. It is built as a TanStack Start single-page app with a Risk Workspace (filterable priority accounts), an Account Detail drawer (explainable health score + evidence), a recommended-action creation flow, an action outcome screen, and a Hypothesis Monitor that exposes the end-to-end conversion funnel. All data is seeded and session-only: nothing persists to a backend, so the prototype is safe to reset, but it cannot survive a page refresh. The current goal is behavioural validation, not production reliability.

## Architecture (plain language)

- **Frontend:** Framework: TanStack Start v1 on Vite, React 19, TypeScript, Tailwind CSS v4. Routing: Route files live under src/routes/. The root route (/) mounts RiskWorkspaceScreen from the feature module. Feature structure: Code is grouped by screen under src/features/retention-engine/: screens/ — five PRD-named screens: Risk Workspace, Account Detail, Recommended Action & Action Creation, Action Detail & Outcome, Hypothesis Monitor. components/ — shared presentation pieces (badges, drawer, timeline, shimmer, etc.). data/ — seeded accounts, metrics, and outcome options. hooks/ — useExperimentSession: sessionStorage-backed experiment state and action mutations. lib/ — evidence derivation (getDriverEvidence). types.ts — shared domain types. State: All user-visible state (selected account, current view, filter/search values, dismissed recommendations, action status/outcome, hypothesis events) is stored in sessionStorage under the key retention-experiment. State mutations live in useExperimentSession. UI primitives: Built on shadcn/ui components (Button, Input, Badge, Dialog, etc.) plus custom drawer and list helpers.
- **Backend / data:** No real backend. All data is static seed data in src/features/retention-engine/data/seed-data.ts. No database or auth. The prototype does not use Lovable Cloud, Supabase, or any external API. Simulated failure: The Arcadia Systems account is hard-coded to surface a stale-telemetry error so the unreliable-data state can be demonstrated. Data model (seeded): Account: id, name, arr, renewalDate, healthScore, risk, seats, activeSeats, engagementTrend, activity, owner. HeadlineMetric: label, value, change, context. Driver / Evidence: derived at render time from account fields. ActionRecord: created when the user initiates an action; status and outcome are updated in session state. ExperimentEvent: tracks funnel transitions (risk identified, account investigated, action initiated, action completed).
- **Key flows:** Risk identification → investigation

User lands on Risk Workspace.
Filter/search the Priority Accounts list; select an account to open Account Detail in a drawer.
investigate() is recorded in session state.
Recommendation → action creation

In Account Detail, the user can open Recommended Action & Action Creation.
Editable fields: owner, due date, action description.
Primary CTA "Create action" records the action and fires createAction() in session state.
Dismiss recommendation fires dismissRecommendation().
Action detail → outcome

"View action" opens Action Detail & Outcome.
User advances status: Not started → In progress → Completed.
On completion, an outcome is selected (Customer contacted / Meeting scheduled / Risk reduced / No response / Other).
completeAction() records the funnel completion.
Hypothesis Monitor

Accessible from the Risk Workspace.
Shows the full funnel with counts, conversion/drop-off, kill-switch status, decision rule, and supporting behavioural evidence.

## What's solid vs. what's duct tape

| Area | State | Notes |
|---|---|---|
| Component structure and naming | solid | Screens match the PRD exactly; data, UI, and state are separated by feature. |
| Hypothesis funnel | solid | The full risk → evidence → decision → intervention → outcome → learning flow is wired and observable. |

## Risks & assumptions for the team

1. Kill switch is manual. The decision to kill or progress the proposition relies on observing qualitative prototype usage, not automated instrumentation.
2. Session state loss. A accidental refresh during a user test wipes the funnel progress.
3. No concurrency model. Multiple users sharing the same preview would not see each other's actions; this is fine for single-tester prototypes but not for team validation.
4. Arcadia error is synthetic. The unreliable-data state looks real but does not represent an actual backend failure path.

## How to run it

```
- The target user (CSM / AM) recognises the metrics (ARR, renewal window, seat utilisation, engagement trend) as meaningful signals.
- A recommended action expressed as "Re-engage the account champion before renewal" is specific enough to trigger action.
- The kill-switch threshold (identify → investigate → initiate → complete) is the right behavioural proxy for value.
- The current visual language from the Northstar Labs reference is acceptable for validation; no further design exploration is needed.
```
