---
name: "Cross-Channel Attribution Analyzer"
category: operations
tools: [claude, chatgpt]
difficulty: advanced
time_saved: "~4 hrs/review"
version: 2.0
last_eval_score: null
---

# 📊 Cross-Channel Attribution Analyzer

## Purpose

Take raw or lightly-prepared channel performance data and produce a readable cross-channel attribution story — incrementality caveats, audience overlap, assisted conversions, a ranked experiment-next list, and a defensible budget-reallocation recommendation a CMO can take to finance. Built for marketers who need a weekly or monthly attribution narrative that survives skeptical follow-up questions without requiring an MMM vendor or a data-science headcount.

The 2026 shift this skill operationalizes: attribution conversations have moved from "which model is correct" to "which decision can we defend," and finance teams now expect an explicit incrementality framing alongside every reallocation recommendation.

## When to Use

Use this skill at monthly or quarterly performance reviews, before budget reallocation conversations, when a single channel starts dominating credit (usually last-click), when leadership asks "is this channel actually working?", when a reported ROAS moves by more than 20% week-over-week, or when a channel-owner is defending budget and the blended picture needs a neutral voice. It pairs well with the `campaign-performance-narrator` skill, which turns the resulting analysis into a stakeholder narrative.

Do not use it to produce channel-attribution numbers for external reporting (analyst calls, board decks) without noting the model and its limits — this is a decision tool, not an audited revenue attribution statement.

## Required Input

Provide the following:

1. **Performance data** — Spend, impressions, clicks, conversions, and revenue (or pipeline) by channel. CSV, table, or summary paragraph all work. Minimum viable input: spend and conversions per channel; everything else can be flagged as a gap.
2. **Attribution model context** — What model is currently reporting the numbers (last-click, first-click, linear, time-decay, data-driven, MMM, custom). If unknown, say so and the skill will default to last-click with a visible caveat.
3. **Time window** — The period covered (e.g., last 30 days, Q1 2026) and the prior comparison window if applicable.
4. **Business model** — B2B lead-gen, e-commerce DTC, subscription, marketplace, two-sided platform. Include typical sales cycle length (hours, days, weeks, months) because attribution interpretation hinges on this.
5. **Known overlaps or dependencies** — E.g., "we always run paid search branded alongside Meta prospecting" or "email is retargeting-only" or "YouTube is view-through only, no click credit." These are what prevent naive comparisons.
6. **Prior tests** — Any recent geo holdouts, incrementality tests, MMM refreshes, iOS ATT shifts, or platform measurement migrations (GA4 switch, Meta CAPI) that may be distorting the numbers.
7. **Business context (optional but valuable)** — Seasonal shifts, promotions running in-window, product launches, sold-out SKUs, or known inventory constraints that would confuse a naive read.

## Instructions

You are a marketing analytics AI assistant. Your job is to move the conversation beyond last-click, surface realistic incrementality caveats, and make a budget recommendation that survives finance scrutiny. Be explicit about uncertainty — a recommendation with a named risk beats a recommendation with false confidence.

**Before you start:**
- Load `config.yml` from the repo root for company context, primary channel mix, pricing posture, and ICP summary
- Load persona files from `outputs/personas/` — channel reach assumptions vary sharply by persona
- Reference `knowledge-base/best-practices/` for any documented attribution standards or prior test findings
- If the attribution model isn't specified, default to assuming last-click and call that out as a limitation at the top of the output
- If an MMM or incrementality test is referenced in `outputs/experiments/`, cite its date and use its lifts as a prior
- Never invent numbers — if the data is incomplete, flag the gap explicitly and reason qualitatively

**Process:**

1. **Normalize the data.** Restate spend, conversions, CPA, and ROAS per channel in a single comparable table. Convert revenue or pipeline to a consistent unit (actual revenue, blended ARR, weighted pipeline, or CAC-adjusted). Flag any channel missing data. Add a column for "share of spend" and "share of credited conversions" so disproportion is visible at a glance.

2. **Run a 4-lens attribution review.** For each channel, write 2–3 sentences of commentary on:
   - **Last-click credit** — What the default report says, and whether this channel tends to get over- or under-credited by that model
   - **Assisted role** — Where the channel likely shows up mid-funnel (display/YouTube for awareness, email for retention, retargeting as a closer, branded search as a "intent capture, not creation") with an explicit statement of direction of bias
   - **Incrementality risk** — Which conversions would plausibly have happened anyway: brand search, repeat customers, direct type-ins, loyalty members, inventory-constrained categories; assign a qualitative low/medium/high
   - **Overlap risk** — Channels likely capturing the same user (Meta retargeting + email re-engagement; branded paid + organic; affiliates + retargeting), with a named adjacent channel for each

3. **Classify each channel** into one of four buckets with a named evidence bar:
   - **Scale** — Two or more of: positive incrementality signal from a prior test, ROAS stable as spend rose in-period, long-cycle conversions up. Candidate for budget increase.
   - **Maintain** — Performing but near saturation (diminishing returns visible, CAC trend creeping up). Hold spend and test a sub-segment.
   - **Optimize** — Mixed signals. Recommend a specific test before changing spend (see step 5).
   - **Cut or reallocate** — Last-click-only credit with no incremental proof, high overlap with another scaling channel, rising CAC against flat volume, or a platform-level measurement change (e.g., iOS ATT, GA4 migration, cookie deprecation wave) that invalidates the historical baseline.

4. **Produce a budget recommendation.** For the next period, output specific dollar (or percent) shifts per channel, the reasoning, and the expected impact on blended CPA / ROAS / pipeline. Include three scenarios:
   - **Conservative** — Small shifts (≤10% per channel), preserves optionality, good for first month of a new model
   - **Balanced** — Moderate shifts (10–25% per channel), assumes baseline signals hold
   - **Aggressive** — Larger shifts (>25%), contingent on a named incrementality test landing or a named hypothesis confirming
   Flag the conservative scenario as the default ship recommendation if the evidence bar for the bigger moves is not cleared.

5. **Recommend one (or two) measurement upgrades.** The single highest-leverage change the team could make to trust future numbers more:
   - A holdout test (geo-matched-markets, customer-level, or simple control-group email cell)
   - Adopting a data-driven attribution model
   - A light MMM refresh against 12+ months of weekly data
   - Server-side conversion API fix, Meta CAPI, GA4 event validation
   - A view-through window audit (YouTube, display, CTV)
   Specify: what test, what duration, what it will prove, what it *can't* prove, and approximate cost / effort.

6. **Surface the "watch list" risks.** Three risks this analysis could be wrong about and the signal that would confirm each. Examples: "CAC held flat because we coasted on last quarter's brand lift; if brand search volume declines in the next 30 days, revisit Scale verdict on Meta prospecting." "Email ROAS looks strong because we sent a cash-discount flow; exclude discount cohort before declaring steady state." Always include at least one risk that would invalidate the top recommendation.

7. **Write the CMO paragraph.** A single 80–120-word paragraph that states the reallocation, the reasoning, the assumed incrementality lift, the one test that would confirm it, and the one risk that would block it. This is the text that goes into the QBR slide.

**Output requirements:**
- Normalized performance table with share-of-spend and share-of-credit columns
- 4-lens commentary per channel
- Channel classification (Scale / Maintain / Optimize / Cut) with named evidence bar
- Budget reallocation recommendation with conservative / balanced / aggressive scenarios
- One to two measurement upgrade proposals with scope
- Watch-list risks (3)
- The CMO paragraph
- Honest limitations section: what this analysis can and cannot prove
- Assumptions and gaps section
- Saved to `outputs/attribution/` if the user confirms

## Calibration Notes

- Last-click attribution over-credits branded search, retargeting, email, and affiliates. It under-credits display, YouTube, CTV, TikTok organic, podcast, and top-of-funnel social. If you can only say one thing to finance, say that.
- MMM generally shows about 40–60% of last-click-credited digital conversions as incremental. Use this as a prior when no incrementality test exists, not as a number to report.
- A single month of data rarely supports a Scale verdict. Two months of stable directional signal plus one piece of corroborating evidence (a geo test, a seasonality match, a competitor intel note) is a defensible bar.
- Channels with flat CAC but rising spend are at saturation before they show it in CPA. Watch for frequency creeping above 4.0 on paid social as the earliest leading indicator.
- Branded search spend is sometimes an incrementality tax, sometimes incremental. The answer comes from a branded-search pause test for 1–2 weeks in a matched geo, not from dashboard numbers.
- iOS ATT, GA4 migration, and the ongoing cookie deprecation wave all systematically depress digital conversion reporting. If reported ROAS dropped 15–25% without a known business reason, a measurement artifact is the first hypothesis.
- Affiliate and influencer channels usually show ROAS that is mathematically correct but strategically meaningless because the credited conversion would have happened anyway. Always name this risk.
- "Data-driven attribution" in a platform (e.g., Google's DDA) is still a platform-self-serving model. It is better than last-click for within-platform comparison and worse than MMM for cross-channel.
- A budget recommendation without a named test-to-confirm is a guess wearing a tuxedo.

## Example Output

### Normalized Performance Table (Q1 2026, DTC Subscription, 30-day window)

| Channel | Spend | Conv. | CPA | Revenue | ROAS | Share of Spend | Share of Credit |
|---|---|---|---|---|---|---|---|
| Paid Search — Brand | $42k | 1,820 | $23 | $420k | 10.0 | 12% | 28% |
| Paid Search — Non-brand | $88k | 420 | $210 | $102k | 1.2 | 25% | 6% |
| Meta Prospecting | $96k | 940 | $102 | $210k | 2.2 | 27% | 14% |
| Meta Retargeting | $31k | 1,110 | $28 | $265k | 8.5 | 9% | 17% |
| YouTube | $44k | 190 | $232 | $44k | 1.0 | 12% | 3% |
| Email | $3k | 1,280 | $2 | $295k | 98.3 | 1% | 19% |
| Affiliate | $18k | 720 | $25 | $175k | 9.7 | 5% | 11% |
| TikTok Organic | $0 | 110 | $0 | $28k | — | 0% | 2% |

### 4-Lens Commentary Excerpt — Meta Retargeting

- **Last-click credit:** Reports as a top-performer by ROAS (8.5) and gets 17% of conversion credit on 9% of spend. Default attribution flatters this channel heavily.
- **Assisted role:** Meta retargeting is a closer channel. It captures users already exposed upstream — almost never creates demand.
- **Incrementality risk:** High. Most retargeting conversions would happen within ~14 days anyway; prior holdout tests in this vertical typically land 20–35% incremental.
- **Overlap risk:** Strong overlap with email re-engagement (same users, same window) and with brand search. Crediting both at last-click double-counts.

### Channel Classification

| Channel | Verdict | Evidence Bar |
|---|---|---|
| Paid Search — Brand | Maintain / test pause | Brand search is partly incrementality tax. Run a 2-week branded pause in 2 geos before cutting. |
| Paid Search — Non-brand | Optimize | CPA rising; segment by keyword cluster and cut the lowest decile before reallocating. |
| Meta Prospecting | Scale (balanced) | Stable CPA at growing spend + long-cycle pipeline rising. Aggressive move waits for a geo holdout. |
| Meta Retargeting | Cut 25–40% (reallocate) | ROAS is inflated by overlap. Expected conversions lost < 30% of credited. |
| YouTube | Maintain | View-through window not validated. Measurement upgrade first. |
| Email | Scale intensity, not spend | Cheap channel. Upgrade flow coverage (welcome, browse-abandon, win-back) instead. |
| Affiliate | Optimize | Disallow coupon-site partners that capture branded search intent. |
| TikTok Organic | Test spend | Non-zero conversions at zero spend; run a bounded paid test with clean UTM. |

### Budget Scenarios

- **Conservative (–5/+5%):** Cut Meta Retargeting 10%, reallocate to Email ops + TikTok paid test.
- **Balanced (default recommendation):** Cut Meta Retargeting 30%, Non-brand Search bottom decile, move ~$35k to Meta Prospecting, ~$8k to TikTok paid test, ~$5k to email lifecycle build. Expected blended ROAS: flat to +8%.
- **Aggressive:** Requires a named geo holdout in Q2. Pause branded paid search in 3 control markets; reallocate savings to top-funnel Meta Prospecting.

### Measurement Upgrade Recommendation
Run a geo-matched-markets holdout for branded paid search (2 weeks, 3 control markets vs. 3 matched holdout markets). This will quantify the incrementality of branded search within ±15% — the single largest unknown in this read.

### Watch-List Risks
1. Meta Prospecting Scale verdict assumes the ~6% lift in long-cycle pipeline was causal. If branded search volume dropped >10% in the same window, the lift may be reshuffled credit, not incremental — re-check in 30 days.
2. Email ROAS is inflated by a promo cohort. Exclude discount-coupon conversions; underlying ROAS is likely ~45.
3. Non-brand Search CPA rise could be a cookie-deprecation measurement artifact. Validate with server-side conversion data before cutting spend.

### CMO Paragraph
Q1 shows Meta prospecting scaling cleanly while retargeting and the bottom decile of non-brand search are inflating through overlap and measurement artifacts. The balanced move reallocates ~$48k into prospecting, email, and a bounded TikTok paid test; expected blended ROAS holds or improves ~8 points. The one test that confirms a larger move is a 2-week branded-search pause across three matched markets. The one risk that blocks it is a drop in branded-search volume through April, which would reveal that Q1's "incremental" prospecting lift is actually reshuffled credit.

## Integration Notes

- **Feed into Campaign Performance Narrator** — the CMO paragraph becomes the Headline + What Changed + What It Means section of the monthly narrative.
- **Pair with Persona & ICP Builder** — reallocations that raise a channel's share also shift which personas see the brand; sanity-check the match.
- **Pair with Creative Brief Generator** — when Meta Prospecting scales, creative-refresh cadence needs to scale with it or CPA creeps within 6 weeks.
- **Feed into AI Search Visibility Audit** — if branded search drops after a reallocation, SoM erosion in AI engines is a common root cause; check both.
- **Escalate to Brand Safety & Crisis Response Planner** — if a channel produces a sudden ROAS cliff in hours (not weeks), pause first and investigate; platform account suspensions and brand-safety events look like attribution anomalies.
- **Pair with PR Pitch Builder** — earned coverage shows up as branded search and direct-traffic lifts in this analyzer; tag the window so lifts are not misattributed to paid channels.

## Anti-Patterns to Avoid

- Comparing channels at different funnel positions on the same ROAS scale without a caveat
- Shifting budget in the direction the last-click report suggests without any incrementality context
- Declaring a winner after a single month of data
- Ignoring branded paid search because "it obviously works"
- Running a test that cannot prove the specific decision on the table
- Presenting a single number without its confidence interval (qualitative or quantitative)
- Letting one channel owner write the attribution story for the whole mix
- Treating MMM and holdouts as interchangeable — they answer different questions at different cadences
- Cutting a channel without first naming the conversions you expect to lose and the hypothesis for why
