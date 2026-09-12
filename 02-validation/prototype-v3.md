# Prototype (v3): The Build That Tests the Hypothesis

> Module 2 · Validation. The prototype is a hypothesis test, not a demo.

## Link

https://lovable.dev/projects/7e8516c3-97ee-42b5-bcfe-77f184522e0c?magic_link=mc_aa61c05e-fcae-42f4-8ecd-76bd3e318a1c

## What it tests

_Tie it back to the validation brief: which assumption does this prototype put in front of a user?_

If Customer Success and Account teams can move from 'this account is at risk' → 'here’s why' → 'here’s what I should do next', they will find the product meaningfully more actionable than a passive churn-risk dashboard.

## Context injected (no placeholders)

- **Real user quotes on screen:** Prioritise: 'Which accounts should I actually focus on?'
Understand: 'Why is this customer considered at risk?'
Act: 'Okay, but what am I supposed to do with this?'
- **Domain metrics on screen:** The prototype now surfaces metrics that are directly relevant to the retention decision rather than generic SaaS dashboard statistics:
Account health score · churn-risk level · primary churn driver · recent customer activity · risk distribution/counts · recommended next action.
The key improvement is that these metrics are connected at account level: the user can see the portfolio-level signal and then drill into the evidence behind an individual account's score.

## Iteration log (v1 → v3)

| Version | Change | Why |
|---|---|---|
| v1 | Built the core retention dashboard and surfaced accounts/health or churn-risk signals. | Test whether consolidating customer-risk information gives users a useful view of where retention attention may be required. |
| v2 | Strengthened the presentation and usability of the risk information, making the dashboard easier to interpret and prioritise. | The first version demonstrated the concept, but remained primarily informational: users could see risk without having enough context to understand or act on it. |
| v3 | Added risk-level filters with counts, shareable filtered views, clickable accounts, account detail panel, health-score breakdown, churn drivers, recent activity and recommended next steps. | Addressed the biggest credibility gap: the dashboard previously stopped at “this account is at risk.” V3 tests whether users need to move seamlessly from signal → explanation → action for Velocity to become part of a real retention workflow. |
