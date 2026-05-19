---
name: "AI Search Visibility Audit (Share of Model)"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~5 hrs/audit"
version: 2.0
last_eval_score: null
---

# 🔎 AI Search Visibility Audit (Share of Model)

## Purpose

Run a category-level visibility audit across the major AI answer engines to measure how often a brand is mentioned, cited, or recommended when users ask category-defining questions — and how that share compares to competitors. Produces a question set, a cross-engine scoring sheet, a gap diagnosis, and a prioritized lift plan. Complements the per-page Answer Engine Optimization (AEO) workflow by operating at the category / portfolio level.

The 2026 shift this skill operationalizes: "Share of Model" (SoM) — the percentage of AI-generated answers in your category that mention or cite your brand — is now a load-bearing leading indicator of discovery pipeline. With Seer Interactive's May 2026 data showing a 61% organic-CTR collapse on AI-feature SERPs and a 93% zero-click rate in Google AI Mode, blue-link rank no longer predicts pipeline by itself; AI citation share does. The SKU-level Product Recommendation Rate (PRR) layer (Emberos Merchant, May 2026) sits underneath SoM for ecommerce — this skill audits at the brand/category level and references PRR for catalog-row-level work.

## When to Use

Use this skill quarterly to establish and re-baseline category-level AI visibility. Use it before major launches to check whether the category's answer landscape is winnable and which questions matter most. Use it reactively when organic traffic drops appear unrelated to classic SEO movements — often the cause is falling AI citation share, not falling blue-link rankings. Use it monthly for high-velocity categories (AI tooling, fintech, ecommerce) where the answer landscape resets faster than the SEO landscape.

Do not use for single-page optimization — that is what the **AEO Content Optimizer** does. This skill scans the category; the AEO skill fixes a specific page. Do not use for SKU-level recommendation tracking in retail — that is the **Agentic Commerce Optimizer**'s PRR discipline, which operates one level below brand SoM.

## Minimum Viable Input

If the user provides only the three fields below, proceed immediately and tag every assumption `[ASSUMED]`:

1. **Brand and category** — Brand name plus one category descriptor (e.g., "Threadline, B2B RevOps platform")
2. **Top 3 competitors** — The three names that would credibly appear in a comparison answer
3. **One ICP question theme** — The single decision question that matters most to the buyer (e.g., "Best RevOps platform for Series B SaaS")

When running in MVI mode: infer additional question themes from the competitor set and category descriptor; assume the audit is a one-time baseline (not yet a recurring program); generate a compressed 15-question set instead of the full 30–60; run a single pass per engine (not the 3-run median) and flag this as a lower-confidence baseline; flag at the bottom of the output the top 2 inputs that would most improve audit fidelity if the user can supply them (typically: full competitor set + tracker-question cadence).

MVI mode produces a usable baseline scorecard in ~45 minutes vs. ~5 hours for the full audit. The MVI baseline is sufficient for a first read on whether SoM is the right next-quarter investment; it is not sufficient for a recurring SoM program report.

## Full Required Input

Provide the following for the highest-fidelity audit:

1. **Brand and category** — Brand name plus 1–2 category descriptors the brand competes in (e.g., "B2B expense management software, mid-market SaaS")
2. **Competitor set** — 3–7 brands that would credibly be cited alongside in an AI answer
3. **ICP question themes** — 3–6 themes that cover the real buyer journey (definitions, comparisons, "best X for Y," pricing questions, implementation questions, objections)
4. **Geography and language** — Primary markets to audit
5. **Current AEO state** — Which pages have been optimized via the AEO skill, with target queries and last update date
6. **Tracking cadence** — Is this a one-time audit or a recurring quarterly program

## Instructions

You are an AI search visibility strategist's AI assistant. Your job is to produce a reproducible audit a non-SEO marketer can actually run, interpret, and act on. Be specific about which questions to ask, which engines to ask them to, and how to score the answers.

**Before you start:**
- Load `config.yml` for brand name variants, canonical product names, primary keyword list, and approved positioning pillars
- Consult `knowledge-base/terminology/` so entity naming is consistent across engines
- Pull the last quarter's audit if one exists; this run's scorecard should be comparable, not a fresh framework

**Process:**

1. **Build the question set (30–60 items; 15 in MVI mode).** Five categories, weighted:
   - **Definition questions (20%)** — "What is X?" "What does X mean in [industry]?"
   - **Category-leader questions (25%)** — "Best X for Y," "top X tools for Z," "leading X providers"
   - **Comparison questions (25%)** — "X vs Y," "how does X compare to Y," "alternatives to X"
   - **Use-case questions (20%)** — "How do I do X with Y?" "X for [specific persona]"
   - **Objection/sensitive questions (10%)** — "Is X safe?" "downsides of X" "X complaints"

   Each question specifies the intent, the answer format it is likely to trigger, and the competitor(s) most likely to appear.

2. **Select the engines and run the queries.** The five target engines for 2026 audits:
   - Google AI Overviews (as they appear on SERPs)
   - Google AI Mode (distinct from AI Overviews — Seer 2026 measures 93% zero-click rate here)
   - ChatGPT (with browsing enabled; note model version; flag whether Self-Serve Ads Manager paid placements are visible as of May 2026 in advertiser-relevant categories)
   - Perplexity
   - Gemini (note: separate from AI Overviews / AI Mode; uses different citation surface)
   - Claude

   For each question × engine combination, capture: the full answer text, the list of cited sources (and their order), whether the brand is mentioned, whether competitors are mentioned, the sentiment of any brand mention, and the query timestamp.

3. **Score each answer on the six-metric rubric.** Per question × engine, record:
   - **Mention** — Is the brand named? (0 / 1)
   - **Citation** — Is the brand's content a source? (0 / 1)
   - **Position** — If cited, position in the source list (1 = first, etc.)
   - **Sentiment** — Positive / Neutral / Negative / Mixed framing of any mention
   - **Claim accuracy** — Flag any hallucinated or outdated claim about the brand (0 = no error, 1 = error; escalate errors to the Brand Safety & Crisis Response playbook if severe)
   - **Competitor share** — How many competitors are mentioned, and whether any are positioned more favorably

4. **Compute Share of Model (SoM) and derived metrics.**
   - **Share of Model (overall)** — Mentions of brand / total questions × 100
   - **Share of Model (weighted)** — Weighted by question category (comparisons and category-leader queries count 1.5×)
   - **Citation share** — Citations of brand-owned content / total citations across audit
   - **Competitor-relative SoM** — Brand SoM vs. each competitor SoM, per category
   - **Accuracy rate** — Answers without claim errors / total answers mentioning brand
   - **Engine split** — SoM by engine, flagging engines where the brand is below the competitor median

5. **Diagnose the gaps.** For each low-SoM question cluster, identify the cause:
   - Missing canonical page — the brand has no on-site content that directly answers this question
   - Page exists but is not extractable — no direct-answer block, no entity clarity, no structured content (route to AEO Content Optimizer)
   - Page exists and is extractable but has poor external credibility signal — no inbound citations, outdated data, no authorship
   - Competitor content is stronger — paste excerpts and diagnose why (data depth, named entities, schema, third-party corroboration)
   - Hallucination baseline — the engine is producing wrong answers no one's content can fully fix yet (escalate monitoring cadence)

6. **Build the prioritized lift plan.** Rank the top 10 interventions by expected SoM lift × effort. Each intervention has:
   - Question cluster it addresses
   - Which page to create, optimize, or retire
   - Whether it should be routed to AEO Content Optimizer, Topic Cluster Planner, or Blog Post Outliner
   - An evidence or data asset to acquire (study, first-party dataset, named customer) if the category requires it
   - A target SoM lift and a re-audit date (30, 60, or 90 days)

7. **Set up the recurring program.** If this is not a one-off:
   - Cadence (quarterly default; monthly for high-velocity categories; semi-annual for stable / regulated categories)
   - The 10–20 "tracker questions" that stay constant across audits for time-series comparability
   - Reporting frame: SoM delta vs. last quarter, top 3 gains, top 3 losses, one lesson
   - Owner per intervention and a standing review meeting

**Output requirements:**
- Question set (30–60 items, or 15 in MVI mode, each with category, intent, and expected format)
- Cross-engine scoring sheet (question × engine × six metrics)
- Share of Model scorecard (overall, weighted, by engine, by category, vs. competitors)
- Gap diagnosis narrative
- Prioritized lift plan (top 10 interventions)
- Recurring program design (if applicable)
- Assumptions, gaps, and sampling-bias notes
- Saved to `outputs/ai-visibility/` if the user confirms

## Calibration Notes

- **Run-to-run variance is real; score the median, not the best.** Answer-engine output varies run-to-run. Score at least three runs per question × engine and report the median. A single-run baseline (MVI mode) is acceptable as a directional first read but should not be the basis for a quarterly program report.
- **Citation share is a longer-lead metric than mention share.** A new page may earn mentions in weeks and citations in months. Do not chase citation share with a quarterly cycle alone; pair it with intentional PR (see PR Pitch Builder), third-party data, and backlink work.
- **Share of Model is a leading indicator, not a revenue number.** Do not promise a direct revenue lift from SoM movement in quarter one. Pair SoM reporting with branded-search trend and direct-traffic trend to build a defensible attribution narrative over two to three quarters.
- **Seer Interactive 2026 data: 61% organic-CTR collapse on AI-feature SERPs; 93% AI Mode zero-click rate.** Classic SEO ranking alone is now a weak predictor of category visibility. Do not conclude "our SEO is fine" from blue-link rankings — check SoM separately. 88% of AI-answer citations do not appear in the organic top 10 for the same query.
- **Conductor 2026 AEO benchmarks: AI Overviews cite list+FAQ blocks 47% of the time; Perplexity includes a numerical claim 62% of the time; cited-source freshness delivers a 2.4× citation-probability lift.** These four numbers tell you which page formats to prioritize in the lift plan: structured Q&A blocks, numbers, freshness signals.
- **Engine-by-engine gap pattern is the most actionable read.** A brand at 60% SoM on Claude but 0% on Perplexity is not a "60% SoM problem" — it's a Perplexity-specific extraction or credibility gap. Engine-split is the diagnosis lens, not the headline number.
- **Negative-sentiment mentions matter as much as missing mentions.** A high-SoM brand with negative-sentiment framing in comparison answers is bleeding pipeline; route such findings to the comparison-page content plan (Topic Cluster Planner), not the PR pitch queue.
- **AI-engine answers are not directly editable.** Plan for multi-quarter lift curves, not instant correction. The only short-term correction path for factual errors goes through the Brand Safety & Crisis Response playbook (hallucination tier).
- **180-day re-run rule for AI-format drift.** Even on a quarterly cadence, the answer-format mix (lists vs. paragraphs vs. cards vs. comparison tables) drifts on each engine over 180 days. Re-baseline the question-set format expectations at six months, not just the SoM numbers.
- **Brand-level SoM and SKU-level PRR are different planes.** For B2B / considered purchase / service categories, brand-level SoM (this skill) is the primary measurement plane. For ecommerce / CPG / structured catalog categories, SKU-level PRR (Agentic Commerce Optimizer + Emberos Merchant May 2026) is the primary plane and SoM is secondary. Choose the right plane before running.
- **Comparison and category-leader queries carry the most pipeline weight.** Weight them 1.5× in the Share of Model (weighted) calc. Definition queries dominate volume but rarely convert; comparison queries dominate decisions.
- **Tracker questions are non-negotiable for trend reading.** A quarterly program needs 10–20 questions that stay constant across audits. Adding or rotating questions every quarter destroys time-series comparability — the most common reason teams "can't tell if SoM moved."
- **Geography is a hidden segment.** A US-English audit can mask 0% SoM in EU-English or LATAM-Spanish. For multi-market brands, audit at least the top two markets separately; do not average them.
- **AI Overviews and AI Mode are different surfaces with different citation behavior.** Audit both; do not aggregate them into a single Google line item. AI Mode's 93% zero-click behavior changes which citations matter.
- **The audit-to-action loop is the value, not the audit itself.** A perfect scorecard with no interventions logged is worse than a 70% scorecard with 5 interventions routed to AEO Content Optimizer, Topic Cluster Planner, and PR Pitch Builder with named owners and re-audit dates.

## Anti-Patterns to Avoid

- **Auditing 100 questions once and never re-running** — SoM is a trend metric, not a snapshot; one-off audits cost as much as a recurring program but produce 1/4 the insight
- **Reporting a single SoM number without engine breakdown** — engines differ enough that the average hides the gap; engine-split is mandatory in any executive-facing summary
- **Confusing "organic traffic dropped" with "SoM dropped"** — check both, they move independently; the 2026 dual-surface attribution split requires both numbers in any traffic-decline analysis
- **Fixing hallucinations with aggressive takedown language** — correction-first via canonical-page direct-answer block, escalation via publisher correction forms second; legal-toned takedown letters almost always lose
- **Creating a new page for every low-SoM question** — prioritize, cluster, and consolidate (Topic Cluster Planner); answer-engine ecosystems reward topical authority not page count
- **Treating SoM as vanity** — tie it to branded-search, direct-traffic, and pipeline movement over two to three quarters before declaring it a headline KPI
- **Single-run scoring in a quarterly program** — without 3-run medians the report will surface engine-variance noise as "SoM movement" and erode executive trust
- **Skipping the AI Mode surface because AI Overviews coverage feels similar** — Seer's 93% AI Mode zero-click rate means these are different pipeline surfaces with different citation behavior; audit both
- **Reporting Share of Model without competitor-relative SoM** — absolute SoM of 35% may be category-leading or category-laggard depending on competitor SoM distribution; always include the relative cut
- **Letting tracker-question composition drift quarter to quarter** — destroys time-series comparability; lock the tracker list at 10–20 and only rotate at the 12-month anniversary
- **Averaging across geographies** — masks regional gaps; the US-English audit cannot speak for the LATAM-Spanish audit
- **Auditing without an intervention ledger** — every low-SoM cluster needs a named intervention, owner, route (AEO / Topic Cluster Planner / Blog Post Outliner / PR Pitch Builder), and re-audit date or the audit is shelfware

## Integration Notes

- **Pair with AEO Content Optimizer** — SoM gaps for existing pages route directly to the AEO workflow; this skill identifies which pages, and AEO fixes them.
- **Pair with Topic Cluster Planner** — category gaps map to new pillar + spoke pages; cluster planning is the structural answer when the gap is "missing canonical page."
- **Pair with Competitive Analysis Brief** — understanding why competitors are cited more often requires a messaging + proof-point teardown; SoM tells you the gap exists, the brief tells you why.
- **Pair with PR Pitch Builder** — high-value AI citations often come from third-party articles; a coordinated PR push with first-party data is the external-credibility lever for citation-share gaps.
- **Pair with Brand Safety & Crisis Response Planner** — hallucinated or negative-framing answers above a threshold escalate into the crisis playbook's AI-era risk addendum (Tier 2 trigger: 2 hallucinations in a rolling 7-day window).
- **Pair with Blog Post Outliner** — low-SoM definition and use-case clusters convert into specific page-level briefs once the audit identifies them.
- **Pair with Brand Voice Guide Generator** — entity naming consistency across engines depends on a single canonical brand vocabulary; the guide is the source of truth this audit references.
- **Pair with Agentic Commerce Optimizer** — for ecommerce brands, brand-level SoM (this skill) is paired with SKU-level PRR (Agentic Commerce Optimizer) as the two-plane measurement frame.
- **Pair with Cross-Channel Attribution Analyzer** — SoM movement is a leading indicator that should show up in branded-search + direct-traffic trend lines 60–120 days later; the attribution analyzer closes that loop.
- **Pair with Campaign Performance Narrator** — quarterly SoM scorecards are inputs to executive performance narratives, not standalone reports.

## Example Output

### Threadline RevOps Platform — Q2 2026 SoM Baseline (excerpt)

**Brand:** Threadline (B2B RevOps platform, US-English primary market)
**Competitor set:** Clari, Gong, RevenueHero, Pavilion-built incumbents (n=4 named)
**Question set:** 42 questions across 5 categories (8 definition / 11 category-leader / 11 comparison / 8 use-case / 4 objection)
**Engines audited:** Google AI Overviews, Google AI Mode, ChatGPT, Perplexity, Gemini, Claude (6 engines × 42 questions × 3 runs = 756 scored answers)

#### Sample Scorecard Row

| Question | Engine | Mention | Citation | Position | Sentiment | Accuracy | Competitor Share |
|---|---|---|---|---|---|---|---|
| "Best RevOps platform for Series B SaaS" | ChatGPT | Yes | Yes | 3 of 5 | Neutral | OK | 4 competitors also cited |
| "Best RevOps platform for Series B SaaS" | Perplexity | No | No | — | — | — | 5 competitors cited |
| "Best RevOps platform for Series B SaaS" | Gemini | Yes | No | — | Positive | OK | 3 competitors cited |
| "Best RevOps platform for Series B SaaS" | AI Overviews | No | No | — | — | — | Top 3 competitors cited |
| "Best RevOps platform for Series B SaaS" | AI Mode | No | No | — | — | — | Top 3 competitors cited |
| "Best RevOps platform for Series B SaaS" | Claude | Yes | Yes | 2 of 4 | Neutral | OK | 3 competitors also cited |

**Derived:** SoM = 50% for this question (3/6 engines mention). Perplexity, AI Overviews, AI Mode are the gap — all citing competitors' category roundup pages Threadline does not appear on.

#### Headline SoM Scorecard

| Metric | Value | vs. Q1 baseline | vs. category median |
|---|---|---|---|
| Share of Model (overall) | 47% | +5pp | +12pp (category median 35%) |
| Share of Model (weighted, comparison + category-leader 1.5×) | 42% | +3pp | +8pp |
| Citation share | 18% | +2pp | +4pp |
| Accuracy rate (mentions without hallucinated claims) | 94% | -2pp | at median |
| Engine split — Claude | 78% | flat | +28pp leader |
| Engine split — ChatGPT | 64% | +8pp | +12pp |
| Engine split — Gemini | 52% | +6pp | +4pp |
| Engine split — AI Overviews | 28% | +2pp | -8pp **gap** |
| Engine split — AI Mode | 19% | new | -14pp **gap** |
| Engine split — Perplexity | 17% | -3pp | -18pp **gap** |

#### Gap Diagnosis

- **Perplexity gap (17% SoM, -18pp vs. category median):** Perplexity is consistently citing one competitor's "RevOps Buyer's Guide 2026" PDF as the canonical source for category-leader and comparison queries. Threadline has no equivalent published asset. **Cause:** Missing canonical category guide; extractability not the issue (existing product pages extract on Claude and ChatGPT) — the issue is no roundup-format page exists.
- **AI Mode gap (19% SoM, -14pp vs. category median):** AI Mode is favoring competitors with structured FAQ schema and numerical claim density. Threadline's product pages have FAQ schema but no numerical density (no benchmark data published). **Cause:** Page format mismatch — pages extract but don't carry the numerical density Conductor 2026 data shows Perplexity and AI Mode reward (62% inclusion when a numerical claim is present).
- **AI Overviews gap (28% SoM, -8pp vs. category median):** AI Overviews is citing third-party articles (G2, TrustRadius, Pavilion blog) more than competitors' own properties. Threadline has thin third-party citation coverage. **Cause:** Citation-credibility gap — fixable via PR Pitch Builder + first-party benchmark dataset.
- **Comparison cluster sentiment skew:** 11 comparison queries; Threadline mentioned in 7; positive in 2, neutral in 4, mixed in 1 (one engine framed Threadline as "newer / less proven"). **Cause:** Missing direct-comparison pages (Threadline vs. Clari, Threadline vs. Gong); existing positioning is missing the comparison surface entirely.

#### Top 10 Lift Plan (excerpt — top 4 shown)

| # | Intervention | Question cluster | Route | Effort | Target SoM lift | Re-audit |
|---|---|---|---|---|---|---|
| 1 | Publish "Best RevOps Platforms for Series B SaaS (2026)" pillar — 3,000-word category guide with comparison table, decision tree, first-party "Threadline 2026 RevOps Cycle Time Benchmark" data (n=312), and 12 deep FAQ entries | Category-leader (11 queries) | Topic Cluster Planner → Blog Post Outliner → AEO Content Optimizer | High (4 wks) | Category-leader cluster 35% → 60% in 90 days; AI Mode + Perplexity surfacing on top tracker question | 60d, 90d |
| 2 | Build comparison-page set (Threadline vs. Clari / Gong / RevenueHero / Pavilion-built incumbents) — 4 pages, each with side-by-side feature matrix, named customer quotes, pricing transparency, and 4 buying-decision FAQs | Comparison (11 queries) | AEO Content Optimizer | Med (2 wks) | Comparison cluster 41% → 65% in 60 days; comparison sentiment from mixed → neutral/positive | 60d |
| 3 | First-party benchmark dataset PR push — pitch "2026 RevOps Cycle Time Benchmark" to MarTech, Pavilion blog, Modern Sales Pros, Sales Hacker, LinkedIn newsletter top 5 (n=10 targets, tier-1 exclusive offered to MarTech) | Citation share (cross-cluster) | PR Pitch Builder | Med (3 wks) | Citation share 18% → 28% in 90 days via third-party article citations | 90d |
| 4 | Add numerical-claim density to existing top-10 product pages — embed 3+ specific numbers per page (benchmark data, customer metrics, ROI claims) with structured-data markup | Use-case + definition (16 queries) | AEO Content Optimizer | Low (1 wk) | AI Mode + Perplexity surfacing 19% → 35% in 30 days | 30d |

#### Recurring Program Design

- **Cadence:** Quarterly (Q3 2026 re-baseline = Aug 15, 2026)
- **Tracker questions:** 18 locked (top 3 per cluster, balanced for engine variance)
- **Reporting frame:** SoM delta vs. last quarter, engine split, top 3 gains, top 3 losses, one lesson, named interventions executed and their measured lift
- **Owner roster:** Marketing lead owns the audit run; AEO Content Optimizer route owned by content lead; PR Pitch Builder route owned by comms; pillar pages owned by topic-cluster lead
- **Re-baseline event:** 180-day AI-format drift check (Nov 15, 2026) — re-assess answer-format mix per engine and adjust question-set format expectations

#### Assumptions and Gaps

- `[ASSUMED]` Series B SaaS as the primary ICP segment for tracker questions; verify with the persona-icp-builder roster before locking
- `[ASSUMED]` US-English audit speaks for the company's primary market; EU-English audit deferred to Q4
- **Gap:** Single-run scoring on 12 of 42 questions (engine throttling); flagged for 3-run re-score in Q3 baseline
- **Gap:** No before-Q1 baseline available — Q2 deltas are vs. a partial Q1 snapshot, not a full prior-quarter audit
