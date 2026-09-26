# Iteration: Analytics, Sprint, Final Recommendation

> Module 6 · Evals & Iteration. Read the analytics, run an iteration sprint, present with evidence.

## What the evidence says

_What real usage showed: numbers if your tool has analytics, counted behaviour if it does not. Put the signal that matters on screen._

- **Primary signal:** Users who reach the Risk workspace take retention action — 8 investigations → 4 actions initiated → 3 completed (50% investigated→initiated, 75% initiated→completed).
- **What moved:** The core workflow converts. 5 signed-in users generated 17 hypothesis events; 3 of 4 initiated actions were completed with a recorded outcome. Session depth backs it: 3.44 pages/visit, 1m 57s average duration, 33% bounce — people who get in, stay and work.
- **What didn't:** Invites — 0 sent, and the peer confirmed why: the metric strip shows invite numbers but starting an action doesn't move them, and there's no way to send an invite from the app. Also the "Actions (3)" menu doesn't open — a dead click at exactly the moment a user wants to review their work.

_Analytics snapshot: visitors 9; page views 31; views per visit 3.44; duration 1m 57s; bounce 33%._

_Observed behaviour: reach 1 of 4; core action 1 of 4; stall point Risk workspace; explained away -; own first run 2, both on call for actions._

## Iteration sprint

| Change | Hypothesis | Result |
|---|---|---|
| Wired workspace to real backend with per-user data (M2) | Persisted, own-only records make the workflow feel real enough to act on | Confirmed — users investigated, created and completed actions that survive reload |
| Live invite metrics on the dashboard (M5) | Real numbers beat hardcoded ones for credibility | Partially failed — metrics read 0 with no way to send an invite; peer expected actions to move them | 
| Skeletons, retry, empty states, pagination | Resilient states keep first-run users from bouncing | Confirmed — 33% bounce, no error-stuck sessions |

## Peer feedback

Well, and deeply built workflows, I would need to spend here more time to digest all the details. Two things I could not figure out how can I impact the key metrics, I thought if I start actions, invites sent will change. Also could not get the details on Actions menu. It is showing there are 3. but clicking does not work.

## The recommendation

**Decision:** ☐ Go  x Iterate  ☐ Kill

_The evidence that justifies the call:_ The core loop provably works — investigated→initiated 50%, initiated→completed 75%, with outcomes recorded. But the kill-switch condition (users understand risk yet don't act) was not triggered; what failed is the periphery: invites are visible but not actionable, and the Actions menu is a dead end. Both are fixable in one sprint, not reasons to kill.

_____

## Final showcase

- **Demo link:** https://rls-radiance-forge.lovable.app/
- **The one-sentence story:** A customer-success manager opens the Risk workspace, sees which accounts are about to churn and why, and turns a recommendation into a completed retention action — with every step measured.
- **Where it landed on the Confidence Line (M2 → now):** From "plausible workflow, untested" (M2) to "core loop validated with real users; invite loop and Actions menu need one iteration" — roughly 7/10.
