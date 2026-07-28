---
name: "Competitive Analysis Brief"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~90 min/brief"
version: 2.3
last_eval_score: 9.5
---

# 🔍 Competitive Analysis Brief

## Purpose

Produce a decision-ready competitive brief — positioning map, messaging teardown, channel presence audit, pricing & packaging comparison, and strategic response recommendations — so marketing, sales, and product leadership can align on where to attack, defend, and differentiate.

## When to Use

Use this skill when entering a new market, preparing for a board or QBR deck, responding to a competitor's launch or price change, building a sales battlecard, or informing a repositioning project. Pair with the `persona-icp-builder` skill for a full go-to-market view.

## Minimum Viable Input

If the user provides only the three fields below, proceed immediately with the brief and tag every inferred item `[INFERRED]` and every confidence-limited data point `[UNVERIFIED]`. Do not ask for more information upfront.

1. **Competitor(s)** — Company name(s) and URL(s); 1–5 max. If `config.yml` declares a `competitors` set, that *is* the default subject list — the user only needs to confirm, add, or drop rather than re-type it
2. **Your positioning context** — One sentence on what your company does and who for (pulled from `config.yml` `value_props` + positioning where present, so the user's own side is not re-typed)
3. **Goal of the brief** — Pick one: battlecard / messaging refresh / pricing review / new-market entry / board landscape

When running in MVI mode: load `config.yml` first so the competitor set, the user's positioning baseline, and the user's pricing are pre-filled and only the competitors' public side is researched; then scrape publicly available signals (homepage hero, pricing page, G2 rating + review count, LinkedIn headcount band, recent press), infer GTM motion from product + pricing page signals, and label every inference. If a competitor has no public pricing, mark "not disclosed" — do not guess. Ask the user at the end of the output to confirm or correct the three highest-impact inferred items.

**Brief-type shortcuts.** Based on the goal, the following steps are emphasized or abbreviated:

| Goal | Emphasize | Abbreviate |
|---|---|---|
| **Battlecard** | Attack / defend / avoid actions (step 8); threat-score ranking (step 6); messaging teardown (step 2) | Pricing detail (step 5); founding history (step 1) |
| **Messaging refresh** | Messaging teardown (step 2); positioning map (step 3); language signatures (step 2) | Pricing (step 5); strength-of-share scoring (step 6) |
| **Pricing review** | Pricing & packaging (step 5); strength-of-share scoring (step 6) | Messaging teardown (step 2); positioning map (step 3) |
| **New-market entry** | Positioning map white space (step 3); channel presence (step 4); SWOT (step 7) | Pricing (step 5 — do a light pass only) |
| **Board landscape** | Threat-score ranking (step 6); SWOT (step 7); strategic response (step 8) | Messaging teardown (step 2 — headline only per competitor) |

## Full Required Input

Provide the following for the highest-fidelity brief:

1. **Competitor(s) to analyze** — 1–5 companies. Include URL, short description, and why they're on the radar
2. **Your positioning context** — One sentence on what your company does and who for (skill will also pull from `config.yml`)
3. **Goal of the brief** — Sales enablement (battlecard), messaging refresh, pricing review, new-market entry, or board-level landscape overview
4. **Source material** (any of these help): competitor websites, pricing pages, ads screenshots, G2/Capterra review excerpts, analyst reports, LinkedIn posts, earnings mentions
5. **Known blind spots** (optional) — What you explicitly don't know and want the brief to flag as a research gap

## Instructions

You are a competitive-intelligence strategist's AI assistant. Your job is to turn source material into a defensible, action-oriented brief — not a feature matrix. Conclusions matter more than data dumps.

**Before you start — load `config.yml` and let it pre-fill the brief's subject set and its baseline, not just the voice (a competitive brief that asks the team to re-type the competitor list config already holds, and then plots the user's company from imagination, is a brief that measures the wrong set against the wrong baseline):**
- `competitors` — **pre-fills the competitor set (Required Input 1 / the MVI competitor field).** Present the config list and ask only which to add or drop for *this* brief, rather than asking the team to name competitors from scratch. Two higher-value moves fall out of this binding: (a) if the goal skill is run alongside the **AI Search Visibility Audit** and an engine names a competitor that `config.competitors` does not, surface it as a **competitive-set drift finding** — the market is positioning a rival into your category that your own competitor list has not caught up to, and that finding is often worth more than the threat-score table itself; (b) a competitor in config that no longer appears in any channel, review site, or engine answer is a candidate to *retire* from the watch set, which keeps the brief force-ranked instead of sprawling.
- `value_props` + positioning statement — **the baseline the whole brief plots against.** The "Our company" column in the messaging teardown (step 2), the user's placement on the positioning map (step 3), and the SWOT's strengths/weaknesses (step 7) are all drawn *relative* to this. Do not synthesize the user's own positioning from the competitor set; load it from config so the brief argues from the positioning the team actually decided, and flag any place a competitor already owns a `value_prop` the team believes is theirs.
- `pricing` — the user's own tier, model, and anchor are ground truth for the pricing & packaging comparison (step 5); config supplies your side of the table so only the competitors' side is inferred (and marked "not disclosed" where it isn't public).
- `services.core` / `services.customer_type` — the ICP and category frame that should drive the positioning-map **axis choice** (step 3, the highest-leverage decision in the exercise) and the segment lens for the SWOT. Axes should be drawn in terms that cost *these* competitors a trade-off in *this* ICP, not generic 2x2s.
- `priorities.top_improvements` / `priorities.pain_points` — **break ties in the strategic-response ranking (step 8).** Where two responses score similarly, the one that advances the team's named priority (e.g., "win more competitive displacements," "raise win rate against [named rival]") is sequenced first, and the brief says so.
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

- **Positioning maps are tools for argument, not truth.** The axis choice is the highest-leverage decision in the whole exercise. If one axis is "has an AI feature," you have produced a competitor comparison, not a positioning map. Pick axes that cost the competitor a trade-off to switch — axes where moving toward one pole requires moving away from the other.
- **Threat-score rankings drift.** A competitor that was #4 on threat six months ago is often #2 today because of a funding round, a product velocity change, or an analyst placement. Re-run at least quarterly and diff against the prior score explicitly. A delta of +1.5 or more in a single quarter is a pipeline-threat signal.
- **Resist the "everyone is a threat" collapse.** If the brief lists 7 competitors all at threat score 4, it is not yet a brief. Force-rank to a top 2–3 and name the criteria that separate them. The most useful competitive brief disagrees with someone's prior assumption about which competitor to watch.
- **Customer love outranks feature breadth as a churn-threat predictor.** Review sentiment and NPS signals are stronger predictors of competitive displacement than raw feature counts. A competitor with 4.7 stars on G2 at 200+ reviews and a feature set 30% narrower than yours is a bigger retention threat than a competitor with 4.2 stars and a full feature matrix.
- **Do not conflate market leader with threat leader.** The largest competitor is sometimes slow enough to be the easiest to attack. The #3 challenger closing fast — higher G2 momentum score, new funding, accelerating hiring — is often the bigger medium-term threat. Track velocity, not just position.
- **A research gap is a deliverable.** If pricing is not disclosed, the brief's job is to say so and name what would close the gap (RFP bid, analyst call, win/loss interview), not to guess. Named research gaps are more useful than confident estimates based on thin data.
- **AI-engine citation share is now a tier-1 competitive signal.** Run the **AI Search Visibility Audit** skill first and bring its Share-of-Model numbers into the brief. A competitor cited 3× more often in ChatGPT or Perplexity on category-leader questions is a pipeline threat even if their organic site traffic looks flat — they are being recommended before the buyer reaches your website.
- **The config competitor set is a prior to pressure-test, not a fence.** Loading `config.yml` `competitors` as the pre-filled subject list is what stops the brief from analyzing a set the team typed from memory — but the highest-value output of that binding is the *mismatch*: a rival the engines, review sites, or paid-SERP scrape keep naming that config does not list is a **competitive-set drift finding**, and it usually means the market has re-drawn the category faster than the watchlist. Surface it explicitly ("named by ChatGPT on 4/10 category questions; absent from `config.competitors` — recommend adding to the watch set"). The inverse is also a finding: a config competitor that has gone quiet across every channel is a candidate to retire, which keeps the force-rank honest. The config set decides where the brief *starts*; the drift check decides whether the set is still right.
- **Seer Interactive May 2026 (25.1M impressions):** 93% AI Mode zero-click rate; organic CTR drops 61% on AI-feature SERPs. Competitors who appear in AI-engine answers are reaching buyers who will never show up in your competitor's GA4 organic traffic data — which means traditional traffic-based competitive analysis systematically underestimates AI-first competitors.
- **Avoid static feature checklists.** Feature parity is table stakes in 2026; the threat story lives in proof stack depth, category language ownership, channel presence, and AI-engine citation share — not in a ✅ / ❌ grid. A feature checklist is a comparison; a positioning map is a brief.
- **The messaging teardown's most actionable output is the language signatures section.** Competitor brands that own specific phrases in the category ("revenue intelligence," "predictive pipeline," "deal room") have established a category-language moat. If those phrases appear in your copy too, you are reinforcing their category ownership. Find the phrase they cannot own and build your content strategy around it.
- **Proof stack depth predicts premium pricing power.** Competitors with 10+ named customer logos, 3+ analyst mentions, and G2 category leader badges can charge 20–40% more than feature-equivalent competitors. Assess proof stack depth as a strategic dimension, not just a marketing signal.
- **Brief-type calibration: battlecard vs. board brief.** A battlecard should be one page — it will be read on a phone 60 seconds before a discovery call. A board brief should be five pages — it needs to hold up to scrutiny from a CFO. The same competitive data serves both, but the emphasis and depth differ; use the brief-type shortcuts to allocate depth correctly.
- **Re-run cadence:** Quarterly for active competitive landscapes (3+ well-funded competitors); semi-annually for stable categories. If a competitor closes a major funding round or ships a product that directly targets your ICP, trigger an unscheduled re-run within 30 days.
- **The SWOT's "Opportunities" section is the brief's highest-value cell.** Most competitive briefs under-invest in the white-space analysis. The positioning map white space is a content-territory and messaging-territory opportunity — feed it directly into the Topic Cluster Planner and Brand Voice skill.
- **Win/loss data is the ground truth that benchmarks synthetic competitive signals.** If your CRM has 20+ documented win/loss interviews, pull them before running this skill. Competitive positioning that contradicts win/loss data should flag a research-gap item, not silently override it.

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
