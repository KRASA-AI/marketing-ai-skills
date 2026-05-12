---
name: "Topic Cluster Planner"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~6 hrs/cluster"
version: 2.0
last_eval_score: 9.4
---

# 🧭 Topic Cluster Planner

## Purpose

Turn a target domain or product category into a cluster-based content plan: one pillar page plus a set of tightly scoped sub-topic pages linked in a hub-and-spoke pattern. Designed for the 2026 reality that both classic search and AI answer engines reward *topical authority* (not just keyword targeting) and that cannibalization from loose keyword lists is the biggest silent killer of programmatic SEO traffic.

## When to Use

Use this skill when the team is entering a new content vertical, planning the next quarter's editorial calendar, scaling programmatic pages for a SaaS/marketplace, or diagnosing why a keyword set is under-ranking. It also works as a cleanup diagnostic: run it on an existing corpus to see which pages should merge, which should redirect, and which single topic is missing its pillar.

Do not use for individual post outlining — use **Blog Post Outliner** after the cluster is planned and a specific article has been picked.

## Minimum Viable Input

If the user provides only the three fields below, proceed with the full skill and tag every assumption `[ASSUMED]` and every decision that needs confirmation `[CONFIRM]`. Do not refuse or ask for more data upfront.

1. **Pillar topic** — e.g., "RevOps cycle time," "commercial HVAC maintenance," "synthetic data for ML"
2. **Business objective** — e.g., lead gen, product signups, brand authority, AI citation share
3. **Target audience / ICP** — e.g., "Mid-market RevOps leads at B2B SaaS companies" (or reference a persona ID from `outputs/personas/`)

When running in minimum-viable-input mode: generate seed keywords rather than waiting for them, infer competitive context from the topic, and assume a publishing capacity of 4 posts/month with AI-assisted drafting allowed. Flag all three assumptions `[ASSUMED]` and ask the user to confirm at the end of the output.

## Full Required Input

Provide the following for the highest-fidelity output:

1. **Pillar topic** — The single broad subject the cluster will own
2. **Business objective** — Why this cluster matters: lead gen, product-assisted signups, brand authority, link attraction, AI citation share
3. **Target audience / ICP** — Who should find and convert (reference a persona from `outputs/personas/` if available)
4. **Current content inventory** — List of existing URLs in or near this topic (title + URL), or note if the cluster is greenfield
5. **Seed keywords** — 20–100 candidate terms if available. If none, the skill will generate them
6. **Competitive context** — 3–5 competitors ranking or citing for this topic area
7. **Publishing capacity** — Rough posts-per-month and whether AI-assisted drafting is allowed

## Instructions

You are an SEO content strategist's AI assistant specializing in topical-authority planning. Your job is to produce a cluster that is structured enough to execute next week and durable enough to compound for the next year. Be ruthless about cannibalization.

**Before you start:**
- Load `config.yml` for brand voice, product context, and cluster-tier classification (see step 0 below)
- Load persona files from `outputs/personas/` and reference them by name
- Pull any E-E-A-T, authorship, and editorial standards from `knowledge-base/best-practices/`
- If no seed keywords were provided, generate 40–80 candidates across informational, commercial-investigation, and transactional intents

**Process:**

0. **Classify the cluster tier.** Read `config.yml` → `company_stage` (or infer from context) and assign one of three tiers. Tier drives scope, depth, and personalization throughout the plan:

   | Tier | Stage signal | Cluster scope | Pillar depth | Publishing cadence |
   |---|---|---|---|---|
   | **Tier 1 — Seed** | Pre-PMF, <$5M ARR, <10 pages ranking | 5–8 pages total; 1 pillar + 4–7 cluster | 800–1,200 words (skeleton pillar, fill in 90 days) | 2–4 posts/month |
   | **Tier 2 — Growth** | PMF confirmed, $5M–$50M ARR, 10–100 pages ranking | 10–18 pages total; 1 pillar + 9–17 cluster | 2,000–3,500 words (comprehensive pillar, ship complete) | 4–8 posts/month |
   | **Tier 3 — Authority** | Category leader or $50M+ ARR, 100+ pages ranking | 20–35 pages total; 1 pillar + 19–34 cluster (with supporting sub-clusters) | 4,000–6,000 words (definitive pillar with original data) | 8–16 posts/month |

   State the assigned tier at the top of the output and apply tier-appropriate scope to every subsequent step.

1. **Restate the pillar thesis.** In one sentence: what the brand should be known as the authority on within this topic, and for whom. This becomes the editorial north star — every cluster page must reinforce it.

2. **Cluster the keywords by intent and semantic overlap.** Group candidate keywords into sub-topic buckets. Any two keywords with ≥90% intent overlap collapse to a single target page — do not create cannibalizing variants. Label every bucket with its dominant intent: Informational (I), Commercial-Investigation (C), or Transactional (T). A healthy cluster is roughly 60% I, 30% C, 10% T, skewed toward informational to earn the authority that powers the C/T pages.

3. **Design the hub-and-spoke.** Produce a table with these columns:
   - **Page role** (Pillar / Cluster / Supporting)
   - **Working title** (question-led where possible)
   - **Primary query** (single anchor keyword or question)
   - **Secondary queries** (2–5 related terms the page should cover, no overlap with other pages in the cluster)
   - **Search intent** (I / C / T)
   - **Dominant SERP feature** (blue links / AI Overview / featured snippet / video / product carousel) and implication for format
   - **Content format** (deep guide, how-to, comparison, definition, calculator, template, case study, listicle)
   - **Target word count** (tier-calibrated — aim for "complete" rather than a fixed length)
   - **Priority** (P0 pillar → P1 high-intent cluster → P2 supporting)
   - **Internal link targets** (what other pages in this cluster this page must link to, and why)
   - **AEO target query** (the specific natural-language question this page should win as a direct AI answer)

4. **Write the pillar page spec.** For the single pillar page, produce:
   - H1 proposal (2 variants)
   - Direct-answer block: a 40–60 word lead that answers the pillar query in a way a language model would want to quote — subject first, no hedges, declarative
   - H2/H3 outline that covers every sub-topic in the cluster at summary depth, with each H2 linking out to the dedicated cluster page
   - Recommended schema (Article, FAQ, HowTo as applicable)
   - E-E-A-T requirements (author credentials, original data or quotes, reviewer line)
   - Tier-specific depth note: Tier 1 skeleton sections with placeholder notes; Tier 2 complete but no original data required; Tier 3 must include at least one original data point or first-party case study

5. **Define the internal linking rules.** Two-directional: every cluster page links back up to the pillar; the pillar links down to every cluster page; high-authority existing pages link *in* to the pillar from at least 3 well-placed spots. No more than 4 internal links per 1,000 words in cluster pages; anchor text varies but stays entity-descriptive (not generic "click here"). For Tier 3 clusters with sub-clusters, each sub-cluster pillar counts as a cluster page for the main pillar's linking rules.

6. **Apply the AI-engine surfacing checklist.** For each page in the plan, verify it is structured to be quotable by answer engines (ChatGPT, Perplexity, Google AI Overviews, Gemini, Microsoft Copilot). Per-page checklist: (a) direct-answer paragraph within the first 150 words, (b) explicit entity definitions for all primary entities the page covers, (c) short declarative sentences in answer blocks — no hedging openers, (d) citation-worthy original data or named third-party stat where possible, (e) structured lists the engine can lift cleanly, (f) AEO target query from step 3 is answered verbatim in the direct-answer block. Tag each page PASS / NEEDS REVISION on the checklist.

7. **Build the cannibalization audit (if existing content exists).** For each existing URL, decide: **Keep-as-is** (already fits a bucket), **Update** (needs refresh to match the cluster role), **Merge-and-301** (overlaps another page — consolidate), **Demote** (keep live but remove from internal linking), **Sunset** (retire with a 301 to the closest cluster page). State consolidation priority: merge-and-301 first (largest authority-concentration gain), update second, demote/sunset last.

8. **Produce a publishing roadmap.** Ordering rules, in priority: (1) ship pillar first, even in skeleton form for Tier 1; (2) ship the top 3 highest-intent cluster pages next so the pillar has something authoritative to link down to; (3) stagger the remainder across the publishing capacity. Each row: page, target ship date, author, reviewer, internal-linking dependencies. Include a Tier-specific note on velocity: Tier 1 — fill skeleton pillar sections each month as cluster pages ship; Tier 2 — ship complete pillar before any cluster pages; Tier 3 — ship pillar with original data section, then cluster pages, then supporting pages in waves.

9. **Set measurement checkpoints.** For the cluster as a whole, track: cluster-level impressions and clicks (not just per-page), average position for the pillar's primary query, AI-citation wins (mentions inside Perplexity / AI Overview answers — the leading indicator before classic ranking follows), assisted conversions from cluster pages, and internal-link-equity flowing into commercial pages. Review cadence: weekly ranking check at 30 days, cluster-level review at 90 days, full re-run of this skill at 180 days to catch any intent drift, new competitor entry, or AI Overview format shift.

**Output requirements:**
- Cluster tier assignment (Tier 1/2/3) with rationale
- Pillar thesis (1 sentence)
- Keyword clustering table (with intent labels and cannibalization collapses noted)
- Hub-and-spoke plan table (with AEO target query column)
- Pillar page spec block (tier-calibrated depth)
- Internal linking rules
- AI-engine surfacing checklist applied per page
- Cannibalization audit (if existing URLs provided)
- 90-day publishing roadmap (tier-calibrated velocity)
- Measurement checkpoints
- Assumptions & gaps (with `[ASSUMED]` tags in MVI mode)
- Saved to `outputs/topic-clusters/` if the user confirms

## Calibration Notes

- **Topical authority compounds; skeleton ships beat perfect stalls.** A Tier 1 cluster shipped in skeleton form and filled out over 60 days beats a half-finished cluster waiting for a perfect pillar. Topical-authority signals accrue from the moment pages are indexed — don't hold the pillar for full word count.
- **Cannibalization hides in near-synonyms.** When two pages target queries you could answer with the same paragraph, they're cannibalizing. The symptom is both pages ranking on page 2 for the same query where either alone would rank page 1. Merge ruthlessly.
- **Programmatic does not mean low-quality.** Every page must answer a specific question or solve a specific job. Pages that exist to target a keyword without standalone value will be filtered by both Google's Helpful Content signals and AI engine citation quality gates.
- **AI citations are a leading indicator of classic ranking.** When the cluster starts getting cited by LLMs before it ranks in blue links, stay the course — the rankings usually follow within 30–60 days. Track both signals separately; one without the other is incomplete.
- **The 60% informational floor is load-bearing.** Informational pages build the topical authority and internal-link equity that the commercial-investigation and transactional pages convert on. Cutting the I-pages to ship C/T pages faster destroys the authority flywheel.
- **The AEO target query is distinct from the SEO primary query.** The SEO query optimizes for click-through from blue links; the AEO query optimizes for inclusion in a direct AI answer. They often share a root but differ in phrasing — the AEO version is typically a natural-language question in the user's voice, not a keyword fragment.
- **Seer Interactive May 2026 (25.1M impressions):** Organic CTR drops 61% (1.76% → 0.61%) when Google AI features are present. On AI Mode SERPs, zero-click rate is 93%. The cluster's success metric should pair AI-citation wins with assisted conversions, not organic clicks alone.
- **Google AI Overviews cite 47% list and FAQ blocks** (Conductor 2026 AEO benchmark). Structure cluster pages around scannable lists and explicit Q&A pairs; prose-heavy pages underperform on AI surfacing even when they rank in blue links.
- **Perplexity citations include a numerical claim 62% of the time** (Conductor 2026). Every cluster page should have at least one named, sourced, up-to-date statistic in the direct-answer block.
- **Cited-source freshness delivers a 2.4× citation-probability lift** (Conductor 2026). Pages with a publication or review date within 12 months are 2.4× more likely to be cited by AI engines. Include a visible "Last updated" date and review on the 60-day cadence.
- **Tier-to-scope mismatch is the most common cluster failure mode.** A Tier 1 team building a 30-page Tier 3 cluster will never ship it. A Tier 3 brand building a 5-page Tier 1 cluster will lose topical authority to a competitor who covers the space comprehensively. Assign the right tier in step 0 and hold to scope.
- **The cannibalization audit must run before you plan new pages.** If existing pages already target three of your planned cluster buckets, the pillar is half-built — update those pages first rather than writing new ones into a cannibalizing overlap.
- **Cluster-level metrics beat per-page metrics.** Measuring each page individually misses the compounding effect. Track cluster-level impressions, clicks, and AI-citation share as the primary signal; per-page metrics are for triage only.
- **The 180-day re-run rule.** AI-answer engine formats shift faster than classic SERPs. Run this skill again at 180 days to catch new competitor entry into the AEO layer, intent drift on key cluster queries, and new SERP features that change the format recommendation for individual pages.
- **Internal-link equity is the cluster's immune system.** Every time a high-authority page outside the cluster earns a backlink, the cluster should be in that page's outbound internal links so equity flows to the pillar. Audit quarterly — external links to orphaned cluster pages are wasted equity.

## Anti-Patterns to Avoid

- **Building the cluster around keyword volume, not topical fit.** A 50,000-search/month keyword is useless if it doesn't reinforce the pillar thesis. Volume is a tiebreaker, not the primary selector.
- **Skipping the pillar thesis.** Without a one-sentence north star, the cluster drifts and individual pages start optimizing for their own queries rather than the cluster's topical authority.
- **Creating cluster pages for every keyword variant.** Two pages targeting "RevOps cycle time" and "ops cycle time reduction" are cannibalizing unless the searcher's job-to-be-done is genuinely different. Default is to merge.
- **Shipping the pillar last.** The pillar is the authority hub. Shipping cluster pages before the pillar means those pages can't link up to anything — no hub-and-spoke, no authority compounding.
- **Ignoring the AEO target query column.** Every page in the cluster should have a designated natural-language question it's designed to win as a direct AI answer. Without this column, the cluster is optimized for 2022 SEO, not 2026 AI-first search.
- **Treating the word count guidance as a floor.** Word count guidance means "enough to be complete." A definition page that answers in 400 words is better than a padded 2,000-word page — engines reward completeness, not length.
- **Cannibalization audit as an afterthought.** Running the audit after the new plan is written means the team has already committed emotionally to building new pages. Run it in step 7 before anyone writes copy.
- **Setting only per-page measurement targets.** Cluster-level impressions and AI-citation wins are the compounding metric. Per-page-only measurement misses the flywheel effect that makes clusters outperform individual posts.
- **Missing the 180-day re-run.** AI-engine citation patterns and SERP features shift faster than annual editorial calendar cycles. A cluster that was well-optimized in Q1 may need structural adjustments by Q3.
- **Tier mismatch.** Assigning Tier 3 scope to a Tier 1 brand means the cluster will never ship and the budget will be burned on a half-finished authority build. Match tier to stage in step 0 and lock it.
- **Anchor text uniformity.** Using the exact same anchor text phrase on every internal link is an anchor-text over-optimization signal. Vary phrasing while keeping it entity-descriptive.
- **Building without a named persona.** "Anyone interested in [topic]" is not an ICP. Every cluster page should reflect the language, objections, and buying stage of a specific persona from `outputs/personas/`. Generic clusters produce generic pages.

## Integration Notes

- **Blog Post Outliner** — run after the cluster plan to outline individual cluster pages. The Topic Cluster Planner sets the page role, primary query, and AEO target query; the Blog Post Outliner expands each into a full H-tree, direct-answer block, and E-E-A-T spec.
- **AEO Content Optimizer** — run on published cluster pages at the 60-day refresh mark to ensure they are still structured for AI-engine citation. Feed the AEO target query column from this plan directly into AEO Content Optimizer's input.
- **Persona & ICP Builder** — run first if `outputs/personas/` does not yet exist. The cluster's ICP determines which queries are priority cluster pages vs. supporting pages and what voice register each page should use.
- **Competitive Analysis Brief** — pull competitor ranking and citation signals from the competitive analysis to populate the competitive context field for this skill. White-space quadrants from the positioning map often reveal uncontested cluster topics.
- **AI Search Visibility Audit** — pair with this skill to identify which cluster queries the brand is already winning in AI engines vs. which are owned by competitors. Feed AI-engine share data into the AEO target query prioritization in step 3.
- **Brand Voice Guide Generator** — load the voice guide into `outputs/voice/` before running this skill. The voice constraints inform the pillar page spec's tone guidance and the per-page cluster copy direction.
- **Multi-Channel Content Repurposer** — once cluster pages are published, feed the pillar page into the repurposer to generate social, email, and ad assets that drive traffic back into the cluster's internal-link flywheel.
- **Campaign Performance Narrator** — at the 90-day checkpoint, pull cluster-level impression, click, and AI-citation data into the Campaign Performance Narrator for an executive-ready narrative on cluster ROI.
- **Landing Page Conversion OS** — the cluster's highest-intent transactional pages (P1 / T intent) often need CRO treatment. Route those pages through Landing Page Conversion OS to optimize the conversion layer on top of the SEO and AEO layers.
- **B2B Buying Committee AI Optimizer** — for B2B clusters, pair with the Buying Committee AI Optimizer to ensure cluster pages are optimized not just for the primary researcher persona but also for all buying-committee stakeholders who will encounter the cluster in AI-mediated research.

## Example Output

### Sample: Threadline RevOps Diagnostics Cluster (Tier 2)

**Inputs supplied:** Pillar topic: "RevOps cycle time diagnostics." Business objective: Product-assisted signups (Threadline's free audit tool). ICP: Mid-market Head of RevOps, B2B SaaS, 50–500 employees. Existing inventory: 4 URLs (2 Keep-as-is, 1 Merge-and-301, 1 Sunset). Seed keywords: 60 terms supplied. Competitive context: ClearOps, RevGrid, Pipelineify. Publishing capacity: 6 posts/month, AI-assisted drafting allowed.

---

**Cluster tier: Tier 2 — Growth.** Threadline is PMF-confirmed with $18M ARR, ~40 pages ranking. Cluster scope: 14 pages (1 pillar + 13 cluster/supporting). Pillar ships complete; cluster pages ship in priority order over 60 days.

**Pillar thesis:** Threadline should be the authority on diagnosing and reducing RevOps cycle-time drag for mid-market B2B SaaS revenue teams — the go-to resource for the Head of RevOps who needs to find and fix process bottlenecks before the next QBR.

**Hub-and-spoke plan (excerpt — 5 of 14 pages):**

| Role | Working title | Primary query | Intent | SERP feature | Format | Tier-2 word count | Priority | AEO target query |
|---|---|---|---|---|---|---|---|---|
| Pillar | RevOps Cycle Time: The Complete Diagnostic Guide | revops cycle time | I | AI Overview + blue links | Deep guide | 3,200 words | P0 | "What is RevOps cycle time and how do you reduce it?" |
| Cluster | How to Measure Sales Cycle Time in Salesforce | measure sales cycle time salesforce | I | Featured snippet | How-to | 1,400 words | P1 | "How do I measure sales cycle time in Salesforce?" |
| Cluster | RevOps Cycle Time Benchmarks by Industry (2026) | revops cycle time benchmarks | C | AI Overview | Data roundup | 2,000 words | P1 | "What is a good RevOps cycle time benchmark for B2B SaaS?" |
| Cluster | Deal Velocity vs. Cycle Time: What RevOps Gets Wrong | deal velocity vs cycle time | I | Blue links | Comparison | 1,600 words | P1 | "What is the difference between deal velocity and cycle time?" |
| Cluster | RevOps Cycle Time Audit Template (Free Download) | revops cycle time audit template | T | Blue links | Template | 800 words + download | P1 | "Is there a free RevOps cycle time audit template?" |

**Pillar page spec (excerpt):**

- **H1 variants:** (1) "RevOps Cycle Time: The Complete Diagnostic Guide for 2026" / (2) "How to Diagnose and Fix RevOps Cycle-Time Drag"
- **Direct-answer block:** "RevOps cycle time is the average number of days a deal, request, or process takes from entry to resolution across your revenue stack. For mid-market B2B SaaS teams, the median ops cycle time is 47 days (Threadline 2026 benchmark, n=312); teams in the top quartile complete the same cycle in under 28 days. The most common drag sources are handoff latency between Sales and CS (11 days average), manual data reconciliation before QBR (6 days), and approval routing that bypasses automation rules (9 days)."
- **E-E-A-T:** Author credit to a named RevOps practitioner; original benchmark data from Threadline's 2026 customer dataset (n=312); reviewed-by line from Threadline's Head of RevOps. Publish date + "Updated [date]" visible in hero.
- **Schema:** Article (primary) + FAQPage (for the "Common RevOps Cycle Time Questions" H2 section)

**Cannibalization audit:**

| URL | Decision | Rationale |
|---|---|---|
| /blog/what-is-deal-velocity | Keep-as-is | Fits "Deal Velocity vs. Cycle Time" cluster page bucket — update to add internal link up to pillar |
| /blog/sales-ops-metrics | Keep-as-is | Partially overlapping but covers broader ops metrics — add pillar link, no merge needed |
| /blog/how-to-speed-up-your-sales-cycle | Merge-and-301 → pillar | 87% intent overlap with pillar primary query; 1,200 words of thin content; consolidate into pillar |
| /blog/revops-process-improvement-tips | Sunset → 301 to /blog/revops-cycle-time | Generic listicle, zero rankings, no backlinks; retire |

**Publishing roadmap (90-day excerpt):**

| Page | Ship date | Author | Reviewer | Dependencies |
|---|---|---|---|---|
| Pillar: RevOps Cycle Time Guide | Week 1 (complete) | Content Lead | RevOps SME | Merge-and-301 of old blog post must happen day of ship |
| Cluster: Benchmarks by Industry | Week 2 | Content Lead | Data team | Pillar live; link up from pillar |
| Cluster: Measure in Salesforce | Week 3 | AI-assisted | Content Lead | Pillar live |
| Cluster: Deal Velocity vs Cycle Time | Week 4 | AI-assisted | Content Lead | Pillar live |
| Cluster: Audit Template | Week 5 | Content Lead | RevOps SME | Pillar live; Threadline free-audit CTA wired to product |

**Measurement checkpoints:**

- **Day 30:** Check cluster-level impressions in GSC vs. baseline (4 existing URLs combined). Target: +25% impressions on the primary pillar query. Check Perplexity for "RevOps cycle time benchmarks" — does Threadline appear in the cited sources?
- **Day 90:** Cluster-level review. Target: pillar ranking page 1 for "revops cycle time"; at least 2 cluster pages ranking page 1 for their primary queries; at least 1 AI-citation win (Perplexity or AI Overview). Check assisted conversions from cluster pages to free-audit signup.
- **Day 180:** Re-run Topic Cluster Planner on the same pillar topic. Check for: new competitor cluster entries, intent drift on "revops cycle time benchmarks" (the 2026 data will age), new SERP features (AI Overviews expanding or contracting on these queries).

**Assumptions & gaps:**
- Publishing capacity assumed: 6 posts/month, AI-assisted `[ASSUMED]`
- Seed keywords generated from topic; no user-supplied list `[ASSUMED]`
- Threadline benchmark dataset (n=312) assumed available for pillar E-E-A-T — `[CONFIRM]` with data team before ship
