# The Retention Engine - Know where to act before renewal risk becomes churn.

_Product School · Vibe Coding Certification · Final Project Showcase_

**Live product:** https://rls-radiance-forge.lovable.app/

## The Problem & Hypothesis

**Problem.** Customer Success Managers and Account Managers can identify accounts showing signs of risk, but existing dashboards largely stop at passive monitoring rather than enabling intervention.
The result is a gap between knowing an account is at risk and acting on that risk: renewals approach without timely intervention, $1.1M ARR is exposed in the next renewal window, 30% of new accounts churn within 90 days, only 22% activate in their first week, and adoption rarely expands beyond the initial buyer, averaging just 1.4 active seats per account.

**Hypothesis.** We believe that transforming the dashboard from a passive risk summary into an actionable retention workflow - with risk filters, account drill-down, explainable health scores, contextual account insights, and recommended next steps - for Customer Success Managers and Account Managers accountable for customer health, renewals, and retention - will enable them to identify priority accounts faster, understand the drivers of risk, and take appropriate retention action earlier. We’ll know we’re right when users consistently progress from risk signal → account investigation → recommended action, with a measurable increase in timely action taken on high-risk accounts.

## The Evidence

9 visitors, 33% bounce, 3.44 views/visit, 1m 57s avg. session. 

Core flow: 8 investigations → 4 actions initiated → 3 completed (50% → 75% conversion). 

Peers: ⚠️ “No way to send an invite” + ‘Actions’ is a dead click.” 

Stall: Risk workspace - core retention action converts, but invite and action-review journeys are blocked.

## Data Signal → The One Fix

Signal: 0 invites sent with no way to send one is a dead end. 

Fix (Build the send-invite flow): A simple "Invite a teammate" dialog (name + email → row in the invites table) would make the metric real and give you a second loop to test.

## The Recommendation

**Verdict: ITERATE, keep refining.**

The evidence that justifies the call:  The core loop provably works - investigated→initiated 50%, initiated→completed 75%, with outcomes recorded. But the kill-switch condition (users understand risk yet don't act) was not triggered; what failed is the periphery: invites are visible but not actionable, and the Actions menu is a dead end. Both are fixable in one sprint, not reasons to kill.

## My Story, Friction · Learning · Aha

I turned a passive retention dashboard into an actionable workflow people actually use - the core loop (spot the risk, investigate, act, record the outcome) proved itself with real users, and every iteration since has been about closing the loops I left open.

What broke:

- M2 (prototype): Everything was hardcoded demo data - 5 fake accounts, a fake "Maya Chen" persona in the sidebar, and metrics that were just numbers on a screen. It looked finished but wasn't real.

- M3 (integration): The moment real users arrived, the cracks showed. The sidebar "Actions" menu showed a hardcoded "3" and clicking it did nothing - 2 of 6 initiated actions got stranded mid-loop with no way back to them.

- Data vs. story: The dashboard showed invite metrics (0 sent) with no way to actually send an invite - my peer reasonably assumed starting retention actions would move "invites sent." I'd built a relationship that didn't exist.

What I learned:

My biggest learning was that vibe coding is not about generating more software faster; it is about progressively constraining AI around a product hypothesis. I moved from prompting for screens to specifying workflows, behaviour, evidence, failure states and measurable outcomes. The product improved most when each iteration was driven by observed user friction rather than by adding functionality.

---
_Built across six modules with an AI build tool, then iterated from live product data. Hosted on GitHub Pages._
