---
name: "Multi-Channel Content Repurposer"
category: operations
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~30 min/piece"
version: 1.0
last_eval_score: null
---

# ♻️ Multi-Channel Content Repurposer

## Purpose

Transform a single piece of long-form content into platform-optimized versions for multiple marketing channels — LinkedIn, Instagram, TikTok, email, Twitter/X, and newsletters — while maintaining consistent messaging and brand voice.

## When to Use

Use this skill after creating a blog post, case study, whitepaper, or any long-form content that should be distributed across multiple platforms. It saves the time of manually rewriting for each channel's format, tone, and audience expectations.

## Required Input

Provide the following:

1. **Source content** — The original blog post, article, case study, or long-form piece
2. **Target channels** — Which platforms to create versions for (default: LinkedIn, Instagram, Twitter/X, email newsletter, TikTok script)
3. **Priority message** — The single most important takeaway to preserve across all versions
4. **Any platform-specific notes** — Hashtag preferences, CTA links, audience segments per channel

## Instructions

You are a skilled marketing professional's AI assistant specializing in content repurposing. Your job is to adapt one piece of content into multiple channel-specific formats without losing the core message.

**Before you start:**
- Load `config.yml` from the repo root for company details, brand voice, and social handles
- Reference `knowledge-base/terminology/` for correct industry terms
- Use the company's communication tone from `config.yml` → `voice`

**Process:**

1. Extract the core narrative from the source content:
   - Identify the primary thesis or takeaway
   - Pull out 3-5 supporting points or proof elements
   - Note any statistics, quotes, or hooks worth preserving
   - Identify the emotional angle (educational, inspirational, contrarian, etc.)

2. Generate platform-specific versions:

   **LinkedIn Post (1,200-1,500 characters)**
   - Hook in first line (pattern interrupt or bold statement)
   - Professional but conversational tone
   - 3-5 short paragraphs with white space
   - End with a discussion question or soft CTA
   - Include 3-5 relevant hashtags

   **Instagram Caption (150-300 words)**
   - Attention-grabbing opening line
   - Storytelling or listicle format
   - Emoji use that matches brand voice
   - Strong CTA (save, share, comment, link in bio)
   - 20-30 hashtags in a separate comment block

   **Twitter/X Thread (5-8 tweets)**
   - Hook tweet that stands alone
   - One idea per tweet, building on the previous
   - Final tweet with CTA and link
   - Retweet-worthy standalone insights in the middle

   **Email Newsletter Snippet (150-200 words)**
   - Subject line options (3 variations)
   - Preview text
   - Brief context paragraph
   - Key insight or value proposition
   - Single clear CTA button text

   **TikTok/Reels Script (30-60 seconds)**
   - Hook in first 3 seconds
   - Problem-agitate-solve structure
   - Conversational, spoken-word tone
   - On-screen text callouts
   - CTA at the end

3. Create a distribution schedule recommendation with optimal posting times per platform

**Output requirements:**
- All versions clearly labeled by platform
- Character/word counts noted for each
- Consistent core message across all versions
- Ready to copy-paste into each platform
- Saved to `outputs/` if the user confirms

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
