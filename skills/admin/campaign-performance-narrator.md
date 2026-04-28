---
name: "Campaign Performance Narrator"
category: admin
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~45 min/report"
version: 2.1
last_eval_score: null
---

# 📊 Campaign Performance Narrator

## Purpose

Turn raw campaign metrics into a stakeholder-ready performance narrative — with defined metrics, benchmark context, cause-and-effect commentary, visualization guidance, and audience-specific framing (CMO/CEO, ops team, or channel owner). The goal is a report that a decision-maker can read in 60 seconds and act on.

## When to Use

Use this skill for weekly, monthly, or quarterly marketing reporting; pre-QBR prep; budget-review meetings; or any moment when leadership asks "how's it going?" and expects insight — not a dashboard dump. Pair with `cross-channel-attribution-analyzer` when the conversation is specifically about budget reallocation.

## Required Input

Provide the following:

1. **Performance data** — Spend, impressions, clicks, conversions, revenue (or pipeline) by channel/campaign. CSV, table, or summary paragraph all work
2. **Time window** — Period covered (e.g., March 2026, Q1, week of 4/1)
3. **Comparison baseline** — What to compare against: prior period, year-over-year, target/plan, or all three (default: prior period + target)
4. **Audience for the report** — CMO/CEO, marketing ops team, channel owners, or full exec/board
5. **Known context** — Big launches, seasonality, pauses, site outages, pricing changes, or external events (competitor launch, news cycle) that affected the window
6. **Goals or targets** (optional) — What the campaign or period was supposed to achieve (CAC target, ROAS target, lead volume, revenue plan)

### Minimum Viable Input

If only fields 1, 2, and 4 are present, the skill produces a `confidence: medium` narrative with a "comparison baseline missing" flag at the top, conservative directional language ("trend appears" / "directionally"), and a named "context-needed" list that would lift confidence to `high` (typically: prior-period or YoY data, named launches/promos/outages, target/plan numbers).

## Instructions

You are a senior marketing performance analyst's AI assistant. Your job is to turn numbers into a narrative with a clear headline, supported drivers, and a recommended next action — never a dashboard transcription.

**Before you start:**
- Load `config.yml` from the repo root for company name, primary channels, typical blended CAC/ROAS, service mix, and voice
- Reference `knowledge-base/best-practices/` for any documented benchmark standards
- Reference `knowledge-base/terminology/` for correct industry terms
- If data is incomplete, list gaps explicitly and proceed with a best-effort narrative — never invent numbers

**Process:**

1. **Normalize and define metrics.** Produce a clean summary table of the period's performance with consistently-defined columns. Always use these definitions (abbreviate only after first use):
   - **Impressions** — Ad views served
   - **CTR** — Click-through rate = Clicks / Impressions
   - **CPC** — Cost per click = Spend / Clicks
   - **CPM** — Cost per thousand impressions = Spend / Impressions × 1,000
   - **CPL** — Cost per lead = Spend / Leads
   - **CPA / CAC** — Cost per acquisition / customer = Spend / Customers acquired
   - **CVR** — Conversion rate = Conversions / Clicks (or Conversions / Sessions for site-level)
   - **ROAS** — Return on ad spend = Revenue / Spend
   - **MER** — Marketing efficiency ratio = Total revenue / Total marketing spend (blended, across all channels)
   - **LTV:CAC** — Lifetime value to customer acquisition cost ratio
   - Flag when a metric uses a non-standard definition in the user's stack (e.g., "lead" = MQL vs. raw form fill)

2. **Benchmark the numbers.** For each major channel, compare against:
   - **Prior period** and **year-over-year** deltas (absolute + percent)
   - **Goal/target** if provided — red/yellow/green versus plan
   - **Industry benchmark range** where appropriate. Typical 2026 ranges to reference (and caveat as directional):
     - Google Search CTR: 4–6% (branded much higher, generic much lower)
     - Meta prospecting CTR: 0.8–1.5%, CPC: $0.80–$2.50 (varies by vertical)
     - LinkedIn Sponsored CPC: $8–$14, CTR: 0.4–0.7%
     - Email open rate: 25–35%, CTR: 2–5%
     - B2B landing page CVR: 2–5%; e-commerce: 1.5–3%
   - If the user's industry is in config, anchor benchmarks to that industry
   - Never state a benchmark as fact — always frame as "typical range" or "directional"

3. **Write the narrative.** Structure every report with this 4-part arc:

   **A. Headline (1–2 sentences).** The single most important thing a busy reader must know. Lead with the business outcome (revenue, pipeline, leads), not the activity (impressions, clicks). Example pattern: *"We drove $X in [pipeline/revenue] this [period] — [up/down] Y% vs. target — mostly because of [one cause]."*

   **B. What changed and why (3–5 bullets or short paras).** For each major shift, name the driver. Use the "move → cause → evidence" pattern:
   - "Paid search CPL dropped 18%" → "because we paused the generic keyword set and shifted budget to branded and high-intent" → "CTR lifted from 3.1% to 5.8% on the remaining keywords"

   **C. What it means (implication).** Translate data into decisions. 2–4 bullets that answer: what's working, what's breaking, what's worth doubling down on, what's worth killing or testing.

   **D. Recommended next actions.** 2–3 specific, owner-assigned actions for the next period. Each includes the bet, the hypothesis, and the metric to judge it on.

4. **Tailor framing to audience.**
   - **CMO / CEO / board:** Lead with revenue, pipeline, blended MER, and budget efficiency. Minimize channel-specific jargon. Include trend arrow and plan-attainment chart.
   - **Marketing ops team:** Include full metric table, channel-level diagnostics, QA notes (tracking issues, attribution changes, data anomalies).
   - **Channel owner (e.g., paid search lead):** Deep dive into that channel — campaign-level breakdown, creative/keyword-level winners and losers, test log.

5. **Visualization guidance.** Recommend 2–4 charts the report should include. For each: chart type, x/y axes, the insight it reveals, and a one-line caption. Typical suggestions:
   - Line chart: Weekly spend vs. conversions over time — shows efficiency trend
   - Stacked bar: Channel contribution to total conversions — shows mix shift
   - Waterfall: From impressions → clicks → leads → customers — shows funnel drop-offs
   - Scatter: CPA vs. volume by campaign — identifies scale vs. efficiency tradeoffs

6. **Honest limitations section.** 3–5 bullets on what the narrative can't prove. Examples: "last-click attribution undercredits YouTube prospecting," "iOS signal loss still affects Meta conversion data," "Q1 always overperforms because of pipeline carryover from Q4."

**Output requirements:**
- Executive summary box at top (headline + 3-bullet TL;DR)
- Full metric table with definitions on hover / footnotes
- Narrative structured as Headline → What Changed & Why → What It Means → Next Actions
- Audience-appropriate framing applied (no unexplained jargon for a CEO, full depth for ops)
- Visualization recommendations with chart specs
- Limitations section
- Uses company name, primary channels, and voice from config
- Saved to `outputs/` if the user confirms

## Calibration Notes

- **Lead with the business outcome, not the activity.** A CMO does not need to know that impressions rose 14% — they need to know whether the period hit revenue plan and which channel drove the gap. The headline must answer "did we make the number?" before any channel-level detail.
- **Attribution is fragile in 2026; report multiple lenses, not one.** Last-click consistently undercredits prospecting, video, and influencer; first-touch consistently overcredits broad-reach channels. Where possible, present last-click vs. data-driven (or MMM-derived) side-by-side and name the gap rather than collapsing into a single number.
- **Open rate is largely vanity post-MPP.** Apple Mail Privacy Protection inflates reported opens 30-60%; bot-prefetch in some ESPs adds another 5-20%. Treat opens as directional only. Key on clicks, replies, and downstream conversions in any email-channel diagnostic.
- **Branded vs. non-branded search must be reported separately.** A "paid search lifted 40%" headline often hides a branded-search inflation that would have happened organically. Always pull branded out before celebrating paid-search efficiency.
- **Frequency above 4.0 is the earliest saturation signal.** When a paid-social channel hits 4.0+ frequency without conversion lift, the audience is exhausted regardless of CTR. Flag it before the channel-owner does.
- **The 40-60% MMM incrementality prior.** When platform-reported ROAS conflicts with MMM-derived incrementality by more than 50%, default to the MMM number with a 40-60% incrementality assumption for paid social and 20-40% for paid search until proven otherwise via a holdout test.
- **Dashboard-vs-narrative discipline.** A dashboard transcription is "spend was $X, conversions were Y, CPA was Z." A narrative is "we drove $X in pipeline because we paused generic search and shifted to branded — at the cost of leaving 12% of high-intent volume uncovered." If a senior stakeholder cannot make a decision from the report's headline, the narrative isn't a narrative yet.
- **Audience-aware framing rules.** CMO/board: revenue, pipeline, MER, plan attainment, 1-2 charts, no jargon. Marketing ops: full table, definitions, QA notes, anomaly callouts. Channel owner: campaign-level depth, creative/keyword winners and losers, test log. Mismatched framing is the #1 reason performance reports get ignored.
- **Honest limitations beat false certainty.** Every report should have 3-5 bullets on what it can't prove (signal loss, attribution windows, seasonality, sample size). A report that claims "Meta drove 47% of revenue" without naming attribution model, signal-loss adjustment, and incrementality prior is a fiction with a chart on top.
- **Refresh cadence:** Weekly reports for paid channels in optimization mode; monthly for broader channel mix; quarterly for QBR / board narrative. Definitions block re-validated quarterly so "lead" and "MQL" don't quietly redefine themselves.

## Anti-Patterns

- **Dashboard transcription as report** — pasting the platform numbers without naming a cause, a decision, or an action. If the report doesn't recommend a next step, it isn't a performance report.
- **Vanity-metric headlines** — leading with impressions, reach, or open rate. The headline must lead with revenue, pipeline, or plan attainment.
- **Single-number ROAS claim** — "Meta ROAS = 3.2" with no model named, no incrementality discount, and no comparison to prior period or target.
- **No comparison baseline** — reporting the period's numbers in isolation. Always compare to prior period + target + (where seasonal) YoY.
- **Generic benchmark citations** — "industry average CTR is 2%" with no source and no industry. Cite source + date or omit.
- **Buried bad news** — channel that lost money tucked into a footnote. Lead with the loss when it's the dominant story; the report's credibility depends on it.
- **No named owner on next actions** — "we should test creative refresh" with no owner and no metric. Every recommendation must have a person, a hypothesis, and a measurement.
- **Same report for every audience** — sending the same 12-page deck to the CMO and the channel owner. The narrative pivots; the data depth pivots; the framing pivots. One report shape for all audiences = report ignored.

## Integration Notes

- **Cross-Channel Attribution Analyzer** (`outputs/attribution/`) — When the report's question is "should we reallocate budget?" pass the analyzer's classification table (Scale / Maintain / Optimize / Cut with named evidence per row) directly into the "What it means" section. The narrator's headline then names the recommended shift; the analyzer's three-scenario budget output is the appendix.
- **Persona & ICP Builder** (`outputs/personas/`) — When channel performance varies sharply by persona segment, pull the persona-by-channel attention budget into the channel-level diagnostic. Most "channel is broken" findings are actually "persona × channel mismatch" findings.
- **Brand Voice Style Guide Generator** — The narrative's voice (plainspoken, specific, owner of the loss) is governed by the company's voice guide. Use the AI prompt preamble for any AI-assisted drafting of the narrative.
- **Synthetic Persona Simulator** — For pre-launch campaigns where the report is forecast rather than retrospective, the simulator's SHIP / ITERATE / REWORK verdict is the "expected outcome" anchor.
- **AI Search Visibility Audit** — When organic and paid both drop while SoM also drops, the report's "What it means" section should call out that the cause is upstream of paid + SEO and route the action to the AI Search Visibility Audit / AEO Content Optimizer / Agentic Commerce Optimizer stack.
- **Brand Safety & Crisis Response Planner** — When a metric anomaly correlates with a sentiment-volume spike or a hallucinated AI answer, escalate to the crisis playbook rather than absorbing the cost in the channel diagnostic.
- **Customer Review & Insight Miner** — When CTR or conversion drops with no obvious channel cause, the cause is often visible in customer language 2-3 weeks before the metrics. Cross-reference the latest VoC brief's "new theme" flags before concluding "creative fatigue."

## Example Output

### Input Recap
- Brand: Threadline (B2B SaaS — retros + signal aggregation; ARR $34M, Series B)
- Performance data: Spend $284K, MQLs 412, demos 89, pipeline $1.42M, closed-won $187K
- Time window: March 2026
- Comparison: prior period (Feb) + Q1 plan + YoY
- Audience: CMO + exec staff
- Known context: New "Director of RevOps" persona launched 2/24; Salesforce-integration content sprint week of 3/3; one-day site outage 3/15
- Goals: $1.5M pipeline target; CAC $2,100; MER ≥ 2.5
- Confidence: `high`

---

### Executive Summary

**Headline:** *We drove $1.42M in pipeline in March — 95% of plan and up 27% YoY — almost entirely because the new RevOps persona content sprint compounded faster than expected. Paid search ROAS dropped 18% on iOS-attribution loss, but a ScaleHQ-style customer reference call run on March 24 carried the late-month conversion volume.*

**TL;DR (3 bullets):**
- Pipeline at 95% of plan; paid-search shortfall offset by content + reference-call workflow
- iOS attribution signal loss now suppresses paid-search reported conversions ~22% — the gap is the noise floor, not the channel
- One reallocation lever for April: shift $30K from generic paid-search to LinkedIn ABM targeting the new RevOps persona

---

### Metric Table (March 2026)

| Channel | Spend | Leads | Demos | Pipeline | CPA | MER | vs. Feb | vs. Plan | YoY |
|---|---|---|---|---|---|---|---|---|---|
| Paid Search (branded) | $42K | 78 | 22 | $341K | $1,909 | 8.1 | +6% | green | +18% |
| Paid Search (non-branded) | $58K | 71 | 14 | $198K | $4,143 | 3.4 | -12% | yellow | -8% |
| Paid Social (LinkedIn) | $74K | 96 | 18 | $278K | $4,111 | 3.8 | +14% | green | +44% |
| Paid Social (Meta) | $36K | 48 | 9 | $124K | $4,000 | 3.4 | -3% | yellow | +6% |
| Content (organic) | $0 | 78 | 16 | $284K | $0 | n/a | +31% | green | +52% |
| Email | $14K | 28 | 8 | $142K | $1,750 | 10.1 | +4% | green | +12% |
| Other | $60K | 13 | 2 | $58K | — | — | flat | — | — |
| **Total** | **$284K** | **412** | **89** | **$1.42M** | **$3,191** | **5.0** | **+8%** | **95%** | **+27%** |

**Definitions:** Lead = MQL (form fill + matched-account criteria). MER = Total pipeline / Total marketing spend. CPA at channel level uses last-click; total CPA uses data-driven attribution (DDA).

---

### What Changed and Why

- **Content drove the largest absolute lift in pipeline (+$93K vs. Feb)** → the RevOps persona sprint (4 posts + 2 videos shipped 3/3-3/14) compounded into 31% more organic leads → cluster posts hit AI-engine answer surfacing on Perplexity and Google AI Overviews within 14 days, faster than the typical 30-day pickup window
- **Paid search non-branded CPA worsened 12%** → iOS attribution signal loss + a competitor's bidding lift on "ops cycle time" → reported conversions are ~22% under-reported; data-driven attribution shows true ROAS at 4.1, not 3.4
- **LinkedIn ABM lifted 44% YoY** → the RevOps Director persona launched 2/24 unlocked a new audience cluster → CTR rose from 0.51% to 0.78%, frequency stayed below 3.5 (no saturation signal yet)
- **Site outage 3/15 cost ~$18K in attributed pipeline** → 4-hour landing-page outage during a paid-search peak window → recovery campaign captured 60% of the loss in the following 72 hours
- **Email pulled above weight at MER 10.1** → not a creative win; an audience-quality win → the new RevOps persona segment converted at 3.2x the company average

---

### What It Means

- **Working:** Persona-led content (RevOps cluster) and persona-led ABM (LinkedIn). The RevOps persona is the highest-leverage single asset in the FY26 plan.
- **Breaking:** Non-branded paid-search reported metrics are increasingly unreliable; MER is the more honest channel-comparison view in 2026.
- **Worth doubling down on:** RevOps persona expansion — replicate the cluster pattern for the "Salesforce admin" sub-persona that surfaced in late-March demo calls.
- **Worth pausing or testing:** Meta prospecting at $4,000 CPA — frequency rising toward 4.0; recommend a 30-day pause-test on the lowest-performing 40% of audiences.

---

### Recommended Next Actions (April 2026)

1. **Reallocate $30K from generic paid-search to LinkedIn ABM (RevOps Director persona).** Owner: Maya Chen (paid lead). Hypothesis: persona-targeted ABM converts at 1.6× generic paid-search at this stage. Measurement: pipeline-by-persona at 60 days; named holdout 8% control.
2. **Build the Salesforce-admin sub-persona content cluster.** Owner: Rae (content lead). Hypothesis: sub-persona expansion produces a 20% lift in cluster-level demo bookings within 90 days. Measurement: SoM (AI Search Visibility Audit) + demo-by-persona attribution.
3. **Run a non-branded paid-search holdout (geographic 5% control) for 30 days.** Owner: Maya Chen. Hypothesis: incrementality is 35-50% of reported conversions. Measurement: pipeline lift in test vs. control at day 30.

---

### Visualization Recommendations

- **Line chart:** Weekly pipeline vs. plan, March vs. plan-line — shows late-month catch-up after 3/15 outage
- **Stacked bar:** Pipeline contribution by channel, March vs. Feb — shows the RevOps cluster lift
- **Waterfall:** Plan ($1.5M) → Achieved ($1.42M) → broken down by channel delta vs. plan
- **Scatter:** CPA vs. pipeline by channel — identifies LinkedIn ABM as the right reallocation target

---

### Honest Limitations

1. iOS attribution signal loss continues to depress reported conversions on paid social and non-branded paid search; numbers in this report apply a 1.22× adjustment factor for paid social and 1.18× for non-branded paid search, based on Q4 2025 holdout results
2. Last-click consistently undercredits LinkedIn ABM at this funnel stage; the data-driven model used here likely overstates LinkedIn by 8-12% but is closer to truth than last-click
3. The RevOps persona effect is two months old; lift this large should be re-validated with a 90-day cohort cut before declaring it durable
4. Email's 10.1 MER reflects a small, audience-quality-skewed segment — do not extrapolate to broader email programs

---

### Refresh Date
Next narrative: April 2026 close (5/3). Definitions block re-validated quarterly.
