---
name: "Creative Brief Generator"
category: operations
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~90 min/brief"
version: 2.0
last_eval_score: null
---

# 📝 Creative Brief Generator

## Purpose

Turn a rough campaign idea, product launch request, or Slack-message-level ask into a structured creative brief that designers, copywriters, agencies, and AI tools can all execute against — without a round of clarifying questions.

## When to Use

Use this skill at the kickoff of any new campaign, ad set, landing page, video, or content sprint where more than one person (or AI tool) will touch the work. It's especially valuable when the request came in informally ("we need something for the spring launch"), when a freelance or agency partner is involved, or when you're prompting AI for creative assets and want consistent output across variants.

## Required Input

Provide the following:

1. **Campaign objective** — What business outcome this work drives (signups, revenue, awareness, retention, launch announcement). Include target metric if known
2. **Audience** — Who the work is for. Reference an existing persona from `outputs/personas/` if available
3. **Product or offer** — What's being marketed, including key features, price, and any launch-window specifics
4. **Channel / format** — Where the output will live: paid social, email, landing page, OOH, video, influencer, etc. Include any spec constraints
5. **Deadline and budget** — When it needs to ship, and any budget or resourcing limits
6. **Mandatories and restrictions** — Required claims, compliance language, brand elements, competitor callouts to avoid, legal constraints

### Minimum Viable Input

If only fields 1, 2, and 4 are provided, the skill produces a `confidence: medium` brief with: an inferred single-minded proposition tagged `[ASSUMED]`, a "best-guess" deliverables list scoped to the named channel, an explicit `[CONFIRM]` block listing what the brief owner must validate before distribution (typically: launch window, budget cap, mandatory legal/compliance copy, named persona file), and three creative springboards labeled with the strategic angle they bet on. The AI-execution addendum is generated using `config.yml` voice defaults; the briefer is told which voice attributes to confirm before pasting into a tool.

## Instructions

You are a senior marketing strategist's AI assistant specializing in creative briefing. Your job is to translate messy input into a clean, execution-ready brief that reduces back-and-forth between strategy, creative, and AI tools.

**Before you start:**
- Load `config.yml` from the repo root for brand voice, core value props, and company context
- Load any existing persona files from `outputs/personas/` that match the audience
- Reference `knowledge-base/terminology/` for approved category language
- Flag any missing input as an assumption rather than stopping — the goal is a workable draft

**Process:**

1. **Extract and restate the single-minded proposition.** In one sentence: what the audience should think, feel, or do after encountering this work. This is the brief's north star. The single-minded proposition test: if a creative team came back with three ideas all serving the proposition, the strategist should say "yes, all three are on-strategy." If two of the three feel off-strategy, the proposition is too broad.

2. **Build the brief structure** with these required sections:
   - **Project name & one-line description**
   - **Business objective** (with measurable success metric — name the number, the source dashboard, and the comparison baseline)
   - **Audience snapshot** (who, the tension or job-to-be-done, current mindset, where they currently shortlist alternatives — including AI answer engines if relevant)
   - **Single-minded proposition** (the one thing — must pass the three-on-strategy-ideas test)
   - **Support points** (3–5 proof points that make the proposition believable — first-party data, named customer outcomes, third-party citations with dates)
   - **Tone and voice** (pulled from `config.yml` → `voice`, with 2–3 adjective descriptors and 1–2 named anti-examples)
   - **Deliverables** (list of every asset, with channel, format, dimensions/length, quantity, file-format expectation)
   - **Mandatories** (legal, brand, compliance requirements — quote the exact required language where applicable)
   - **Restrictions** (what the work must not do, claim, or imply — including competitor-naming policy and any banned phrases from the voice guide)
   - **Timeline** (milestones: kickoff, first round, revisions, final, launch — with named decision-maker per gate)
   - **Budget & resourcing** (if known — include AI-generation policy: which tools are sanctioned, which need disclosure, and which output requires human review before publication)
   - **Success measurement** (how you'll know the work worked — primary KPI, secondary KPIs, holdout or read-window where applicable)

3. **Add an AI-execution addendum.** A short block formatted for reuse as a preamble when prompting AI creative tools: voice descriptors, tone guardrails, mandatories, and restrictions — in the exact format the team's preferred tool expects (system prompt, image-gen style block, video-gen Shot Grammar, etc.). Include the named brand voice preamble file from the Brand Voice Style Guide Generator output, if one exists.

4. **Generate 3 "creative springboards."** Short directional concepts (1–2 sentences each) that satisfy the brief but take different strategic angles (e.g., empathy-first / proof-first / contrarian). These are starters for creative partners, not final ideas. Each springboard names the messaging angle it bets on so the creative team knows which lever to pull.

5. **Flag assumptions and gaps.** List anything you had to assume, and any missing input the brief owner should confirm before distribution. Use confidence tags on the brief itself: `confidence: high` if all six required inputs are present and the persona is named; `confidence: medium` if MVI mode applied; `confidence: low` if more than one mandatory or audience field is `[ASSUMED]`.

**Output requirements:**
- Creative brief in markdown, formatted for pasting into Notion, Google Docs, or agency briefing tools
- AI-execution addendum block ready to copy into prompts
- 3 creative springboards
- Assumptions & gaps section with confidence tag
- Saved to `outputs/briefs/` if the user confirms

## Calibration Notes

- **The single-minded proposition is the brief.** Everything else is scaffolding. If the SMP isn't sharp, the brief produces inconsistent creative no matter how detailed the deliverables list. Spend disproportionate effort here. Test it: can three different creative partners produce three on-strategy ideas from this SMP? If two come back off-strategy, the SMP is too broad.
- **AI-execution addendum is now a first-class deliverable.** In 2026, more than half of creative briefs will be partially executed by AI tools (image-gen, video-gen, copy-gen). The voice / mandatory / restriction block must be paste-ready into a system prompt or image-gen style block, not buried in prose. If the brief doesn't ship with a copy-paste preamble, AI execution silently drifts off-brief by week two.
- **Mandatories beat aspirations in the brief.** A creative team can interpret "professional but warm." A creative team cannot guess "must use the Q3 2026 corporate certification badge with full TM mark, never crop, minimum 24px height." Spell out the non-negotiables literally; let the aspirational tone live in the voice section.
- **Audience must include where they shortlist.** "Homeowners 35–55" is insufficient in 2026. Specify: where they currently search (Google, ChatGPT, Perplexity, AI Overviews, TikTok), what platforms they use to compare options (Capterra, G2, Reddit, AI engines), and which trust signals they actually weight (peer review, named credential, reviewer count above a threshold). The creative partner needs this to choose the right proof.
- **Three on-strategy springboards beat one perfect concept.** The brief owner doesn't pick the springboard — they confirm the brief is castable into multiple angles. A brief that produces only one viable creative direction is too narrow and will fail when one element of execution fails.
- **Budget and resourcing must include AI policy.** Specify which AI tools are sanctioned for which assets, whether output requires human review before publication, and any disclosure obligation (FTC AI-disclosure rules, agency contract clauses, platform-specific labels). Briefs that omit this surface conflict at publication, not at kickoff.
- **Refresh cadence.** Re-validate the brief if the launch date slips by more than 14 days, if the persona file is updated by the Persona & ICP Builder, or if a new compliance rule lands (FTC, platform policy, regulator update). A 6-week-old brief on a moving target is half-stale.
- **Success measurement names the dashboard.** "Improved engagement" is not a KPI. "Click-through rate above 1.2% on the demo-page sequence as measured in HubSpot Marketing Hub, against the trailing-90-day baseline of 0.8%, with a 10% holdout" is a KPI. The brief without a named source dashboard ends in argument, not measurement.
- **Banned phrases live with the voice section, not the brief root.** Pull from the Brand Voice Style Guide Generator output where one exists. Don't reinvent the banned-phrase list per brief — the voice guide is the source of truth.

## Anti-Patterns

- **The proposition-by-committee** — single-minded proposition reads like four propositions joined with "and." Violates the three-on-strategy-ideas test. Force one idea, one verb, one outcome.
- **Aspirational mandatories** — "Should feel premium" listed under Mandatories. Mandatories are non-negotiable specs (logo size, claim language, legal copy). Tone goes in the voice section.
- **The TBD KPI** — Success measurement reads "we'll track engagement and conversions." No named metric, no baseline, no source. Brief is unmeasurable on day one.
- **Persona = "marketing leaders"** — Audience snapshot is a job title with no tension, no shortlisting behavior, no buying-committee context. Pull a real persona from `outputs/personas/` or generate one with the Persona & ICP Builder before continuing.
- **No AI-execution addendum** — Brief ships in 2026 without a copy-paste preamble for AI tools. Creative drift starts week two.
- **The everything deliverable** — Deliverables section lists "social assets, email, landing page, video, OOH" with no specs, no quantity, no formats. Deliverables list is a checklist of files, not a wish list of channels.
- **Budget = "TBD"** — Resourcing decisions deferred. Brief gets distributed, partners scope to the maximum, conflict at invoice. Either name a range or name the budget approval gate.
- **Banned phrases reinvented per brief** — Voice section bans "leverage, synergy, best-in-class" but doesn't reference the brand voice guide. New brief next month bans different words. Brand voice drifts because of inconsistent briefs.

## Integration Notes

- **Persona & ICP Builder** (`outputs/personas/`) — Audience snapshot pulls verbatim from the persona's tension, job-to-be-done, and shortlisting-behavior sections. Reference the persona by file name in the brief's frontmatter so creative partners can read the source.
- **Brand Voice Style Guide Generator** — The voice section, banned-phrase list, and AI prompt preamble all flow from the voice guide. Never re-author voice rules in a brief; cite the voice guide version and copy the preamble verbatim.
- **Customer Review & Insight Miner** — Support points (proof points) and audience tension language pull from the verbatim-quote bank and buyer-language dictionary. Customer language beats marketing-team paraphrase 9 times out of 10.
- **Competitive Analysis Brief** (`outputs/competitive-analysis/`) — Restrictions section ("competitor callouts to avoid") and the contrarian springboard option pull from the competitive analysis. If no recent analysis exists, flag it as a gap before distributing.
- **Creator Brief Builder** — When a creator/influencer asset is in the deliverables list, the Creator Brief is the downstream document; this brief produces the input. Pass the SMP, voice block, and mandatories directly.
- **Campaign Performance Narrator** — Success measurement frame from this brief is what the Performance Narrator reports against. Define the comparison baseline and holdout up-front; otherwise the post-campaign narrative defaults to anecdote.
- **Multi-Channel Content Repurposer** — When deliverables span 4+ channels, the Repurposer is the execution document; this brief sets the priority message and voice. Note in deliverables which channel is the source-of-truth long-form and which are repurposes.
- **Synthetic Persona Simulator** — Springboards can be pre-tested against a simulator persona before creative partners spend hours. Useful especially for high-stakes launches where springboard selection matters.
- **AEO Content Optimizer / Blog Post Outliner** — When a blog post or landing page is on the deliverables list, the AEO Optimizer (existing pages) or Blog Post Outliner (new posts) is the downstream skill. The brief's SMP and mandatories become inputs to those skills' direct-answer block and entity definitions.

## Example Output

### Input Recap

- **Campaign objective:** Drive a 25% lift in qualified demo bookings in Q3 2026 from the Series-B-and-up RevOps segment, measured in HubSpot vs. trailing-90-day baseline of 38 demos / week
- **Audience:** Persona "Priya, the Pragmatic Head of RevOps" (`outputs/personas/priya-revops.md`)
- **Product:** Threadline RevOps Diagnostic — a free 30-min ops cycle time audit (lead-magnet → demo conversion path)
- **Channels:** Paid LinkedIn (Sponsored Content + Conversation Ads), email (3-touch sequence), landing page, retargeting display
- **Deadline:** Launch Aug 4, 2026; mid-campaign read Aug 25; close-out Sept 16
- **Budget:** $48K paid media + $12K creative production
- **Mandatories:** "Threadline" with TM on first use; FTC AI-disclosure footnote on any AI-generated visual; SOC 2 badge required on any landing page; legal-approved version of the "3-week leading indicator" claim only
- **Restrictions:** No competitor naming (Salesforce, HubSpot, Gong) per legal; no urgency-only framing; no AI-stock illustrations of "robotic" workers
- **Confidence:** `high`

---

### Project Name

**Threadline Q3 RevOps Diagnostic Launch — "The 3-Week Leading Indicator"**

One-line: Drive 25% demo lift among Series B+ RevOps leaders by promoting a free ops cycle time audit, anchored to the empirical claim that ops cycle time leads revenue plan attainment by 3 weeks.

---

### Business Objective

| Field | Value |
|-------|-------|
| Primary KPI | Qualified demo bookings (Priya-tier ICP) |
| Source dashboard | HubSpot Marketing Hub → "Demo Funnel — Q3 2026" |
| Baseline | 38 demos / week (trailing-90-day median, May–Jul 2026) |
| Target | 48 demos / week sustained for the final 3 weeks of Q3 (+25%) |
| Holdout | 10% of paid LinkedIn audience held out for 6 weeks; measure incrementality |
| Read window | Aug 25 mid-campaign read; Sept 16 close-out |

---

### Audience Snapshot

**Who:** Priya — Head of RevOps at a Series B–C SaaS company, 100–500 FTE, 18 months in role, owns the metric that the CRO uses for the QBR. (Source: `outputs/personas/priya-revops.md`)

**Tension / job-to-be-done:** She's about to be asked at the QBR why revenue plan attainment slipped, and she suspects ops cycle time is the leading indicator — but doesn't have a clean way to measure it. Internal political pressure to defend the RevOps team's ROI without admitting the broken-handoff pattern.

**Current mindset:** Skeptical of vendor pitches; trusts peer benchmarks (RevOps Co-op community, Pavilion); reads Reforge essays; comparison-shops on G2 and through LinkedIn DMs to peers.

**Where she shortlists:** ChatGPT and Perplexity for category research; Reddit r/RevOps for peer credibility; G2 for comparison; LinkedIn DM peers ("anyone using X for cycle time?") as the final filter before booking a demo.

---

### Single-Minded Proposition

**"Ops cycle time is the leading indicator your CRO will quote at the next QBR — get the audit before they ask the question."**

(Three on-strategy ideas that pass the test: an empathy concept ("you have 2 weeks to find this number"), a proof concept ("the 3-week lead time is real, here's the math"), a contrarian concept ("RevOps measures the wrong thing and ScaleHQ proved it") — all serve the SMP.)

---

### Support Points

1. Threadline 2026 RevOps benchmark (n=47 customer cohort, FY26): ops cycle time leads revenue plan attainment by 21 days
2. ScaleHQ named case study: cut ops cycle time 31% in 90 days, hit revenue plan attainment in next two consecutive quarters
3. Forrester 2026 RevOps benchmark (analyst report): ops cycle time named as top-3 RevOps health metric for Series B+
4. RevOps Co-op community thread (Apr 2026, 142 comments): organic peer validation — RevOps leaders independently surfacing ops cycle time as the missing metric
5. Threadline diagnostic completion data: 80% of 30-min audits identify a measurable handoff loss; average $340K annualized revenue exposure surfaced

---

### Tone and Voice

- **Voice attributes (3):** Plainspoken, specific over clever, engineer-respectful (Threadline voice guide v2.0)
- **Anti-examples:** Avoid "leverage / synergy / unlock," avoid "revolutionize / transform," avoid the "AI-powered" framing applied to non-AI features
- **Voice preamble file:** `outputs/voice/threadline-voice-preamble-v2.0.md` — paste verbatim into AI tools

---

### Deliverables

| # | Asset | Channel | Spec | Quantity |
|---|-------|---------|------|----------|
| 1 | Sponsored Content posts | LinkedIn | 1200×627 image + 150-word post + 70-char headline | 4 variants |
| 2 | Conversation Ad sequences | LinkedIn | 4-message branched flow + 3 CTAs | 2 variants |
| 3 | Demo landing page | Web | 1 hero + 5 sections + FAQ block + CTA | 1 page |
| 4 | Email nurture | HubSpot | 3-touch sequence (Day 0/3/7) | 1 sequence |
| 5 | Retargeting display | Display | 300×250, 728×90, 160×600 | 3 sizes × 2 variants |
| 6 | Diagnostic worksheet PDF | Asset | 8-page guided worksheet, on-brand template | 1 PDF |
| 7 | Sales enablement one-pager | Internal | 1-page printable + 1-page slide | 1 set |

**File format expectations:** Image = JPG sRGB ≤ 5MB; PDF = print-ready 300dpi; copy = Google Doc with version history.

---

### Mandatories

- "Threadline" with ™ symbol on first use, every asset
- FTC AI-disclosure footnote on any visual generated wholly or in part by AI image-gen tools
- SOC 2 badge required on the demo landing page (above the fold)
- Only the legal-approved phrasing of the 3-week leading-indicator claim is permitted: "Ops cycle time leads revenue plan attainment by ~3 weeks in B2B SaaS at 100–500 FTE (Threadline 2026 benchmark, n=47 customer cohort)"
- Customer logos require permission-on-file (check Salesforce → Marketing → "Logo Use Permissions") before deployment

---

### Restrictions

- No competitor naming (Salesforce, HubSpot, Gong) per legal
- No urgency-only framing ("Only 3 spots left!" — banned)
- No AI-stock illustrations depicting "robotic" workers, AI-generated faces of fictional customers, or hands-typing-on-keyboard clichés
- No comparison claims unsupported by named source + date
- No "leverage / synergy / unlock / best-in-class / revolutionize" (per voice guide v2.0)

---

### Timeline

| Gate | Date | Decision-maker |
|------|------|----------------|
| Brief sign-off | Jul 7 | Maya Chen (Head of Marketing) |
| Creative round 1 | Jul 17 | Maya + creative agency |
| Round 1 review | Jul 22 | Maya + Priya-internal-mirror persona-test |
| Creative round 2 | Jul 28 | Maya |
| Final approval | Jul 31 | Maya + Legal (mandatory copy review) |
| Launch | Aug 4 | — |
| Mid-campaign read | Aug 25 | Maya + RevOps team |
| Close-out report | Sept 16 | Maya + CRO QBR |

---

### Budget & Resourcing

- **Paid media:** $48K (LinkedIn $36K + Display retargeting $12K)
- **Creative production:** $12K (agency partner — Studio Verb)
- **AI policy:** Image-gen sanctioned for ideation only; final assets must be photographed or human-illustrated. Copy-gen sanctioned for first drafts; all body copy passes through human edit. Video-gen not sanctioned this campaign. FTC AI-disclosure required on any partially AI-generated visual.

---

### Success Measurement

- **Primary:** Qualified demo bookings — 25% lift over 38/week baseline, sustained 3 weeks (HubSpot Marketing Hub)
- **Secondary:** Landing page conversion rate (target ≥ 4.2% — current 3.1%); email click-through (target ≥ 3.8% — current 2.9%); LinkedIn CPL (target ≤ $190 — current $240)
- **Holdout / incrementality:** 10% paid LinkedIn audience held out 6 weeks
- **Anti-vanity guard:** Open rate is not a primary KPI in this campaign (MPP-inflated, not actionable)

---

### AI-Execution Addendum (paste-ready preamble)

> **Voice:** Plainspoken, specific over clever, engineer-respectful. Never use leverage, synergy, unlock, revolutionize, best-in-class, or AI-powered (when not literal). Prefer concrete nouns ("ops cycle time," "Series B SaaS," "SFDC handoff") over abstract phrases ("digital transformation," "growth journey").
>
> **Tone:** Calm authority, not urgency. Peer-to-peer with a senior RevOps leader, not vendor-to-prospect. Honest about limitations.
>
> **Mandatories:** Always Threadline™ on first use. Cite "Threadline 2026 benchmark, n=47 customer cohort" when using the 3-week claim. SOC 2 badge above the fold on the landing page.
>
> **Restrictions:** No competitor naming. No urgency framing. No AI-generated faces of fictional customers. No "leverage / synergy" family of phrases.
>
> **Source:** `outputs/voice/threadline-voice-preamble-v2.0.md` v2.0 (Jul 2026 refresh)

---

### Creative Springboards

1. **The Calendar Page (empathy-first).** A simple, dated calendar page; the August row is highlighted; the headline reads "your CRO is asking about this in 14 days." The audit is positioned as the answer to the question Priya knows is coming. Bets on temporal-tension.

2. **The Dashboard Receipt (proof-first).** A stylized dashboard screenshot showing ops cycle time leading revenue plan attainment by 21 days at ScaleHQ; a small "n=47" footnote. Headline: "the metric that beat the forecast." Bets on first-party-data credibility.

3. **The Wrong Question (contrarian).** A list of "RevOps metrics that aren't predictive" (pipeline coverage, win rate, sales cycle length); each is crossed out. The single uncrossed line: ops cycle time. Headline: "everyone's measuring the wrong thing." Bets on contrarian-clarity. **Risk:** must be defensibly true; legal review of competitor-adjacent framing.

---

### Assumptions & Gaps

- **Confirmed:** persona file, mandatories language (legal-approved), budget, channel mix
- **Assumed:** Priya is the primary economic buyer for the diagnostic CTA (validate against current account data)
- **Gap:** No fresh competitive analysis since Q1 2026 — recommend running Competitive Analysis Brief before springboard 3 (contrarian framing) ships
- **Gap:** Creator Brief not yet built — if the campaign expands to LinkedIn creator-led posts, run Creator Brief Builder downstream

**Confidence:** `high` (all six required inputs present; persona named; mandatories quoted verbatim)

---

### Refresh Date

- Brief auto-refreshes if launch slips beyond Aug 18 (14-day rule)
- Voice preamble re-validated at the next Brand Voice Style Guide Generator refresh (Q4 2026)
- Persona file re-validated quarterly per Persona & ICP Builder cadence
