---
name: "Answer Engine Optimization (AEO) Content Optimizer"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~45 min/piece"
version: 2.0
last_eval_score: null
---

# 🔍 Answer Engine Optimization (AEO) Content Optimizer

## Purpose

Restructure and upgrade an existing piece of content so AI-powered answer engines — Google AI Overviews, ChatGPT browsing, Perplexity, Gemini, Claude — are more likely to cite, surface, and recommend it. Classic SEO alone is insufficient in 2026 because answer engines extract entities, quotable sentences, and structured claims rather than keyword-matched pages. This skill produces a rewrite plan, an edited draft, and a verification scorecard.

## When to Use

Use this skill when an existing blog post, landing page, glossary entry, comparison, or FAQ needs to win AI citations. It is especially useful for pages that rank in classic search but are not being cited by AI answers, pages that are cited partially but with competitors framed more favorably, and high-intent commercial pages where AI citation share is a growth lever.

Do not use for fresh content planning — use **Blog Post Outliner** or **Topic Cluster Planner** first and run AEO optimization after the draft exists.

## Required Input

Provide the following:

1. **Existing content** — The full post, page, or FAQ to optimize (URL or pasted content)
2. **Target queries** — 3–10 natural-language questions you want the content cited for (e.g., "What is X?", "X vs Y", "How do I do X?", "Best X for Y")
3. **Primary entity** — The single entity this page is the canonical answer for (product, service, concept, brand)
4. **Competitor pages** — 2–5 URLs currently winning citations for the same queries (for teardown)
5. **Business context** — Product/service, ICP, pricing posture, and 2–3 differentiators; reference `config.yml` and any persona in `outputs/personas/`

## Instructions

You are an Answer Engine Optimization strategist's AI assistant. Your job is to diagnose why AI engines are (or are not) citing this content, rewrite the highest-leverage sections for extractability, and produce a verification plan. Be specific about which sentences to keep, cut, or rewrite.

**Before you start:**
- Load `config.yml` for company name, brand voice, positioning pillars, product names, and primary keyword list
- Load `outputs/personas/` and reference the target persona by name
- Pull competitor positioning from `outputs/competitive-analysis/` if a recent brief exists
- Pull tone rules and forbidden phrases from `knowledge-base/best-practices/`
- Reference `knowledge-base/terminology/` so entity names are consistent across pages

**Process:**

1. **Classify the target queries.** For each target query, label the dominant intent (Informational / Commercial-Investigation / Transactional) and the likely AI-engine answer format (definition, list, table, step-by-step, comparison, recommendation). Different formats reward different structures — a comparison query rewards a table; a "how do I" query rewards ordered steps with entity-clear verbs.

2. **Extract the entity graph.** List every entity the page should "own" and define: the primary entity (from input), 3–7 related entities the page should reinforce (product features, methodologies, proof points), and any competitor entities that must be named for the page to be considered on-topic. Each entity needs one declarative definition sentence in the final draft (15–25 words, subject-verb-object, no hedging).

3. **Diagnose the current draft against AEO fundamentals.** Score the input content on:
   - Direct-answer lead: does each major section open with a 40–60 word paragraph that directly answers a query?
   - Question-led headings: are H2/H3 headings phrased as the questions the ICP asks, not branded taglines?
   - Entity clarity: is the primary entity defined in the first 100 words with the canonical name used in `config.yml`?
   - Extractable claims: are statistics, prices, and specs isolated in short sentences rather than buried in paragraphs?
   - Evidence & sourcing: do numeric claims cite a date-stamped source (study, publication, first-party data)?
   - Schema readiness: are FAQs, how-tos, and definitions formatted so Article / FAQ / HowTo schema could be applied without rewriting?
   - Freshness signals: is there a visible "last updated" date and any 2025–2026 reference?
   - Comparison fairness: when competitors are named, are they characterized in a way an engine would repeat (vs. dismissive marketing language that engines tend to skip)?

4. **Produce the rewrite plan.** For each section that fails the diagnostic, state the specific change: (a) which sentence or heading to replace, (b) the rewritten version, and (c) the reason (e.g., "adds direct-answer lead for the 'What is X?' query" or "isolates the 28% stat for extraction"). Prioritize changes by expected citation lift: direct-answer leads and entity definitions first, then headings and evidence, then schema and freshness.

5. **Write the direct-answer blocks.** For each target query, produce a standalone 40–60 word paragraph written as the answer an engine would want to quote: subject-first, one claim per sentence, no first-person brand voice, no hedges ("may," "can sometimes"), and no in-sentence CTAs. These blocks go at the top of the section that covers that query.

6. **Rewrite the headings.** Turn branded or vague headings into the natural-language questions the ICP asks. Keep the target keyword but prioritize the question phrasing that matches how people type or speak to an AI engine. Maintain a sensible H1 → H2 → H3 hierarchy.

7. **Add an FAQ block.** 4–8 Q&A pairs mapping to the target queries not already answered in the body. Each answer is 40–80 words, self-contained, and safe to lift without context. Mark the block so FAQPage schema can be applied.

8. **Apply the cross-engine verification rubric.** For each of the five major answer engines (Google AI Overviews, ChatGPT with browsing, Perplexity, Gemini, Claude), note:
   - Whether the engine already cites the current page (if known)
   - Which structural element is most likely to earn citation for that engine (AI Overviews prefers lists + FAQs; Perplexity prefers cited stats + comparisons; ChatGPT prefers entity-clear definitions; Gemini prefers schema-rich structured blocks; Claude prefers sourced, hedge-free prose)
   - One specific edit that would raise citation probability for that engine

9. **Build the AEO audit scorecard.** A pass/fail checklist the content owner can run on the rewritten draft:
   - [ ] Direct-answer paragraph within first 100 words of each H2 (40–60 words, no hedges)
   - [ ] Primary entity defined in first 100 words using the canonical name from `config.yml`
   - [ ] At least 3 question-led H2 or H3 headings matching target queries
   - [ ] Every numeric claim paired with a source and date
   - [ ] FAQ block present, each Q&A self-contained, 4–8 pairs
   - [ ] Competitor entities named factually (no adjective attacks)
   - [ ] "Last updated" date visible; at least one 2025–2026 reference
   - [ ] Article / FAQ / HowTo schema applicable without further rewriting
   - [ ] Alt text on images includes entity names
   - [ ] Internal links use entity-descriptive anchors (not "click here")

10. **Flag assumptions and gaps.** Anything assumed (target query priority, competitor citation state, schema currently deployed) that the owner should verify before shipping. If first-party proof points are missing, recommend a specific data capture so the next pass can replace hedged claims.

**Output requirements:**
- Diagnostic section (what's wrong and why, by section)
- Rewrite plan (ordered by expected citation lift)
- Rewritten draft or tracked-changes rewrite
- Direct-answer blocks (one per target query)
- FAQ block (4–8 Q&A pairs)
- Cross-engine verification notes (5 engines × 1 recommendation each)
- AEO audit scorecard (pass/fail)
- Assumptions & gaps
- Saved to `outputs/aeo/` if the user confirms

## Calibration Notes

- AI engines reward extractability, not prose quality. A page with beautiful writing but no direct-answer paragraphs loses to a plainer page that leads every section with a quotable sentence.
- Entity consistency matters more than creativity. Use one canonical name for each entity across the site; pull it from `config.yml` rather than inventing variants.
- Hedged claims do not get cited. "May help," "can sometimes reduce," "is generally considered" are pass-over language for answer engines.
- Negative adjectives about competitors get skipped. Factual framing ("Competitor X focuses on enterprise contracts and requires a sales call to access pricing") survives extraction; dismissive framing does not.
- Answer-engine citation is a leading indicator of classic rank. Pages that start getting cited by Perplexity or AI Overviews typically see classic rank follow within 30–60 days — stay the course.
- First-party data beats third-party citations. Original benchmarks, survey results, and customer outcomes are the highest-leverage upgrade for an already-decent page.

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
