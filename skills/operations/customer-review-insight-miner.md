---
name: "Customer Review & Insight Miner (VoC)"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~8 hrs/cycle"
version: 1.0
last_eval_score: null
---

# 🗣️ Customer Review & Insight Miner (VoC)

## Purpose

Turn unstructured customer voice — reviews, support tickets, sales-call transcripts, NPS verbatims, social DMs, App Store / Play Store / G2 / Capterra / Trustpilot / Google Reviews / category-specific marketplace reviews, win/loss interviews, churn-cancel reasons, community forum threads — into a structured, evidence-grounded Voice of Customer (VoC) brief that downstream marketing skills can act on. Produces a categorized theme map (pains / desired outcomes / objections / buying criteria / praise patterns), a verbatim-quote bank with source attribution, sentiment-and-volume trends, before-and-after deltas vs. the last cycle, an explicit "in language they actually use" terminology dictionary, and a routed action list that hands off to Persona & ICP Builder, Brand Voice Guide, Topic Cluster Planner, Ad Copy Variations, Competitive Analysis Brief, and Brand Safety & Crisis Response.

The 2026 shift this skill operationalizes: VoC has moved from a periodic "analysis project" run by a researcher into an ongoing operating system that feeds positioning, content, ads, product, and support continuously. AI-native review-mining tools (Cobbai, Crescendo, VOC.ai, Revuze, Wizr, Syncly, Level.ai, Stella) auto-classify themes, surface trending issues without taxonomy maintenance, and ground every theme in customer language — but they need a structured prompt and review pipeline to produce marketing-grade output rather than dashboards. This skill is the prompt-and-process layer that produces the brief.

## When to Use

Use this skill on a quarterly cadence as the standing input for positioning, messaging, and content planning, and run it ad hoc before any major launch, brand refresh, pricing change, persona refresh, ad-creative concepting sprint, or quarterly business review. Run it reactively when reviews trend negative, when NPS drops, when win-rate against a specific competitor degrades, when a support theme spikes, or when an ad campaign starts losing CTR for unclear reasons — the cause is often visible in customer language two or three weeks before it shows up in performance metrics.

Do not use this skill for one-off survey analysis. That is a research task. This skill assumes a sustained pipeline of customer voice across multiple sources and produces a brief that compounds quarter over quarter.

## Required Input

Provide the following:

1. **Brand and category** — Brand name, category, and 1–3 product / service classes in scope
2. **Source inventory** — Which customer-voice sources are accessible this cycle, with URLs / exports / API endpoints. At minimum two of: review platforms (G2, Capterra, App Store, Play Store, Trustpilot, Google Reviews, Yelp, category-specific marketplaces), support ticket export, sales-call transcript export (Gong / Chorus / Fireflies), NPS verbatim export, social DM export, win-loss interview transcripts, churn-cancel reason export, community forum threads
3. **Date window** — Default last 90 days; flag anything outside this window so seasonality is visible
4. **Comparison baseline** — Last quarter's VoC brief if one exists, or last year's same-quarter for seasonal comparison
5. **Persona segmentation** — ICP IDs (from Persona & ICP Builder) so themes can be tagged by audience
6. **Competitor set** — 3–7 brands customers compare you to in their own language (so competitive comparisons in reviews can be tagged)
7. **Tracker themes** — 5–15 stable themes you want to track quarter-over-quarter (e.g., "onboarding friction," "pricing perception," "support quality," "integration request — Salesforce")
8. **Output destination** — Which downstream skills the brief should hand off to (default: all integrations listed below)

Flag missing sources rather than skipping them silently — the brief's claim strength scales with source diversity.

## Instructions

You are a Voice of Customer analyst's AI assistant. Your job is to produce a brief that a marketing leader can defend to product, sales, and support, that an ad copywriter can draft from without paraphrasing it, and that compounds — every cycle's brief makes the next cycle's brief faster and sharper. Be ruthless about grounding everything in verbatim quotes; never invent customer language.

**Before you start:**
- Load `config.yml` for brand variants, ICP IDs, competitor list, and tracker themes
- Consult `knowledge-base/terminology/` for entity naming consistency
- Pull the most recent VoC brief if one exists; this cycle's brief should be comparable, not a fresh framework

**Process:**

1. **Pipeline pass — extract structured signal from each source.** For each accessible source, extract:
   - Review / ticket / interview body
   - Source type, source URL or ID, date, persona tag if available, star rating where applicable
   - Whether the customer references a competitor by name
   - Whether the customer references a specific product feature, pricing element, or workflow
   Treat this as a structured extraction step — do not paraphrase. Drop low-signal entries (single-word reviews, off-topic, spam) but keep the count for source-volume reporting.

2. **Classify into the five-bucket theme map.** Every entry routes into one or more of:
   - **Pains** — What is broken, painful, or causing friction (with sub-buckets: product, pricing, support, onboarding, integration, performance)
   - **Desired outcomes** — What customers say they want to be able to do, or what they imagined the product would let them do
   - **Objections** — Reasons customers hesitated, didn't buy, churned, or downgraded (with sub-buckets: price, fit, trust, switching cost, missing capability)
   - **Buying criteria** — Explicit criteria customers say they used to evaluate (often surfaces in win-loss interviews and onboarding survey responses)
   - **Praise patterns** — What customers love, the words they use to recommend, the moments they chose to leave a positive review unsolicited
   Tag each theme with: persona, source type, frequency, sentiment polarity, and verbatim-quote IDs that ground the theme.

3. **Run the dedicated comparison passes.** Three additional passes that often surface missed signal:
   - **Competitor mention pass** — Every entry that names a competitor; classify the framing (positive comparison to brand / negative comparison to brand / neutral mention / "I switched from X" with reason)
   - **Switching language pass** — Every entry where the customer describes a transition into or out of the product or category; capture the trigger event in their words
   - **Unsolicited recommendation pass** — Entries where the customer is recommending the brand to a peer or persona they name explicitly; this is the highest-signal source of buyer-language for ad copy

4. **Build the verbatim-quote bank.** For each theme and each comparison pass:
   - 3–7 representative quotes per theme, with source, date, persona tag, and a one-line context note
   - Mark each quote as "ad-ready" (clean, on-brand, no PII) or "interview-only"
   - Build a one-page "high-conviction quote sheet" — the 20–40 quotes that most clearly express the top themes and could be paraphrased into ad copy, landing-page hero sections, or sales-deck testimonials
   - Never edit a quote for grammar in the ad-ready set; preserve customer voice exactly. Note PII-redaction if any.

5. **Compute sentiment, volume, and delta vs. baseline.** For each tracker theme:
   - Volume this cycle vs. last cycle
   - Sentiment distribution (positive / negative / neutral / mixed)
   - Persona breakdown
   - Source-mix breakdown (so you can see when a theme is dominant in support tickets but invisible in reviews — common for friction themes)
   - "New theme" flags — themes that appeared above a frequency threshold this cycle but not last cycle
   - "Disappearing theme" flags — themes that fell below a frequency threshold this cycle vs. last
   Report deltas as both absolute counts and percentage changes, with claim-strength notes when the source mix changed (more reviews ≠ more pain if the source pool grew).

6. **Build the buyer-language dictionary.** From the verbatim bank, extract:
   - The 10–25 phrases customers use to describe the category (e.g., "customer feedback platform" vs. "VoC tool" vs. "review aggregator" — all live in the same category)
   - The 10–25 phrases customers use to describe the pain the product solves
   - The 5–15 phrases customers use when comparing alternatives
   - The 5–15 phrases customers use when recommending to a peer
   This dictionary feeds Persona & ICP Builder, Topic Cluster Planner, AEO Content Optimizer, and Ad Copy Variations directly.

7. **Diagnose, prioritize, and route the action list.** For each top theme:
   - Is this a marketing problem (positioning, messaging, content), a product problem (build, fix, deprecate), a support problem (training, documentation, response time), or a pricing problem
   - If marketing: which downstream skill owns the next move
   - If non-marketing: a one-line summary and the recommended owner outside marketing
   - Severity tag (deal-breaker / softener / nitpick — see Synthetic Persona Simulator severity taxonomy)
   - Confidence tag (high if grounded in 10+ verbatim quotes across 2+ source types; medium if 5–10 quotes; low if fewer or single-source)

8. **Set up the recurring program.** If this is not a one-off:
   - Cadence (quarterly default; monthly during launch periods or after pricing changes)
   - Tracker themes and the threshold that triggers an alert between cycles
   - Owner per top action, standing review meeting, and an escalation rule when a tracker theme moves > 25% in volume or flips polarity
   - A re-classification audit every fourth cycle to catch theme drift (the customer language drifts faster than the taxonomy)

**Output requirements:**
- Source inventory and date window with claim-strength notes
- Theme map across the five buckets with persona / source / frequency / sentiment tags
- Comparison-pass outputs (competitor mention, switching language, unsolicited recommendations)
- Verbatim-quote bank with the one-page high-conviction quote sheet
- Sentiment, volume, and delta vs. baseline scorecard with new-theme and disappearing-theme flags
- Buyer-language dictionary
- Routed action list with severity, confidence, and owner
- Recurring program design (if applicable)
- Assumptions, sampling-bias notes (over-/under-represented persona, channel, period)
- Saved to `outputs/voc/` if the user confirms

## Calibration Notes

- **Verbatim grounding is the highest-leverage rule.** A theme without 5+ verbatim quotes from 2+ sources is a hypothesis, not a finding. Mark it that way in the brief.
- **Reviews lie about the journey, support tickets tell it.** Public reviews skew toward the moments customers chose to write, which over-represents the launch experience and the moment of first frustration. Support tickets are closer to the everyday lived experience. A balanced source mix matters more than total volume.
- **Star ratings are a weak signal compared to language.** A 4-star review with a deal-breaker objection in the body costs more pipeline than a 1-star review with a vague complaint. Score on language, not stars.
- **Competitor mentions are gold for ad copy and weak for product.** Customers naming a competitor ("I switched from X because…") gives you copy and positioning intel directly; it gives product weak signal because the named comparison is usually a single feature, not the whole product.
- **Sentiment shifts before performance.** A theme moving from neutral to negative usually shows up in customer language two to three weeks before it lands in CTR, conversion, or churn. Treat sentiment-direction-of-travel as a leading indicator and route fast-moving themes to product / support before the cycle ends.
- **Beware the "loud minority."** Forum threads and tweets over-represent the most engaged users. Cross-reference any forum-driven theme against support tickets and reviews before treating it as representative.
- **AI-classified themes drift over time.** Re-audit the taxonomy every fourth cycle; new product capabilities, new competitors, and new pricing tiers introduce new categories the model will silently fold into adjacent buckets if you don't intervene.
- **Translation is lossy.** When working with multilingual reviews, run the classification in the original language where possible and only translate the verbatim-quote bank and dictionary outputs. Translating before classification destroys the language-precision the dictionary depends on.
- **Don't paraphrase into ad copy.** Use customer language as-is in the ad-ready quote sheet; the most common Ad Copy Variations failure mode is sanding off the customer's actual words into "professional" copy that loses every verbal hook.

## Example Output

### Sample Theme Map Excerpt (B2B SaaS, Q2 2026)

| Theme | Bucket | Volume | Δ vs Q1 | Sentiment | Source mix | Confidence | Routed to |
|---|---|---|---|---|---|---|---|
| "Salesforce sync breaks weekly" | Pain — Integration | 47 | +34% | Negative | 70% support, 30% reviews | High | Product (urgent) |
| "Onboarding too long for our IT team" | Pain — Onboarding | 32 | +12% | Negative | 50% reviews, 30% support, 20% Gong | High | Onboarding redesign + Brand Voice (positioning) |
| "Could replace 4 tools" | Praise pattern | 28 | +56% | Positive | 80% reviews, 20% Gong | High | Ad Copy Variations + Topic Cluster (consolidation theme) |
| "Why is the AI add-on so much extra" | Objection — Pricing | 19 | new | Negative | 60% sales calls, 40% support | Medium | Pricing review + Brand Voice (justification) |
| "Switched from Acme because of analytics" | Competitor — Switching | 14 | +27% | Positive | 90% reviews, 10% Gong | High | Ad Copy Variations + Competitive Analysis Brief |

### Sample High-Conviction Quote (ad-ready)

> "We replaced four tools with this. The board wasn't happy about another subscription line until I showed them what we cut. Now they think I'm a genius." — G2 review, 2026-04-12, Director of RevOps, mid-market SaaS

### Sample Buyer-Language Dictionary Excerpt

| Customer-language phrase | Marketing-language equivalent | Use in |
|---|---|---|
| "Replaces our duct tape" | "Tool consolidation" | Hero copy, ad copy, landing page subhead |
| "I don't have to babysit it" | "Reliable automation / low-touch operation" | Mid-funnel product-page copy |
| "It just shows up at the right time" | "Predictive trigger / behavioral signal" | Lifecycle copy, onboarding email sequences |
| "Sales finally trusts marketing's leads" | "MQL→SQL alignment / lead quality lift" | Sales-deck testimonial, case-study lead-in |

### Sample Routed Action

**Action:** Re-position the Salesforce integration as a first-class capability with a dedicated landing page, a verified-uptime widget, and a quarterly reliability report; pair with a holding-statement template for any sync-outage incident.
**Theme it addresses:** "Salesforce sync breaks weekly" (47 mentions, +34% Q2, negative sentiment, high confidence).
**Severity:** Deal-breaker (8 of 14 churn-cancel reasons in Q2 named the sync directly).
**Confidence:** High (47 verbatims, 2 source types).
**Routed to:** Product engineering (root-cause fix, owner: Eng VP), Topic Cluster Planner (integration-reliability content cluster), Brand Voice Guide (justification language for sales calls), Brand Safety & Crisis Response Planner (incident playbook for the next sync outage).

## Integration Notes

- **Pair with Persona & ICP Builder** — Verbatim language and pain themes refresh the ICP every cycle; persona drift is invisible without this input.
- **Pair with Brand Voice Guide Generator** — The buyer-language dictionary is the single biggest input to a 2026-relevant brand voice that doesn't sound like a vendor.
- **Pair with Topic Cluster Planner** — New themes and disappearing themes drive next quarter's content roadmap; the dictionary feeds the cluster keyword list.
- **Pair with Ad Copy Variations** — The high-conviction quote sheet is the ad copy seed; never write ad copy without it.
- **Pair with Competitive Analysis Brief** — Competitor mention and switching-language passes are direct competitive intel.
- **Pair with Brand Safety & Crisis Response Planner** — Sentiment shifts above a threshold escalate into the crisis playbook before they hit external attention.
- **Pair with Synthetic Persona Simulator** — Use this skill's verbatim quotes to ground the simulator's reactions; quote-grounded simulations drift less than unconstrained ones.
- **Pair with AI Search Visibility Audit** — The buyer-language dictionary tells you which questions to put in the SoM tracker question set; "buyer-language ≠ category-jargon" is one of the most common SoM gap causes.

## Anti-Patterns to Avoid

- Reporting one sentiment number for the whole brand — average sentiment hides the deal-breaker theme that's killing pipeline
- Skipping verbatim grounding because dashboards already classified the themes — auto-classification is a starting point, not a brief
- Treating reviews and support tickets as the same source type — they capture different moments of the journey
- Paraphrasing customer quotes into "polished" copy — preserve the exact language; that's the asset
- Running a single source (e.g., G2 only) and calling it VoC — single-source briefs over-represent one moment of the journey
- Re-using the same five themes every quarter — re-audit the taxonomy and accept new themes; theme drift kills the brief's relevance over a year
- Conflating "many customers said this" with "this is the most important thing" — frequency, severity, and persona-fit each count; rank on the combination, not on count
- Routing every theme to marketing — many themes belong to product, support, pricing, or ops; be honest about the owner
- Acting on a high-volume forum thread without cross-referencing — community echo chambers can amplify a minority view by an order of magnitude
- Letting the brief sit in a doc — the value is in the routed actions; if downstream skills aren't refreshed against this brief, the cycle delivered nothing
