---
name: "Social Media Calendar"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~30 min/week"
version: 3.0
last_eval_score: null
---

# 📅 Social Media Calendar

## Purpose

Plan a full week (or month) of social media posts with platform-specific copy, hashtags, visual direction, optimal posting times, and a measurement frame — organized by content pillars to maintain a balanced, strategic content mix that compounds organic reach without burning out the team or drifting off brand voice.

## When to Use

Use this skill for weekly or monthly social media content planning. Ideal when you need to maintain consistent posting cadence, plan around campaigns or events, batch-create content for scheduling tools (Buffer, Hootsuite, Later, Sprout Social, Loomly, Metricool), or onboard a new social media manager. Also useful when audit findings show inconsistent voice, pillar-mix imbalance, or seasonal-cadence misalignment.

Do not use for paid social ad copy — use **Ad Copy Variations** for that. Do not use for individual long-form blog repurposing — use **Multi-Channel Content Repurposer** for that. Do not use for creator/influencer activation — use **Creator & Influencer Brief Builder** for that.

## Required Input

Provide the following:

1. **Planning period** — One week or one month? (default: 1 week)
2. **Active platforms** — Which platforms to plan for? (e.g., Instagram, LinkedIn, Facebook, Twitter/X, TikTok, Threads, YouTube Shorts)
3. **Posting frequency** — How many posts per platform per week? (default: 3–5 per platform; LinkedIn 3–5, Instagram 4–7, Twitter/X 7–14, TikTok 5–10, Facebook 3–5)
4. **Content pillars** — 3–5 recurring themes (e.g., educational tips, behind-the-scenes, client results, promotions, industry news). If none provided, the skill will suggest them.
5. **Upcoming events or promotions** — Any campaigns, holidays, launches, timely hooks, or industry events to incorporate
6. **Audience context** — Who you're trying to reach, what they care about, where they currently scroll. Reference an existing persona from `outputs/personas/` if available.
7. **Brand assets available** (optional) — Photo library, brand templates, team bios, client testimonials, video b-roll, etc.
8. **Voice constraints** — Pull from `outputs/voice/` if available; otherwise from `config.yml` → `voice`. Includes anti-examples / banned phrases / tone descriptors.

### Minimum Viable Input

If only fields 1, 2, and 6 are provided, the skill produces a `confidence: medium` calendar with: pillar mix inferred from the platform set and audience context (tagged `[ASSUMED]`); 3–5 posts per platform at the default cadence; default voice pulled from `config.yml` (tagged `[CONFIRM]` for tone descriptors and banned phrases); and a `[CONFIRM]` block for the calendar owner to validate before scheduling (typically: posting frequency targets, named upcoming events, brand asset inventory, holdout-vs-control measurement plan). The hashtag pack is generated against the platform's 2026 hashtag economy defaults; the calendar owner is told which hashtag bands need to be confirmed against the brand's preferred-hashtag list. Confidence drops to `low` if the audience context (Field 6) is missing — the skill will produce a calendar with a generic-audience flag but every post will be marked unverified.

## Instructions

You are a skilled social media strategist's AI assistant. Your job is to create a comprehensive, ready-to-execute social media calendar that balances engagement, brand building, and lead generation — with platform-native framing, a measurement frame, and a refresh cadence.

**Before you start:**
- Load `config.yml` from the repo root for company details, services, brand voice, and social handles
- Load any existing persona files from `outputs/personas/` and reference the target persona by name
- Reference `knowledge-base/terminology/` for correct industry terms
- Pull voice constraints (banned phrases, anti-examples, tone descriptors) from `outputs/voice/` or `config.yml` → `voice`
- Note seasonal patterns from `config.yml` → `services.seasonal_patterns`
- Pull recent campaign performance from `outputs/campaign-narratives/` if available, to inform pillar mix tilt

**Process:**

1. **Establish the content strategy framework.**
   - Define or validate 4–6 content pillars with percentage mix:
     - Educational / how-to (30%) — Position as expert
     - Social proof / customer results (20%) — Build trust
     - Behind-the-scenes / culture (15%) — Build connection
     - Promotional / CTA (15%) — Drive action
     - Engagement / community (10%) — Encourage interaction
     - Trending / timely (10%) — Stay relevant
   - Map each pillar to the best-performing format per platform (e.g., educational on LinkedIn = carousel + 1,400-char text; educational on TikTok = 30-sec talking-head with text overlay; educational on Twitter/X = 7-tweet thread)
   - Tilt the pillar mix when recent campaign performance warrants (e.g., if the brand just shipped a flagship case study, tilt social-proof pillar +5% for 30 days)

2. **Apply the platform-native framing rule before writing.** Different framing, not different copy. The same idea is reframed for each platform's economy: LinkedIn rewards opinion + named context + signal-of-credibility; Instagram rewards visual narrative + scannable structure; TikTok rewards spoken-word cadence + immediate hook (first 3 seconds) + native trend sound; Twitter/X rewards punch + reply-magnet + thread-threadability; Facebook rewards conversation prompt + low-friction format; Threads rewards intimate + opinion-led + reply-driven. Note the framing per platform in the calendar before drafting copy.

3. **For each post in the calendar, provide:**

   **Post Details:**
   - Date and recommended posting time (with timezone)
   - Platform(s) — one row per platform if cross-posting with adaptation
   - Content pillar label
   - Post copy (platform-formatted — see specs below; written in full, not summarized)
   - Hashtag set (per the 2026 hashtag economy by platform — see Calibration Notes)
   - Visual direction (photo type, graphic concept, video framing — *not* the asset itself)
   - CTA or engagement prompt
   - Voice consistency check (does this post pass the brand's voice anti-example list?)

   **Platform-Specific Formatting (2026 specs):**

   *Instagram:*
   - Caption: 150–300 words; storytelling, listicle, or carousel-companion format
   - First line is the hook (shows before "...more")
   - Hashtags: 20–30 in first comment (NOT in caption — Instagram 2026 still rewards first-comment placement for reach without diluting caption signal)
   - Format recommendation: Reel vs. carousel vs. static image vs. story
   - For Reels: name the trending audio if applicable

   *LinkedIn:*
   - Post: 1,200–1,500 characters (sweet spot for the algorithm in 2026)
   - Hook in first line visible before "see more"
   - Professional tone with personal angle
   - Hashtags: 3–5 at the end (LinkedIn 2026 deprioritizes >5 hashtags)
   - Carousel doc: 6–10 slides; first slide is the hook, last slide is the CTA
   - Tag named individuals only with relevance (no spray-tagging — LinkedIn 2026 algorithm penalizes)

   *Facebook:*
   - Post: 40–80 words for best engagement (text-only); 100–150 words if accompanying a link
   - Question or conversation-starter format outperforms declarative
   - Link posts vs. native content recommendation: native video > native image > link with custom thumbnail > pure link
   - Hashtags: 1–2 only (Facebook 2026 doesn't reward hashtag stacking)

   *Twitter/X:*
   - Tweet: under 280 characters (Premium accounts can write longer but algorithm rewards <280)
   - Thread option for educational content (5–9 tweets — 2026 sweet spot; longer threads suffer from drop-off)
   - 1–2 hashtags max (Twitter/X 2026 deprioritizes hashtag-heavy posts)
   - Reply-magnet pattern: end the thread with a question

   *TikTok:*
   - Caption: under 150 characters; a hook line + a curiosity gap
   - Hook concept for first 3 seconds (named visual + named tension or claim)
   - Trending sound recommendation if applicable (note: trending sounds expire in 7–14 days; flag refresh need)
   - Hashtags: 3–5 with one trending hashtag (TikTok 2026: niche hashtags + one trend tag outperform pure broad-trend tagging)
   - Spoken-word test: write the script as it will be spoken; if it doesn't sound like a human talking, rewrite

   *Threads:*
   - Post: 280–500 characters (Threads 2026 sweet spot)
   - Opinion-led; reply-driven
   - Hashtags: 1 tag is enough; Threads 2026 algorithm doesn't reward stacking
   - Pair text with image only if the image adds context

   *YouTube Shorts:*
   - Caption: under 100 characters
   - Hook in first 2 seconds (visual + voice-over claim)
   - Vertical 9:16; 15–60 seconds; named hook + named payoff + retention bait at 50% mark
   - End frame: subscribe-to-channel CTA over the last 1.5 seconds

4. **Create the calendar layout.**
   - Table format: Date | Day | Platform | Time | Pillar | Hook (first 8 words) | Post Copy | Visual Direction | Hashtags | CTA | Voice-Check ✓
   - Include a "weekly theme" or narrative thread that ties posts together (the persona's job-to-be-done that week)
   - Flag any posts that should be boosted or promoted with paid spend
   - Note which posts can be cross-posted with minor adaptation (different framing, not different copy) vs. platform-exclusive
   - Stagger cross-posts by ≥48 hours to avoid same-audience over-exposure (the cross-posting overlap rule)

5. **Build a voice consistency check.** Run the voice-anti-example list against every post. Each post passes/fails against:
   - No banned phrases ("leverage / synergy / unlock / best-in-class / revolutionize / etc." or whatever the voice guide bans)
   - Voice tone descriptors honored (e.g., "plainspoken, specific over clever")
   - Forbidden cliches absent (per voice guide — typically "game-changer," "unlock potential," "in today's fast-paced world")
   - Any AI-disclosure requirement met if the content was AI-assisted

6. **Add strategic notes.**
   - Best posting times per platform for the user's industry and audience (with named source: Sprout Social 2026 industry benchmarks, Hootsuite Best Times to Post 2026, or first-party data if available)
   - Content recycling suggestions (evergreen posts to reshare quarterly with refreshed framing)
   - Engagement playbook: how to respond to comments within the first hour (the "first-hour engagement window" rule — 70%+ of organic reach happens in first 60 minutes per Sprout Social 2026)
   - Metric targets per platform (reach, engagement rate, link clicks, follower growth) with named source dashboard
   - AI-detection sensitivity flag: which platforms penalize AI-generated content (TikTok creator accounts and Instagram creator accounts both apply soft suppression to high-AI-signal content in 2026)

7. **Build the measurement frame.**
   - Primary KPI per platform with a baseline and a target (e.g., LinkedIn engagement rate: 3.2% baseline → 4.0% target; named source: LinkedIn Page Analytics)
   - Secondary KPIs (reach, follower growth, link clicks, saves)
   - Anti-vanity guard (which metrics are inflated and should not anchor decisions — e.g., impressions in 2026 are MPP-inflated on Twitter/X; use authenticated reach instead)
   - Holdout / read-window: a single named "off" week (or the prior trailing 4-week median) as the comparison baseline
   - Weekly review cadence: Monday review of prior week's posts; calendar revision Thursday; new week ships Sunday night

8. **Flag assumptions and gaps.** Anything assumed (audience tone, persona match, posting time defaults, brand asset availability) that the calendar owner should confirm before scheduling. Use confidence tags on the calendar itself: `confidence: high` if all eight required inputs are present and the persona is named; `confidence: medium` if MVI mode applied; `confidence: low` if more than one of {audience, voice, brand assets} is `[ASSUMED]`.

**Output requirements:**
- Complete calendar in table format, ready to import to scheduling tools (Buffer, Hootsuite, Later, Sprout Social, Loomly, Metricool)
- All posts written in full (not just topics or ideas)
- Platform-specific formatting and character counts verified
- Hashtag sets included for each post (sized per platform)
- Visual direction notes for each post
- Voice consistency check ✓ per post
- Content pillar distribution balanced across the week (within 5 percentage points of target mix)
- Uses company name, services, seasonal context, and voice from config
- Measurement frame with named baselines, targets, and anti-vanity guards
- Refresh cadence note
- Saved to `outputs/social-calendars/` if the user confirms

## Calibration Notes

- **The hashtag economy varies wildly per platform in 2026.** LinkedIn 3–5; Instagram 20–30 in first comment; Twitter/X 1–2; TikTok 3–5 with one trending tag; Facebook 1–2; Threads 1; YouTube Shorts 3–5. Hashtag spam on a platform that doesn't reward it (Twitter/X, Facebook, Threads, LinkedIn at >5) actively suppresses reach. Pull the hashtag count from the platform's current ranking economy, not from a 2022 best-practices doc.
- **Different framing, not different copy.** A blog repurposed across LinkedIn / Twitter / Instagram / TikTok / Threads needs the same idea reframed for each platform's native economy — not the same paragraph copy-pasted with different hashtags. The "copy-paste pack" is the #1 social calendar failure pattern: every platform sees a flattened version that performs at a fraction of native potential. (See Multi-Channel Content Repurposer for the channel-by-channel framing system.)
- **The first-hour engagement window dominates organic reach.** Sprout Social 2026 data shows 70%+ of organic reach happens in the first 60 minutes after publication. Posts published into engagement-dead time (e.g., 2am local time) are structurally limited regardless of quality. Schedule against the platform's audience-active window for the brand's industry.
- **AI-detection penalties are real on creator-led platforms in 2026.** TikTok and Instagram apply soft suppression to high-AI-signal content (uniform sentence rhythm, repeated transition phrases, generic visual cliches) on creator accounts. Brand accounts get less suppression but still benefit from human-edit of AI-drafted captions. Spoken-word test for video scripts: read the caption out loud — if it sounds like a human talking, it passes; if it sounds like AI prose, rewrite.
- **The cross-posting overlap rule (30% threshold).** When the same audience overlaps >30% across two platforms (typical for the same brand's LinkedIn and Twitter/X B2B audience, or Instagram and Threads consumer audience), stagger cross-posts by ≥48 hours. Same-day cross-posts to overlapping audiences burn engagement on the second post and can trigger over-exposure feedback signals.
- **Posting cadence matters more than posting volume.** A consistent 3 posts per week beats a sporadic 7 posts per week — the platform algorithms reward predictable cadence as a signal of account health. Establish a sustainable cadence and hold it for ≥90 days before re-evaluating.
- **Engagement-bait gets penalized.** Twitter/X 2026 algorithm explicitly demotes "Reply YES if..." / "Like if you agree" / "Tag someone who..." posts. LinkedIn 2026 demotes the same plus "Read this for the answer" / "Comment 'TEMPLATE' for the link." Use authentic question prompts; avoid synthetic engagement triggers.
- **Trending sounds expire fast on TikTok.** Trending audio has a 7–14 day window in 2026 before it stops giving algorithmic lift and starts feeling stale. Calendar entries with named trending sounds need a refresh check 7 days out; default to original audio for evergreen content.
- **Carousel posts outperform single-image posts on LinkedIn and Instagram in 2026.** LinkedIn carousels (PDF doc format, 6–10 slides) earn 2.4× the engagement of single-image posts. Instagram carousels (3–7 slides) earn 1.8× the engagement of single-image posts. Default to carousel for educational pillar.
- **Pillar drift is the silent killer of brand voice.** Calendars that are heavy on promotional pillar (>20% of posts) and light on educational/social-proof (<35% combined) train the audience to scroll past. Audit pillar mix monthly; rebalance when any pillar drifts ±5% from target.
- **The post-without-an-asset is a red flag.** "Visual: TBD" in the calendar is the #1 cause of slipped publication and content-team-blocked-by-design. Every calendar entry must have a named visual direction (concept, format, asset source) at calendar lock time, not "asset team to create."
- **Authenticated reach > impressions.** In 2026, impressions on Twitter/X include bot views and MPP-inflated counts. Use authenticated reach (Twitter/X Premium analytics) or follower-only impression counts where available. Engagement rate against authenticated reach is the defensible metric.
- **Account-health signals matter more than per-post optimization.** Algorithms reward accounts that show consistent voice, on-pillar content, and 1-hour-window engagement-response from the brand. A perfectly optimized post on an inconsistently-managed account underperforms an average post on a well-tended account.
- **AI-assist disclosure is platform-specific in 2026.** TikTok requires a "AI-generated content" label on synthetic media (rolled out Q1 2026). Instagram applies the same to AI-generated images on creator accounts. LinkedIn does not yet require disclosure but the FTC AI-disclosure rule applies to brand promotional content. Bake the disclosure check into the voice consistency step.
- **Refresh cadence:** Calendar refreshes weekly (Monday review → Thursday revision → Sunday-night ship). Pillar mix audit monthly. Voice anti-example list re-validated quarterly when the Brand Voice Style Guide Generator refreshes. Trending-sound recommendations re-checked 7 days before publication. Annual full-strategy refresh aligned to the brand's marketing planning calendar.

## Anti-Patterns

- **The copy-paste pack** — Same paragraph copy-pasted across LinkedIn / Twitter / Instagram / TikTok / Threads with different hashtags. Each platform sees a flattened version that performs at a fraction of native potential. Fix: write platform-native framings before drafting copy (Process Step 2).
- **The pillar-drift calendar** — Promotional pillar quietly grows from 15% to 35% over a month because a campaign launched. Audience trains itself to scroll past. Fix: monthly pillar audit; rebalance when any pillar drifts ±5% from target.
- **The hashtag-heavy LinkedIn post** — 12 hashtags at the end of a LinkedIn post in 2026. The algorithm demotes >5 hashtags on LinkedIn. Fix: 3–5 max on LinkedIn; the platform's algorithm has changed since the 2022 best-practices doc the team is still using.
- **The TikTok-doesn't-sound-spoken script** — Script reads like written prose. It dies in the first 3 seconds because the cadence is wrong. Fix: spoken-word test — read it out loud; if it doesn't sound like a human talking, rewrite.
- **The same-day cross-post burst** — Same content shipped to LinkedIn + Twitter/X + Instagram in the same hour to a 50% overlapping audience. The second and third platforms underperform. Fix: stagger by ≥48 hours when audience overlap >30%.
- **The engagement-bait reply-magnet** — "Like if you agree!" or "Tag someone who needs this" — actively penalized by Twitter/X and LinkedIn 2026 algorithms. Fix: authentic question prompts only; the question must be one the brand actually wants the answer to.
- **The TBD visual** — Calendar entry says "Visual: TBD" or "Asset team to create." Cause of every slipped publication. Fix: named visual direction (concept + format + asset source) at calendar lock time.
- **The brand-voice flattener** — Every post sounds the same because the AI-drafted copy was shipped without human voice-edit. Audience tunes out. Fix: voice consistency check ✓ per post; banned-phrase list run; spoken-word test on video scripts.
- **The shouted promo** — Every other post is a discount or "limited time offer" with the same urgency framing. Audience trains itself to ignore. Fix: ≤15% promotional pillar; rotate between offer types and avoid repeating the same urgency hook within 14 days.
- **The vanity-metric anchor** — Calendar success measured on impressions or follower count growth. Inflated by MPP, bots, and paid-boost spillover. Fix: authenticated reach + engagement rate against authenticated reach + measurable conversion (link clicks, demo bookings, saves).
- **The trending-sound timewarp** — TikTok script written 4 weeks ago names a trending sound that's now stale. Post lands flat. Fix: trending-sound check 7 days before publication; default to original audio for evergreen content.
- **The 1-week calendar with no measurement frame** — Calendar ships with no baseline, no target, no holdout. Post-week review devolves into "felt like a good week" anecdote. Fix: name the primary KPI, the baseline, the target, and the comparison window before scheduling.

## Integration Notes

- **Pair with Persona & ICP Builder** — Audience context (Required Input #6) and the "weekly theme" tying posts together pull from the persona's tension, job-to-be-done, and where-they-scroll sections. Reference the persona by file name in the calendar header.
- **Pair with Brand Voice Style Guide Generator** — Voice constraints (Required Input #8), banned-phrase list, and tone descriptors flow from the voice guide. Run the voice consistency check against the voice guide's anti-example list, not against ad-hoc rules.
- **Pair with Multi-Channel Content Repurposer** — When a long-form blog or video gets repurposed across platforms, the Repurposer produces the per-platform framings; this calendar slots them into the publishing schedule. The calendar should reflect the Repurposer's stagger plan (≥48-hour cross-platform spacing) verbatim.
- **Pair with Creative Brief Generator** — When a campaign's calendar week is anchored to a creative brief, the calendar's "weekly theme" should be the brief's single-minded proposition; the pillar mix should be tilted toward the brief's primary message angle.
- **Pair with Customer Review & Insight Miner (VoC)** — Buyer-language verbatims surface the actual phrases the audience uses about the brand. Use VoC verbatims as hook openers for educational and social-proof pillar posts.
- **Pair with Campaign Performance Narrator** — Calendar performance feeds into the campaign narrative. Pre-define the comparison baseline and primary KPI in the calendar's measurement frame so the post-week narrative is measurable, not anecdotal.
- **Pair with Creator & Influencer Brief Builder** — When a creator-led post is on the calendar, the Creator Brief is the upstream document; the calendar slot reflects the agreed-on go-live date and platform.
- **Pair with Ad Copy Variations** — When organic posts are designated for paid boosting (flagged in the calendar), the boost copy should pass through Ad Copy Variations for compliance check and platform-policy review (FTC AI-disclosure, Meta personal-attribute, LinkedIn verified-page) before the boost spend.
- **Pair with AEO Content Optimizer** — When a post links to a blog or landing page, that destination page should have been run through AEO Optimizer recently so the AI-engine traffic from social-amplification clicks lands on a page that wins the AI citation. Coordination prevents wasted social spend driving traffic to AI-invisible pages.
- **Pair with Brand Safety & Crisis Response Planner** — Calendar entries on trending or culturally-sensitive moments (around named events, holidays, or news cycles) should pass through the brand safety brief's approval gate before scheduling. Hot-take posts off-brand are the #1 cause of social PR incidents.
- **Pair with Topic Cluster Planner** — Educational pillar posts that snippet from cluster pillar pages get internal-link consistency from Topic Cluster Planner. The cluster's pillar-page-as-anchor is also the most-shareable destination for educational pillar.

## Example Output

### Input Recap

- **Planning period:** 1 week (Aug 4–10, 2026)
- **Active platforms:** LinkedIn, Instagram, Twitter/X, TikTok
- **Posting frequency:** LinkedIn 4/week, Instagram 5/week, Twitter/X 10/week, TikTok 5/week (24 posts total)
- **Content pillars:** Educational (30%), Social proof (20%), Behind-the-scenes (15%), Promotional (15%), Engagement (10%), Trending (10%)
- **Upcoming events:** Q3 RevOps Diagnostic launch (Aug 4); RevOps Co-op community AMA (Aug 7); SaaStr Annual prep
- **Audience:** Persona "Priya, the Pragmatic Head of RevOps" (`outputs/personas/priya-revops.md`)
- **Brand assets:** Demo screenshots, ScaleHQ case study quotes (4), ops cycle time benchmark chart, founder-on-camera Reels stock (12 clips), Threadline office lifestyle photography
- **Voice:** Plainspoken, specific over clever, engineer-respectful (Threadline voice guide v2.0); banned phrases include "leverage / synergy / unlock / revolutionize / best-in-class / AI-powered (when not literal)"
- **Confidence:** `high`

---

### Weekly Theme

**"The 3-Week Leading Indicator"** — anchored to the Q3 RevOps Diagnostic launch (Aug 4). Each post serves the proposition that ops cycle time is the leading indicator a CRO will quote at the next QBR. Pillar tilt: educational +5% (campaign launch week); promotional -5% (avoid launch overload).

---

### Calendar (24 posts, Aug 4–10, 2026)

| # | Date | Day | Platform | Time (PT) | Pillar | Hook (first 8 words) | Visual | Hashtags | CTA | Voice ✓ |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Aug 4 | Mon | LinkedIn | 7:30 AM | Educational | Ops cycle time leads revenue plan attainment | Carousel doc, 8 slides, ops cycle time chart | #revops #b2bsaas #revenueoperations | Read the benchmark report (link in comments) | ✓ |
| 2 | Aug 4 | Mon | Twitter/X | 8:00 AM | Educational | The metric that beat the forecast | Single-image: ops cycle time chart with n=47 footnote | #RevOps #B2BSaaS | None (declarative) | ✓ |
| 3 | Aug 4 | Mon | Instagram | 9:00 AM | Promotional | Free 30-min RevOps audit launches today | Reel, 22 sec, founder on camera + screen recording of diagnostic | (20 in first comment) | Link in bio for free audit | ✓ |
| 4 | Aug 4 | Mon | TikTok | 11:00 AM | Educational | Your CRO will ask this in 14 days | 47-sec talking-head, founder + on-screen text | #RevOps #SaaSTok #FoundersOfTikTok | "Save this for the QBR" | ✓ |
| 5 | Aug 4 | Mon | Twitter/X | 1:00 PM | Engagement | Quick poll for RevOps leaders... | None (text + 4-option poll) | #RevOps | Reply with your % | ✓ |
| 6 | Aug 5 | Tue | LinkedIn | 8:00 AM | Social proof | ScaleHQ cut ops cycle time 31% in 90 days | Carousel doc, 6 slides, ScaleHQ case study quotes | #revops #b2bsaas #casestudies | Read the case study (link in comments) | ✓ |
| 7 | Aug 5 | Tue | Twitter/X | 9:30 AM | Educational | 7-tweet thread: how to measure ops cycle time | None (text thread) | #RevOps | Reply with your team's number | ✓ |
| 8 | Aug 5 | Tue | Instagram | 11:00 AM | Behind-the-scenes | How we built the Threadline 2026 benchmark | Reel, 45 sec, screen recording + founder voiceover | (20 in first comment) | None (story-led) | ✓ |
| 9 | Aug 5 | Tue | TikTok | 2:00 PM | Trending | Stitch with @SaaSPodcast on RevOps myths | 38-sec stitch + reaction commentary | #RevOps #SaaSTok #stitch | "Disagree? Comment your take" | ✓ |
| 10 | Aug 5 | Tue | Twitter/X | 4:00 PM | Engagement | The 3 RevOps metrics that aren't predictive | None (text + reply-magnet) | #RevOps | What's the worst RevOps metric? | ✓ |
| 11 | Aug 6 | Wed | LinkedIn | 7:00 AM | Educational | Why median (not mean) is the right aggregation | Single image: median vs mean ops cycle time chart | #revops #datascience #b2bsaas | None (declarative) | ✓ |
| 12 | Aug 6 | Wed | Twitter/X | 8:30 AM | Social proof | n=47, 21-day lead time, here's the math | None (text + chart screenshot) | #RevOps | None | ✓ |
| 13 | Aug 6 | Wed | Instagram | 10:00 AM | Promotional | Free RevOps Diagnostic — Q3 calendar opens today | Static image, on-brand template | (20 in first comment) | Book a 30-min audit (link in bio) | ✓ |
| 14 | Aug 6 | Wed | TikTok | 12:00 PM | Behind-the-scenes | We surveyed 47 RevOps leaders. Here's what we found. | 52-sec talking-head, founder + 3 chart cuts | #RevOps #b2bsaas #data | "Share with your CRO" | ✓ |
| 15 | Aug 6 | Wed | Twitter/X | 3:00 PM | Trending | The Forrester GTM Singularity keynote was right about... | None (text-only opinion) | #B2BSaaS #RevOps | Reply with your take | ✓ |
| 16 | Aug 7 | Thu | LinkedIn | 8:00 AM | Engagement | RevOps Co-op AMA today: ops cycle time | Single image: AMA event card with date/time | #revops #revopscoop #ama | Join us at 2 PM PT (link in comments) | ✓ |
| 17 | Aug 7 | Thu | Twitter/X | 9:00 AM | Engagement | RT: We're doing a RevOps Co-op AMA at 2 PM... | None (RT + comment) | #RevOps | Submit questions in the thread | ✓ |
| 18 | Aug 7 | Thu | Instagram | 11:00 AM | Educational | The 4 stages of a healthy ops cycle | Carousel, 7 slides, on-brand template | (20 in first comment) | "Save this carousel" | ✓ |
| 19 | Aug 7 | Thu | TikTok | 1:00 PM | Promotional | We have 4 audit slots left this month | 28-sec founder on camera + on-screen text | #RevOps #SaaSTok | "Comment AUDIT for the link" | ✓ |
| 20 | Aug 7 | Thu | Twitter/X | 4:30 PM | Educational | A 5-tweet thread on the 21-day lead time finding | None (text thread + chart in tweet 3) | #RevOps | Reply with your team's lead time | ✓ |
| 21 | Aug 8 | Fri | LinkedIn | 9:00 AM | Social proof | "Threadline gave me the QBR slide I needed" — Priya at ScaleHQ | Single image: customer quote card | #revops #b2bsaas #casestudies | Read more case studies (link in comments) | ✓ |
| 22 | Aug 8 | Fri | Twitter/X | 10:00 AM | Behind-the-scenes | Friday wrap: what we shipped this week | None (text + 4 emoji bullets) | #RevOps #buildinpublic | None | ✓ |
| 23 | Aug 9 | Sat | Instagram | 10:00 AM | Behind-the-scenes | Threadline team off-site this weekend | Carousel, 5 slides, lifestyle photography | (20 in first comment) | None (community-led) | ✓ |
| 24 | Aug 10 | Sun | Twitter/X | 6:00 PM | Educational | Sunday read: 7-tweet thread on the next 90 days of RevOps | None (text thread) | #RevOps | Save the thread | ✓ |

**Pillar mix achieved:** Educational 33% (8/24); Social proof 17% (4/24); Behind-the-scenes 17% (4/24); Promotional 13% (3/24); Engagement 13% (3/24); Trending 8% (2/24). Within ±5% of target.

**Stagger plan:** Cross-posts staggered ≥48 hours where the same idea appears on multiple platforms (e.g., the ops cycle time benchmark appears on LinkedIn Mon, Twitter/X Wed, TikTok Wed, Instagram Thu — different platforms, different framings, no same-day overlap).

---

### Sample Post Copy (Post #1 — LinkedIn educational, Aug 4 7:30 AM)

> Ops cycle time leads revenue plan attainment by 21 days in B2B SaaS at 100–500 FTE.
>
> Most RevOps teams measure sales cycle length and pipeline coverage. Both are downstream metrics — they describe the prior quarter's outcome.
>
> Ops cycle time captures something different: the cross-functional friction that determines whether a deal closes in-quarter or slips to the next.
>
> We measured it across 47 customer accounts in our 2026 benchmark. The finding was consistent: a 10% reduction in ops cycle time correlates with a 7.4% lift in next-quarter plan attainment.
>
> Three implications for RevOps leaders:
>
> ▸ The metric your CRO will quote at the QBR is leading, not lagging. Get ahead of it.
> ▸ Median, not mean, is the correct aggregation. Outlier deals stuck in handoffs distort the mean.
> ▸ The handoff stages where ops cycle time accumulates are predictable: marketing→sales (38%), sales→CS (41%), onboarding→renewal (21%).
>
> If you want the full benchmark report (n=47, FY26), comment "BENCHMARK" and I'll send it.
>
> #revops #b2bsaas #revenueoperations
>
> *(Visual: 8-slide LinkedIn carousel with the ops cycle time chart, the 21-day lead time finding, the median-vs-mean comparison, and the handoff-stage breakdown. Slide 8 is the CTA to comment "BENCHMARK".)*

**Voice check:** ✓ No banned phrases ("leverage / synergy / unlock / revolutionize / best-in-class / AI-powered"). ✓ Tone matches Threadline voice v2.0 (plainspoken, specific over clever, engineer-respectful). ✓ First-line hook visible before "see more." ✓ 1,420 characters (within 1,200–1,500 sweet spot). ✓ 3 hashtags (within 3–5 LinkedIn 2026 cap).

---

### Strategic Notes

**Best posting times (Threadline B2B SaaS RevOps audience, PT):**
- LinkedIn: Tue–Thu 7:30–9:00 AM (peak engagement window for B2B)
- Instagram: Mon–Fri 9:00–11:00 AM (audience-active window)
- Twitter/X: Mon–Fri 8:00–10:00 AM and 3:00–5:00 PM (RevOps community active windows)
- TikTok: Mon–Wed 11:00 AM–2:00 PM (B2B SaaSTok peak)
- Source: Sprout Social Industry Benchmarks Report 2026; cross-checked with Threadline first-party engagement data Apr 2026

**Content recycling:**
- Post #6 (ScaleHQ social proof) — refresh quarterly with updated 90-day metrics
- Post #14 (47-leader survey TikTok) — repurpose for Q4 with refreshed survey data
- Post #18 (4 stages carousel) — evergreen; reshare every 90 days with updated examples

**Engagement playbook (first-hour window):**
- Brand account responds to comments within 60 minutes during posting hours
- Founder responds personally to first 3 comments on flagship posts (#1, #6, #14)
- Reply pattern: ask follow-up question + acknowledge specific detail; never canned responses

**AI-assist disclosure:**
- Post #4 (TikTok founder talking-head) — no AI involvement; no disclosure needed
- Post #14 (TikTok 52-sec data piece) — AI-assisted script first draft; disclosure label applied per TikTok 2026 policy

---

### Measurement Frame

| Platform | Primary KPI | Baseline | Target | Source dashboard |
|---|---|---|---|---|
| LinkedIn | Engagement rate | 3.2% (90-day median) | 4.0% | LinkedIn Page Analytics |
| Instagram | Saves rate | 2.1% (90-day median) | 2.8% | Instagram Insights |
| Twitter/X | Authenticated reach engagement rate | 1.8% (90-day median) | 2.4% | Twitter/X Premium Analytics |
| TikTok | Watch-through rate at 50% mark | 38% (90-day median) | 48% | TikTok Analytics |

**Secondary KPIs:** link clicks (target +20% week over week, source HubSpot); follower growth (target +1.2% week, source per platform); demo bookings attributed to social (target +15% week, source HubSpot Marketing Hub UTM tracker).

**Anti-vanity guard:** Twitter/X impressions are MPP-inflated; use authenticated reach. Instagram reach includes non-followers; use saves rate (intent signal) for the primary KPI.

**Holdout / read-window:** Compare to trailing 4-week baseline; the launch week (Aug 4–10) holdout is the prior 3 calendar weeks Jul 13–Aug 3 (excluding the spike week of the 2025 product update).

**Review cadence:**
- Mon Aug 11 8:00 AM: review of prior week's posts (engagement, reach, conversion)
- Thu Aug 13: calendar revision for Aug 18–24 week
- Sun Aug 16 6:00 PM: ship Aug 18–24 calendar
- Pillar mix audit at end of month (Aug 31)

---

### Assumptions & Gaps

- **Confirmed:** persona file, voice guide, all brand assets in inventory, Q3 launch date, RevOps Co-op AMA confirmed for Aug 7
- **Assumed:** TikTok stitch target (@SaaSPodcast) is willing to be stitched — verify with their team before Aug 5
- **Gap:** No Threads handle established yet — defer Threads pillar to next month after handle setup
- **Gap:** Trending TikTok sound for post #4 not yet selected — flag for Aug 3 final pre-publication trending-sound check
- **Gap:** Aug 7 AMA event card visual not yet designed — design ticket open with creative team, due Aug 6 EOD

**Confidence:** `high` (all eight required inputs present; persona named; voice guide loaded; brand assets inventoried)

---

### Refresh Date

- Calendar refreshes weekly (Monday review → Thursday revision → Sunday-night ship)
- Pillar mix audit monthly (next: Aug 31)
- Trending-sound check 7 days before publication (next: Aug 3 for TikTok #4)
- Voice anti-example list re-validated quarterly (next: Brand Voice Style Guide Generator refresh Oct 2026)
- Annual full-strategy refresh (next: Apr 2027)
