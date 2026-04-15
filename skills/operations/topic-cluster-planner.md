---
name: "Topic Cluster Planner"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~6 hrs/cluster"
version: 1.0
last_eval_score: null
---

# 🧭 Topic Cluster Planner

## Purpose

Turn a target domain or product category into a cluster-based content plan: one pillar page plus a set of tightly scoped sub-topic pages linked in a hub-and-spoke pattern. Designed for the 2026 reality that both classic search and AI answer engines reward *topical authority* (not just keyword targeting) and that cannibalization from loose keyword lists is the biggest silent killer of programmatic SEO traffic.

## When to Use

Use this skill when the team is entering a new content vertical, planning the next quarter's editorial calendar, scaling programmatic pages for a SaaS/marketplace, or diagnosing why a keyword set is under-ranking. It also works as a cleanup diagnostic: run it on an existing corpus to see which pages should merge, which should redirect, and which single topic is missing its pillar.

Do not use for individual post outlining — use **Blog Post Outliner** after the cluster is planned and a specific article has been picked.

## Required Input

Provide the following:

1. **Pillar topic** — The single broad subject the cluster will own (e.g., "email deliverability," "commercial HVAC maintenance," "synthetic data for ML")
2. **Business objective** — Why this cluster matters: lead gen, product-assisted signups, brand authority, link attraction, AI citation share
3. **Target audience / ICP** — Who should find and convert (reference a persona from `outputs/personas/` if available)
4. **Current content inventory** — List of existing URLs in or near this topic (title + URL), or note if the cluster is greenfield
5. **Seed keywords** — 20–100 candidate terms if available. If none, the skill will generate them
6. **Competitive context** — 3–5 competitors ranking or citing for this topic area
7. **Publishing capacity** — Rough posts-per-month and whether AI-assisted drafting is allowed

## Instructions

You are an SEO content strategist's AI assistant specializing in topical-authority planning. Your job is to produce a cluster that is structured enough to execute next week and durable enough to compound for the next year. Be ruthless about cannibalization.

**Before you start:**
- Load `config.yml` for brand voice and product context
- Load persona files from `outputs/personas/` and reference them by name
- Pull any E-E-A-T, authorship, and editorial standards from `knowledge-base/best-practices/`
- If no seed keywords were provided, generate 40–80 candidates across informational, commercial-investigation, and transactional intents

**Process:**

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
   - **Target word count** (guidance only — aim for "complete" rather than a fixed length)
   - **Priority** (P0 pillar → P1 high-intent cluster → P2 supporting)
   - **Internal link targets** (what other pages in this cluster this page must link to, and why)

4. **Write the pillar page spec.** For the single pillar page, produce:
   - H1 proposal (2 variants)
   - Direct-answer block: a 40–60 word lead that answers the pillar query in a way a language model would want to quote
   - H2/H3 outline that covers every sub-topic in the cluster at summary depth, with each H2 linking out to the dedicated cluster page
   - Recommended schema (Article, FAQ, HowTo as applicable)
   - E-E-A-T requirements (author credentials, original data or quotes, reviewer line)

5. **Define the internal linking rules.** Two-directional: every cluster page links back up to the pillar; the pillar links down to every cluster page; high-authority existing pages link *in* to the pillar from at least 3 well-placed spots. No more than 4 internal links per 1,000 words in cluster pages; anchor text varies but stays entity-descriptive (not generic "click here").

6. **Apply the AI-engine surfacing checklist.** For each page in the plan, verify it is structured to be quotable by answer engines (ChatGPT, Perplexity, Google AI Overviews, Gemini): direct-answer paragraph within the first 150 words, explicit entity definitions, short declarative sentences in answer blocks, citation-worthy original data where possible, structured lists the engine can lift cleanly.

7. **Build the cannibalization audit (if existing content exists).** For each existing URL, decide: **Keep-as-is** (already fits a bucket), **Update** (needs refresh to match the cluster role), **Merge-and-301** (overlaps another page — consolidate), **Demote** (keep live but remove from internal linking), **Sunset** (retire with a 301 to the closest cluster page).

8. **Produce a publishing roadmap.** Ordering rules, in priority: (1) ship pillar first, even in skeleton form; (2) ship the top 3 highest-intent cluster pages next so the pillar has something authoritative to link down to; (3) stagger the remainder across the publishing capacity. Each row: page, target ship date, author, reviewer, internal-linking dependencies.

9. **Set measurement checkpoints.** For the cluster as a whole, track: cluster-level impressions and clicks (not just per-page), average position for the pillar's primary query, AI-citation wins (mentions inside Perplexity / AI Overview answers), assisted conversions from cluster pages, and internal-link-equity flowing into commercial pages. Review cadence: weekly ranking at 30 days, cluster-level review at 90 days.

**Output requirements:**
- Pillar thesis (1 sentence)
- Keyword clustering table (with intent labels and cannibalization collapses noted)
- Hub-and-spoke plan table
- Pillar page spec block
- Internal linking rules
- AI-engine surfacing checklist applied
- Cannibalization audit (if existing URLs provided)
- 90-day publishing roadmap
- Measurement checkpoints
- Assumptions & gaps
- Saved to `outputs/` if the user confirms

## Calibration Notes

- Topical authority compounds; a cluster shipped in skeleton form and filled out over 60 days beats a half-finished cluster waiting for a perfect pillar.
- Cannibalization hides in near-synonyms. When two pages target queries you could answer with the same paragraph, they're cannibalizing — merge.
- Programmatic does not mean low-quality. Every page must answer a specific question or solve a specific job. Pages that exist to target a keyword without standalone value will be filtered by both Google and AI answer engines.
- AI citations are a leading indicator of classic ranking. When the cluster starts getting cited by LLMs before it ranks in blue links, stay the course — the rankings usually follow.

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
