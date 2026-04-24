---
name: "AI Search Visibility Audit (Share of Model)"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~5 hrs/audit"
version: 1.0
last_eval_score: null
---

# 🔎 AI Search Visibility Audit (Share of Model)

## Purpose

Run a category-level visibility audit across the major AI answer engines to measure how often a brand is mentioned, cited, or recommended when users ask category-defining questions — and how that share compares to competitors. Produces a question set, a cross-engine scoring sheet, a gap diagnosis, and a prioritized lift plan. Complements the per-page Answer Engine Optimization (AEO) workflow by operating at the category / portfolio level.

The 2026 shift this skill operationalizes: "Share of Model" (SoM) — the percentage of AI-generated answers in your category that mention or cite your brand — is emerging as a leading indicator of discovery pipeline as AI answer engines intermediate more buyer research.

## When to Use

Use this skill quarterly to establish and re-baseline category-level AI visibility. Use it before major launches to check whether the category's answer landscape is winnable and which questions matter most. Use it reactively when organic traffic drops appear unrelated to classic SEO movements — often the cause is falling AI citation share, not falling blue-link rankings.

Do not use for single-page optimization — that is what the **AEO Content Optimizer** does. This skill scans the category; the AEO skill fixes a specific page.

## Required Input

Provide the following:

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

1. **Build the question set (30–60 items).** Five categories, weighted:
   - **Definition questions (20%)** — "What is X?" "What does X mean in [industry]?"
   - **Category-leader questions (25%)** — "Best X for Y," "top X tools for Z," "leading X providers"
   - **Comparison questions (25%)** — "X vs Y," "how does X compare to Y," "alternatives to X"
   - **Use-case questions (20%)** — "How do I do X with Y?" "X for [specific persona]"
   - **Objection/sensitive questions (10%)** — "Is X safe?" "downsides of X" "X complaints"

   Each question specifies the intent, the answer format it is likely to trigger, and the competitor(s) most likely to appear.

2. **Select the engines and run the queries.** The five target engines for 2026 audits:
   - Google AI Overviews (as they appear on SERPs)
   - ChatGPT (with browsing enabled; note model version)
   - Perplexity
   - Gemini
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
   - Cadence (quarterly default; monthly for high-velocity categories)
   - The 10–20 "tracker questions" that stay constant across audits for time-series comparability
   - Reporting frame: SoM delta vs. last quarter, top 3 gains, top 3 losses, one lesson
   - Owner per intervention and a standing review meeting

**Output requirements:**
- Question set (30–60 items with category, intent, and expected format)
- Cross-engine scoring sheet (question × engine × six metrics)
- Share of Model scorecard (overall, weighted, by engine, by category, vs. competitors)
- Gap diagnosis narrative
- Prioritized lift plan (top 10 interventions)
- Recurring program design (if applicable)
- Assumptions, gaps, and sampling-bias notes
- Saved to `outputs/ai-visibility/` if the user confirms

## Calibration Notes

- Answer-engine output varies run-to-run. Score at least three runs per question × engine and report the median, not the best single answer.
- Citation share is a longer-lead metric than mention share. A new page may earn mentions in weeks and citations in months. Do not chase citation share with a quarterly cycle alone; pair it with intentional PR, third-party data, and backlink work (see PR Pitch Builder).
- Share of Model is a leading indicator, not a revenue number. Do not promise a direct revenue lift from SoM movement in quarter one. Pair SoM reporting with branded-search trend and direct-traffic trend to build a defensible attribution narrative over two to three quarters.
- 88% of AI-answer citations do not appear in the organic top 10 for the same query. Classic SEO ranking alone is a weak predictor of AI citation. Do not conclude "our SEO is fine" from blue-link rankings.
- Negative mentions matter. A high-SoM brand with negative-sentiment framing in comparison answers is bleeding pipeline; route such findings to the comparison-page content plan, not the PR pitch queue.
- AI-engine answers are not editable. Plan for multi-quarter lift curves, not instant correction. The only short-term correction path for factual errors goes through the Brand Safety & Crisis Response playbook.

## Example Output

### Sample Scorecard Row

| Question | Engine | Mention | Citation | Position | Sentiment | Accuracy | Competitor Share |
|---|---|---|---|---|---|---|---|
| "Best B2B expense management software for mid-market" | ChatGPT | Yes | Yes | 3 of 5 | Neutral | OK | 4 competitors also cited |
| "Best B2B expense management software for mid-market" | Perplexity | No | No | — | — | — | 5 competitors cited |
| "Best B2B expense management software for mid-market" | Gemini | Yes | No | — | Positive | OK | 3 competitors cited |
| "Best B2B expense management software for mid-market" | AI Overviews | No | No | — | — | — | Top 3 competitors cited |
| "Best B2B expense management software for mid-market" | Claude | Yes | Yes | 2 of 4 | Neutral | OK | 3 competitors also cited |

**Derived:** SoM = 60% for this question (3/5 engines mention). Perplexity and AI Overviews are the gap; both are citing competitors' category roundup pages we don't appear on.

### Sample Top-of-List Intervention

**Intervention:** Publish a category guide "Best mid-market B2B expense management tools (2026)" — 2,500-word pillar page with comparison table, decision-tree, first-party research snippet, and 10 deep FAQ entries.
**Rationale:** Four of our five gap questions are "Best X for Y" variants; AI engines are citing category roundup pages, and we don't have one.
**Route to:** Topic Cluster Planner → Blog Post Outliner → AEO Content Optimizer
**Target lift:** Move SoM from 35% to 60% for the "Best X" cluster within 90 days, and surface on at least three of five engines for the top tracker question.
**Re-audit:** 60 days, then 90.

## Integration Notes

- **Pair with AEO Content Optimizer** — SoM gaps for existing pages route directly to the AEO workflow; this skill identifies which pages, and AEO fixes them.
- **Pair with Topic Cluster Planner** — category gaps map to new pillar + spoke pages; cluster planning is the structural answer.
- **Pair with Competitive Analysis Brief** — understanding why competitors are cited more often requires a messaging + proof-point teardown.
- **Pair with PR Pitch Builder** — high-value AI citations often come from third-party articles; a coordinated PR push with first-party data is the external-credibility lever.
- **Pair with Brand Safety & Crisis Response Planner** — hallucinated or negative-framing answers above a threshold escalate into the crisis playbook.

## Anti-Patterns to Avoid

- Auditing 100 questions once and never re-running — SoM is a trend metric, not a snapshot
- Reporting a single SoM number without engine breakdown — engines differ enough that the average hides the gap
- Confusing "organic traffic dropped" with "SoM dropped" — check both, they move independently
- Fixing hallucinations with aggressive takedown language — correction-first, escalation-second, almost always wins
- Creating a new page for every low-SoM question — prioritize, cluster, and consolidate; answer-engine ecosystems reward topical authority not page count
- Treating SoM as vanity — tie it to branded-search, direct-traffic, and pipeline movement over two to three quarters before declaring it a headline KPI
