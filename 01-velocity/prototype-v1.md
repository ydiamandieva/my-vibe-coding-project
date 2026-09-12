# Prototype v1: First Build (Lab 1)

> Module 1 · Velocity. Fifteen minutes from a vague problem to a clickable, shareable URL, instinct over methodology.

## Scenario

_Tick the scenario you built in Lab 1 (the same one you selected in the lab guide), or name your own._

- [x] Scenario 01 · The Retention Engine
- [ ] Scenario 02 · The Internal Tool Nobody Uses
- [ ] Scenario 03 · The Marketplace Trust Problem
- [ ] Scenario 04 · The Dashboard Nobody Reads
- [ ] My own (instructor-approved): _____

## Launch path

- [ ] Copy & Customize (started from a scenario starter prompt)
- [x] First Screen Method (built only the very first screen the user sees)

## The build

- **What I built:** A dashboard showing why new B2B customers churn in their first 90 days, with a ranked at-risk account list, a churn-driver chart and a detailed view per account. It uses realistic built-in data (about 24 accounts). The first screen is live: 12 accounts ranked by 30-day churn risk, each with a health score, risk band and the single biggest reason it's slipping.
- **Tool used:** Lovable
- **Shareable link:** https://lovable.dev/projects/e4e653e4-8bba-469d-ac32-2c89b260db33?magic_link=mc_700c02c8-e2a9-4ed6-b7d8-600dc4a2b266

## Show & Swap read

_What a partner understood from your build with no verbal setup, their reaction is your first piece of product evidence._

- **What they understood immediately:** It is a report that displays some accounts from enterprises and their likelihood to churn in the next 30 days
- **What confused them:** I do not understand the score, the possible values per range and what it actually means. What are the variables and their weights so as to understand the reasons and takes actions
- **The assumption they thought you were testing:** 1.      The behaviour in the first 90 days should be crucial so as to analyse and assume the churn rate in the next 30 days
2.      The variables calculated for the score are assumed to be: time to first value, seat activation, usage trend, integrations, sponsorship, support friction and onboarding progress (but it is not clear what is assumed as critical, at risk etc)
- **The gap between what you intended and what they read:** The prototype clearly communicates its core purpose: identifying enterprise accounts that are at risk of churning within the next 30 days based on early customer behaviour. However, the churn score lacks sufficient transparency to make the insight actionable - the score range, thresholds, contributing variables, and relative weighting of those variables are not clear. The prototype appears to be testing the assumption that behaviour during the first 90 days - such as time to first value, seat activation, usage trends, integrations, sponsorship, support friction and onboarding progress - can reliably predict near-term churn, but it needs to show which signals matter most and why an account is classified as critical or at risk so users can determine the appropriate intervention.
