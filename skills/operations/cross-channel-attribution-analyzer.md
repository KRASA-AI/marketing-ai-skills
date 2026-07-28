---
name: "Cross-Channel Attribution Analyzer"
category: operations
tools: [claude, chatgpt]
difficulty: advanced
time_saved: "~4 hrs/review"
version: 3.1
last_eval_score: 9.5
---

# 📊 Cross-Channel Attribution Analyzer

## Purpose

Take raw or lightly-prepared channel performance data and produce a readable cross-channel attribution story — incrementality caveats, audience overlap, assisted conversions, a ranked experiment-next list, and a defensible budget-reallocation recommendation a CMO can take to finance. Built for marketers who need a weekly or monthly attribution narrative that survives skeptical follow-up questions without requiring an MMM vendor or a data-science headcount.

The 2026 shift this skill operationalizes: attribution conversations have moved from "which model is correct" to "which decision can we defend," and finance teams now expect an explicit incrementality framing alongside every reallocation recommendation.

## When to Use

Use this skill at monthly or quarterly performance reviews, before budget reallocation conversations, when a single channel starts dominating credit (usually last-click), when leadership asks "is this channel actually working?", when a reported ROAS moves by more than 20% week-over-week, or when a channel-owner is defending budget and the blended picture needs a neutral voice. It pairs well with the `campaign-performance-narrator` skill, which turns the resulting analysis into a stakeholder narrative.

Do not use it to produce channel-attribution numbers for external reporting (analyst calls, board decks) without noting the model and its limits — this is a decision tool, not an audited revenue attribution statement.

## Minimum Viable Input

If the user provides only the three fields below, proceed immediately and tag every assumption `[ASSUMED]`:

1. **Spend + conversions by channel (one window)** — Even a sparse table is enough; flag missing CPA / ROAS / revenue cells rather than fabricating them
2. **Business model** — One line (e.g., "DTC subscription, 30-day cycle" or "B2B SaaS, 60–90-day cycle")
3. **One reallocation decision on the table** — The actual question the user is trying to answer (e.g., "Should we cut retargeting and move to TikTok?")

When running in MVI mode: default the attribution model to last-click with a visible caveat at the top; skip the 4-lens commentary on channels with <5% of spend; produce a single balanced scenario (no conservative/aggressive variants) plus a one-paragraph "what would change my mind"; ship one named measurement upgrade (always a 2-week geo holdout on the channel central to the decision); flag at the bottom the top 2 inputs that would most improve the analysis (typically: a known overlap map + the result of any prior incrementality test).

MVI mode produces a defensible 1-page reallocation recommendation in ~30 minutes vs. ~4 hours for the full analysis. The MVI output is sufficient for a single reallocation decision in a weekly performance review; it is not sufficient for a quarterly budget reset, a board-deck attribution claim, or a CFO-facing CAC/payback rewrite.

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

**Before you start — load `config.yml` and let it decide two things the analysis otherwise guesses: which measurement upgrade is actually runnable, and what the reallocation is optimizing *toward* (an attribution analysis that recommends a test the team's stack cannot run, or optimizes ROAS when the team is trying to fix payback, is a defensible-looking answer to the wrong question):**
- `tools` (analytics, testing, and CRM stack) — **gates the measurement-upgrade recommendation in step 5.** The step defaults to a geo-matched-markets holdout, but the runnable path depends on the stack: a GA360 team gets **Meridian-in-Analytics-360 + QFC** as a self-serve in-platform MMM (not "a 12-month vendor project"); a team with a lifecycle/ESP stack gets the near-free cell-level email holdout first; a team with no geo-experiment surface at all gets a server-side-conversion-validation upgrade before any holdout, because you cannot trust the lift number until the pipeline is clean. Name the upgrade in the team's actual tooling, and where the stack cannot run the ideal test, recommend the strongest test it *can* run and name the gap — a measurement upgrade the team cannot execute is shelfware, not a recommendation.
- `priorities.top_improvements` — **sets the reallocation objective (step 4) and breaks ties in the Scale / Maintain / Optimize / Cut verdicts (step 3).** A team whose named priority is "improve blended CAC / payback" gets a recommendation optimized on CAC-adjusted contribution, not raw ROAS; a team optimizing pipeline volume gets a different default scenario. State the objective the reallocation serves at the top, drawn from config, so the CMO paragraph argues in the finance team's actual terms.
- `services.customer_type` + business model + typical sales-cycle length — pre-fills Required Input 4 (the interpretation of every attribution signal hinges on cycle length; a 60–90-day B2B cycle and a 30-day DTC subscription read the same last-click table completely differently).
- primary channel mix — pre-fills the channel list in Required Input 1, so a sparse pasted table can be reconciled against the channels the team actually runs (a channel in config missing from the data is a data-completeness flag, not an absent channel).
- `pricing` posture and rates — ground truth for any CAC / payback / LTV math the reallocation leans on; bind it so the payback window is the team's real number, not an assumed one.
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
- **Meridian-in-Analytics-360 + QFC change the conversation for GA360 customers.** Google Marketing Live 2026 (May 20) put open-source Meridian MMM directly inside Analytics 360 and added Qualified Future Conversions as a Gemini-powered predictive metric. When the advertiser is on GA360, the MMM-refresh recommendation collapses from "12 months and a vendor engagement" to "self-serve in-platform." Naming the path (Meridian-in-Analytics-360, not "an MMM project") moves the conversation faster.
- **Agent-mediated traffic is now a measurement category.** Universal Cart (Search / Gemini app / YouTube / Gmail), UCP, Klarna Agent Mode, Amazon Buy for Me, Microsoft Copilot Checkout, and ChatGPT product-feed buys carve out a cohort where standard click-attribution breaks down — last-click reports the agent surface as the converter, but the upstream demand signal sits elsewhere. When >5% of converting traffic is agent-surfaced, segment that cohort and analyze it on its own plane.
- **ChatGPT Ads is now an attributable channel.** As of June 5, 2026 OpenAI's Ads Manager supports CPA / conversion-optimized campaigns with daily / lifetime budgets and granular US geo-targeting. CPM has drifted from $60 → ~$25 as inventory expanded. The cleanest attribution model for ChatGPT Ads in 2026 is a standalone geo holdout (not last-click platform reporting), because the upstream awareness lift compounds with the direct response click and naive credit double-counts.
- **iOS ATT / GA4 / cookie deprecation depresses digital conversion reporting by 15–25% systematically.** If reported ROAS dropped 15–25% without a known business reason, a measurement artifact is the first hypothesis. Audit the server-side conversion pipeline (Meta CAPI, Google Enhanced Conversions, GA4 event validation) before reallocating a single dollar.
- **Holdout test calibration: geo-matched-markets is the workhorse.** Cost is usually 5–10% of total channel spend over a 2-week window; produces a directional incrementality estimate within ±15% for branded paid search, retargeting, and most paid social cohorts. Cell-level holdouts on email and lifecycle are nearly free and the most underused test in 2026. Don't propose a customer-level or panel-based test when geo will answer the question for less.
- **The first-month-of-a-new-model rule.** When a measurement migration just landed (GA4 → GA4 360, cookie wave, server-side rollout, Meridian-in-Analytics-360 onboarding), default to the conservative reallocation scenario for the first 30 days regardless of signal direction. The variance in measurement transit periods routinely produces 20–30% noise on channel CPA reports.
- **The measurement upgrade must be runnable on the team's stack, or it is not a recommendation.** Step 5's default is a geo holdout, but the right upgrade is a function of `config.yml` `tools`: a GA360 team should be pointed at Meridian-in-Analytics-360 + QFC (self-serve, in-platform) rather than told to scope an MMM engagement; a team with an ESP but no geo-experiment surface should run the near-free cell-level email holdout first; a team whose conversion pipeline is unvalidated should fix server-side conversions (Meta CAPI, Enhanced Conversions, GA4 event validation) *before* any holdout, because a lift number off a leaky pipeline is worse than no number. Read the stack, name the upgrade in the team's own tooling, and when the ideal test is out of reach, prescribe the strongest test the stack can run and flag the gap — the most common failure of this skill is a beautifully-reasoned recommendation for a test the team has no way to execute.
- **Optimize toward the team's declared objective, not toward ROAS by default.** ROAS is the reflexive optimization target, but it is the wrong one for a team whose named priority (`config.yml` `priorities`) is blended CAC, payback period, or pipeline volume. A reallocation that lifts ROAS while lengthening payback can be exactly backwards for a team managing to a cash-payback constraint. State the objective the reallocation serves — pulled from config — at the top of the analysis, and let it break the ties in the Scale/Cut verdicts, so the CMO paragraph lands in the finance team's actual terms rather than a generic efficiency frame.

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
- **Pair with Agentic Commerce Optimizer** — the agent-mediated traffic cohort routinely shows up as a phantom-uplift in the last-click report; segment it on its own plane and analyze separately.
- **Pair with Customer Review Insight Miner** — VoC sentiment shifts often precede ROAS swings by 2–3 weeks; cross-reference suspect channel anomalies against the latest VoC delta scorecard before declaring a measurement artifact.
- **Pair with Topic Cluster Planner** — when branded search volume is reshuffling channel credit, the SEO/AEO content roadmap is the upstream lever; rotate the reallocation question into the cluster roadmap rather than treating it as a paid-budget question.
- **Pair with Brand Voice Guide Generator** — creative refresh cadence on a Scale verdict requires brand-voice consistency at higher volume; route brief-to-asset volume increases through the voice guide.

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
- Treating agent-mediated converting traffic (Universal Cart, UCP, ChatGPT product feed, Klarna Agent, Microsoft Copilot Checkout, Amazon Buy for Me) on the same plane as click-attributed traffic
- Reallocating in the first 30 days after a measurement migration (GA4 → GA4 360, cookie wave, server-side rollout, Meridian-in-Analytics-360 onboarding) without naming the noise band
- Recommending an MMM "project" to a GA360 customer when Meridian-in-Analytics-360 + QFC is now the self-serve in-platform path
