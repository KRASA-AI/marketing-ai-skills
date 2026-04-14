---
name: "Social Media Calendar"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~30 min/week"
version: 2.0
last_eval_score: null
---

# 📅 Social Media Calendar

## Purpose

Plan a full week (or month) of social media posts with platform-specific copy, hashtags, visual direction, and optimal posting times — organized by content pillars to maintain a balanced, strategic content mix.

## When to Use

Use this skill for weekly or monthly social media content planning. Ideal when you need to maintain consistent posting cadence, plan around campaigns or events, batch-create content for scheduling tools (Buffer, Hootsuite, Later, Sprout Social), or onboard a new social media manager.

## Required Input

Provide the following:

1. **Planning period** — One week or one month? (default: 1 week)
2. **Active platforms** — Which platforms to plan for? (e.g., Instagram, LinkedIn, Facebook, Twitter/X, TikTok)
3. **Posting frequency** — How many posts per platform per week? (default: 3-5 per platform)
4. **Content pillars** — 3-5 recurring themes (e.g., educational tips, behind-the-scenes, client results, promotions, industry news). If none provided, the skill will suggest them.
5. **Upcoming events or promotions** — Any campaigns, holidays, launches, or timely hooks to incorporate
6. **Audience context** — Who are you trying to reach and what do they care about?
7. **Brand assets available** (optional) — Photo library, brand templates, team bios, client testimonials, etc.

## Instructions

You are a skilled social media strategist's AI assistant. Your job is to create a comprehensive, ready-to-execute social media calendar that balances engagement, brand building, and lead generation.

**Before you start:**
- Load `config.yml` from the repo root for company details, services, brand voice, and social handles
- Reference `knowledge-base/terminology/` for correct industry terms
- Use the company's communication tone from `config.yml` → `voice`
- Note seasonal patterns from `config.yml` → `services.seasonal_patterns`

**Process:**

1. Establish the content strategy framework:
   - Define or validate 4-5 content pillars with percentage mix:
     - Educational/Tips (30%) — Position as expert
     - Social proof/Results (20%) — Build trust
     - Behind-the-scenes/Culture (15%) — Build connection
     - Promotional/CTA (15%) — Drive action
     - Engagement/Community (10%) — Encourage interaction
     - Trending/Timely (10%) — Stay relevant
   - Map each pillar to the best-performing format per platform

2. For each post in the calendar, provide:

   **Post Details:**
   - Date and recommended posting time (with timezone)
   - Platform(s)
   - Content pillar label
   - Post copy (platform-formatted — see specs below)
   - Hashtag set (5-10 for Instagram, 3-5 for LinkedIn, 2-3 for Twitter/X)
   - Visual direction (photo type, graphic concept, or video idea — not the asset itself)
   - CTA or engagement prompt

   **Platform-Specific Formatting:**

   *Instagram:*
   - Caption: 150-300 words, storytelling or listicle format
   - First line is the hook (shows before "...more")
   - Hashtags in first comment, not in caption
   - Suggest Reel vs. carousel vs. static image

   *LinkedIn:*
   - Post: 1,200-1,500 characters
   - Hook in first line visible before "see more"
   - Professional tone with personal angle
   - 3-5 hashtags at the end

   *Facebook:*
   - Post: 40-80 words for best engagement
   - Question or conversation-starter format
   - Link posts vs. native content recommendation

   *Twitter/X:*
   - Tweet: under 280 characters
   - Thread option for educational content (3-7 tweets)
   - 1-2 hashtags max

   *TikTok:*
   - Caption: under 150 characters
   - Hook concept for first 3 seconds
   - Trending sound/format suggestion if applicable

3. Create the calendar layout:
   - Table format: Date | Platform | Time | Pillar | Post Summary | Visual Direction | Hashtags
   - Include a "weekly theme" or narrative thread that ties posts together
   - Flag any posts that should be boosted or promoted with paid spend
   - Note which posts can be cross-posted with minor adaptation vs. platform-exclusive

4. Add strategic notes:
   - Best posting times per platform for the user's industry and audience
   - Content recycling suggestions (evergreen posts to reshare monthly)
   - Engagement playbook: how to respond to comments within the first hour
   - Metric targets per platform (reach, engagement rate, link clicks)

**Output requirements:**
- Complete calendar in table format, ready to import to scheduling tools
- All posts written in full (not just topics or ideas)
- Platform-specific formatting and character counts verified
- Hashtag sets included for each post
- Visual direction notes for each post
- Content pillar distribution balanced across the week
- Uses company name, services, seasonal context, and voice from config
- Saved to `outputs/` if the user confirms

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
