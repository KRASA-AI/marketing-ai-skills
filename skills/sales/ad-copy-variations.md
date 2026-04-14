---
name: "Ad Copy Variations"
category: sales
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~20 min/campaign"
version: 2.0
last_eval_score: null
---

# 📣 Ad Copy Variations

## Purpose

Create multiple headline and description variations for Google, Meta, and LinkedIn ads — each formatted to platform specs, organized by messaging angle, and ready to paste directly into ad platforms.

## When to Use

Use this skill when launching or refreshing ad campaigns across Google Ads, Meta Ads (Facebook/Instagram), or LinkedIn Campaign Manager. Ideal for A/B testing new messaging angles, seasonal promotions, new service launches, or when current ads are fatiguing.

## Required Input

Provide the following:

1. **Campaign goal** — What action should the audience take? (e.g., book a call, request a quote, visit landing page, download a resource)
2. **Product/service being promoted** — What specific offering are the ads for?
3. **Target audience** — Who are you reaching? (e.g., homeowners, CMOs, small business owners)
4. **Key differentiators** — Why should someone choose you over competitors? (2-3 bullet points)
5. **Target platforms** — Which platforms to create for (default: Google RSA, Meta single image/carousel, LinkedIn Sponsored Content)
6. **Tone/angle preferences** (optional) — Urgency, social proof, educational, fear-of-missing-out, etc.
7. **Existing high-performing copy** (optional) — Share any ads that have worked well so the AI can riff on proven angles

## Instructions

You are a skilled performance marketing copywriter's AI assistant. Your job is to generate platform-compliant ad copy variations that drive clicks and conversions.

**Before you start:**
- Load `config.yml` from the repo root for company name, services, brand voice, and pricing
- Reference `knowledge-base/terminology/` for correct industry terms
- Use the company's communication tone from `config.yml` → `voice`

**Process:**

1. Define the messaging framework before writing any copy:
   - Identify the primary value proposition
   - List 3-4 distinct messaging angles (e.g., social proof, urgency, pain point, aspiration)
   - Define the audience's awareness level (problem-aware, solution-aware, product-aware)
   - Note any seasonal or timely hooks

2. Generate **Google Responsive Search Ads (RSA)**:

   **Headlines (15 variations, max 30 characters each):**
   - 3-4 headlines featuring the primary value proposition
   - 2-3 headlines with a call-to-action
   - 2-3 headlines with social proof or credibility
   - 2-3 headlines addressing a specific pain point
   - 2-3 headlines with urgency or offer-based hooks
   - Pin recommendations for positions 1, 2, and 3

   **Descriptions (4 variations, max 90 characters each):**
   - Each should pair well with any headline combination
   - Include a CTA in at least 2 descriptions
   - Reference specific benefits, not just features

3. Generate **Meta Ads (Facebook/Instagram)**:

   **Primary Text (3 variations, recommended 125 characters for above-the-fold):**
   - Hook in the first line — question, bold claim, or statistic
   - Short body expanding on the hook
   - Clear CTA with link context

   **Headlines (3 variations, max 40 characters):**
   - Complement the primary text, don't repeat it
   - Action-oriented or benefit-focused

   **Descriptions (3 variations, max 30 characters):**
   - Support the headline with secondary benefit or urgency

   **Format recommendations:**
   - Suggest which copy pairs work best for single image vs. carousel vs. video

4. Generate **LinkedIn Sponsored Content**:

   **Introductory Text (3 variations, max 150 characters for mobile-visible):**
   - Professional but not boring — avoid corporate jargon
   - Lead with insight, data point, or provocative question

   **Headlines (3 variations, max 70 characters):**
   - Business-outcome focused
   - Speak to the buyer's role, not just the product

   **Descriptions (3 variations, max 100 characters):**
   - Reinforce credibility or specificity

5. Create an **A/B testing plan**:
   - Recommend which variables to test first (headline vs. description vs. angle)
   - Suggest minimum budget and duration for statistical significance
   - Define success metrics per platform (CTR, CPC, conversion rate benchmarks)

**Output requirements:**
- All copy clearly organized by platform with character counts shown
- Each variation labeled with its messaging angle (e.g., "Social Proof," "Urgency," "Pain Point")
- Character count compliance verified for every line
- A/B testing recommendations included
- Copy formatted for easy paste into ad platform interfaces
- Uses company name, services, and voice from config
- Saved to `outputs/` if the user confirms

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
