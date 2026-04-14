---
name: "Blog Post Outliner"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~45 min/post"
version: 2.0
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

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
