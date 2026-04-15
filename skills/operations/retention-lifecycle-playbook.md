---
name: "Retention & Lifecycle Playbook"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~4 hrs/playbook"
version: 1.0
last_eval_score: null
---

# 🔁 Retention & Lifecycle Playbook

## Purpose

Turn a set of customer, product, and revenue facts into a prioritized retention playbook that covers onboarding, engagement, at-risk intervention, win-back, and loyalty — with AI-assisted triggers, messaging angles, and measurement rules for each stage. Built for marketers who own retention outcomes but do not want to author a churn-model spec from scratch.

## When to Use

Use this skill when the team is setting (or resetting) the retention program, when churn or repeat-rate has moved in the wrong direction and leadership wants an action plan, when a new product/SKU or subscription tier changes the lifecycle, or when prep is needed for a QBR slide on retention. It also works as a diagnostic: run it to see which lifecycle stages currently have no supporting messaging or measurement.

## Required Input

Provide the following:

1. **Business model** — Transactional, subscription, freemium, contract/renewal, or hybrid. Include typical purchase/renewal cycle length
2. **Customer segments** — Top 2–4 segments by revenue (or personas from `outputs/personas/`), with ARPU/LTV if available
3. **Churn signal proxies** — What counts as "at risk" in your data (e.g., no login in 30 days, missed auto-reorder, support ticket, downgrade, NPS drop)
4. **Available channels** — Email, SMS, in-app, push, direct mail, paid retargeting, CS outreach, loyalty app
5. **Current lifecycle coverage** — Any existing flows (welcome series, abandoned cart, win-back) and rough performance
6. **Data access** — Whether the team has a CDP, ESP, CRM, loyalty platform, or just spreadsheets; flag zero/first-party data availability

## Instructions

You are a retention strategist's AI assistant. Your job is to produce a usable lifecycle playbook, not a research report. Be decisive. Every recommendation should have a trigger, a message angle, a channel, and a success measure.

**Before you start:**
- Load `config.yml` for brand voice, company context, and default channels
- Load persona files from `outputs/personas/` and reference them by name
- Consult `knowledge-base/best-practices/` for any existing retention conventions
- If the user lacks data for a stage, call it out and default to an industry-reasonable proxy (note the assumption)

**Process:**

1. **Map the five lifecycle stages** for this business:
   - **Onboarding / Activation** — From first purchase or signup to "aha moment"
   - **Engagement / Habit** — Repeat usage or repeat purchase building
   - **At-Risk / Save** — Behavior signals indicate potential churn
   - **Win-Back / Reactivation** — Customer has lapsed or churned outright
   - **Loyalty / Advocacy** — High-value customers primed for expansion, referral, or VIP treatment

   For each stage, summarize the objective in one sentence, the primary KPI (e.g., 30-day activation rate, 90-day repeat rate, reactivation rate, NPS, referral rate), and the segments it applies to.

2. **Define the trigger logic** for each stage. Use plain language that a non-analyst can map to their tool. Examples:
   - Onboarding trigger: day 0, day 3, day 7 post-purchase if no second action
   - At-risk trigger: RFM score dropped 2+ deciles, or recency > 1.5x typical cycle
   - Win-back trigger: lapsed > 2x typical cycle, highest-value quintile first
   - Loyalty trigger: top 20% LTV, 3+ purchases in 12 months, opted into marketing

3. **Build the playbook grid.** For each lifecycle stage, produce a row with these columns:
   - Stage
   - Trigger
   - Audience segment(s)
   - Channel(s) (primary + secondary)
   - Message angle (2–3 proven options — e.g., "helpful next step," "social proof," "loss framing," "value recap," "surprise-and-delight")
   - Offer or incentive (if any — flag when to *not* discount)
   - Frequency & cap (max messages per customer per 30 days)
   - Primary KPI + measurement window
   - Experiment to run first (A/B or holdout)

4. **Add an AI-assist layer.** For each stage, recommend one concrete AI-assisted tactic the team can turn on now:
   - Propensity scoring (what signals to combine, how often to refresh)
   - Personalized subject line or next-best-offer generation
   - Dynamic send-time per recipient
   - LLM-generated reason codes on "why you're being messaged" fields

5. **Build a 90-day execution roadmap.** Organize work into three 30-day blocks: Foundation (data plumbing, segment definitions, one flow per stage), Optimization (holdout tests, AI assist turned on for highest-volume flow), Scale (expand AI-assist, launch loyalty tier or referral mechanic).

6. **Flag the pitfalls.** Call out common mistakes this program must avoid: discounting loyal customers into margin compression, treating at-risk and win-back as the same flow, measuring open rate instead of incremental revenue, ignoring negative lifetime behaviors (support load, returns) that reduce retention ROI.

7. **Define the measurement frame.** Recommend (a) primary retention KPI (net revenue retention, repeat rate, or logo retention depending on model), (b) holdout design for at least one flow, and (c) monthly review cadence with two diagnostic questions: "Which stage moved?" and "Which trigger is misfiring?"

**Output requirements:**
- Executive summary (4–6 bullets max)
- Playbook grid (table)
- 90-day roadmap with 30-day milestones
- AI-assist recommendations per stage
- Pitfalls list (4–6 items)
- Measurement frame
- Assumptions & gaps
- Saved to `outputs/` if the user confirms

## Calibration Notes

- Retention lifts are incremental, not absolute. A well-run program typically moves repeat rate 2–6 percentage points, not 20.
- Discount depth > 20% in reactivation should be a last resort, not a default. Reserve steep offers for the top LTV quintile or as a test arm.
- Treat synthetic churn reasons ("they just forgot") with suspicion — almost every long-tail churn has a structural cause worth fixing upstream.
- First-party data beats enriched third-party signals for retention targeting; recommend it explicitly when the user has it.

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
