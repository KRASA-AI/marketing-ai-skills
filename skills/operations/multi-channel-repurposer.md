---
name: "Multi-Channel Content Repurposer"
category: operations
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~30 min/piece"
version: 2.0
last_eval_score: null
---

# ♻️ Multi-Channel Content Repurposer

## Purpose

Transform a single piece of long-form content into platform-optimized versions for multiple marketing channels — LinkedIn, Instagram, TikTok, email, Twitter/X, and newsletters — while maintaining consistent messaging and brand voice.

## When to Use

Use this skill after creating a blog post, case study, whitepaper, or any long-form content that should be distributed across multiple platforms. It saves the time of manually rewriting for each channel's format, tone, and audience expectations. Works especially well downstream of the Blog Post Outliner / AEO Content Optimizer once a long-form post is published — repurposing is the multiplier on time invested in the source.

## Required Input

Provide the following:

1. **Source content** — The original blog post, article, case study, or long-form piece (URL, file path, or pasted content)
2. **Target channels** — Which platforms to create versions for (default: LinkedIn, Instagram, Twitter/X, email newsletter, TikTok script)
3. **Priority message** — The single most important takeaway to preserve across all versions (the "if-they-only-read-one-sentence" line)
4. **Audience per channel** — Who you're reaching on each platform (often differs: LinkedIn = decision-makers, TikTok = end users, email = existing list)
5. **Platform-specific notes** — Hashtag preferences, CTA links, audience segments per channel, do-not-cross-post requirements
6. **Cadence and stagger plan** — Same-day burst vs. staggered (e.g., LinkedIn Mon, IG Wed, Twitter Thu, email Fri); platform-native vs. cross-pollination strategy
7. **AI-detection sensitivity** (optional) — If the source author publishes in their own name, flag this; the rewrite layer must protect distinctive voice signals

### Minimum Viable Input

If only fields 1, 2, and 3 are provided, the skill produces a `confidence: medium` repurpose pack with: same audience inferred for every channel and tagged `[ASSUMED — may need separate framings]`, default hashtag sets per platform pulled from `config.yml`, default same-day-burst cadence with a `[CONFIRM]` note that staggered usually outperforms, and an explicit gap list naming which inputs would lift confidence to `high` (typically: per-channel audience, CTA per channel, voice preamble file). The voice preamble loads from `config.yml` defaults; the user is told which voice attributes to confirm before publishing.

## Instructions

You are a skilled marketing professional's AI assistant specializing in content repurposing. Your job is to adapt one piece of content into multiple channel-specific formats without losing the core message — and without the "obviously-the-same-post-six-times" pattern that suppresses reach on every platform.

**Before you start:**
- Load `config.yml` from the repo root for company details, brand voice, and social handles
- Reference `knowledge-base/terminology/` for correct industry terms
- Use the company's communication tone from `config.yml` → `voice`
- Pull the AI prompt preamble from `outputs/voice/` if a Brand Voice Style Guide Generator output exists
- Pull persona context from `outputs/personas/` for any channel where the audience is named

**Process:**

1. **Extract the core narrative from the source content:**
   - Identify the primary thesis or takeaway (the priority message)
   - Pull out 3–5 supporting points or proof elements
   - Note any statistics, quotes, or hooks worth preserving — including verbatim numbers, named customer outcomes, and self-contained quotable sentences (15–25 words)
   - Identify the emotional angle (educational, inspirational, contrarian, empathy-first, proof-first)
   - Identify the source's distinctive voice signals (sentence-length pattern, signature phrases, structural quirks) — these must survive into all repurposes

2. **Map channel-by-channel framing.** Before writing, decide *what each channel does with the same idea*:
   - LinkedIn: peer-to-peer authority — usually narrows to one supporting point with a named outcome and a discussion-prompt CTA
   - Instagram: visual-first storytelling or carousel teaching — preserves emotional angle, breaks proof points across slides
   - Twitter/X thread: idea-per-tweet escalation — opens with the contrarian or counterintuitive frame, builds proof, ends with link
   - Email newsletter: trusted-context delivery — uses subscriber relationship as warm-up, can be longer and more personal
   - TikTok / Reels: hook-led problem-agitate-solve — one tight idea spoken aloud, on-screen text reinforces
   - Each channel gets a *different framing of the same priority message*, not a copy-paste

3. **Generate platform-specific versions:**

   **LinkedIn Post (1,200–1,500 characters)**
   - Hook in first line (pattern interrupt, named-outcome stat, or bold claim)
   - Professional but conversational tone — peer-to-peer, not vendor-to-prospect
   - 3–5 short paragraphs with white space
   - End with a discussion question or soft CTA
   - 3–5 relevant hashtags at the end (not in the body)
   - **Anti-cliche rule:** no "I'll never forget when…" openers, no "Here's what nobody tells you" framing, no leadership-aphorism endings

   **Instagram Caption (150–300 words)**
   - Attention-grabbing opening line (visible before the "...more" cut)
   - Storytelling or listicle format
   - Emoji use that matches brand voice (zero is fine; do not add for "warmth" if the voice guide bans them)
   - Strong CTA (save, share, comment, link in bio)
   - Hashtag strategy: 20–30 in a separate first comment, not in caption
   - **Format recommendation:** suggest static / carousel / Reel based on content type (educational → carousel; outcome story → Reel; quote card → static)

   **Twitter/X Thread (5–8 tweets)**
   - Hook tweet that stands alone and earns the click to expand
   - One idea per tweet, building on the previous
   - Final tweet with CTA and link
   - Retweet-worthy standalone insights in the middle (a 15–20-word self-contained line that survives screenshot)
   - **Engagement-bait guard:** no "follow for more," no "Bookmark this thread"

   **Email Newsletter Snippet (150–200 words)**
   - Subject line options (3 variations — different angles, not synonyms)
   - Preview text (35–50 chars, complements not duplicates the subject)
   - Brief context paragraph (assumes the reader knows you)
   - Key insight or value proposition
   - Single clear CTA button text
   - **Compliance note:** plain-text version generated; List-Unsubscribe-Post header expected per Gmail/Yahoo Feb 2024 bulk-sender rules

   **TikTok / Reels Script (30–60 seconds)**
   - Hook in first 3 seconds (visual + spoken)
   - Problem-agitate-solve structure
   - Conversational, spoken-word tone — read it aloud before submitting; if it doesn't sound like a person talking, rewrite
   - On-screen text callouts at 5–7 word density per beat
   - CTA at the end (verbal + on-screen)
   - **Format note:** specify whether the video is talking-head, b-roll, screen-record, or POV — affects production scope

4. **Voice consistency check.** After writing all five versions, run a paste-test: paste the LinkedIn post and the email snippet side-by-side. Do they sound like the same brand wrote both? If one reads "engineer-respectful, plainspoken" and the other reads "energetic, exclamation-mark-heavy," the voice has drifted. Either rewrite the off-voice version or note the discrepancy as a confidence flag.

5. **Distribution schedule recommendation.** Provide a stagger plan with optimal posting times per platform (per the `config.yml` audience timezone), and flag whether each piece should be cross-pollinated (LinkedIn → Twitter same week) or kept platform-exclusive (Reel content rarely repurposes back to static). Include a "do not post on the same day" guard for any two channels that share more than 30% audience overlap.

6. **AI-assist layer.** For each version, optionally provide a 1-line "amplification idea" — a short follow-up the team can post 3–5 days later if the original underperforms. Examples: "if LinkedIn post underperforms, repost as a carousel of the 4 supporting points"; "if email click-through < 2%, A/B the subject line option C against current subject."

**Output requirements:**
- All versions clearly labeled by platform with character/word counts noted per piece
- Hashtag sets included where applicable
- Visual direction or asset notes per platform
- Consistent core message across all versions, but distinct framing per channel
- Voice consistency check completed (paste-test result noted)
- Distribution schedule with named days/times per channel
- AI-assist amplification ideas
- Confidence tag (`high` / `medium` / `low`)
- Saved to `outputs/repurpose/[source-slug]/` if the user confirms

## Calibration Notes

- **Different framing, not different copy.** The single most common failure mode is the same hook reused across LinkedIn, Twitter, and Instagram. Every platform has different *why-people-stop-scrolling* triggers; the priority message stays, the framing changes. A repurpose pack where the hook is identical across three platforms is a copy-paste pack, not a repurpose pack — engagement collapses on at least two of the three.
- **The "spoken-word test" rule for video scripts.** If the TikTok / Reels script doesn't sound like a person talking when you read it aloud, it doesn't survive contact with the camera. Run the test before you ship.
- **Hashtag economy varies wildly by platform in 2026.** LinkedIn rewards 3–5 specific hashtags; Instagram still rewards 20–30 but in the first comment to keep captions clean; Twitter / X penalizes more than 1–2 (the algorithm down-weights "looks like a marketer wrote this"); TikTok rewards 3–5 highly specific hashtags and 1 trending one. Pull the per-platform recipe from `config.yml` rather than reinventing.
- **Email is not social.** Email assumes a relationship and can be longer, more personal, and less hooky. The "make it punchier" instinct that works on social often *reduces* email performance — readers signed up for the longer-form version.
- **AI-detection penalties are real on creator-led platforms.** Author-name LinkedIn / Twitter / TikTok content runs higher AI-detection scrutiny than brand-account content. Preserve the source's distinctive voice signals (sentence-length variation, signature phrases) — voice-flattening is the #1 AI-detection signal.
- **Cross-posting overlap rule.** Don't post to LinkedIn and Twitter / X on the same day if your audience overlap is above 30%. The same person seeing the same idea twice in 4 hours suppresses the second piece's reach. Stagger by 48–72 hours minimum.
- **Visual direction is part of the deliverable.** A repurpose without visual direction (photo type, graphic concept, video format) is half-finished. Specifying "static brand-template quote card with the 21-day stat" beats "make a graphic" every time.
- **Refresh cadence.** Re-run on evergreen source content every 60 days — platform-native formats shift quickly (Reel length norms, hashtag economy, LinkedIn algorithm preferences). A 6-month-old repurpose pack ships against last-quarter's algorithm.
- **Repurposing extends, doesn't replace, original creation.** A team that *only* repurposes hits a saturation curve at 90 days. Repurposing should multiply the reach of original work, not substitute for it.
- **Don't paraphrase customer language.** When the source uses a customer verbatim quote, that quote stays verbatim in every repurpose. Marketing-team paraphrase loses 40–60% of the quote's persuasive weight.

## Anti-Patterns

- **The copy-paste pack** — same hook, same priority message, same CTA across LinkedIn / Twitter / Instagram with only the character count clipped. Engagement collapses; algorithm flags as low-effort.
- **The shouted email** — exclamation marks, "🚨 BREAKING" prefix, urgency-only framing imported from social into email. Subscriber relationship erodes.
- **The voice flattener** — every version reads "energetic, exclamation-mark-heavy, emoji-frequent" regardless of source. Brand voice drift; AI-detection risk on creator-led accounts.
- **The hashtag spam** — Twitter / X version posted with 8 hashtags. Algorithm flags. Reach ~30–50% lower than 1-hashtag baseline.
- **The TikTok-doesn't-sound-spoken** — Reel script reads like a paragraph; can't be spoken in 45 seconds without sounding robotic. Either rewrite or cut.
- **The same-day burst** — LinkedIn + Twitter + Instagram all posted within 4 hours to overlapping audience. Second and third posts suppressed by algorithm.
- **The CTA mismatch** — LinkedIn CTA = "book a demo" but the source post is awareness-stage. CTA must match the audience's stage on each channel.
- **The TBD visual** — repurpose pack ships with copy only and "design TBD" everywhere. Designer reverse-engineers visuals from copy alone, output is generic. Visual direction is part of the deliverable.

## Integration Notes

- **Blog Post Outliner** — When the source is a blog post, the outline already names the quotable sentences and the FAQ block; both are direct inputs to the LinkedIn / Twitter / Instagram repurposes. Pull from the outline, not from the published post.
- **AEO Content Optimizer** — The AEO direct-answer block (40–60 words) is often the best LinkedIn opener and the best email body paragraph. Repurpose pulls these verbatim.
- **Brand Voice Style Guide Generator** — Voice preamble is the system prompt for any AI-assisted version; the banned-phrase list applies to every channel. Cite the voice guide version in the repurpose pack frontmatter.
- **Persona & ICP Builder** — Per-channel audience pulls from named persona files. Different channels often serve different personas (LinkedIn = economic buyer; TikTok = end user; email = existing customer base).
- **Customer Review & Insight Miner** — Verbatim customer quotes are the highest-conversion proof element across all channels; pull from the verbatim-quote bank rather than paraphrasing.
- **Synthetic Persona Simulator** — When a repurpose includes a high-stakes claim (proof point, named customer outcome), pre-test against the simulator persona before publishing.
- **Social Media Calendar** — The repurpose pack feeds directly into the calendar. Calendar handles the date-and-time placement; this skill handles the platform-specific authoring.
- **Campaign Performance Narrator** — Performance is reported per channel; this skill's distribution schedule defines the read window for each piece. Stagger plan and audience overlap notes flow into the post-campaign narrative.
- **Email Sequence Builder** — When the email snippet evolves into a multi-touch sequence, pass the snippet as touchpoint 1 and let Email Sequence Builder author the follow-ups.
- **Multi-Channel Content Repurposer ↔ Ad Copy Variations** — When a high-performing organic post becomes paid creative, Ad Copy Variations is the downstream skill. Pass the top-performing organic version as the "existing high-performing copy" input.

## Example Output

### Input Recap

- **Source:** Blog post — "Ops Cycle Time: The 3-Week Leading Revenue Indicator Most RevOps Teams Miss" (1,950 words, published Aug 4, 2026)
- **Channels:** LinkedIn, Twitter/X, Instagram, email newsletter, TikTok / Reel
- **Priority message:** Ops cycle time leads revenue plan attainment by 3 weeks — measure it before your CRO does
- **Audience per channel:**
  - LinkedIn: Persona Priya (Head of RevOps, Series B+)
  - Twitter / X: RevOps Co-op community + engineering managers
  - Instagram: Threadline brand-affinity audience (existing customers + warm prospects)
  - Email: Newsletter subscribers (mixed RevOps + GTM ops)
  - TikTok / Reel: Tech-curious early-career RevOps (top-of-funnel awareness)
- **CTA per channel:** LinkedIn → demo book; Twitter → blog read; Instagram → save / share; email → demo book; TikTok → "follow for the next one in the series"
- **Cadence:** Stagger Mon (LinkedIn) → Wed (Twitter thread) → Thu (email) → Fri (Instagram) → following Tue (TikTok / Reel)
- **Voice preamble:** `outputs/voice/threadline-voice-preamble-v2.0.md`
- **Confidence:** `high`

---

### Core Narrative Extract

- **Priority message:** Ops cycle time leads revenue plan attainment by ~3 weeks (B2B SaaS, 100–500 FTE)
- **Supporting points:** (1) Threadline 2026 benchmark, n=47 cohort; (2) ScaleHQ cut 31% in 90 days; (3) measurable without a CDP; (4) most teams measure the wrong thing (sales cycle length, not ops cycle time)
- **Verbatim claim (do not paraphrase):** "Ops cycle time leads revenue plan attainment by 3 weeks in B2B SaaS at 100–500 FTE."
- **Emotional angle:** Proof-first, contrarian, calm-authority

---

### LinkedIn Post (1,418 chars)

> Most RevOps teams measure the wrong cycle time.
>
> Sales cycle length is the lagging indicator. Ops cycle time — the median time a deal sits in any stage without an action — is the leading one.
>
> Threadline ran the math across a 47-customer cohort in FY26. The result: ops cycle time leads revenue plan attainment by 3 weeks.
>
> When ops cycle time worsened by 1 day in March, revenue plan attainment dropped 4–6% in April.
>
> ScaleHQ saw it first. They cut ops cycle time 31% in 90 days. Two consecutive quarters of revenue plan attainment followed — including the part that didn't work in month 2 (we share that in the case study).
>
> If your CRO is asking about the forecast at the next QBR, this is the metric they're going to surface — even if they don't know to call it by name.
>
> The audit takes 30 minutes. Worth doing before the question gets asked.
>
> #RevOps #SaaS #SalesOps #CycleTime #B2B

**CTA:** "30-minute audit — link in comments." (Soft.)
**Visual direction:** Threadline brand-template chart — ops cycle time vs. revenue plan attainment, 21-day offset annotated.
**Confidence flag:** `high` (named persona, named outcome, proof source cited)

---

### Twitter / X Thread (7 tweets)

**1/** Most RevOps teams measure the wrong cycle time.

Sales cycle length is the lagging indicator.
Ops cycle time is the leading one — and it leads revenue plan attainment by 3 weeks.

Receipts ↓

**2/** "Ops cycle time" = the median time a deal sits in any stage without an action.

Not how long the deal takes. How long the *handoff* takes between tools, teams, or stages.

It's the seam. Most stacks have a broken one.

**3/** Threadline ran the math across 47 customers in FY26.

When ops cycle time worsened by 1 day in March → revenue plan attainment dropped 4–6% in April.

The lead time was 21 days. Consistent across the cohort.

**4/** ScaleHQ saw it first.

Cut ops cycle time 31% in 90 days.

Hit revenue plan attainment in Q2 and Q3.

(They missed once in month 2. We share that part too — failure data is the most useful kind.)

**5/** Healthy ranges by stage:
• Series A: 2–4 days
• Series B: 3–7 days
• Series C+: 5–12 days

Above the range = silent forecast risk.

**6/** You don't need a CDP to measure it.

Native Salesforce reports + 1 spreadsheet column = enough.

The full method (no vendor required) is in the post.

**7/** If your CRO is going to surface this metric at the next QBR, find the number first.

Full breakdown: [blog link]

#RevOps

**Visual direction:** Tweet 1 attached to a chart card; tweet 4 attached to the ScaleHQ outcome card.
**Confidence flag:** `high`

---

### Instagram Caption (224 words)

**Hook:** Your CRO is about to ask about a metric you might not be tracking.

(Visible before the "...more" cut.)

**Body:**
Sales cycle length is the lagging indicator. Most RevOps teams measure that one.

Ops cycle time — the median time a deal sits in any stage without an action — is the leading indicator. When ops cycle time worsens by 1 day, revenue plan attainment drops 4–6% in the following month.

The lead time is about 3 weeks.

We ran the math across a 47-customer cohort in FY26. ScaleHQ proved it first — cut their ops cycle time 31% in 90 days, hit revenue plan attainment in Q2 and Q3 (and missed once in month 2 — failure data is the most useful kind).

Healthy ranges:
• Series A: 2–4 days
• Series B: 3–7 days
• Series C+: 5–12 days

You don't need a CDP to measure it. Native Salesforce reports + 1 spreadsheet column gets you the number.

Save this for the next QBR.

**CTA:** Save & share with your RevOps lead.

**Format recommendation:** Carousel (5 slides — hook / definition / Threadline benchmark / ScaleHQ outcome / healthy ranges).

**Hashtags (in first comment):** #RevOps #SalesOps #B2BSaaS #PipelineVelocity #SalesEnablement #GoToMarket #SaaSGrowth #RevenueOperations #BusinessOperations #DataDrivenSales #SalesProcess #CRMOptimization #SalesAnalytics #Forecasting #SaaSMetrics #StartupOps #SeriesB #SeriesC #Threadline #LeadingIndicator

**Confidence flag:** `high`

---

### Email Newsletter Snippet (188 words)

**Subject line options (3 angles):**
1. The metric your CRO is about to ask about (proof-first)
2. Sales cycle length is the wrong number (contrarian)
3. 3 weeks of warning before the forecast slips (urgency-restrained)

**Preview text:** Ops cycle time leads revenue plan attainment by 21 days.

**Body:**
You measure sales cycle length. Your CRO measures revenue plan attainment. The number that connects them — ops cycle time — usually doesn't get measured at all.

It's the median time a deal sits in any stage without an action. The seam between tools, the handoff between teams, the moment when nothing's wrong yet but the forecast is already changing.

Threadline ran the math across a 47-customer cohort. When ops cycle time worsened by 1 day, revenue plan attainment dropped 4–6% in the next 30 days. The lead time is consistently about 3 weeks.

ScaleHQ proved it first. They cut theirs 31% in 90 days — and we share the part where it didn't work.

The audit takes 30 minutes. Worth doing before the question gets asked.

**CTA button text:** Run the 30-minute audit

**Compliance:** plain-text version generated; List-Unsubscribe-Post header attached.
**Confidence flag:** `high`

---

### TikTok / Reel Script (47 seconds)

**Format:** talking-head + b-roll cuts to a Salesforce screen-record (mid-roll)

**Hook (0:00–0:03):** "Your CRO is about to ask about a metric you might not be tracking."
*(On-screen text: "Most RevOps teams miss this.")*

**Problem (0:03–0:12):** "Most RevOps teams measure sales cycle length. That's the lagging indicator. The leading one is called ops cycle time."
*(B-roll: a calendar showing the 21-day offset.)*

**Agitate (0:12–0:25):** "When ops cycle time worsens by one day, revenue plan attainment drops 4 to 6 percent in the next month. We ran the math across 47 customers — the lead time is three weeks. Consistent."
*(Screen-record: Salesforce report, ops cycle time annotation.)*

**Solve (0:25–0:40):** "You don't need a CDP. Native Salesforce reports plus one spreadsheet column will get you the number. Healthy range for Series B: three to seven days. Above seven, your forecast is at risk and you don't know it yet."

**CTA (0:40–0:47):** "We're doing a series on the 5 RevOps metrics that actually predict revenue. Follow for the next one — measuring without a CDP."
*(On-screen text: "Follow for part 2.")*

**Spoken-word test:** read aloud — sounds conversational, no marketing-jargon stumbling.
**Confidence flag:** `high`

---

### Voice Consistency Check

Pasted LinkedIn + email + TikTok side-by-side:
- Sentence-length variation: similar across all three (mix of 5-word + 12-word + 22-word lines — Threadline signature)
- Banned phrases: none present (no leverage, no synergy, no revolutionize)
- Voice attributes (plainspoken / specific / engineer-respectful): present in all five
- Anti-cliche guard: no "I'll never forget," no "Here's what nobody tells you," no leadership-aphorism endings
- **Result:** voice consistent across all five repurposes. ✓

---

### Distribution Schedule

| Channel | Day | Time (US-PT) | Notes |
|---------|-----|---------------|-------|
| LinkedIn | Mon Aug 4 | 8:00 AM | Algorithm prefers Tue–Thu but launch-day priority overrides |
| Twitter / X | Wed Aug 6 | 9:30 AM | 48-hr stagger from LinkedIn (audience overlap ~22%, under 30% threshold) |
| Email newsletter | Thu Aug 7 | 7:00 AM | Send to full list; 10% holdout for incrementality |
| Instagram | Fri Aug 8 | 11:00 AM | Carousel format; visual asset finalized Wed |
| TikTok / Reel | Tue Aug 12 | 6:00 PM | 4-day rest before second video drops in series |

---

### AI-Assist Amplification Ideas

- **LinkedIn underperforms (< 1.2% engagement):** Repost as a 5-slide carousel of the supporting points + ScaleHQ outcome on Day 7
- **Email click-through < 2%:** A/B subject line option C against current send on the newsletter resend (Day 5)
- **Twitter thread under 50 retweets:** Quote-tweet thread with the standalone proof-tweet (#3) as a fresh top-of-thread on Day 4
- **Instagram carousel < 5% save rate:** Re-cut as a 30-second Reel on Day 10 using the same script
- **TikTok < 8K views:** Iterate the hook line ("Your CRO is about to ask…") and re-shoot — voice over the same b-roll

---

### Confidence

`high` — all six required inputs present, persona named per channel, voice preamble applied, voice consistency check passed, stagger plan respects 30% audience-overlap rule.

---

### Refresh Date

- Re-run repurpose if blog post hits a major update (60-day review)
- Refresh per-platform format recipes against the next platform algorithm shift (typically Q3 + Q1 each year)
- Re-validate voice preamble at the next Brand Voice Style Guide Generator refresh
