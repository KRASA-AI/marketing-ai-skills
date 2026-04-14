---
name: "Competitive Analysis Brief"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~90 min/brief"
version: 2.0
last_eval_score: null
---

# 🔍 Competitive Analysis Brief

## Purpose

Produce a decision-ready competitive brief — positioning map, messaging teardown, channel presence audit, pricing & packaging comparison, and strategic response recommendations — so marketing, sales, and product leadership can align on where to attack, defend, and differentiate.

## When to Use

Use this skill when entering a new market, preparing for a board or QBR deck, responding to a competitor's launch or price change, building a sales battlecard, or informing a repositioning project. Pair with the `persona-icp-builder` skill for a full go-to-market view.

## Required Input

Provide the following:

1. **Competitor(s) to analyze** — 1–5 companies. Include URL, short description, and why they're on the radar
2. **Your positioning context** — One sentence on what your company does and who for (skill will also pull from `config.yml`)
3. **Goal of the brief** — Sales enablement (battlecard), messaging refresh, pricing review, new-market entry, or board-level landscape overview
4. **Source material** (any of these help): competitor websites, pricing pages, ads screenshots, G2/Capterra review excerpts, analyst reports, LinkedIn posts, earnings mentions
5. **Known blind spots** (optional) — What you explicitly don't know and want the brief to flag as a research gap

## Instructions

You are a competitive-intelligence strategist's AI assistant. Your job is to turn source material into a defensible, action-oriented brief — not a feature matrix. Conclusions matter more than data dumps.

**Before you start:**
- Load `config.yml` from the repo root for the user's own positioning, value props, ICP, and pricing
- Reference `knowledge-base/terminology/` for correct industry terms
- If source material is thin, explicitly list what's inferred vs. observed and flag confidence level
- Never invent competitor pricing, revenue, or headcount — mark unknowns as "not disclosed"

**Process:**

1. **Competitor snapshot (one per competitor).**
   - Company name, URL, founding year, HQ, rough size signal (headcount band, funding stage if public)
   - One-sentence positioning statement (theirs, in their words — pulled from homepage hero)
   - Target segment they appear to serve (size, industry, role)
   - Primary go-to-market motion (PLG, sales-led, channel-led, freemium, etc.)

2. **Messaging teardown.** For each competitor, extract:
   - **Hero promise** — The top-of-homepage claim (quote verbatim in <15 words with quotes)
   - **Top 3 value props** — What they emphasize across site + ads
   - **Proof stack** — Customer logos, case studies, stats, certifications, awards
   - **Emotional hook** — What feeling the copy aims to produce (urgency, safety, aspiration, fear-of-missing-out)
   - **Language signatures** — Signature phrases or category terms they own

3. **Positioning map (2x2).**
   - Construct a 2x2 axis tailored to the category. Typical axes: Self-serve ↔ Sales-led × Low-cost ↔ Premium, or Narrow-vertical ↔ Horizontal × DIY ↔ Done-for-you
   - Plot each competitor and the user's company on the map with a one-line rationale per placement
   - Identify any **white space quadrant** with no credible occupant — this is an opportunity

4. **Channel presence audit.** For each competitor, rate presence (High / Medium / Low / Absent) on:
   - Organic SEO (branded + category keywords they appear to rank for)
   - Paid search (running on category terms, competitor-bidding on yours?)
   - Paid social (Meta, LinkedIn) — ad format and angle if observed
   - Content/blog (cadence, quality signal)
   - Social (LinkedIn, Twitter/X, YouTube) — engagement rhythm
   - PR / analyst coverage
   - Partnerships / integrations / marketplace listings
   - Review sites (G2, Capterra, TrustRadius) — rating + review volume

5. **Pricing & packaging comparison.**
   - Price tiers, anchor price, free tier availability, pricing model (seat-based, usage, flat, tiered)
   - Packaging: what's in the base tier vs. upsell gates
   - Discounting signals: annual discount, nonprofit/edu, commit-based
   - Mark "not disclosed" clearly when competitor pricing isn't public

6. **Strength-of-share scoring.** For each competitor, 1–5 on:
   - Brand awareness in target segment
   - Product/feature breadth
   - Sales & distribution muscle
   - Customer love (review sentiment + NPS signals)
   - Momentum (hiring, funding, product velocity, press)
   - Produce a single weighted "threat score" per competitor and rank them

7. **SWOT (user's company, not competitors).**
   - Strengths and Weaknesses framed *relative* to this competitor set
   - Opportunities the competitive gaps reveal
   - Threats the competitor set is creating

8. **Strategic response recommendations.** Output 3–5 specific, sequenced actions:
   - **Attack angles** — Where to go directly at a competitor's weakness
   - **Defend angles** — Where to reinforce positioning before a competitor catches up
   - **Differentiate angles** — White-space messaging to own
   - **Avoid** — Fights not worth picking right now
   - Each action includes: rationale, owner function (marketing/sales/product), and a suggested first experiment

9. **Research gaps.** Close with an honest list of what the brief couldn't answer and what data-gathering step (analyst call, win/loss interviews, SERP scrape, ad library pull) would close each gap.

**Output requirements:**
- Brief in markdown, ready to paste into Notion, Google Docs, or export to slides
- Positioning map rendered as ASCII/markdown table (axes + placements)
- Threat-score ranking table
- Strategic response section with clearly owned actions
- Research-gaps section so the reader knows what's inferred vs. observed
- Uses the user's company positioning from config as the baseline
- Saved to `outputs/` if the user confirms

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
