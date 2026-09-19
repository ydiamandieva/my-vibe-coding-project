# PROMPTS.md: Living Prompt Pack

> Module 3 · Prompt Chaining. Re-architect the build with prompt chains; capture the reusable ones here.

## How to use this pack

_Each prompt is a reusable step. Chain them: the output of one becomes the input to the next._

## Prompt chain: [name your flow]

### Step 1: Complete the end-to-end retention workflow
```
Build the next phase of this app in a strict sequence:
1. Add a screen “Recommended Action & Action Creation”. Match the layout and spacing of the attached Northstar Labs Account Detail screenshot. Preserve the existing navigation, typography, cards, colour treatment, drawer pattern, risk badges and visual hierarchy. Show:
Recommended action: Re-engage the account champion before renewal
Why: Product engagement has fallen 31% in 30 days, only 1 of 18 seats is active, and renewal is in 14 days
Account: Northstar Labs
Owner: Maya Chen
Due date: Before renewal
Allow owner, due date and action description to be edited.
Primary CTA: Create action
Secondary CTA: Dismiss recommendation
After creation, show: “Action created — Re-engage account champion has been assigned to Maya Chen.”
CTA: View action
Creating the action updates the Hypothesis Monitor from Action initiated: 0 → 1.
2. Add a screen “Action Detail & Outcome”. Match the data density of the attached Northstar Labs Account Detail screenshot. Show:
Account
Owner
Due date
Risk being addressed
Recommended intervention
Status: Not started → In progress → Completed
When completed, ask “What happened?” with: Customer contacted / Meeting scheduled / Risk reduced / No response / Other.
Completing the action updates the Hypothesis Monitor from Action completed: 0 → 1.
Include access to the supporting risk evidence. Each health driver should expose source metric, current value, previous value/trend, time period, last updated and relevant account activity.
Example: Engagement trend — Current: 31% decline; Period: Last 30 days; Previous period: 8% decline; Last updated: Today, 09:42; Source: Product usage telemetry.
3. Navigation: write the logic so Recommended Action & Action Creation links to Action Detail & Outcome. The existing Northstar Labs account-detail view should lead into Screen A, Create action should create the action, and View action should open Screen B. From Screen B, completing the action should update the existing Hypothesis Monitor. The Hypothesis Monitor should remain accessible and show the complete funnel: Risk identified → Account investigated → Action initiated → Action completed, including conversion/drop-off, kill-switch status, decision rule and supporting behavioural evidence.
Build these in order so Recommended Action & Action Creation is the anchor for Action Detail & Outcome. Preserve all existing screens and functionality. Do not redesign the existing experience or introduce a new visual language. The completed journey should be: risk → evidence → decision → intervention → outcome → product learning.
```

### Step 2: Behavior, hard-code the states
```
Apply the following logic constraints to the Risk Workspace and Account Detail flow:
- Use skeleton screens for the Priority Accounts list and recalculating risk signals loading state. Retain previously available dashboard information where possible and display: “Updating account risk signals… Analysing product usage, renewal and account activity.” Do not use a generic full-page spinner.
- If no data is present because the current search or filters return zero results, show the empty state: “No accounts match these filters. Try changing the risk level, renewal window or search criteria.” Include a Clear filters CTA that restores the full Priority Accounts list. If there are genuinely no critical/high-risk accounts, instead show: “No critical accounts need attention right now. We’ll surface accounts here when their risk signals cross the attention threshold.”
- On fetch failure or stale product-telemetry data, trigger the error state: “Health score temporarily unavailable. Product activity hasn’t synced since 18 Sep, 14:20.” Do not display an authoritative health score when its underlying data is unreliable. Include Retry and View available evidence actions. Retry should trigger the loading state before restoring the score or returning the error; View available evidence should preserve available account evidence while clearly identifying unavailable signals.
Maintain the same design language throughout and tether all behavior strictly to these rules. Preserve user context, never present stale data as current fact, and ensure every error state provides a recovery path. Do not make any other visual or functional changes in this pass.
```

### Step 3: Audit first, then make one surgical UI improvement
```
The Northstar Labs Account Detail screen needs a professional enterprise SaaS polish.
Start by listing the 3 biggest gaps in typography and spacing compared to the attached Northstar Labs Account Detail reference screenshot, focusing specifically on visual hierarchy, readability, information density, and the relationship between the health score, risk drivers, and recommended action.
Once you've identified those, resize the headers to create a clearer hierarchy and update the “Why this account is at risk / Weighted health drivers” element to match. Refine each driver so it communicates:
Driver name · relative significance
Plain-language evidence
Impact on health score · View evidence ›
For example:
Engagement trend · strongest risk driver
Usage ↓31% in the last 30 days
24-point negative impact · View evidence ›
Adoption breadth
Only 1 of 18 licensed seats is active
11-point negative impact · View evidence ›
Keep the existing health score and risk colour system. View evidence should continue to use the existing evidence drill-down interaction.
Don't change anything else in the project or touch the underlying logic. Do not redesign the drawer, navigation, Recommended Action flow, charts, loading/empty/error states, or any unrelated components.
```

## Reusable techniques learned

- Expand the workflow before polishing it — complete the missing user journey first, then improve resilience and presentation.
- Naming the exact screen and UI element prevents the AI from redesigning unrelated parts of the product.
- Anchoring new screens to an existing reference keeps layout, spacing and visual language consistent.
- Building screens in a strict sequence gives the second screen a concrete design and interaction anchor.
- Specify navigation and state changes explicitly — a screen alone does not create an end-to-end workflow.
- Hard-code loading, empty and error behaviour with exact copy rather than leaving edge states for the AI to infer.
- Separate genuinely empty data from filtered-to-zero results because they require different user responses.
- Preserve context during failures — expose available evidence rather than turning an incomplete data state into a dead end.
- Audit before refining — identify the specific visual problem before asking the AI to change anything.
- Constrain refinement to one named component to prevent “polish” from becoming an uncontrolled redesign.
- Passing the README and existing prototype as context keeps each stage aligned to the same hypothesis and experiment.
- Use explicit “do not change” boundaries to protect working screens, navigation and underlying logic between iterations.

## What broke (and the fix)

_Where a single mega-prompt failed and chaining fixed it._

A single mega-prompt blurred three different jobs — workflow expansion, behavioural edge cases and visual refinement. That gave the AI too much freedom to solve everything simultaneously, increasing the likelihood of unrelated UI changes, inconsistent new screens, inferred behaviour and regression of already-working components.
The fix was chaining. Expand established the missing action journey and navigation first. Behavior then added deterministic loading, empty, stale-data and recovery states without changing that journey. Refine finally audited the completed experience and made one tightly scoped improvement to the weighted health-driver component without touching the logic.
The key lesson is that each prompt should have one type of responsibility and inherit the output of the previous one:
Expand → make the journey complete.
Behavior → make the journey resilient.
Refine → make the important interaction clearer.
That makes the framework portable: the specific screens will change in the next prototype, but the Expand / Behavior / Refine skeleton stays the same.
