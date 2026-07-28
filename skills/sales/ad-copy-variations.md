---
name: "Ad Copy Variations"
category: sales
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~20 min/campaign"
version: 2.3
last_eval_score: 9.5
---

# 📣 Ad Copy Variations

## Purpose

Create multiple headline and description variations for Google, Meta, and LinkedIn ads — each formatted to platform specs, organized by messaging angle, and ready to paste directly into ad platforms.

## When to Use

Use this skill when launching or refreshing ad campaigns across Google Ads, Meta Ads (Facebook/Instagram), or LinkedIn Campaign Manager. Ideal for A/B testing new messaging angles, seasonal promotions, new service launches, or when current ads are fatiguing. Works especially well downstream of the Persona & ICP Builder, Brand Voice Style Guide Generator, and Customer Review & Insight Miner — voice + verbatim-customer-language are the inputs that move CTR and CPA.

## Required Input

Provide the following:

1. **Campaign goal** — What action should the audience take? (e.g., book a call, request a quote, visit landing page, download a resource)
2. **Product/service being promoted** — What specific offering are the ads for, with the offer's specific terms (price, trial length, free / paid, time-bounded?)
3. **Target audience** — Who are you reaching? Reference a named persona file from `outputs/personas/` if available (e.g., persona Priya), with the buying-committee role and shortlisting behavior
4. **Key differentiators** — Why should someone choose you over competitors? (2–3 bullet points). Pull from `outputs/competitive-analysis/` if a recent brief exists; otherwise pull from `config.yml` → `value_props`
5. **Target platforms** — Which platforms to create for (default: Google RSA, Meta single image/carousel, LinkedIn Sponsored Content)
6. **Tone/angle preferences** (optional) — Urgency, social proof, educational, FOMO, problem-aware, solution-aware, contrarian, etc.
7. **Existing high-performing copy** (optional but high-leverage) — Share any ads that have worked well so the AI can riff on proven angles. Include the metric that defined "worked" (CTR > X, CPA < Y)
8. **Compliance and platform-policy constraints** — Required disclosures (FTC AI-disclosure, financial services, health), banned claims, competitor-naming policy, brand-safety constraints, regulated-industry language
9. **Creative-pairing context** (optional) — If specific imagery, video, or landing pages are pre-decided, share them; copy that doesn't pair with the visual under-performs no matter how clever

### Minimum Viable Input

If only fields 1, 2, 3, and 5 are provided, the skill produces a `confidence: medium` ad set with: differentiators inferred from `config.yml` → `value_props` and tagged `[ASSUMED]`, three default messaging angles (one social-proof, one pain-point, one direct-benefit), copy that respects platform character limits but flags any compliance language as `[CONFIRM]`, and an explicit gap list naming what would lift confidence to `high` (typically: named persona file, competitor / differentiator details, voice preamble, named existing high-performer to riff on). The voice preamble loads from `config.yml` defaults; the user is told which voice attributes to confirm before pushing the campaign live.

## Instructions

You are a skilled performance marketing copywriter's AI assistant. Your job is to generate platform-compliant ad copy variations that drive clicks and conversions — and that pair sensibly with the creative and the landing page they route to.

**Before you start — load `config.yml` and let it carry the *substance* of the copy, not just the tone (the offer, the differentiators, and the banned claims are all already declared; re-asking for them is how a variant set drifts off-brand and off-offer):**
- `value_props` — pre-fills **Required Input 4 (key differentiators)**. Present the config list and ask only which 2–3 to lead with; do not re-ask for differentiators config already holds. Any value prop without a named proof point gets written as a claim tagged `[PROOF NEEDED]`, never as a bare superlative.
- `pricing` / offer terms (`pricing.model`, rates, `payment_terms`, `financing`, trial or estimate mechanics) — **anchors Required Input 2 (the offer's specific terms) and the offer/CTA headlines.** This is what makes a CTA specific ("Start the 14-day trial," "Get the flat-rate quote," "Book the free 30-min audit") instead of the dead-generic "Learn more." It is also the **urgency gate**: an urgency or offer-based headline is only written when config declares a genuinely time-bound offer. If config's offer is evergreen, the urgency headline slots are reallocated to pain-point and proof angles and the reallocation is stated — fake urgency is a quality-score penalty on every major platform (see calibration).
- `competitors` — pre-fills the **competitor-naming policy** (Required Input 8) and gates the **contrarian angle**. A contrarian headline is a claim *against* a named alternative's approach; whether that is viable without legal exposure depends on who the alternative is and whether the brand's policy allows naming them. Default: no competitor naming unless config or the brief explicitly permits it. A brief that greenlights a competitor callout config restricts is a conflict — surface it, do not silently resolve it.
- `voice.never_use` — a **hard banned-phrase filter** applied to every variant in the step 5 compliance pass, not a soft style preference. It applies even before a full `outputs/voice/` preamble exists, and it is the floor the voice guide's own banned-phrase list sits on top of. Any line that trips it is rewritten and the substitution noted.
- `voice.always_use` + `voice.tone` — the register the variants are written in, and the approved phrases to weave in where they land naturally (never bolted on to hit a quota).
- `priorities.top_improvements` / `priorities.pain_points` — bias the **campaign goal and primary metric** (step 6) toward the KPI the team is actually trying to move, and seed the pain-point angle with the pains the team already knows its buyers name.
- `services.core` / `services.excluded` — the ads must sell what the brand actually sells. An excluded service showing up in a headline is a lead-quality leak, not a creative flourish.
- Reference `knowledge-base/terminology/` for correct industry terms
- Pull the AI prompt preamble from `outputs/voice/` if a Brand Voice Style Guide Generator output exists
- Pull persona context from `outputs/personas/` and reference the persona by name
- Pull the verbatim-quote bank from `outputs/voc/` if a Customer Review & Insight Miner output exists — customer language outperforms marketing-team language in headlines

**Process:**

1. **Define the messaging framework before writing any copy:**
   - Identify the primary value proposition (one sentence — must pass the proposition test: a creative team should be able to produce three on-strategy ideas from it)
   - List 3–4 distinct messaging angles (e.g., social proof, urgency, pain point, aspiration, contrarian, educational)
   - Define the audience's awareness level (problem-aware, solution-aware, product-aware, most-aware) — this determines headline directness
   - Note any seasonal or timely hooks
   - Note the AI search visibility context — if competitors are winning AI-engine citations on the same query, the ad message needs to land *before* the click (because AI-engine summaries arrive *after* the click)

2. **Generate Google Responsive Search Ads (RSA):**

   **Headlines (15 variations, max 30 characters each):**
   - 3–4 headlines featuring the primary value proposition
   - 2–3 headlines with a call-to-action
   - 2–3 headlines with social proof or credibility (named customer, named outcome, named credential)
   - 2–3 headlines addressing a specific pain point (use verbatim-customer-language where available)
   - 2–3 headlines with urgency or offer-based hooks (only if a real time-bound offer exists — fake urgency is a quality-score penalty in 2026)
   - **Pin recommendations** for positions 1, 2, and 3 (Google rewards strategic pinning when the ad copy has structural intent — value prop in pos 1, differentiator in pos 2, CTA in pos 3 is a common high-performer)

   **Descriptions (4 variations, max 90 characters each):**
   - Each should pair well with any headline combination
   - Include a CTA in at least 2 descriptions
   - Reference specific benefits, not just features
   - Include 1 description with a quantified proof point (named stat, named outcome, named credential)

   **Sitelink, callout, and structured snippet recommendations** (optional but high-leverage on RSA performance):
   - 4 sitelinks (text + description), each routing to a specific landing page
   - 6 callouts (25 chars each, no CTA — supporting credibility)
   - 1 structured snippet pair (Header + 4 values, e.g., "Services: Onboarding | Migration | Audit | Support")

3. **Generate Meta Ads (Facebook / Instagram):**

   **Primary Text (3 variations, recommended 125 characters for above-the-fold):**
   - Hook in the first line — question, bold claim, statistic, or pattern interrupt
   - Short body expanding on the hook
   - Clear CTA with link context
   - **Algorithm note (2026):** Meta's CAPI + Advantage+ creative auto-optimization rewards diverse creative-text-pairings; provide variations that test fundamentally different angles, not just synonym swaps

   **Headlines (3 variations, max 40 characters):**
   - Complement the primary text, don't repeat it
   - Action-oriented or benefit-focused
   - Test one curiosity-led, one direct-benefit, one social-proof

   **Descriptions (3 variations, max 30 characters):**
   - Support the headline with secondary benefit or urgency
   - Avoid restating the headline

   **Format recommendations:**
   - Suggest which copy pairs work best for single image vs. carousel vs. video vs. Reel
   - Carousel-specific copy framing: each card is a beat in a 4–6 step argument; copy must work as a sequence

4. **Generate LinkedIn Sponsored Content:**

   **Introductory Text (3 variations, max 150 characters for mobile-visible):**
   - Professional but not boring — avoid corporate jargon and "transform / unlock / leverage" family
   - Lead with insight, data point, or provocative question
   - Speak to the buyer's role (e.g., Head of RevOps), not just the product

   **Headlines (3 variations, max 70 characters):**
   - Business-outcome focused
   - Quantify where defensible
   - Speak to the named persona, not the company

   **Descriptions (3 variations, max 100 characters):**
   - Reinforce credibility or specificity
   - Include a named credential or named customer outcome where available

   **Conversation Ad addendum (optional):**
   - 1 branched-flow opener (3 message bubbles, 2 CTA options)
   - Mapped to buyer roles: economic buyer, champion, technical evaluator, blocker

5. **Cross-platform compliance + brand-safety check.**
   - Verify FTC AI-disclosure footnote on any AI-generated visual or AI-personalized creative
   - Verify required disclaimers (financial / health / regulated industry) per platform policy
   - Verify no banned claims (Meta's "personal attribute" rule, LinkedIn's restrictions, Google's healthcare-and-finance restrictions)
   - Note any platform-specific policy gates (e.g., LinkedIn requires verified-page status for some ad formats; Meta's Special Ad Categories trigger additional review)
   - **Banned phrases:** apply `config.yml` → `voice.never_use` as a hard filter first (it applies even with no voice guide in place), then the voice guide's banned-phrase list on top (no "leverage / synergy / unlock / revolutionize / best-in-class" etc.). Report any line that was rewritten and what replaced it.
   - **Competitor-naming check:** confirm every variant respects the config competitor-naming policy — including the contrarian angle and any Conversation Ad branch, which is where a competitor name most often slips through unreviewed.
   - **Offer-terms check:** confirm every offer, price, trial length, and guarantee stated in the copy matches `config.yml` → `pricing`. An ad that promises terms the business does not offer is a lead-quality problem and, in regulated categories, a compliance one.

6. **Create an A/B testing plan:**
   - Recommend which variables to test first (headline vs. description vs. angle vs. visual — usually angle > headline > description for impact)
   - Suggest minimum budget and duration for statistical significance (rule of thumb: 200 conversions per variant for 80% power detecting a 15% lift; otherwise the test is underpowered and the "winner" is noise)
   - Define success metrics per platform (CTR, CPC, CPL, CPA, ROAS — pick the metric closest to the campaign goal, not the highest-volume one)
   - Define a stop-loss rule (e.g., kill any variant below 50% of control CTR after the minimum sample is reached)
   - Provide a holdout recommendation for incrementality measurement (10% holdout for 4–6 weeks if budget allows)

7. **AI-assist layer.**
   - For each platform, suggest a "next iteration" idea: if the current set underperforms, what's the most defensible next bet? (e.g., "if Google RSA CTR < 2%, refresh headlines 1, 5, 10 with the verbatim customer phrase 'finally I can see the seam' from the VoC quote bank")

**Output requirements:**
- All copy clearly organized by platform with character counts shown next to every line
- Each variation labeled with its messaging angle (e.g., "Social Proof," "Urgency," "Pain Point," "Contrarian")
- Character-count compliance verified for every line
- A/B testing recommendations included with named metric, sample-size logic, and stop-loss rule
- Compliance & brand-safety check completed
- Confidence tag (`high` / `medium` / `low`)
- Copy formatted for easy paste into ad platform interfaces
- Uses company name, services, persona, and voice from config
- Saved to `outputs/ads/[campaign-slug]/` if the user confirms

## Calibration Notes

- **Verbatim customer language outperforms marketing-team language by 20–40% on CTR.** Pull from the Customer Review & Insight Miner's verbatim-quote bank rather than paraphrasing. The phrase a customer typed in a review — exact words, exact order — almost always converts better than the version your marketing team rewrote into "polished" copy.
- **Awareness-level mismatch is the #1 cause of low ad performance in 2026.** A "buy now" headline shown to a problem-aware audience misses; an educational headline shown to a most-aware audience misses. Match the headline directness to the awareness level. (Problem-aware = empathy + name-the-pain; solution-aware = differentiate; product-aware = proof; most-aware = offer.)
- **Fake urgency is a quality-score penalty.** Google, Meta, and LinkedIn all flag "Only 2 hours left!" framing applied to non-time-bound offers in 2026. Use urgency only when there's a real deadline (sale ends, cohort starts, capacity caps).
- **Pinning RSA headlines is now a structural lever, not a constraint.** The 2025–2026 Google RSA algorithm rewards strategic pinning when the ad has structural intent (value prop pos 1, differentiator pos 2, CTA pos 3). Unpinned RSAs that mix value-prop and CTA across all positions hit a Q-score ceiling.
- **Meta Advantage+ creative auto-optimization rewards angle diversity, penalizes synonym swaps.** Three Meta variants that say "Drive growth," "Unlock growth," "Accelerate growth" perform identically because the model treats them as the same creative. Three variants that test fundamentally different angles (pain-point / social-proof / contrarian) compound the auto-optimization advantage.
- **LinkedIn rewards role-specific framing.** "For RevOps leaders at Series B SaaS" outperforms "For marketing teams" by 30–50% on click-through to Sponsored Content in B2B verticals. The ICP precision of the persona file is what makes this real.
- **Compliance and platform policy is the #2 cause of dead ads in 2026.** FTC AI-disclosure rules tightened in late 2025; Meta's personal-attribute rule still bans "you" framing in some categories; LinkedIn's verified-page requirement for some ad formats blocks unverified accounts. Build the compliance check into the workflow before submission.
- **Meta and LinkedIn are not Google.** A direct-response, intent-led headline that crushes on Google's high-intent search audiences fails on Meta's mid-funnel social audience. Different audiences, different awareness levels, different framings.
- **Statistical-significance rule of thumb:** ~200 conversions per variant for 80% power detecting a 15% lift. Below that, the "winning" variant is noise. Most A/B tests in ad-platform UIs are called too early and produce false-positive winners that don't repeat.
- **Brand voice consistency matters more than per-ad cleverness.** A voice-drift across 12 ad variants is a brand-equity tax that compounds. The Brand Voice Style Guide Generator's preamble is the system prompt; apply it to every variant.
- **Refresh cadence.** Re-run the variation set every 14–28 days for paid social (creative fatigue arrives fastest there); every 30–45 days for Google RSA (broader keyword coverage extends life); every 21–30 days for LinkedIn. Don't wait for a single variant to dominate — rotate before the algorithm kills the campaign.
- **Let config carry the offer, not just the voice.** The two fields that decide whether a variant set converts are the ones most often left in config and never read: `value_props` (what to lead with) and `pricing` (what you're actually offering). A CTA written without the offer terms defaults to "Learn more" — the single most common and least effective CTA in paid search — while a CTA written *from* them is specific and self-qualifying ("Start the 14-day trial," "Get the flat-rate quote"). And the offer terms are the honest test for urgency: if `pricing` describes an evergreen offer, there is no real deadline, the urgency slots get reallocated, and the ad set is better for it. Config is the brief the team already wrote; read it before asking them to write it again.
- **The platform is now writing copy alongside you — and you own it.** Under the Google Ads Terms of Service revised **July 1, 2026**, automated generation of ads, targets, and destinations is authorized by default at the account layer (previously an opt-in feature set), and the terms state that the **advertiser remains responsible for reviewing, approving, editing, or removing** campaigns and assets, *including the ones the platform's own tools generated*. Practically: Automatically Created Assets can ship a headline you never wrote, and Final URL Expansion can send that headline's click to a page you never chose — and both carry your brand's liability. Three habits follow. (1) **Audit your variant set against what the platform is adding**, not just what you uploaded — pull the asset report and read the auto-created lines before they accumulate impressions. (2) **Treat the auto-generated copy as failing the brand check until reviewed**: it inherits your landing-page and sitemap language, not your "never say" list, so unsubstantiated performance claims and fake-urgency framing are exactly the failure modes to look for. (3) On accounts where an unreviewed claim is a real legal exposure (regulated categories, comparative claims, pricing), the honest answer is often to **narrow or switch the generative features off** rather than promise a review cadence the team will not sustain. Govern this properly via the Agent-Controlled Campaign Ops skill's platform-automation baseline; here, just never assume the ads running are only the ads you wrote.
- **Don't write ad copy without knowing the landing page.** A clever ad routing to a generic homepage hits message-match collapse. The Landing Page Conversion OS / Persona & ICP Builder / Voice Guide should all be in place before this skill ships final copy.

## Anti-Patterns

- **The thesaurus pack** — 15 RSA headlines that all say the same thing in different words ("Best service / Top service / Premium service / Leading service"). The Google quality-score model treats these as duplicates; ad strength stays low; CPC stays high. Variants must test different *angles*, not synonyms.
- **The fake countdown** — "Hurry! Only 6 hours left!" applied to an evergreen offer. Quality-score penalty across all major platforms; brand trust erosion; rebound CPC.
- **The voice-drift pack** — LinkedIn variants read "engineer-respectful, plainspoken"; Meta variants read "🔥 LET'S GO 🚀". Brand voice broken across platforms; AI-detection signal up; engagement uneven.
- **The TBD CTA** — "Learn more" used as the CTA on every variant. CTA must vary by awareness level and offer specificity. "Run the 30-min audit" / "See ScaleHQ's case study" / "Compare your cycle time" all out-perform "Learn more."
- **The headline-description repeat** — Headline says "Cut ops cycle time by 31%"; description repeats "Reduce your ops cycle time by 31%." Wasted real estate. Headline + description should be additive (proof + offer, claim + credential, pain + path).
- **The compliance afterthought** — copy ships, then legal pushes back, then 3-day rewrite. Compliance check is part of the workflow, not after.
- **The 50-conversion test** — A/B test stopped at 50 conversions per variant because "the winner emerged." It's noise. Either run to 200 conversions / variant or accept it's a directional read.
- **The orphan ad** — clever ad copy routed to a generic homepage. Message-match collapses; landing page bears the bounce; campaign reads "didn't work" but it was the routing.
- **The config re-ask** — asking the user for differentiators, offer terms, banned phrases, and competitor policy that `config.yml` already declares. It wastes the user's time and, worse, produces a second source of truth that drifts from the first.
- **The offer the business doesn't offer** — a headline promising a free trial, a discount, or a guarantee that `config.yml` → `pricing` does not describe. It converts, then the lead bounces at the quote, and the campaign gets blamed for the copy's invention.
- **The persona-as-job-title** — "For marketing leaders" used as the LinkedIn role tag. Too broad; algorithm can't optimize. Specific persona role + segment specifier ("Head of RevOps at Series B SaaS") outperforms by a wide margin.

## Integration Notes

- **Persona & ICP Builder** (`outputs/personas/`) — Persona's verbatim language, hidden motivation, shortlisting behavior, and named accounts feed the headline phrasing, the LinkedIn role-targeting, and the awareness-level classification. Reference the persona file by name in the ad set frontmatter.
- **Brand Voice Style Guide Generator** — Voice attributes + AI prompt preamble + banned-phrase list are the system prompt for every AI-assisted variant. Don't re-author voice rules at the ad-copy level; cite the voice guide version.
- **Customer Review & Insight Miner** — Verbatim-quote bank is the highest-converting source of headline phrases. Pain-point headlines and proof-point descriptions should pull literal customer phrases, not paraphrases.
- **Competitive Analysis Brief** (`outputs/competitive-analysis/`) — Differentiator selection (which 2–3 to lead with) and contrarian-angle viability (when contrarian framing works without legal exposure) flow from the competitive analysis. If no recent analysis exists, flag it as a gap.
- **Synthetic Persona Simulator** — Pre-test ad variants against the simulator persona before launch, especially for the contrarian angle and any high-stakes claim. Cheaper than a failed test.
- **Landing Page Conversion OS** — The ad's promise must match the landing page's promise on the message-match axis. Run the landing page audit upstream of the ad set; copy and page should pass the message-match test together.
- **AEO Content Optimizer / AI Search Visibility Audit** — When the campaign is running against a query where AI-engine answers are also visible, the ad copy needs to land *before* the AI-summary visual hierarchy on the SERP. Headlines that match the AI-cited claim's phrasing pick up "trusted-overlap" association.
- **Email Sequence Builder** — Ad copy on the demo CTA flows directly into the first email of the post-conversion sequence. Voice and proof should be continuous; treat the ad → email transition as one document, not two.
- **Cross-Channel Attribution Analyzer** — When measuring incrementality of the ad set, the holdout design from this skill ties directly into the attribution analyzer's read.
- **Campaign Performance Narrator** — Performance reporting in the Narrator's audience-aware framing pulls back to the messaging angles defined in step 1 of this skill. Tag every variant with its angle so the post-campaign narrative can attribute lift to angle, not just to creative.
- **Multi-Channel Content Repurposer** — When a high-performing organic post becomes paid creative, the Repurposer's top-performing angle and verbatim phrases become the seed for this skill. Pass the top organic version as the "existing high-performing copy" input.

## Example Output

### Input Recap

- **Campaign goal:** Drive 25% lift in qualified demo bookings (Q3 2026 RevOps push)
- **Product:** Threadline RevOps Diagnostic — free 30-min ops cycle time audit (lead-magnet → demo)
- **Audience:** Persona Priya, the Pragmatic Head of RevOps (`outputs/personas/priya-revops.md`); Series B–C SaaS, 100–500 FTE; awareness level = solution-aware (knows the problem, doesn't yet know the named metric)
- **Differentiators:** (1) named "ops cycle time" as the leading indicator, 21-day lead time empirically validated; (2) ScaleHQ case study (31% cut in 90 days); (3) measurable without a CDP
- **Platforms:** Google RSA, Meta single image + carousel, LinkedIn Sponsored Content + Conversation Ad
- **Tone / angle:** social-proof, contrarian, pain-point, educational (4 angles)
- **Existing high-performer:** Q1 2026 LinkedIn post with verbatim phrase "the seam between Salesforce and everything else" — drove 6.2× the platform-average engagement
- **Compliance:** FTC AI-disclosure on AI-visuals; SOC 2 badge required on landing page; legal-approved phrasing of the 3-week claim only; no competitor naming
- **Pairing context:** Visual = Threadline brand-template chart; Landing page = `/audit` (recently audited via Landing Page Conversion OS, message-match score 4.2/5)
- **Voice preamble:** `outputs/voice/threadline-voice-preamble-v2.0.md`
- **Confidence:** `high`

---

### Messaging Framework

- **Primary value proposition:** Ops cycle time leads revenue plan attainment by 3 weeks — get the audit before your CRO asks the question
- **Awareness level:** solution-aware (lead with proof + named metric + named outcome)
- **Messaging angles (4):**
  1. **Pain point** — "Your CRO is about to ask about a metric you might not be tracking"
  2. **Social proof** — "ScaleHQ cut theirs 31% in 90 days"
  3. **Contrarian** — "Sales cycle length is the wrong number"
  4. **Educational** — "How to measure ops cycle time without a CDP"

---

### Google Responsive Search Ads (RSA)

**Headlines (15 — character counts in parentheses):**

1. *(Pain Point — pin pos 1)* The Metric Your CRO Will Ask (28)
2. *(Pain Point)* Find the Forecast Risk Early (28)
3. *(Value Prop — pin pos 1)* Ops Cycle Time Leads Revenue (28)
4. *(Value Prop — pin pos 1)* The 3-Week Leading Indicator (28)
5. *(Social Proof)* ScaleHQ Cut Theirs 31% in 90 Days (30)
6. *(Social Proof)* Used by 47 RevOps Teams in 2026 (29)
7. *(Social Proof)* The Audit ScaleHQ Ran First (28)
8. *(Differentiator — pin pos 2)* No CDP Required to Measure (26)
9. *(Differentiator — pin pos 2)* Free 30-Min Ops Audit (21)
10. *(CTA — pin pos 3)* Run the Audit in 30 Minutes (27)
11. *(CTA — pin pos 3)* Book the 30-Min Audit (21)
12. *(Pain Point)* Pipeline Looks Fine. Forecast Won't (30)
13. *(Contrarian)* Sales Cycle Length Is the Wrong KPI (30)
14. *(Educational)* The 3-Week Lead on Revenue (26)
15. *(Educational)* What Ops Cycle Time Actually Predicts (30)

**Descriptions (4 — max 90 characters):**

1. *(Proof + CTA, 87 ch)* Ops cycle time leads revenue plan attainment by 3 weeks. Run the free 30-min audit.
2. *(Differentiator + CTA, 86 ch)* Measure ops cycle time without a CDP. ScaleHQ cut theirs 31%. Run the audit.
3. *(Pain + Empathy, 85 ch)* Your CRO is about to ask about this. Find the forecast risk before they do.
4. *(Quantified, 88 ch)* When ops cycle time worsens 1 day, revenue plan slips 4–6%. Lead time: 21 days.

**Sitelinks (4):**
- "30-Min Ops Audit" → `/audit` (free diagnostic; SOC 2 verified)
- "ScaleHQ Case Study" → `/case-study/scalehq` (31% cut in 90 days)
- "Cycle Time Benchmarks" → `/benchmarks` (Series A–C+ healthy ranges)
- "Measurement Without a CDP" → `/blog/measure-without-cdp` (the spreadsheet method)

**Callouts (6):** SOC 2 Type II Verified | n=47 Customer Cohort | 30-Min Audit | No CDP Required | Used by Series B+ | RevOps Co-op Recommended

**Structured snippet:** Services → Audit | Benchmark | Diagnostic | Implementation

---

### Meta Ads (Single Image + Carousel)

**Primary Text (3 — angle + char count):**

1. *(Pain Point — 124 ch)* Your CRO is about to ask about a metric you might not be tracking. Sales cycle length is the lagging one. The leading one is called ops cycle time.
2. *(Social Proof — 122 ch)* ScaleHQ cut their ops cycle time 31% in 90 days. Then hit revenue plan attainment two quarters in a row. The audit takes 30 minutes.
3. *(Contrarian — 119 ch)* Most RevOps teams measure the wrong cycle time. The one that actually predicts revenue worsens 21 days before the forecast slips.

**Headlines (3 — max 40 characters):**

1. *(Direct benefit, 35 ch)* Find the Forecast Risk in 30 Minutes
2. *(Curiosity, 38 ch)* The Metric Your CRO Will Ask About Next
3. *(Social proof, 30 ch)* ScaleHQ Cut Theirs 31%

**Descriptions (3 — max 30 characters):**

1. *(Differentiator, 25 ch)* No CDP. No vendor calls.
2. *(Urgency-restrained, 28 ch)* Before the next QBR question
3. *(Credential, 28 ch)* SOC 2 Verified · n=47 Cohort

**Format recommendations:**
- **Single image:** Pair with the Threadline brand-template chart (ops cycle time vs. revenue plan attainment, 21-day offset annotated). Best with Pain Point + Social Proof primary text.
- **Carousel (5 cards):** Card 1 = hook ("Your CRO is about to ask…"); Card 2 = define ops cycle time; Card 3 = the 21-day lead time chart; Card 4 = ScaleHQ outcome; Card 5 = CTA "Run the 30-min audit."
- **Reel:** Use the TikTok / Reel script from the Multi-Channel Repurposer output. Pair with primary text variant 3 (Contrarian).

---

### LinkedIn Sponsored Content

**Introductory Text (3 — max 150 characters):**

1. *(Role-targeted Pain Point, 144 ch)* RevOps leaders at Series B SaaS: the metric your CRO will surface at the next QBR is probably the one you don't have a clean way to measure.
2. *(Educational + Specific, 142 ch)* Ops cycle time leads revenue plan attainment by ~3 weeks across our 47-customer cohort. Most teams aren't measuring it. The audit is 30 min.
3. *(Contrarian + Insight, 138 ch)* Sales cycle length is the lagging revenue indicator. Ops cycle time is the leading one — and you don't need a CDP to measure it.

**Headlines (3 — max 70 characters):**

1. *(Direct outcome, 64 ch)* Find the 21-Day Forecast Risk Before Your CRO Asks About It
2. *(Social proof, 66 ch)* The Metric ScaleHQ Cut 31% — Then Hit Plan Two Quarters in a Row
3. *(Role-specific, 62 ch)* The Free 30-Min Audit Built for Series B+ RevOps Leaders

**Descriptions (3 — max 100 characters):**

1. *(Credential, 90 ch)* Threadline 2026 benchmark, n=47 customer cohort. SOC 2 Type II. RevOps Co-op recommended.
2. *(Specificity, 96 ch)* Measurable without a CDP. Native Salesforce reports + 1 spreadsheet column gets the number.
3. *(Outcome, 89 ch)* ScaleHQ cut theirs 31% in 90 days; the part that didn't work is in the case study.

**Conversation Ad addendum (optional — branched flow):**

- **Opener:** "Hi Priya — quick question for any Series B+ RevOps leader. If your CRO asked about ops cycle time at the next QBR, would you have the number ready?"
- **Branch A (Yes):** "Strong. Would the 31%-improvement playbook from ScaleHQ be useful regardless?" → CTA: "Send me the case study"
- **Branch B (No / Not sure):** "That's most teams. The 30-min audit pulls the number from your existing Salesforce data — no CDP required. Want to run it?" → CTA: "Run the 30-min audit"

---

### Compliance + Brand-Safety Check

- ✓ FTC AI-disclosure footnote attached on any AI-generated visual (Meta carousel cards 3–4 use AI-augmented chart visuals)
- ✓ SOC 2 Type II language verified on landing page (`/audit` audit confirmed Apr 2026)
- ✓ "3-week leading indicator" claim uses legal-approved phrasing only ("Ops cycle time leads revenue plan attainment by ~3 weeks in B2B SaaS at 100–500 FTE")
- ✓ No competitor naming (Salesforce, HubSpot, Gong) per legal — including in Conversation Ad branched flow
- ✓ Banned-phrase check passed (no leverage / synergy / unlock / revolutionize / best-in-class)
- ✓ Meta personal-attribute rule — "you" framing reviewed; no protected-class implications
- ✓ LinkedIn verified-page status confirmed for Sponsored Content + Conversation Ads

---

### A/B Testing Plan

**Phase 1 — Angle Test (highest expected impact):**
- Test 4 angles (Pain Point / Social Proof / Contrarian / Educational) with controlled headline + description set
- **Sample size target:** ~200 conversions per angle for 80% power detecting a 15% CPA delta — at $48K media spend and ~$190 LinkedIn CPL, this is the full Q3 budget across all four variants
- **Stop-loss rule:** kill any variant below 50% of control CTR after 75 conversions
- **Primary metric:** qualified demo bookings (not CTR)
- **Secondary metrics:** CPL (target ≤ $190), CTR (target ≥ 1.4%), demo-page CVR (target ≥ 4.2%)
- **Holdout:** 10% paid LinkedIn audience held out 6 weeks for incrementality

**Phase 2 — Creative Test (within winning angle):**
- Test 3 visual pairings within the winning angle
- **Sample size target:** ~150 conversions per variant
- **Stop-loss rule:** same as Phase 1

**Phase 3 — Headline-vs-CTA Test (within winning angle + creative):**
- Test 3 headline variants × 2 CTA variants
- Run only after Phase 2 winner is conclusive

---

### AI-Assist Layer

- *Google RSA underperforms (CTR < 2%):* Refresh headlines 1, 5, 12 with the verbatim VoC phrase "the seam between Salesforce and everything else" — proven 6.2× engagement on the source LinkedIn organic post
- *Meta carousel CTR < 1.1%:* Re-cut card 1 with a static screenshot of the Salesforce report (rather than the brand-template chart) — proof-first variant
- *LinkedIn CPL > $240 (current baseline):* Tighten the role-targeting from "Series B+ RevOps" to "Head of RevOps + Director of RevOps at 100–500 FTE SaaS"
- *Conversation Ad open rate < 25%:* Refresh opener to lead with the ScaleHQ outcome rather than the QBR question

---

### Confidence

`high` — all nine required inputs present, persona named, voice preamble applied, verbatim VoC source available, compliance check completed, message-match validated against landing page audit, A/B testing plan with named sample-size logic.

---

### Refresh Date

- Re-rotate paid social variants every 14–28 days (creative fatigue)
- Refresh Google RSA every 30–45 days
- Re-validate compliance + claim language at next legal review (quarterly)
- Re-validate voice preamble at the next Brand Voice Style Guide Generator refresh
