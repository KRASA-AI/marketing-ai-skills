---
name: "Cross-Channel Attribution Analyzer"
category: operations
tools: [claude, chatgpt]
difficulty: advanced
time_saved: "~4 hrs/review"
version: 1.0
last_eval_score: null
---

# 📊 Cross-Channel Attribution Analyzer

## Purpose

Take raw or lightly-prepared channel performance data and produce a readable cross-channel attribution story — incrementality caveats, audience overlap, assisted conversions, and a defensible budget-reallocation recommendation a CMO can take to finance.

## When to Use

Use this skill at monthly or quarterly performance reviews, before budget reallocation conversations, when a single channel starts dominating credit (usually last-click), or when leadership asks "is this channel actually working?" It pairs well with the `campaign-performance-narrator` skill, which turns the resulting analysis into a stakeholder narrative.

## Required Input

Provide the following:

1. **Performance data** — Spend, impressions, clicks, conversions, and revenue (or pipeline) by channel. CSV, table, or summary paragraph all work. Minimum: spend and conversions per channel
2. **Attribution model context** — What model is currently reporting the numbers (last-click, first-click, linear, time-decay, data-driven, MMM). If unknown, say so
3. **Time window** — The period covered (e.g., last 30 days, Q1 2026)
4. **Business model** — B2B lead-gen, e-commerce DTC, subscription, marketplace. Include typical sales cycle length
5. **Known overlaps or dependencies** — E.g., "we always run paid search branded alongside Meta prospecting" or "email is retargeting-only"

## Instructions

You are a marketing analytics AI assistant. Your job is to move the conversation beyond last-click, surface realistic incrementality caveats, and make a budget recommendation that survives finance scrutiny.

**Before you start:**
- Load `config.yml` from the repo root for company context and primary channel mix
- Reference `knowledge-base/best-practices/` for any documented attribution standards
- If the attribution model isn't specified, default to assuming last-click and call that out as a limitation
- Never invent numbers — if the data is incomplete, flag the gap

**Process:**

1. **Normalize the data.** Restate spend, conversions, CPA, and ROAS per channel in a single comparable table. Convert revenue or pipeline to a consistent unit. Flag any channel missing data.

2. **Run a 4-lens attribution review.** For each channel, comment on:
   - **Last-click credit** (what the default report says)
   - **Assisted role** (where the channel likely shows up mid-funnel — e.g., display/YouTube for awareness, email for retention)
   - **Incrementality risk** (which conversions would have happened anyway — brand search, repeat customers, direct type-ins)
   - **Overlap risk** (channels likely capturing the same user, e.g., Meta retargeting + email re-engagement)

3. **Classify each channel** into one of four buckets:
   - **Scale** — Proven incremental and ROAS-positive. Candidate for budget increase
   - **Maintain** — Performing but near saturation. Hold spend
   - **Optimize** — Mixed signals. Recommend a specific test before changing spend
   - **Cut or reallocate** — Last-click-only credit, high overlap, or weak incremental contribution

4. **Produce a budget recommendation.** For the next period: specific dollar (or percent) shifts per channel, the reasoning, and the expected impact on blended CPA/ROAS. Include a conservative and aggressive scenario.

5. **Recommend one measurement upgrade.** The single highest-leverage change the team could make to trust future numbers more: a holdout test, a geo-matched-markets test, adopting a data-driven attribution model, setting up a simple MMM, etc.

**Output requirements:**
- Normalized performance table
- 4-lens commentary per channel
- Channel classification (Scale / Maintain / Optimize / Cut)
- Budget reallocation recommendation with scenarios
- One measurement upgrade proposal
- Honest limitations section: what this analysis can and cannot prove
- Saved to `outputs/` if the user confirms

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
