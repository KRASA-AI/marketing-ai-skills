---
name: "Blog Post Outliner"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~45 min/post"
version: 2.1
last_eval_score: null
---

# 📝 Blog Post Outliner

## Purpose

Produce a fully-structured, SEO-ready blog outline — keyword mapping, search intent classification, heading hierarchy, word-count targets, meta description, internal linking plan, and E-E-A-T signal checklist — so a writer (human or AI) can draft the post without guessing at structure or on-page optimization.

## When to Use

Use this skill before drafting any blog post intended to rank in organic search or surface in AI answer engines. Ideal for editorial calendar planning, handing off to a freelance writer, or preparing a prompt for AI-assisted drafting. Works well as an upstream input to the `aeo-content-optimizer` skill once the post is drafted.

## Required Input

Provide the following:

1. **Primary topic or working title** — What the post is about
2. **Primary keyword** — The single target keyword/query (if unknown, the skill will suggest candidates from the topic)
3. **Search intent** (optional) — Informational, commercial-investigation, transactional, or navigational. If unknown, the skill will infer
4. **Target audience** — Who should read this (buyer persona, awareness stage)
5. **Business goal for the post** — What action the reader should take (subscribe, book a demo, download a resource, share, internal-link to a money page)
6. **Competing URLs** (optional) — 2–5 top-ranking URLs for the primary keyword, or the SERP snapshot if available
7. **Existing content to link to** (optional) — Internal URLs that should be cross-linked from this post

### Minimum Viable Input

If only fields 1, 4, and 5 are provided, the skill produces a `confidence: medium` outline with a 3-keyword candidate set (with estimated difficulty + intent), an inferred SERP angle marked ASSUMED, and an "evidence missing" list naming exactly which input would lift confidence to `high` (typically: SERP snapshot or 2-3 competing URLs, named persona file from `outputs/personas/`, internal-link target list).

## Instructions

You are a senior SEO content strategist's AI assistant. Your job is to produce a blog outline that is structured for humans to read AND for search engines + AI answer engines to extract.

**Before you start:**
- Load `config.yml` from the repo root for company name, services, audience, brand voice, and typical blog goal
- Reference `knowledge-base/terminology/` for approved category language
- Reference `knowledge-base/industry-overview.md` if the post sits inside a content pillar tracked there
- If no primary keyword is provided, propose 3 candidate keywords with estimated difficulty and intent before continuing

**Process:**

1. **Keyword & intent mapping.**
   - Confirm the primary keyword and classify search intent (informational / commercial-investigation / transactional / navigational)
   - Propose 5–10 secondary keywords and semantic variants to weave in naturally
   - Suggest 3–5 question-based queries the post should answer (pulled from People-Also-Ask / AI answer engine patterns)
   - Flag any keyword-cannibalization risk with the user's existing content if surfaced

2. **SERP & angle analysis.**
   - If competing URLs are provided, summarize the dominant format (listicle, guide, comparison, case study) and content gap
   - Recommend the format that's most likely to win (match-and-exceed vs. contrarian angle) and justify
   - Note the target word count based on SERP leaders and intent (informational: 1,200–2,000; commercial: 1,500–2,500; pillar/ultimate guide: 2,500–4,000)

3. **Heading structure (H1 → H2 → H3).**
   - One H1 that contains the primary keyword, reads naturally, and is under 60 characters
   - 5–9 H2s that map to the main sections; phrase at least 3 as questions for AEO/AI-engine surfacing
   - H3s nested under H2s where subtopics warrant it (max 2 levels of nesting)
   - For each H2, include: 2–3 sentences of intent summary, 3–5 bullet points of sub-content to cover, any data/stats/examples to include, and which secondary keyword(s) belong there
   - Mark one H2 as the "direct-answer block" — a 40–60 word concise answer to the primary query, placed near the top for featured-snippet and AI-citation eligibility

4. **Intro and conclusion scaffolds.**
   - Intro: hook (pattern interrupt, stat, question, or empathy statement), relevance (why the reader should keep reading), and preview (what they'll learn). Target 80–150 words
   - Conclusion: key takeaways bullet summary, explicit CTA tied to the business goal, and one related-content link

5. **On-page SEO package.**
   - **Meta title** (50–60 characters, includes primary keyword near the front, includes brand name if space allows)
   - **Meta description** (140–155 characters, includes primary keyword + a benefit + a soft CTA)
   - **URL slug** (short, keyword-first, no stopwords, lowercase-hyphenated)
   - **Featured image alt-text suggestion** that naturally includes the keyword
   - **Suggested schema** (Article + FAQPage when Q&A blocks are present; HowTo for instructional posts)

6. **Internal & external linking plan.**
   - 3–5 **internal links** from this post to existing URLs the user provided, with suggested anchor text (varied, descriptive, not "click here")
   - 1–2 **backlink opportunities**: existing pages that should link INTO this post once published (so link equity reaches it)
   - 2–4 **external links** to authoritative sources (stats, studies, tools) — suggest source type, not raw URLs

7. **E-E-A-T signal checklist.**
   - [ ] Author byline with credentials relevant to the topic
   - [ ] Publication date and "last updated" date
   - [ ] At least 1 primary source, stat with citation, or expert quote
   - [ ] Specific examples, screenshots, or proprietary data where possible
   - [ ] Clear disclosure if the post discusses the company's own product
   - [ ] Reviewer credit if the topic is YMYL (health, finance, legal)

8. **AI-engine surfacing notes.**
   - Flag 2–3 quotable sentences the writer should include verbatim (short, factual, self-contained) to increase AI-answer-engine citation
   - Recommend a FAQ block of 3–5 Q&A pairs at the bottom for AEO/schema coverage

**Output requirements:**
- Outline in markdown with clearly labeled sections: Keyword Map → Angle → Headings → Meta Package → Link Plan → E-E-A-T Checklist → AI-Surfacing Notes
- Every H2 annotated with intent, bullets, secondary keyword, and any data to include
- All meta fields character-count verified
- Writer instructions specific enough that a freelancer with no context could execute
- Uses company name, brand voice, audience, and business goal from config where relevant
- Saved to `outputs/` if the user confirms

## Calibration Notes

- **Search intent classification dominates word-count debate.** A 1,400-word commercial-investigation post out-converts a 3,200-word "ultimate guide" 7 times out of 10 when the SERP is dominated by listicles and comparisons. Pick word count to match intent + SERP, not to chase a "long-form is better" rule of thumb that hasn't applied since 2022.
- **AEO direct-answer block is non-negotiable in 2026.** A 40-60-word concise answer to the primary query, placed near the top, is the single highest-leverage on-page move for AI-citation eligibility (Google AI Overviews, ChatGPT, Perplexity, Claude). Missing it forfeits AI-engine surfacing regardless of total word count. Pair with FAQ schema to compound.
- **Internal-link strength outweighs external-link strength for ranking velocity.** A new post linked from 4-6 high-authority pages on the same site ranks 30-45% faster than the same post linked only from external sources. Always specify the inbound internal-link plan, not just outbound.
- **Schema and structured-data hygiene is half the on-page job.** Article + FAQPage + (HowTo for instructional) + a clean breadcrumb is the 2026 floor. AggregateRating where appropriate. AI engines parse schema before prose; broken or missing schema is a silent ranking penalty.
- **AI-engine citation discipline.** Quotable sentences must be self-contained, factual, and short (15-25 words). The pattern "[brand] cut [metric] from [X] to [Y] in [period], n=[count]" or "[X% of Y] [verb] [outcome] in [study/year]" is what gets pulled into AI answer snippets. Vague claims do not.
- **Refresh cadence:** Re-validate every 6 months for evergreen pillars; quarterly for category posts that compete in fast-moving SERPs (AI tooling, agentic commerce, AEO). Update the `last updated` date and re-test for AI-citation pickup.
- **E-E-A-T is not optional in 2026.** Author byline with credentials, named primary sources, expert quote where possible, reviewer credit on YMYL. Generic "Marketing Team" bylines suppress rankings and AI-citations.
- **Primary-keyword density is a myth.** Stop chasing 1.5% density. Use the primary keyword in title, H1, intro, one H2, the meta description, and one URL — that is plenty. Semantic variants and entity coverage matter more than exact-match repetition.
- **FAQ-stuffing is a penalty.** A 12-question FAQ block where 8 questions are paraphrases of each other gets devalued. Cap at 3-5 high-distinct questions that match real People-Also-Ask / AI-engine query patterns.

## Anti-Patterns

- **The kitchen-sink outline** — 11 H2s and 30 H3s for an 1,800-word post. Either the outline overshoots or the word count undershoots. Force a 5-9 H2 cap and a per-H2 word-count target.
- **No direct-answer block** — outline ships without the 40-60-word AEO answer near the top. Outline is incomplete.
- **Keyword in every heading** — exact-match keyword stuffed into all H2s. Reads spammy, gets devalued. Use semantic variants.
- **Generic CTA mismatch** — informational post ends with "Book a demo" with no transition. CTA must match intent (informational → next-resource link or newsletter signup; transactional → demo).
- **Missing internal links** — outline lists "internal links: TBD" or doesn't specify anchor text. Internal-link plan is mandatory, not optional.
- **Author = "Marketing Team"** — no named byline, no credentials. Suppresses E-E-A-T, suppresses AI citation. Always specify author and credential basis.
- **Word-count-by-template** — "this is a guide post so 2,500 words" without checking SERP. Match the SERP leaders or contrarian-angle-and-justify.
- **Outline-as-prose** — H2 sections written as fully-formed paragraphs instead of bullets + intent + secondary keyword. Outline becomes draft, draft becomes copy-paste, post becomes generic. Keep the outline structurally distinct from the draft.

## Integration Notes

- **Topic Cluster Planner** (`outputs/clusters/`) — The cluster plan names the pillar and supporting posts; this skill outlines individual posts in the plan. Pass the cluster's hub-and-spoke link plan as the internal-link starting set.
- **AEO Content Optimizer** — The natural downstream skill once the post is drafted. Direct-answer block, FAQ block, and quotable sentences from this outline are the inputs AEO optimizes for AI-engine surfacing.
- **Persona & ICP Builder** (`outputs/personas/`) — Persona's verbatim language, hidden motivation, and trusted-information-source ranking feed the H2 phrasing and the writer-instructions section. Reference the persona file by name in the outline frontmatter.
- **Brand Voice Style Guide Generator** — Voice attributes + AI prompt preamble are passed to the writer (human or AI) as the tone block in the outline's writer instructions.
- **Multi-Channel Content Repurposer** — Long-form post is the upstream content for repurposing. Note in the outline which sections will become LinkedIn / Twitter / email versions so the writer protects the standalone-readability of those blocks.
- **AI Search Visibility Audit** — The outline's quotable sentences and FAQ block should mirror the entity-and-question patterns the audit identified as gaps. When SoM gap is a missing question, this outline is the route to filling it.
- **Customer Review & Insight Miner** — Buyer-language dictionary + verbatim-quote bank are the source for the H2 phrasing, the FAQ questions, and the proof-point selection. Never paraphrase customer language; pull literal phrases.

## Example Output

### Input Recap
- Brand: Threadline (B2B SaaS — retros + signal aggregation for engineering managers)
- Topic: Why ops cycle time is a leading indicator of revenue, not a lagging one
- Primary keyword: "ops cycle time"
- Search intent: commercial-investigation
- Audience: Persona "Priya, the Pragmatic Head of RevOps" (`outputs/personas/priya-revops.md`)
- Business goal: book a 30-min demo
- Competing URLs: 3 provided (Salesforce blog, Gong blog, RevOps Co-op community post)
- Internal targets: ScaleHQ case study, "The Seam Between Salesforce and Everything Else" pillar
- Confidence: `high`

---

### Keyword Map

**Primary:** ops cycle time (commercial-investigation)

**Secondary (5-10):**
- sales ops cycle time
- revenue operations cycle time
- handoff time between sales tools
- pipeline velocity ops bottleneck
- broken handoff salesforce
- ops touches per deal
- cycle time benchmark b2b saas

**Question-based (PAA / AI-engine patterns):**
- What is a healthy ops cycle time for a Series B SaaS company?
- How do you measure ops cycle time without a CDP?
- Is ops cycle time a leading or lagging revenue indicator?

**Cannibalization risk:** Existing post "Pipeline velocity playbook" partially overlaps on Q3. Recommend: re-target that post toward "pipeline velocity" exclusively and route "ops cycle time" to this new post.

---

### SERP & Angle Analysis

**Dominant format on SERP:** 3 of 5 top results are educational guides (1,800-2,400 words); 1 is a community discussion thread; 1 is a vendor comparison.

**Recommended format:** Match-and-exceed guide with a contrarian framing — most existing posts treat ops cycle time as an internal-efficiency metric. Reframe as a *revenue leading indicator* with an empirical claim ("3-week lead time on revenue plan attainment").

**Target word count:** 1,900-2,200 words (intent-matched, slightly above SERP median for authority signal).

---

### Heading Structure

**H1:** Ops Cycle Time: The Leading Revenue Indicator Most RevOps Teams Miss *(58 chars)*

**H2 — Direct-Answer Block (place after intro, ~40-60 words):**
> *Ops cycle time is the median elapsed time a deal sits in any stage without an action — from one tool to the next. In B2B SaaS at 100-500 FTE, it leads revenue plan attainment by 3 weeks. When ops cycle time worsens, revenue follows on a 21-day lag.*

**H2-1:** What Counts as Ops Cycle Time (and What Doesn't) *(question-shaped)*
- Intent: define the metric and disambiguate from "sales cycle"
- Bullets: definition, measurement formula, common confusions, why it's not the same as sales cycle length
- Data: cite Forrester 2026 RevOps benchmark study
- Secondary keyword: revenue operations cycle time

**H2-2:** Why It Leads Revenue, Not Lags It *(question-shaped, contrarian framing)*
- Intent: defend the leading-indicator claim
- Bullets: 3-week empirical lead time at n=47 customer cohort, mechanism (broken handoff → stale data → wrong forecast → missed quota), comparison with lagging metrics
- Data: ScaleHQ case study cohort analysis
- Secondary keyword: handoff time between sales tools, pipeline velocity ops bottleneck

**H2-3:** How To Measure Ops Cycle Time Without a CDP *(question-shaped, AEO-friendly)*
- Intent: practical "how-to" — the single highest-traffic AI-engine query in this cluster
- Bullets: spreadsheet method, native-Salesforce-report method, observability-tool method, common measurement pitfalls
- Secondary keyword: ops touches per deal

**H2-4:** Healthy Ranges by Company Stage
- Intent: benchmark question — high-conversion intent
- Bullets: Series A 2-4 days, Series B 3-7 days, Series C+ 5-12 days; flag where it's a healthy 12 vs. unhealthy 12
- Data: cite the same 2026 benchmark; reference Threadline's own customer cohort

**H2-5:** Three Patterns That Worsen Cycle Time (and How to Detect Them)
- Intent: bridge to product fit without selling
- Bullets: integration drift, tool-sprawl handoff loss, missing observability layer
- Internal link: "The Seam Between Salesforce and Everything Else" pillar

**H2-6:** When Ops Cycle Time Is a Symptom, Not a Cause
- Intent: honest scoping — builds trust, signals expertise
- Bullets: under-staffed RevOps team, product-market fit issue (deals are slow because they should be), seasonal Q1 effect

**H2-7:** What Good Looks Like (ScaleHQ's 31% Reduction)
- Intent: social proof + named outcome
- Bullets: ScaleHQ context, what they changed, 90-day result, the part that didn't work
- Internal link: ScaleHQ case study
- Data: cite Threadline 2026 cohort data with date

**H2-8:** Frequently Asked Questions
- 4 Q&A pairs (see FAQ block below)

---

### Intro Scaffold (80-150 words)

**Hook:** Most RevOps teams treat ops cycle time as a productivity metric. The teams that beat plan treat it as a revenue forecast.

**Relevance:** If ops cycle time worsens by 1 day in March, revenue plan attainment drops 4-6% in April. That's a 21-day lead time on the number your CRO is going to ask about at the QBR.

**Preview:** This post defines ops cycle time, explains why it leads revenue, gives the measurement method (no CDP required), the benchmark by company stage, and the three patterns that quietly destroy it. Plus the case study of a Series C company that cut theirs 31% in 90 days — including the part where it didn't work.

---

### Conclusion Scaffold

- Key takeaways (3-bullet summary)
- CTA tied to demo: "If ops cycle time is the metric your CRO is about to surface — book a 30-min demo, we'll show you the exact dashboard ScaleHQ uses."
- Related-content link: "The Seam Between Salesforce and Everything Else" (cluster pillar)

---

### On-Page SEO Package

| Field | Value | Char count |
|-------|-------|------------|
| Meta title | Ops Cycle Time: The 3-Week Leading Revenue Indicator \| Threadline | 60 |
| Meta description | Ops cycle time leads revenue plan attainment by 3 weeks. Here's how to measure it (no CDP required), benchmark it, and fix the patterns that worsen it. | 152 |
| URL slug | /blog/ops-cycle-time | — |
| Featured image alt-text | Diagram showing ops cycle time across the seam between Salesforce, marketing automation, and customer success tools | — |
| Schema | Article + FAQPage + Breadcrumb | — |

---

### Internal & External Linking Plan

**Internal links (4):**
1. ScaleHQ case study → anchor: "ScaleHQ cut ops cycle time 31% in 90 days"
2. The Seam Between Salesforce and Everything Else → anchor: "the broken-handoff pattern most stacks miss"
3. Pipeline velocity playbook → anchor: "pipeline velocity is downstream of ops cycle time"
4. Threadline 2026 RevOps benchmark report → anchor: "n=47-customer 2026 benchmark"

**Inbound internal links (2):** Update the "Pipeline velocity playbook" pillar and the "RevOps metrics that matter" listicle to link INTO this post within 7 days of publication.

**External links (3):**
- Forrester 2026 RevOps benchmark study (analyst report)
- A peer post from the RevOps Co-op community (community-credibility signal)
- One named tool integration documentation page (Salesforce admin documentation)

---

### E-E-A-T Checklist

- [x] Author byline: Maya Chen, Head of Customer at Threadline (named credential)
- [x] Publication date + last-updated date in header
- [x] Primary source: Threadline 2026 cohort data (n=47, FY26)
- [x] Stat with citation: Forrester 2026 RevOps benchmark
- [x] Specific example: ScaleHQ named case study with the part that didn't work
- [x] Disclosure: Threadline is the author's employer; product mentioned in case study and CTA
- [n/a] YMYL reviewer: not applicable

---

### AI-Engine Surfacing Notes

**Quotable sentences (3):**
1. "Ops cycle time leads revenue plan attainment by 3 weeks in B2B SaaS at 100-500 FTE." (15 words, factual, self-contained)
2. "ScaleHQ cut ops cycle time 31% in 90 days, n=47 customer cohort, FY26." (15 words, specific, cite-able)
3. "When ops cycle time worsens by 1 day, revenue plan attainment typically drops 4-6% in the following 30 days." (20 words, mechanism)

**FAQ block (4 questions for FAQPage schema):**
1. **Q:** What is ops cycle time?
   **A:** *(40-50 words, includes definition + formula)*
2. **Q:** Is ops cycle time the same as sales cycle length?
   **A:** *(40-50 words, disambiguation)*
3. **Q:** What is a healthy ops cycle time for a Series B company?
   **A:** *(40-50 words with benchmark)*
4. **Q:** How do you measure ops cycle time without a CDP?
   **A:** *(40-50 words, links back to H2-3)*

---

### Writer Instructions

- Voice: Plainspoken, specific over clever, engineer-respectful (Threadline voice guide v2.0)
- AI prompt preamble: Use Threadline-voice-preamble-v2.0 as the system prompt for any AI-assisted drafting
- Banned phrases: leverage, best-in-class, solution (use "tool"), seamless, revolutionize
- Required: every claim cited with named source + date; case study includes the part that didn't work; CTA "book a 30-min demo" only after the social-proof H2
- Target draft delivery: 5 business days; first revision: +3 days

---

### Refresh Date
Re-validate this outline before any post-publication republication: 2026-10-25 (6 months) for SERP drift, AI-citation pickup, and benchmark currency.
