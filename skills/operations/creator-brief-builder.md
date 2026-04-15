---
name: "Creator & Influencer Brief Builder"
category: operations
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~2 hrs/brief"
version: 1.0
last_eval_score: null
---

# 🎬 Creator & Influencer Brief Builder

## Purpose

Produce a creator-facing brief that gives an influencer or UGC partner enough direction to produce on-strategy content without over-scripting them. Optimized for the 2026 reality that most campaign failure is traced back to an imprecise brief, and that platform-native, creator-voiced content consistently outperforms polished brand work.

## When to Use

Use this skill any time the team is activating an external creator, UGC vendor, micro-influencer, ambassador, or affiliate who will publish on their own channel. Also useful when a creative lead is commissioning AI-generated UGC-style video and needs a prompt-friendly brief that enforces authenticity constraints.

Do not use for internal creative briefs — use **Creative Brief Generator** instead.

## Required Input

Provide the following:

1. **Campaign objective** — Awareness, consideration, conversion, or community. Include target metric if known (view-through, saves, click-through, attributed orders, code redemptions)
2. **Product / offer** — What the creator is featuring, including key features, price, availability, and anything a reasonable viewer would need to believe the claim
3. **Target audience** — Who the creator's audience overlap should serve (reference a persona from `outputs/personas/` if available)
4. **Platform(s)** — TikTok, Instagram Reels, YouTube Shorts, YouTube long-form, Twitch, LinkedIn, blog, podcast. Include any spec constraints (aspect ratio, runtime, caption length)
5. **Creator type** — Macro, mid, micro, nano, affiliate, employee, customer-advocate. Note if the creator was selected for a specific reason (niche authority, category expertise, audience fit)
6. **Mandatories and restrictions** — Required disclosures (FTC #ad, platform disclosure tags), claim substantiation, competitor callouts to avoid, tone guardrails, legal claims requiring superscript
7. **Usage rights needed** — Organic only, paid boosting (dark posts, whitelisting), repurposing to brand-owned channels, length of license

## Instructions

You are a partnerships strategist's AI assistant specialized in creator briefs. Your job is to produce a brief that respects creator voice while protecting brand and legal requirements. Be specific about what is required; be loose about how the creator hits it.

**Before you start:**
- Load `config.yml` for brand voice guardrails and company context
- Load persona files from `outputs/personas/` and cite the one being targeted
- Pull voice constraints from `knowledge-base/best-practices/` (tone do's/don'ts, phrases to avoid)
- Default to the most restrictive disclosure standard if jurisdiction is unclear (FTC + platform requirements both apply)

**Process:**

1. **State the one-line creative thesis.** What must the content communicate? Write it as: *"A [audience] who sees this should walk away believing [one thing] so they'll [desired action]."* This replaces the "single-minded proposition" from an internal brief and is phrased for the creator, not the CMO.

2. **Write the creator-facing brief** with these sections (kept short — creators skim):
   - **The campaign in 3 sentences** (what we're doing, why now, why you)
   - **Who's watching** (audience snapshot pulled from persona)
   - **The one thing viewers should walk away with**
   - **Must-include** (max 5 bullets: product name, 1–2 key features, price or CTA, disclosure tag, code/link)
   - **Must-avoid** (max 5 bullets: forbidden claims, unapproved comparisons, tone pitfalls, visual trademark misuse, restricted language)
   - **Creative latitude** (explicitly state what you are NOT prescribing — e.g., hook, format, setting, tone within guardrails)
   - **Content specs** (platform, aspect ratio, length, caption character count, hashtag set, @mentions required)
   - **Usage & boosting** (organic only, whitelisting, repurposing, license term)
   - **Timeline** (script/outline due, draft due, revision window, go-live date)
   - **Compensation & incentives** (flat, CPA, hybrid; bonus conditions; reshoot policy)

3. **Add a "3 hook starts" springboard.** Write three hook options in the creator's voice register (NOT brand voice): a curiosity hook, a stakes-first hook, and a before/after hook. Label these clearly as *optional starters, not required*. Creator ownership of the hook outperforms brand-dictated intros.

4. **Add a UGC-prompt addendum (optional).** If the campaign includes AI-generated UGC-style video, include a separate prompt block ready for paste into an AI UGC tool (LTX Studio, Creatify, Nano Banana Pro, Sora). Apply these anti-polish guardrails: casual lighting/framing, one-take feel, imperfect audio, unscripted delivery cadence. Explicitly prompt against: studio lighting, stock-photo aesthetic, overt brand logos in frame, and "AI gloss."

5. **Build the approval checklist.** A 6–10 item checklist the brand reviewer can run on the draft: claim substantiation matches evidence, disclosures visible in first 3 seconds / first line of caption, code/link works, brand mention pronounced correctly, no prohibited competitor claims, captions match spoken dialogue, thumbnail-safe first frame.

6. **Flag assumptions and gaps.** Anything assumed (e.g., creator's audience overlap, platform choice, usage rights) that the brief owner should confirm before the brief is sent.

**Output requirements:**
- Creator-facing brief in markdown, formatted to paste into email, a Google Doc, or a creator-management platform
- Three hook options (labeled optional)
- UGC-prompt addendum block (if applicable)
- Approval checklist
- Assumptions & gaps
- Saved to `outputs/` if the user confirms

## Calibration Notes

- Over-scripting is the #1 cause of underperformance. If the brief tells the creator word-for-word what to say, the audience will feel the ad. Script must-includes, not the whole video.
- Disclosure compliance is non-negotiable. Default to disclosure at the start of the content and in the first line of the caption; do not hide it in bio or end-screen.
- Claim evidence > cleverness. If a creator must say "proven," "clinically tested," "#1," or a numeric claim, the brief must link the underlying evidence.
- Authenticity scores higher than production value at every budget tier. A real creator on an iPhone often outperforms a studio-lit AI UGC clip for the same spend.

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
