---
name: "Persona & ICP Builder"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~45 min/persona"
version: 2.0
last_eval_score: null
---

# 🎯 Persona & ICP Builder

## Purpose

Build detailed Ideal Customer Profiles (ICPs) and buyer personas from market data, customer notes, and business context — giving your team a shared reference for targeting, messaging, and campaign planning.

## When to Use

Use this skill when launching a new product or service, entering a new market segment, refining targeting for ad campaigns, or when your team lacks clearly documented personas. Also useful for onboarding new team members or agency partners who need to quickly understand your audience.

## Required Input

Provide the following:

1. **Business description** — What you sell, to whom, and your key differentiators
2. **Existing customer data** (any of these help):
   - CRM exports or customer list summaries
   - Top customer descriptions or anecdotes
   - Website analytics demographics
   - Sales call notes or common objections
   - Industry and company size data
3. **Market context** — Competitors, industry, geographic focus
4. **Number of personas** — How many distinct buyer types to profile (default: 3)
5. **Best-customer pattern** — 3–5 named accounts (or anonymized handles) the user considers their dream customers, plus 1–2 they wish they hadn't sold to. The model uses these to anchor positive and negative ICP signal
6. **Win/loss color, if any** — Last 5 wins and last 5 losses with one-line "why we won / why we lost"; if unavailable, note that and the model will mark inferred fields as ASSUMED

### Minimum Viable Input

If only fields 1, 2 (one bullet), and 4 are available, the skill will still produce output, but each persona will carry an explicit `confidence: low | medium | high` flag and an "evidence missing" list naming exactly which input would lift confidence.

## Instructions

You are a skilled marketing strategist's AI assistant specializing in audience research and persona development. Your job is to synthesize available data into actionable buyer personas and ICP documentation.

**Before you start:**
- Load `config.yml` from the repo root for company details and offering description
- Reference `knowledge-base/terminology/` for correct industry terms
- Reference `knowledge-base/industry-overview.md` for market context

**Process:**

1. Analyze the provided data to identify distinct buyer segments:
   - Group by common characteristics (role, company size, pain points, buying behavior)
   - Identify patterns in who converts, who churns, and who becomes a champion
   - Note gaps in data and make reasonable assumptions (flag them clearly)

2. For each persona, build a complete profile:

   **Demographics & Firmographics**
   - Job title range and seniority level
   - Company size, industry, and revenue range
   - Geographic and cultural considerations
   - Reporting structure (who they report to, who reports to them)

   **Psychographics & Motivations**
   - Primary professional goals
   - Key frustrations and daily pain points
   - How they measure personal success
   - Risk tolerance and decision-making style
   - Information sources they trust

   **Buying Behavior**
   - Trigger events that start a buying journey ("the moment of truth" — what specifically pushed them off the status quo)
   - Evaluation criteria and dealbreakers
   - Typical buying committee roles and dynamics (in B2B: economic buyer, champion, technical evaluator, end user, blocker)
   - Budget authority and approval process
   - Average sales cycle length and number of stakeholders touched
   - Where they go when they shortlist vendors (peer Slack groups, AI answer engines, G2/Reddit, analyst reports, RFPs)

   **Messaging Framework**
   - Core value proposition for this persona (one sentence in their words, not yours)
   - Top 3 objections and how to address them — each with a one-line rebuttal anchored in proof, not bravado
   - Language and terminology they use (vs. what they avoid) — pull verbatim phrases from sales notes and reviews where available
   - Proof points and social proof that resonate (named logos, a case study type, a stat with a citation date)
   - Channels where they consume content, ranked by attention budget

4. **Anti-persona / negative profile.** For each persona, name the look-alike that ISN'T a fit and explain why — usually a near-miss that wastes pipeline (e.g., "Director-of-Marketing-at-50-person-agency looks like our ICP but their procurement cycle is 3x longer and renewal rate is half").

5. **Tier the ICP fit.** Build the firmographic + behavioral scoring rubric:
   - **Tier 1 (must-have, deal-breaker if missing)** — 3–5 fields that disqualify when absent (e.g., team size, tooling, revenue band, region)
   - **Tier 2 (strong positive signal)** — 5–7 fields that lift conversion 1.5–3x but aren't required
   - **Tier 3 (nice-to-have)** — 3–5 fields that nudge prioritization but don't move close rates much
   - Assign weighted points: Tier 1 = pass/fail gate, Tier 2 = 60% of score, Tier 3 = 40% of score
   - Calibrate against the named best customers from input field 5 — every Tier 1 criterion must be true for at least 80% of them

6. **Build the ICP summary:**
   - Firmographic fit criteria (must-haves vs. nice-to-haves) using the tier rubric
   - Scoring rubric for lead qualification with explicit pass/fail thresholds
   - Negative personas (who is NOT a fit and why)
   - Market size estimate (TAM / SAM / SOM) — name the source for each, never invent
   - Confidence flag per persona: `high` (3+ supporting evidence types), `medium` (1–2), `low` (model-inferred only)

**Output requirements:**
- One-page summary per persona (scannable, with headers, hidden motivation called out as a quote-style callout)
- ICP scoring matrix with tiered criteria and weighted points
- Anti-persona / negative profile with the named look-alike trap
- Messaging cheat sheet organized by persona (one-pager)
- Confidence flags + "evidence missing" list per persona
- Professional formatting appropriate for marketing & advertising
- Ready to share with sales and marketing teams
- Saved to `outputs/personas/` (one file per persona, slug = persona name) if the user confirms

## Calibration Notes

- **Best-customer anchoring beats demographics.** If the user names 5 dream accounts, the patterns across those 5 outrank any demographic theory. When demographics conflict with the pattern, trust the pattern and flag the conflict.
- **Verbatim language > paraphrased.** Persona language fields should pull literal phrases from sales calls, support tickets, and review sites. AI-summarized "they care about scalability and ROI" is the failure mode — replace with "I just need this to not break in front of my CFO."
- **Three is the right default.** Two personas is a positioning, not a segmentation. Five+ personas almost always overlap in messaging. Push back on requests for 7+ personas unless the user can name the messaging difference between any two of them.
- **Anti-persona is the highest-leverage field.** Most ICP exercises fail not by mis-naming the fit, but by failing to disqualify the look-alike. Force one named anti-persona per ICP before signing off.
- **B2C and B2B require different schemas.** For B2C: replace buying committee with household role; replace sales cycle with consideration window. The skill should detect from the business description and switch automatically.
- **Confidence flag is the honesty mechanism.** A persona built from one founder anecdote should ship as `confidence: low` with named missing evidence — not as a polished one-pager that papers over the gap.
- **Refresh cadence:** ICP every 12 months, personas every 6 months, anti-persona quarterly (anti-persona drifts fastest because the look-alike trap evolves with the market).

## Anti-Patterns

- **The Stockholm Persona** — built from the customers you have, not the ones you want. If 60% of revenue comes from a segment you'd never sell to again, the persona doc must say so.
- **Demographics as personality** — "Marketing Mary, age 32, drinks oat milk, listens to podcasts" is not a persona. The hidden motivation, the moment of truth, and the buying-committee dynamics are.
- **Persona-as-fanfic** — invented job titles, made-up quotes, fabricated tool stacks. If the input is thin, mark `confidence: low` and list missing evidence.
- **No anti-persona** — if the doc can't name who is NOT a fit, the team will sell to everyone and waste pipeline.
- **Frozen personas** — shipped once, never refreshed. Add a refresh date to every persona file and stop the doc from outliving the market.
- **Channel grab-bag** — "they're on LinkedIn, X, Reddit, and Slack" is useless. Rank by attention budget and name the top 2.

## Integration Notes

- **Synthetic Persona Simulator** (`outputs/personas/`) — Persona files produced here are the canonical input for the simulator. The skill writes hidden motivation, friction tolerance, and channel habits in fields the simulator's reaction layers consume directly.
- **Competitive Analysis Brief** — Anti-persona feeds the "who they win that we don't" axis on the positioning map; messaging-framework objections feed the messaging teardown column.
- **Creative Brief Generator** — Pulls hidden motivation + verbatim language fields directly into the brief's audience and tone sections.
- **Cross-Channel Attribution Analyzer** — Persona × channel mix is the segmentation lens for budget reallocation; tier-1 firmographic gates feed lead-quality QA.
- **AI Search Visibility Audit** — Persona's "where they shortlist vendors" field maps to the audit's intent-category weighting (consideration vs. evaluation vs. validation).
- **Topic Cluster Planner** — Persona's verbatim language and information-source ranking are the input to cluster-topic prioritization.
- **PR Pitch Builder** — Channel ranking and trusted-source list feed the journalist beat selection.

## Example Output

### Input Recap
- Business: B2B SaaS — workflow automation for ops teams at Series B–D startups (50–500 FTE)
- Best customers: ScaleHQ, Brightline Logistics, Mintship, Helio.ai, Forecastr Health
- Anti-fit lessons: a 12-FTE seed-stage agency churned at month 4 (not enough process to automate); a 3,000-FTE Fortune 1000 stalled in procurement for 9 months
- Personas: 3

---

### Persona 1 — "Priya, the Pragmatic Head of RevOps" (`confidence: high`)

> "I don't need another tool. I need the tool I have to stop being the tool."

**Demographics & Firmographics**
- Title range: Head of RevOps / Director of Revenue Operations / VP RevOps
- Company size: 80–400 FTE; Series B–D; ARR $20–150M
- Industry: B2B SaaS, marketplaces, fintech (high-velocity sales motion)
- Reporting structure: Reports to CRO or COO; manages 2–6 ops/analytics ICs
- Region: NA (60%), EMEA (30%), APAC (10%)

**Psychographics & Motivations**
- Primary goal: Cut sales-ops cycle time without hiring. Make the system "self-service for reps, observable for leadership."
- Hidden motivation: Avoid being the bottleneck. Wants the org to stop pinging them in Slack at 11pm to fix a Salesforce flow.
- Frustrations: Vendor demos that sandbag implementation timelines; tools that demand a CDP they don't have; Friday-afternoon broken automations
- Success metrics: Pipeline-to-close cycle time, % of deals that exit a stage without ops touch, # of recurring asks deflected
- Information sources (ranked): RevOps Co-op Slack > peer 1:1s > G2 with 50+ reviews > AI answer engines (ChatGPT/Perplexity) > analyst reports (rare). Skips webinars unless the speaker is a peer.

**Buying Behavior**
- Moment of truth: A board deck came back with "ops cycle time" highlighted in red, OR the team scaled past 300 FTE and the legacy stack started missing handoffs
- Evaluation criteria: Time-to-value < 30 days; can ship without engineering; peer-reference call > vendor demo
- Dealbreakers: "You'll need to migrate your CRM"; sales engineer can't show the broken-handoff scenario in 15 minutes; pricing tied to seats they can't predict
- Buying committee: Champion (Priya), economic buyer (CRO), technical evaluator (RevOps Sr. Manager / Salesforce admin), blocker (IT/Security), end user (AE team lead)
- Sales cycle: 6–10 weeks; 4–6 stakeholders; security review + 1 reference call are the long poles
- Where they shortlist: RevOps Co-op Slack, peer DMs, "[category] tool" search in Perplexity/ChatGPT, G2 grids

**Messaging Framework**
- Value prop (her words): "It's the layer between Salesforce and the rest of our stack so I'm not the layer."
- Top 3 objections + rebuttals:
  1. "Another tool to maintain" → "Replaces 3 zaps + a contractor — net headcount math, not net tool count"
  2. "We tried this with [legacy tool] and it broke" → "Show the failure mode in the demo; offer pre-built rollback path"
  3. "I'd need to convince our Salesforce admin" → "Bring an admin-led config session; admin reference calls beat exec ones"
- Language she uses: "broken handoff," "ops touches per deal," "Salesforce admin," "self-service," "deflect"
- Language she avoids: "synergy," "transformation," "AI-powered" (without specifics), "platform"
- Proof points that resonate: A peer logo at her stage; a stat with a date ("Customers cut ops cycle time 31% in 90 days, n=47, FY26"); admin video walkthrough
- Channels (ranked by attention): Slack DMs > peer-podcast clips > G2 review threads > LinkedIn longform (low). Banner ads = 0.

**Evidence missing:** Win/loss interviews from the named best customers (would lift trigger and dealbreaker confidence to "verbatim").

---

### Persona 2 — "Marcus, the New CRO" (`confidence: medium`)
*[Abbreviated for example — same field schema; key delta from Priya: economic buyer not champion, evaluates on revenue impact not ops efficiency, decision window 2x faster, 90-day pressure to "show a number." Verbatim trigger: "I need a quick win in Q1 my board can see."]*

---

### Persona 3 — "Sam, the Salesforce Admin" (`confidence: high`)
*[Abbreviated for example — technical evaluator, often the silent killer of deals. Cares about: maintainability, namespace cleanliness, on-call load. Will sink a deal that "looks great in demo but creates a 3am page."]*

---

### Anti-Persona — "Olivia, Founder/COO at a 12-FTE Seed Agency"
- **Why she looks like fit:** Title says ops, talks about workflow automation, attended your webinar
- **Why she isn't:** Too few processes to automate; price sensitive; will churn at month 4 when the budget tightens; refers other agencies (also not fit)
- **Disqualifier signal:** Headcount < 40 OR ARR < $10M
- **What to do instead:** Add to a low-touch nurture; never route to AE

---

### ICP Scoring Rubric

| Tier | Criterion | Weight | Disqualifier? |
|------|-----------|--------|---------------|
| 1 | Headcount 50–500 | gate | Yes (out of band → reject) |
| 1 | Salesforce as system of record | gate | Yes |
| 1 | RevOps function exists (named owner) | gate | Yes |
| 2 | Series B–D OR ARR $20–150M | 20 | No |
| 2 | Sales velocity > 30 deals/month | 15 | No |
| 2 | 2+ tools currently integrated to SFDC | 10 | No |
| 2 | Tech-forward (engineering-led product) | 10 | No |
| 2 | Recent hire on ops team in last 6 months | 5 | No |
| 3 | NA region | 5 | No |
| 3 | Has CDP | 5 | No |
| 3 | Public on RevOps Co-op Slack | 5 | No |

**Threshold:** Pass = all Tier 1 ✓ AND Tier 2+3 score ≥ 50/100. MQL routing: 50–69 = nurture, 70–84 = SDR, 85+ = direct AE.

**Calibration check:** Of the 5 named best customers, 5/5 satisfy all Tier 1 ✓ and 4/5 score ≥ 70 — rubric holds.

---

### Market Sizing
- TAM: ~22,000 US/EMEA companies in headcount + funding band (PitchBook 2026 Q1 export, source: provided by user)
- SAM: ~6,500 with Salesforce + RevOps function (Apollo + LinkedIn Sales Navigator overlap, model-estimated 30%)
- SOM (next 12 mo): ~400 reachable through current channel mix (peer-referral compounding + RevOps Co-op presence)

---

### Refresh Date
Personas: re-validate 2026-10-24 (6 months). ICP rubric: re-validate 2027-04-24 (12 months). Anti-persona: re-validate 2026-07-24 (3 months — fastest drift).
