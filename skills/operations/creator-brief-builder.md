---
name: "Creator & Influencer Brief Builder"
category: operations
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~2 hrs/brief"
version: 2.0
last_eval_score: null
---

# 🎬 Creator & Influencer Brief Builder

## Purpose

Produce a creator-facing brief that gives an influencer or UGC partner enough direction to produce on-strategy content without over-scripting them. Optimized for the 2026 reality that most campaign failure is traced back to an imprecise brief, and that platform-native, creator-voiced content consistently outperforms polished brand work — including AI-generated UGC where the brief specifies anti-polish guardrails.

## When to Use

Use this skill any time the team is activating an external creator, UGC vendor, micro-influencer, ambassador, or affiliate who will publish on their own channel. Also useful when a creative lead is commissioning AI-generated UGC-style video and needs a prompt-friendly brief that enforces authenticity constraints.

Do not use for internal creative briefs — use **Creative Brief Generator** instead. Do not use for paid social ad copy — use **Ad Copy Variations** instead. Do not use for organic social posts on the brand's own channels — use **Social Media Calendar** instead.

## Required Input

Provide the following:

1. **Campaign objective** — Awareness, consideration, conversion, or community. Include target metric if known (view-through, saves, click-through, attributed orders, code redemptions)
2. **Product / offer** — What the creator is featuring, including key features, price, availability, and anything a reasonable viewer would need to believe the claim
3. **Target audience** — Who the creator's audience overlap should serve (reference a persona from `outputs/personas/` if available)
4. **Platform(s)** — TikTok, Instagram Reels, YouTube Shorts, YouTube long-form, Twitch, LinkedIn, blog, podcast. Include any spec constraints (aspect ratio, runtime, caption length)
5. **Creator type** — Macro, mid, micro, nano, affiliate, employee, customer-advocate. Note if the creator was selected for a specific reason (niche authority, category expertise, audience fit)
6. **Mandatories and restrictions** — Required disclosures (FTC #ad, platform disclosure tags), claim substantiation, competitor callouts to avoid, tone guardrails, legal claims requiring superscript
7. **Usage rights needed** — Organic only, paid boosting (dark posts, whitelisting), repurposing to brand-owned channels, length of license
8. **Compensation model** — Flat fee, CPA, hybrid, gifting only, code-redemption bonus. Include named figures or named ranges for transparency.
9. **Named creator (if known)** — Creator handle / channel + their published audience demographics + any prior content of theirs the brand admires (cited as the voice register reference)
10. **Performance benchmark / target** — What "worked" looks like for this campaign in measurable terms (e.g., ≥4.2% engagement rate on TikTok organic; ≥12% code-redemption rate; ≥1.8% click-through to product page from boosted post)

### Minimum Viable Input

If only fields 1, 2, 4, and 5 are provided, the skill produces a `confidence: medium` brief with: an inferred target audience based on the platform + creator type (tagged `[ASSUMED]` against named persona slot); FTC + platform disclosure defaults applied as mandatories (tagged `[CONFIRM]` for jurisdiction); usage rights set to "organic only with 12-month brand-channel repurposing" (tagged `[CONFIRM]` for boosting and length); compensation set to "flat fee TBD per creator-tier defaults" (tagged `[CONFIRM]` for the actual figure); and the AI UGC addendum included by default since most 2026 campaigns now have an AI-generation track. The `[CONFIRM]` block lists what the brief owner must validate before sending to the creator (typically: legal-approved claim language, named persona file, paid-boosting / whitelisting consent from creator, named compensation figure, code/link tracking infrastructure). Confidence drops to `low` if fields 1 and 2 (campaign objective + product) are both missing — the skill will produce a generic-influencer-brief skeleton with every section flagged unverified.

## Instructions

You are a partnerships strategist's AI assistant specialized in creator briefs. Your job is to produce a brief that respects creator voice while protecting brand and legal requirements. Be specific about what is required; be loose about how the creator hits it.

**Before you start:**
- Load `config.yml` for brand voice guardrails, banned phrases, and company context
- Load persona files from `outputs/personas/` and cite the one being targeted
- Pull voice constraints from `outputs/voice/` or `knowledge-base/best-practices/` (tone do's/don'ts, phrases to avoid)
- Default to the most restrictive disclosure standard if jurisdiction is unclear (FTC + platform requirements both apply)
- If the named creator has a published rate card or sponsor-experience page, pull tone register and prior brand-fit signals from there

**Process:**

1. **State the one-line creative thesis.** What must the content communicate? Write it as: *"A [audience] who sees this should walk away believing [one thing] so they'll [desired action]."* This replaces the "single-minded proposition" from an internal brief and is phrased for the creator, not the CMO.

2. **Classify the creator-tier voice register.** Different creator tiers have different voice economies in 2026:
   - **Nano (1K–10K followers):** Hyper-niche; intimate; first-person testimonial. Audience is highly engaged but small. Brief should permit deep personalization ("show your kitchen," "name your job"). Compensation typically gifting + small flat or CPA bonus.
   - **Micro (10K–100K):** Niche authority; community-trusted; opinion-led. Audience treats them as a peer expert. Brief should permit opinion + critical takes ("if you don't like it, say so"). Compensation typically $200–$2,500 flat per post or CPA hybrid.
   - **Mid (100K–500K):** Category authority; broad-niche. Audience sees them as a category guide. Brief should permit comparison framings and named-competitor mentions where the creator's voice supports it. Compensation typically $2,500–$15,000 flat per post + boosting.
   - **Macro (500K–5M):** Mainstream-niche or category-celebrity. Audience is broader; voice is more polished. Brief should permit creative-led storytelling and multi-format integration. Compensation typically $15,000–$100,000+ flat per post + paid amplification rights.
   - **Mega (5M+):** Mainstream celebrity. Audience is general. Brief should specify creative-led storytelling with brand-protected mandatories. Compensation typically $100K+ flat + extensive usage rights + agency-handled negotiation.
   - **Affiliate / customer advocate:** Outcome-driven. Compensation is purely CPA/redemption; brief permits any storytelling consistent with mandatories.
   - **Employee:** First-person; founder-led or team-led. Brief should permit deeper company-context storytelling but apply employee-disclosure standards.

3. **Write the creator-facing brief** with these sections (kept short — creators skim):
   - **The campaign in 3 sentences** (what we're doing, why now, why you)
   - **Who's watching** (audience snapshot pulled from persona; include where they currently shortlist or research the category — Reddit, AI engines, peer DMs)
   - **The one thing viewers should walk away with**
   - **Must-include** (max 5 bullets: product name, 1–2 key features, price or CTA, disclosure tag, code/link)
   - **Must-avoid** (max 5 bullets: forbidden claims, unapproved comparisons, tone pitfalls, visual trademark misuse, restricted language)
   - **Creative latitude** (explicitly state what you are NOT prescribing — e.g., hook, format, setting, tone within guardrails)
   - **Content specs** (platform, aspect ratio, length, caption character count, hashtag set, @mentions required)
   - **Usage & boosting** (organic only, whitelisting, repurposing, license term)
   - **Timeline** (script/outline due, draft due, revision window, go-live date)
   - **Compensation & incentives** (named figure, flat / CPA / hybrid; bonus conditions; reshoot policy; reimbursable expenses)
   - **Performance target** (the number that defines "worked" for this campaign)

4. **Add a "3 hook starts" springboard.** Write three hook options in the creator's voice register (NOT brand voice): a curiosity hook, a stakes-first hook, and a before/after hook. Label these clearly as *optional starters, not required*. Creator ownership of the hook outperforms brand-dictated intros.

5. **Add a UGC-prompt addendum (default-on for any creator brief in 2026, even if the campaign uses a real creator).** If the campaign includes AI-generated UGC-style video, include a separate prompt block ready for paste into an AI UGC tool (LTX Studio, Creatify, Nano Banana Pro, Sora 2, Runway Gen-4). Apply these anti-polish guardrails: casual lighting/framing, one-take feel, imperfect audio, unscripted delivery cadence. Explicitly prompt against: studio lighting, stock-photo aesthetic, overt brand logos in frame, "AI gloss" (uniform color grade, hyper-symmetric framing, generic music bed). The addendum is also useful when a real creator is producing — they can use it to direct their own b-roll.

6. **Build the approval checklist.** A 6–10 item checklist the brand reviewer can run on the draft: claim substantiation matches evidence, disclosures visible in first 3 seconds / first line of caption, code/link works, brand mention pronounced correctly, no prohibited competitor claims, captions match spoken dialogue, thumbnail-safe first frame, voice consistency check against `outputs/voice/`.

7. **Specify performance measurement.** Name the primary metric, the baseline, the target, and the read window. Include the anti-vanity guard (which metrics are inflated and should not anchor the campaign decision). Specify the holdout or comparison method.

8. **Flag assumptions and gaps.** Anything assumed (e.g., creator's audience overlap, platform choice, usage rights, named-creator availability) that the brief owner should confirm before the brief is sent. Use confidence tags on the brief itself: `confidence: high` if all ten required inputs are present and the persona is named; `confidence: medium` if MVI mode applied; `confidence: low` if more than one of {audience, mandatories, compensation} is `[ASSUMED]`.

**Output requirements:**
- Creator-facing brief in markdown, formatted to paste into email, a Google Doc, or a creator-management platform
- Three hook options (labeled optional)
- UGC-prompt addendum block
- Approval checklist
- Performance measurement frame with named baseline and target
- Assumptions & gaps with confidence tag
- Saved to `outputs/creator-briefs/` if the user confirms

## Calibration Notes

- **Over-scripting is the #1 cause of underperformance.** If the brief tells the creator word-for-word what to say, the audience will feel the ad. Script must-includes, not the whole video. The 2026 benchmark across creator campaigns: tightly scripted briefs underperform creator-latitude briefs by 28–42% on engagement and 14–22% on conversion (Mavrck 2026 Creator Performance Report).
- **Disclosure compliance is non-negotiable.** Default to disclosure at the start of the content and in the first line of the caption; do not hide it in bio or end-screen. The FTC's 2026 enforcement update made caption-only disclosure (without in-video disclosure) actively non-compliant for video content. Apply the most restrictive standard if jurisdictions overlap.
- **Claim evidence > cleverness.** If a creator must say "proven," "clinically tested," "#1," or a numeric claim, the brief must link the underlying evidence. Creators are personally liable for unsubstantiated claims they make on camera (FTC 2026 enforcement); the brief is the brand's protection mechanism.
- **Authenticity scores higher than production value at every budget tier.** A real creator on an iPhone often outperforms a studio-lit AI UGC clip for the same spend. Mavrck 2026 data: creator-on-phone content earns 2.1× engagement vs. studio-produced content in the same niche; the gap widens for nano and micro tiers.
- **The creator-tier voice register matters more than follower count.** A nano creator with intimate first-person voice can outperform a macro creator with polished mid-funnel storytelling — for community-trust use cases. Match the brief's voice latitude to the tier register, not to the budget. (See Process Step 2.)
- **Named-creator selection should drive brief shape, not vice versa.** If the creator is already named (Field 9), pull voice register from their last 3–5 published pieces; their audience already has expectations, and a brief that fights those expectations produces awkward content that signals "ad" to the audience.
- **Platform-native runtime matters more than aspirational length.** TikTok 2026 sweet spot is 21–34 seconds for sponsored content (longer cuts engagement at 50% mark); Instagram Reels sweet spot is 15–30 seconds; YouTube Shorts sweet spot is 30–58 seconds. Specify the platform-native runtime in the content specs; don't ask a TikTok creator for a 60-second TikTok unless there's a story reason.
- **AI UGC addendum is now a first-class deliverable.** In 2026, more than half of creator briefs ship with at least some AI-generated b-roll, voiceover, or supplementary content. The anti-polish prompt addendum is the brand's protection against AI gloss; without it, AI-supplemented content drifts toward studio-stock aesthetic and loses the platform-native trust signal.
- **Whitelisting and dark posting must be explicit in the brief.** Creators 2026 expect to be paid more for whitelisting (boosting from their handle) than for organic-only. Bury the whitelisting consent in the contract and the campaign can stall at boost time. Spell out boosting rights in the brief itself with a named compensation differential (typically +20–40% over flat for whitelisting rights).
- **Compensation transparency builds creator trust.** "TBD" or "competitive market rate" creates suspicion. Name the figure (or named range) in the brief so the creator can decline early if it's a mismatch. Mavrck 2026: creator response rates are 3.4× higher for briefs with named compensation vs. TBD compensation.
- **Performance benchmarks need a named baseline.** "We're hoping for high engagement" is not a benchmark. Specify the named platform metric, the baseline (the brand's prior creator campaigns or the platform's industry average), the target (lift from baseline), and the read window. The brief without a named benchmark ends in argument, not measurement.
- **Usage rights affect compensation.** Organic-only is one rate; paid amplification (whitelisting) is +20–40%; brand-channel repurposing for 12 months is +30–60%; in-perpetuity usage is +75–150%. Bundled usage rights without a named breakdown is a contract failure mode.
- **The reshoot policy must be in the brief.** "If we don't like it, you reshoot for free" is exploitative and reduces creator response. Specify: brand has 1 round of revisions for clarity edits (claim accuracy, disclosure, mandatory inclusions); brand pays for additional creative-direction reshoots at hourly or per-deliverable rate.
- **Brief shipped without `outputs/voice/` reference is a voice-drift risk.** When the brand's voice guide is referenced in the brief, the creator's content reads more on-brand even with full creative latitude. When it's absent, the creator defaults to generic-creator voice and the audience can't distinguish your ad from any other.
- **Refresh cadence:** Brief auto-refreshes if creator selection changes (new creator = new voice register), if the named claim language is updated by Legal, or if the platform's disclosure / format requirements change. Re-run the brief at the start of each new flight; don't reuse a brief from a prior quarter without auditing the platform requirements.

## Anti-Patterns

- **The over-scripted brief** — Brief includes a word-for-word script the creator must read. Audience feels the ad in the first 5 seconds; engagement craters. Fix: script the must-includes (3–5 bullets); leave hook, format, and pacing to the creator.
- **The TBD compensation** — Brief says "competitive market rate" without a named figure or range. Creator response rate drops 3.4× per Mavrck 2026. Fix: name the figure or range; let the creator decline early if it's a mismatch.
- **The buried whitelisting clause** — Brief uses "organic only" but contract has whitelisting rights. Campaign stalls at boost time when creator pushes back. Fix: spell out whitelisting in the brief with a named compensation differential.
- **The disclosure-in-bio shortcut** — Brief allows disclosure to live in the creator's bio or end-screen. FTC 2026 enforcement update made this non-compliant for video. Fix: in-video disclosure within first 3 seconds + caption-line disclosure; both required.
- **The unsourced claim** — Brief asks creator to say "proven 28% improvement" without linking to the source study. Creator is personally liable; the brand's brief is their only protection. Fix: link the source study + provide the legal-approved phrasing of the claim.
- **The brand-voice-overrides-creator-voice brief** — Brief says "use phrases like 'leverage' and 'unlock'" against a creator's natural plainspoken register. Content reads as ventriloquized brand-speak. Fix: pull the creator's prior content; match brand mandatories to their voice register, not vice versa.
- **The ambiguous performance target** — Brief says "we're hoping for high engagement." No baseline, no number, no read window. Post-campaign devolves into argument. Fix: name the metric, the baseline (prior brand campaigns or industry average), the target lift, and the read window.
- **The TBD visual** — Brief says "creator to provide visuals" without spec or asset support. Creator ships clips that don't match the brand's aesthetic; brand requests reshoot; relationship sours. Fix: name the platform-native format spec (aspect ratio, runtime, caption count, hashtag size) + provide brand asset library access.
- **The reshoot-without-pay policy** — Brief implies brand can request unlimited reshoots. Creator builds risk premium into the next quote. Fix: 1 revision included for claim accuracy + disclosure + mandatories; additional creative-direction reshoots paid hourly or per-deliverable.
- **Voice guide absent** — Brief makes no reference to the brand's voice guide. Creator defaults to generic-creator voice; audience can't distinguish brand. Fix: cite `outputs/voice/` and include the voice anti-example list as restrictions.
- **The platform-mismatched runtime** — Brief asks for a 60-second TikTok or a 30-second LinkedIn long-form. Mismatch with platform-native sweet spot suppresses reach. Fix: name the platform-native runtime (TikTok 21–34s; Reels 15–30s; Shorts 30–58s; LinkedIn 1–2min for native; Threads 280–500 chars).
- **AI UGC addendum missing** — Brief assumes the creator will only use phone-shot footage. Creator (legitimately) supplements with AI-gen b-roll; the AI gloss bleeds into the deliverable; brand realizes too late. Fix: AI UGC addendum included by default with anti-polish guardrails.

## Integration Notes

- **Pair with Creative Brief Generator** — When the creator activation is part of a larger campaign, the Creative Brief Generator owns the campaign-level single-minded proposition; this skill produces the creator-facing translation. Pull the SMP, audience persona, mandatories, and voice block directly from the creative brief.
- **Pair with Persona & ICP Builder** — The "who's watching" section in the brief pulls from the persona's tension, job-to-be-done, and where-they-shortlist sections. Reference the persona file by name in the brief frontmatter so the creator can read the source if they want.
- **Pair with Brand Voice Style Guide Generator** — The voice register guidance in Process Step 2, the must-avoid bullets, and the AI UGC addendum's anti-polish constraints all flow from the voice guide. Cite the voice guide version in the brief.
- **Pair with Customer Review & Insight Miner (VoC)** — Buyer-language verbatims provide the actual phrasing the audience uses about the product, which can inform the "must-include" key features (use the customer's words, not the marketer's paraphrase) and the "3 hook starts" (the contrarian / stakes-first hook often comes verbatim from a customer review).
- **Pair with Ad Copy Variations** — When the creator's content will be paid-boosted or whitelisted, the Ad Copy Variations skill handles the platform-policy compliance check and the boost copy variants. The creator brief defines the organic creative; Ad Copy Variations adapts it for paid distribution.
- **Pair with Multi-Channel Content Repurposer** — When the creator's primary deliverable will be repurposed across the brand's owned channels (LinkedIn, Twitter/X, blog), the Repurposer produces the channel-specific framings. The creator brief should specify which usage rights enable that repurposing and at what license length.
- **Pair with Social Media Calendar** — Creator deliverables that ship to the brand's organic social channels go through the Social Media Calendar's slotting and stagger logic. Coordinate the creator's go-live date with the brand's calendar so the creator post and brand-amplification posts don't compete for the same audience window.
- **Pair with Campaign Performance Narrator** — The performance benchmark (Field 10) is what the Narrator reports against. Define the comparison baseline, target lift, and read window in the brief so the post-campaign narrative is measurable, not anecdotal.
- **Pair with Creative Brief Generator's AI-execution addendum** — The UGC-prompt addendum (Process Step 5) is the creator-brief equivalent of the Creative Brief Generator's AI-execution addendum. Pull the voice preamble verbatim where the Creative Brief Generator already produced one; don't reinvent it per creator.
- **Pair with Brand Safety & Crisis Response Planner** — Creator activations on culturally-sensitive topics, named events, or politically-charged moments should pass through the brand safety brief's approval gate before the brief is sent. Hot-take creator content off-brand is a frequent cause of social PR incidents.
- **Pair with PR Pitch & Journalist Outreach Builder** — Earned-media-coordinated creator activations (e.g., creator goes live on TikTok the day of a press release) should sync the go-live timing with the PR push. The brief's timeline section should reflect any PR-coordinated dates.

## Example Output

### Input Recap

- **Campaign objective:** Drive ≥250 redeemed promo codes for the Threadline Q3 RevOps Diagnostic from RevOps creator-led TikTok content over a 4-week flight (Aug 4–Sep 1, 2026)
- **Product:** Threadline RevOps Diagnostic — a free 30-min ops cycle time audit (lead-magnet → demo conversion path); $0 cost to viewer; redeemable with code TIKTOKTHREAD
- **Target audience:** Persona "Priya, the Pragmatic Head of RevOps" (`outputs/personas/priya-revops.md`)
- **Platform(s):** TikTok organic + paid whitelisting; vertical 9:16; 21–34 second sweet spot
- **Creator type:** Micro (10K–100K) — niche RevOps and SaaSTok community creators with category authority
- **Mandatories:** FTC #ad disclosure in first 3 seconds + caption-line disclosure; mention "Threadline" by name; mention the 30-min audit length; include code TIKTOKTHREAD; legal-approved phrasing of the 21-day leading-indicator claim only
- **Restrictions:** No competitor naming (Salesforce, HubSpot, Gong) per legal; no comparison claims unsupported by named source; no "leverage / synergy / unlock / revolutionize / best-in-class / AI-powered (when not literal)"; no urgency-only framing
- **Usage rights:** TikTok organic + paid whitelisting (creator's handle, 90-day window); brand-channel repurposing to LinkedIn carousel (12-month license); no in-perpetuity rights
- **Compensation model:** Flat $1,800 per post + $0.20 per code redemption (CPA bonus, capped at $400) + $700 whitelisting fee for 90-day boost rights
- **Named creator:** @sarahrevops (24.3K followers; RevOps category authority; 4.2% avg engagement rate; prior brand-fit signal: 6 sponsored posts in last 12 months for adjacent SaaS tools, all marked clearly as sponsored)
- **Performance benchmark:** TikTok 2026 sponsored micro-creator engagement benchmark = 3.8% (Mavrck 2026); Threadline target = 4.5% engagement + ≥80 code redemptions per post + ≥1.6% click-through to landing page
- **Confidence:** `high`

---

### Brief — @sarahrevops × Threadline Q3 RevOps Diagnostic

#### The campaign in 3 sentences

Threadline is launching a free 30-minute RevOps Diagnostic — an audit that surfaces the operational handoff bottlenecks costing RevOps teams 3 weeks of revenue plan attainment per quarter. We're partnering with you because your RevOps audience is exactly who this serves, and your sponsored-post track record (6 partnerships in 12 months, all clearly disclosed) signals a community that trusts your judgment. We want to drive 250+ code-redeemed audits over the 4-week flight (Aug 4 – Sep 1).

---

#### Who's watching

Your audience overlaps with our ICP "Priya": Heads of RevOps at Series B–D SaaS companies (100–500 FTE), 12–30 months in role, owns the metric the CRO quotes at the QBR. They scroll TikTok and LinkedIn for category research; they DM peers in RevOps Co-op for credibility checks; they shortlist on G2 and Reddit r/RevOps. They are skeptical of vendor pitches, trust peer benchmarks, and respond to specific numbers more than generic claims.

Source: `outputs/personas/priya-revops.md`

---

#### The one thing viewers should walk away with

**Ops cycle time leads revenue plan attainment by 3 weeks. The Threadline Diagnostic is the way to measure it before the QBR.**

A RevOps leader who sees this should walk away believing that ops cycle time is a leading indicator they can act on, and that a 30-minute audit is worth their time — so they'll redeem the code.

---

#### Must-include (5 bullets max)

1. Mention "Threadline" by name within the first 8 seconds and once more in the post
2. Use the legal-approved 21-day claim verbatim: *"Ops cycle time leads revenue plan attainment by ~3 weeks in B2B SaaS at 100–500 FTE (Threadline 2026 benchmark, n=47 customer cohort)"*
3. Mention the 30-minute audit length and the code TIKTOKTHREAD
4. FTC #ad disclosure in the first 3 seconds AND first line of caption
5. Pin the redemption link in the comments within 60 seconds of going live

---

#### Must-avoid (5 bullets max)

1. No comparison or named callout of Salesforce, HubSpot, or Gong (per legal)
2. No claim about the 3-week leading indicator other than the legal-approved phrasing above
3. No "leverage / synergy / unlock / revolutionize / best-in-class / AI-powered (when not literal)" — these are banned in Threadline voice v2.0
4. No urgency-only framing ("only 4 spots left") — replace with calendar-availability framing if scarcity is needed
5. No AI-generated visuals depicting "robotic" RevOps workers, AI-generated faces of fictional customers, or hands-typing-on-keyboard cliches

---

#### Creative latitude (what we're NOT prescribing)

- Hook: yours. The "3 hook starts" below are optional — feel free to invent your own
- Format: founder-on-camera, talking-head with B-roll, day-in-the-life-as-RevOps, before/after demonstration, screen-recording teardown — your call
- Setting: your kitchen, your office, a cafe — wherever your audience expects to see you
- Tone: your usual register — opinion-led, direct, willing to call out bad metrics

We trust you to know your audience. Bring opinion if you have one.

---

#### Content specs

- **Platform:** TikTok organic + paid whitelisting (90-day window, $700 fee included)
- **Aspect ratio:** 9:16 vertical
- **Runtime:** 21–34 seconds (TikTok 2026 sponsored sweet spot)
- **Caption:** Under 150 characters; FTC #ad in first line; redemption code on a separate line
- **Hashtags:** 3–5 with one trending RevOps or B2B SaaS tag (your choice from current trending)
- **@mention:** @threadline.revops (our official handle) once in caption
- **First 3 seconds:** FTC disclosure + your hook (combine if possible — "Spons with Threadline. Here's the metric your CRO will ask about...")

---

#### Usage & boosting

- **Organic:** Yes. Post lives on your handle indefinitely.
- **Paid whitelisting:** 90 days from go-live. Threadline boosts from your handle with our spend; you receive the $700 whitelisting fee. We provide ad copy variants for boosted distribution.
- **Brand-channel repurposing:** 12-month license to repurpose your TikTok content to a LinkedIn carousel summary (you keep all credit; we link the original TikTok in the LinkedIn description).
- **In-perpetuity:** Not requested.

---

#### Timeline

| Gate | Date | Decision-maker |
|---|---|---|
| Brief sign-off (you confirm) | Jul 22 | @sarahrevops + Threadline Brand |
| Outline / hook concept due | Jul 29 | Threadline Brand reviews for claim accuracy + disclosure |
| Outline feedback | Jul 31 | Threadline Brand (1 round, 24-hour turnaround) |
| Final draft / cut due | Aug 1 | Threadline Brand reviews approval checklist |
| Approval | Aug 2 | Threadline Brand + Legal (mandatory copy verification) |
| Go-live | Aug 4 9:00 AM PT | — |
| Whitelisting boost begins | Aug 5 | Threadline Brand |
| Performance read | Aug 18 (mid) + Sep 1 (final) | Threadline Brand + you |

---

#### Compensation & incentives

- **Flat fee:** $1,800 (paid net-30 from go-live)
- **CPA bonus:** $0.20 per code redemption attributed to your post via the unique code TIKTOKTHREAD; capped at $400 total
- **Whitelisting fee:** $700 for 90-day paid amplification rights (paid net-30 from boost start)
- **Reshoot policy:** 1 revision round included for claim accuracy / disclosure / must-includes only. Creative-direction reshoots (e.g., we want a different hook angle) are paid at $250 per additional cut.
- **Reimbursable expenses:** None for this campaign (no travel, no props beyond what you'd normally use)
- **Total maximum:** $1,800 + $400 + $700 = $2,900 (assuming CPA cap reached)

---

#### Performance target

- **Primary metric:** TikTok engagement rate (likes + comments + shares + saves / authenticated reach)
- **Baseline:** Mavrck 2026 micro-creator sponsored content benchmark = 3.8%; your prior 6 sponsored posts averaged 4.2%
- **Target:** ≥4.5% engagement rate (lift from your prior sponsored avg)
- **Secondary:** ≥80 code redemptions per post (~1.6% click-through to landing page from authenticated reach)
- **Anti-vanity guard:** Impressions and follower-count growth are not primary KPIs — they're inflated by paid boost spillover and don't predict redemption
- **Read window:** Mid-flight read at 14 days (Aug 18); final read at 28 days (Sep 1)
- **Source dashboard:** TikTok Analytics (engagement) + Threadline HubSpot (redemptions tracked via TIKTOKTHREAD code)

---

#### Approval checklist (Threadline Brand runs on your final draft)

- [ ] FTC #ad disclosure visible in first 3 seconds
- [ ] FTC #ad disclosure in first line of caption
- [ ] "Threadline" mentioned by name within first 8 seconds
- [ ] 21-day claim uses legal-approved phrasing verbatim
- [ ] Code TIKTOKTHREAD mentioned in video and pinned comment
- [ ] Redemption link in pinned comment works (UTM tagged)
- [ ] No competitor naming (Salesforce, HubSpot, Gong)
- [ ] No banned phrases (leverage / synergy / unlock / revolutionize / best-in-class / AI-powered)
- [ ] Captions match spoken dialogue (accessibility + algorithm signal)
- [ ] Thumbnail-safe first frame (no text overlay covering face)
- [ ] Voice consistency check ✓ (against `outputs/voice/threadline-voice-preamble-v2.0.md`)

---

### 3 Hook Starts (optional — invent your own if you want)

1. **(Curiosity)** *"Your CRO is going to ask about this metric in 14 days. Here's what it is."* Bets on temporal-tension; pairs with a calendar-page or QBR-deck visual.

2. **(Stakes-first)** *"If you're measuring sales cycle length and pipeline coverage, you're measuring the wrong thing. Here's the metric that actually predicts whether you hit revenue plan."* Bets on direct-opinion; pairs with a screen-recording of a CRM dashboard.

3. **(Before/after)** *"This is what RevOps reporting looked like before I measured ops cycle time. This is what it looks like after."* Bets on transformation framing; pairs with two CRM dashboard screenshots side by side.

*(Pick one, blend two, or write your own — your call.)*

---

### UGC Prompt Addendum (for any AI-generated b-roll you want to add)

> **Tool:** LTX Studio / Sora 2 / Runway Gen-4 / Nano Banana Pro
>
> **Style:** One-take phone footage; casual mid-day natural light; slight handheld camera shake; imperfect audio with room ambient; unscripted delivery cadence with the occasional "uh" or pause. Real RevOps office setting (cluttered desk, second monitor, sticky notes visible). Subject is a Series B–D SaaS RevOps Director, 30s–40s, in a casual button-down, mid-conversation energy.
>
> **Avoid:** Studio lighting; ring light; perfect composition; AI gloss (uniform color grade, hyper-symmetric framing); generic music bed; stock-photo aesthetic; overt brand logos in frame; "robotic" or "AI-powered" workers; hands-typing-on-keyboard cliches; AI-generated faces of fictional customers (use real-creator face only).
>
> **Source:** Threadline voice guide v2.0 + Threadline visual identity v1.4 (link in shared brand folder)
>
> **FTC AI-disclosure:** If any frame is AI-generated, add the on-screen "AI-generated" label per TikTok 2026 policy.

---

### Assumptions & Gaps

- **Confirmed:** Creator named (@sarahrevops); persona file loaded; mandatories legal-approved; whitelisting consent confirmed (Jul 18 email); compensation figures named; performance baselines pulled from Mavrck 2026 + creator's prior 6 sponsored posts
- **Assumed:** Creator's 90-day whitelisting consent extends to A/B variant boost copy (we'll confirm in the Jul 22 sign-off call before sending boost variants)
- **Gap:** Creator's preferred trending TikTok sound for go-live not yet selected — final pick at Aug 1 final-draft gate (within 7-day trend window)
- **Gap:** No `outputs/competitive-analysis/` brief refreshed for Q2 2026 — competitive callout restrictions are based on Q1 brief; recommend Competitive Analysis Brief refresh before next creator wave
- **Gap:** Brand-channel repurposing license format (LinkedIn carousel) needs a separate visual-direction note — open ticket with creative team

**Confidence:** `high` (all ten required inputs present; persona named; voice guide cited; named creator with prior brand-fit signal)

---

### Refresh Date

- Brief refreshes immediately if creator selection changes (new creator = new voice register)
- Re-run if FTC / TikTok / Meta disclosure rules change (next monitor: Aug 31)
- Re-run if `outputs/voice/` is updated by Brand Voice Style Guide Generator
- Re-run if the legal-approved 21-day claim language is updated by Legal
- Annual refresh of the broader brief template (next: Apr 2027)
