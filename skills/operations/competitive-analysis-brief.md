---
name: "Competitive Analysis Brief"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~90 min/brief"
version: 2.1
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

## Calibration Notes

- Positioning maps are tools for *argument*, not *truth*. The axis choice is the highest-leverage decision in the whole exercise. If one axis is "has an AI feature," you have produced a competitor comparison, not a positioning map. Pick axes that cost the competitor a trade-off to switch.
- Threat-score rankings drift. A competitor that was #4 on threat six months ago is often #2 today because of a funding round, a product velocity change, or an analyst placement. Re-run at least quarterly and diff against the prior score explicitly.
- Resist the "everyone is a threat" collapse. If the brief lists 7 competitors all at threat score 4, it is not yet a brief. Force-rank to a top 2–3.
- The "customer love" signal on G2 / Capterra is usually stronger than feature breadth as a predictor of churn threat. Weight review sentiment and NPS signals higher than raw review count.
- Do not conflate market leader with threat leader. The largest competitor is sometimes slow enough to be the easiest to attack. The #3 challenger closing fast is often the bigger medium-term threat.
- A research gap is not a failure — it is a deliverable. If pricing is not disclosed, the brief's job is to *say* it is not disclosed and name what would close the gap (RFP bid, analyst call, win/loss interview), not to guess.
- AI-engine citation share is now a viable competitive signal. Run the **AI Search Visibility Audit** skill first and bring its Share-of-Model numbers into the brief; a competitor citing 3× more often in ChatGPT on category-leader questions is a pipeline threat even if their site traffic looks flat.
- Avoid static feature checklists. Feature parity is table stakes in 2026; the threat story lives in proof stack depth, category language, and channel presence — not in a ✅ / ❌ grid.

## Example Output

### Competitor Snapshot — "Acme Analytics" (sample)

- **Who they are:** Seed-stage (raised $12M Series A in Feb 2026), 40 employees, HQ Austin, shipped in 2023.
- **Positioning (theirs):** "Revenue intelligence for the unfair advantage."
- **Target segment:** Mid-market B2B SaaS, 50–500 employees, RevOps-led purchase.
- **GTM motion:** Product-led with sales assist above $25k ACV. Free tier gated at 5 seats.

### Messaging Teardown

| Dimension | Acme Analytics | Our company |
|---|---|---|
| Hero promise | "Revenue intelligence for the unfair advantage" | "Unified pipeline reporting in 14 days" |
| Top 3 value props | Speed-to-insight, CRM-native install, AI-powered recommendations | Data lineage, Salesforce-native, fast deployment |
| Proof stack | 3 named mid-market logos, 2 G2 badges, 1 analyst inclusion | 5 named logos, Salesforce ISV listing, 1 case study |
| Emotional hook | Aspiration + urgency ("unfair advantage") | Relief + competence ("you'll look good in QBR") |
| Language signatures | "Revenue intelligence," "predictive pipeline" | "Unified pipeline," "clean data lineage" |

### Positioning Map (Self-serve ↔ Sales-led × Narrow-vertical ↔ Horizontal)

```
                    Sales-led
                       ↑
       [LegacyCo]      |     [Enterprise Inc.]
                       |
Narrow ←———————————————+——————————————————→ Horizontal
                       |
       [Us]            |     [Acme Analytics]
                       |     [ChallengerBrand]
                       ↓
                   Self-serve
```
White space: narrow-vertical × self-serve quadrant is uncontested. This is the opportunity the brief recommends defending and owning.

### Threat-Score Ranking

| Competitor | Brand | Product | Sales muscle | Customer love | Momentum | Weighted threat |
|---|---|---|---|---|---|---|
| Acme Analytics | 3 | 4 | 3 | 4 | 5 | 3.8 |
| Enterprise Inc. | 5 | 4 | 5 | 3 | 2 | 3.8 |
| ChallengerBrand | 2 | 3 | 2 | 4 | 4 | 3.0 |
| LegacyCo | 5 | 3 | 5 | 2 | 1 | 3.2 |

### Strategic Response (3–5 actions)

1. **Attack — Acme's speed claim.** Publish a named-customer "14-day deployment" case study with a video quote. Owner: Marketing. First experiment: landing page hero test against control, 4-week window.
2. **Defend — Salesforce-native positioning.** Acme markets as "CRM-native;" we have the deeper integration. Add AppExchange badge above the fold and a ranked partner listing. Owner: Product Marketing + BD.
3. **Differentiate — Own "clean data lineage" language.** Neither Acme nor Enterprise Inc. credibly claim lineage. Build a pillar page + audit-ready proof and feed it to the Topic Cluster Planner.
4. **Avoid — ChallengerBrand's price war.** They are racing to the bottom on freemium. Holding pricing firm and differentiating on service is the defensible posture.
5. **Watch — Acme's momentum.** 3.8 weighted threat driven mostly by momentum (5/5). If hiring slows or funding stalls, threat drops. Revisit in 60 days.

### Research Gaps
- Pricing above Acme's $49/seat published tier is not disclosed — close via win/loss interviews
- Acme's ad spend scale is inferred from SpyFu estimates (confidence: medium); confirm with Meta Ad Library + paid-SERP scrape
- NPS signal for Enterprise Inc. is based on 18 recent G2 reviews — a thin sample; flag as low confidence

## Integration Notes

- **Pair with AI Search Visibility Audit** — competitor SoM becomes the strongest modern threat signal; route gaps into this brief.
- **Pair with Persona & ICP Builder** — positioning axes should be drawn in terms that matter to the ICP, not to the product team.
- **Pair with Topic Cluster Planner** — white-space messaging opportunities become content-territory assignments.
- **Feed into Ad Copy Variations** — attack angles become A/B test copy directly.
- **Feed into Battlecard workflow (sales enablement)** — threat ranking + attack / defend / differentiate / avoid framework is the spine of a sales battlecard.
- **Escalate to Brand Safety & Crisis Response Planner** — if a competitor is running negative-framing comparison content against our brand in paid channels, that is a tier-2 monitoring signal.

## Anti-Patterns to Avoid

- Feature-matrix grids presented as strategy
- Axes on the positioning map that both slide toward "we are better"
- Ranking all competitors evenly to avoid picking a fight
- Quoting a competitor's hero claim as proof they are winning the category (claims are cheap, proof is scarce)
- Citing pricing as "public" when it was only inferred from a sales demo
- Skipping the research-gaps section (the brief's credibility dies if every claim is presented as known)
- Writing for the executive audience and forgetting that sales will use the same brief in the field — add a battlecard-style one-pager if sales is an audience
