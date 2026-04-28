---
name: "Retention & Lifecycle Playbook"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~4 hrs/playbook"
version: 2.0
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

### Minimum Viable Input

If only fields 1, 2, and 4 are present, the skill produces a `confidence: medium` playbook with industry-default trigger logic for each lifecycle stage, named assumptions per stage, and a "data needed before launch" checklist (typically: defined churn signals, current flow performance, zero/first-party data inventory) that would lift confidence to `high`.

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

- **Retention lifts are incremental, not absolute.** A well-run program typically moves repeat rate or net revenue retention 2-6 percentage points, not 20. Programs claiming a 20-point lift have either started from a broken baseline or are reporting non-incremental halo. Pre-commit to a holdout-anchored measurement.
- **Discount depth > 20% in reactivation should be a last resort.** Reserve steep offers for the top LTV quintile or as a 30-day test arm. Default reactivation should lead with new value, named product changes since lapse, or a peer-relevance hook — not a discount. Discount-led reactivation systematically attracts the most price-sensitive segment, which churns again.
- **Treat synthetic churn reasons with suspicion.** "They just forgot" is almost always a structural failure: failed onboarding, unrealized first value, support friction, integration breakage. Audit the cause before designing the save flow.
- **First-party data beats enriched third-party signals for retention targeting.** Recommend it explicitly. Zero- and first-party data also age more slowly than third-party (which now decays faster as cookie deprecation, ATT, and platform restrictions compound).
- **Holdout > A/B for sequence-level decisions.** A/B answers "which message is better." Holdout answers "is the program incremental at all." A retention program without a 5-10% holdout is reporting fiction.
- **Churn-prediction noise floor is real.** Even the best propensity models have a 30-50% false-positive rate on long-tail churn. Build the at-risk flow assuming half the people targeted weren't going to churn anyway; this changes the messaging tone (helpful, not pleading).
- **RFM is segmentation, not behavior.** Recency-Frequency-Monetary buckets are useful as a starting frame but cannot replace behavioral signals (last login, missed reorder, integration error, support theme). Combine, never replace.
- **Loyalty programs decay without rotation.** A loyalty mechanic launched in Year 1 has 60-70% of its lift by Year 2 if unchanged. Plan the rotation cadence (new tier benefit, new partner, new exclusive) at launch — not as a Year 2 emergency.
- **Never discount a renewal-only customer who would have renewed.** The cardinal sin of subscription retention. Score renewal likelihood before adding any retention offer; reserve incentives for renewal-at-risk segments only.
- **Refresh cadence:** Re-validate playbook every 6 months (faster for transactional / DTC, slower for enterprise SaaS). Trigger logic re-validated quarterly because cycle lengths and signal proxies drift with audience composition.

## Anti-Patterns

- **The discount-default save flow** — every at-risk and win-back email leads with a percentage off. Trains the segment to expect discounts, compresses margin, and attracts the most price-sensitive cohort. Lead with new value or peer-relevance first; reserve discount for the bottom of the flow and the top LTV quintile.
- **At-risk and win-back as the same flow** — at-risk customers are still in the relationship; win-back customers have left. The tone, offer, and cadence are different. One flow for both reads as tone-deaf.
- **Open-rate as the primary KPI** — already-vanity in 2026 post-MPP. Net revenue retention or repeat-rate lift is the truth signal.
- **Loyalty program for the bottom 80%** — VIP tiers that everyone qualifies for stop being VIP. The named loyalty mechanic is for the top 20% LTV by definition.
- **Discount-stacking through the flow** — 10% in email 2, 15% in email 3, 25% in email 4. Customers learn to wait for the bottom of the flow and the program loses its margin.
- **Ignoring the support side of churn** — most retention programs are owned by marketing alone. Support data (ticket themes, response time deltas, repeat-issue cohorts) is the strongest non-product churn predictor. Pull it in.
- **Frozen flow** — sequence shipped, never revisited. Audience composition shifts continuously; flow refresh cadence is mandatory.
- **No exit conditions** — recipient renews / converts / unsubscribes mid-flow but keeps receiving emails 4-5. Branch logic + suppression on the conversion event is mandatory.

## Integration Notes

- **Persona & ICP Builder** (`outputs/personas/`) — Persona's hidden motivation, channel attention budget, and trigger event feed the playbook's stage-by-stage messaging angles. Reference persona file by name in the playbook frontmatter.
- **Brand Voice Style Guide Generator** — Voice attributes + AI prompt preamble govern the tone of every flow's copy. The save-flow tone is plainspoken and helpful, not pleading.
- **Email Sequence Builder** — The retention playbook names the stages and triggers; the sequence builder writes the actual emails per stage. Pass the playbook grid as the input. Holdout discipline is shared.
- **Cross-Channel Attribution Analyzer** — Retention program incrementality (vs. baseline) feeds the analyzer's incrementality priors. Holdout results overwrite last-click for save-flow attribution.
- **Campaign Performance Narrator** — Stage-by-stage retention KPIs (activation rate, save rate, win-back rate, NPS, referral rate) feed the narrator's monthly/quarterly retention diagnostic.
- **Customer Review & Insight Miner** (`outputs/voc/`) — VoC brief's "pains" and "objections" themes are the highest-signal source of save-flow message angles. The "switching language" pass identifies who churned and why in their own words; the "disappearing theme" flags name issues that lapsed segments stopped raising (often because they left).
- **Synthetic Persona Simulator** — Run the at-risk and win-back flows through the simulator before launch. The simulator's SHIP / ITERATE / REWORK verdict is a required gate at the highest-cost flow (typically save).

## Example Output

### Input Recap
- Brand: Threadline (B2B SaaS — retros + signal aggregation; subscription, $99-$499/seat/mo)
- Business model: subscription, monthly + annual, 14-day free trial, typical renewal cycle 12 months
- Top segments: Persona "Priya, the Pragmatic Head of RevOps" (`outputs/personas/priya-revops.md`) — 60% revenue; "Marcus, the New CRO" — 25%; "Sam, the Salesforce Admin" — 15% (technical evaluator, often blocker)
- Churn signal proxies: no login >14 days, missed weekly retro, integration error >2× in 7 days, downgrade, NPS <7, support ticket >3× in 30 days
- Channels: in-app, email, Slack notifications (where opted-in), CS outreach, retargeting (paid)
- Existing flows: welcome series (medium-performing); no at-risk, no win-back, no formal loyalty
- Data: CDP (Segment) + ESP (Customer.io) + CRM (Salesforce) + product analytics (Amplitude); zero/first-party data is rich
- Confidence: `high`

---

### Lifecycle Stage Map

| Stage | Objective | Primary KPI | Segments |
|---|---|---|---|
| Onboarding / Activation | Reach "weekly retro shipped within 14 days" milestone | 14-day activation rate (target 65%) | All new accounts |
| Engagement / Habit | 4 retros shipped per month, signal aggregation enabled | 90-day habit rate (target 55%) | Activated accounts |
| At-Risk / Save | Reverse one of three named churn signals before renewal | Save rate (target 35% of at-risk) | At-risk by signal |
| Win-Back / Reactivation | Reactivate lapsed accounts with named product change | 90-day reactivation rate (target 8%) | Lapsed > 60 days |
| Loyalty / Advocacy | Expansion + referral + community contribution | Net revenue retention (target ≥110%) | Top 20% LTV |

---

### Playbook Grid

| Stage | Trigger | Audience | Primary Channel | Secondary | Message Angle | Offer | Frequency / Cap | Primary KPI | Test |
|---|---|---|---|---|---|---|---|---|---|
| Onboarding | Day 0 / 3 / 7 / 14 post-signup if no retro shipped | All new | In-app + email | Slack notif (if opted) | "Helpful next step" + named "weekly retro shipped" milestone | None (value-led) | 4 emails / 14 days | 14-day activation rate | A/B onboarding video vs. text-only |
| Engagement | 2nd month, retro count <2 | Activated, sub-target | Email + in-app | CS check-in | "Pattern you're missing" — named insight from their own data | None | 2 emails / 30 days | 90-day habit rate | Holdout 10% control |
| At-Risk (login lapse) | No login >14 days AND prior login frequency >weekly | At-risk by behavior | Email + in-app | CS Slack DM (if Champion CSM) | "Status check + known issue" — surface the most likely cause | None (first 14 days), then a free expert-call offer | 2 emails / 14 days | Save rate | A/B: helpful-question vs. expert-call offer |
| At-Risk (integration error) | Integration error >2× in 7 days | At-risk by signal | In-app + CS | Email | "Fix-first" — named cause + named fix | None | 1 in-app + 1 CS reach / 7 days | Save rate | Holdout 10% |
| At-Risk (NPS <7) | NPS detractor | At-risk by NPS | CS-led | Email follow-up | "Tell me what we got wrong" — non-survey, real reply | None | 1 CS reach / 30 days | Save rate + NPS recovery | Holdout 10% |
| Win-Back | Lapsed > 60 days, prior MRR > $200/mo | Highest-value lapsed first | Email | Retargeting | "What's new" — named product change since lapse | 30-day extended trial OR 20% off year 1 (gated by quintile) | 3 emails / 30 days | 90-day reactivation rate | A/B: extended trial vs. discount; required holdout 10% |
| Loyalty | Top 20% LTV + ≥3 retros/month + opted into marketing | Champion segment | Email + community + 1:1 | CS + invite-only events | "Insider + advocacy + expansion" — pre-release + peer connection | Loyalty tier benefits (named annually) + referral mechanic | Quarterly + ad hoc | Net revenue retention + referral rate | None — measured continuously |

**Exit conditions:** activation milestone reached → exit onboarding; renewal closed → exit at-risk; reactivation booked → exit win-back; opted-out → full suppression; named-friction-cause-fixed → exit at-risk + log the fix.

---

### AI-Assist Layer

| Stage | AI tactic | Implementation note |
|---|---|---|
| Onboarding | LLM-generated next-best-action recommendation per account based on first-week behavior | Pulls from product analytics; ESP fallback to default sequence if data sparse |
| Engagement | Personalized "pattern in your data" insight email per account | Bounded set of 6-8 insight templates; LLM fills the variable named insight, never authors freely |
| At-Risk | Propensity scoring across login + integration-error + NPS signals (refresh nightly) | Combine, don't replace; named threshold for at-risk = top 2 deciles of propensity |
| Win-Back | Reason-code field on every email — "we noticed you stopped logging weekly retros after [date]" — LLM-fills the variable from product analytics | Never invent a cause; if no signal, use a generic "what's new" framing |
| Loyalty | Predictive expansion-readiness scoring for AE handoff | Top 20% LTV + named expansion signal = warm AE outreach; the rest = community + content |

---

### 90-Day Execution Roadmap

**Days 1-30 — Foundation**
- Define the at-risk signal taxonomy in CDP (login lapse, integration error, NPS, support theme)
- Build the at-risk save flow (highest cost, highest leverage) — required before win-back
- Stand up holdout discipline: 10% control on every flow that goes live this quarter
- Audit existing welcome series — fix or replace before adding new flows

**Days 31-60 — Optimization**
- Launch at-risk save flow with 10% holdout
- AI-assist on the engagement "pattern in your data" email — measure incrementality vs. control
- Add the win-back flow targeting lapsed > 60 days, top quintile only (test before broad rollout)
- Run the at-risk save flow through Synthetic Persona Simulator before launch (Priya + Marcus + Sam reaction layers); SHIP / ITERATE / REWORK gate before send

**Days 61-90 — Scale**
- Win-back flow expanded to all lapsed segments based on Day 60 holdout results
- Loyalty tier launched for top 20% LTV: named exclusive benefit + 1:1 community access + early access to product changes
- Expansion-readiness scoring routed to AE; warm-handoff playbook defined
- Quarterly review meeting cadence locked: "Which stage moved? Which trigger is misfiring?"

---

### Pitfalls to Avoid

1. Discounting renewal-only customers who would have renewed — always score renewal likelihood first
2. Treating at-risk and win-back as the same flow — different tone, different offer, different cadence
3. Open rate as the primary KPI — net revenue retention and stage-by-stage KPIs are the decision metrics
4. Loyalty programs everyone qualifies for — the top 20% LTV is the cap by definition
5. Ignoring support data in churn diagnostics — pull ticket themes, response-time deltas, repeat-issue cohorts
6. No holdout — every flow ships with 5-10% control, no exceptions
7. Discount-stacking through the flow — train customers to wait, lose margin
8. No exit conditions — converted/lapsed/unsubscribed customers must exit the flow within 24 hours

---

### Measurement Frame

- **Primary KPI (program-level):** Net revenue retention (target ≥110% Year 1; the lift comes from save flow + loyalty expansion combined; flow-level holdouts attribute the share)
- **Holdout design:** 10% control on every new flow; results read at flow end + 30 days; ship-to-broad-launch gate at 1.5× incremental lift over control
- **Monthly review cadence:** "Which stage moved?" (compare KPI deltas across the five stages); "Which trigger is misfiring?" (compare propensity precision and at-risk save rate by signal); review save-rate by signal and reactivation-rate by tenure quintile
- **Quarterly review:** rotate loyalty mechanic if Year 1 lift compressed >30%; re-validate trigger logic against drifted audience; re-run the playbook through Synthetic Persona Simulator
- **Pause condition:** at-risk flow unsubscribe rate > 1% per send pauses the flow within 48 hours; CS reviews root cause before resume

---

### Assumptions & Gaps

- "14-day activation rate" target of 65% is benchmarked to Threadline FY26 data; revisit if expanding into a new ICP segment
- "Top 20% LTV" qualifier for loyalty assumes current ARPU distribution holds; recompute quarterly
- AI-assist incrementality assumed at 12-18% lift over non-AI-assisted variants; revisit after the first 60-day holdout result
- Win-back 8% reactivation target assumes the named-product-change framing; if no notable change since lapse, drop target to 4-5% and run "category trend" framing instead

---

### Refresh Date
Playbook: re-validate 2026-10-25 (6 months). Trigger logic: re-validate quarterly (2026-07-25). Loyalty mechanic rotation: planned at launch + 12 months.
