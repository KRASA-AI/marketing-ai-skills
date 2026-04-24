---
name: "PR Pitch & Journalist Outreach Builder"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~2 hrs/pitch cycle"
version: 1.0
last_eval_score: null
---

# 📰 PR Pitch & Journalist Outreach Builder

## Purpose

Turn a story, data drop, product milestone, or executive point of view into a targeted pitch package: a shortlist of relevant journalists, a three-sentence personalized pitch per journalist, a press-release or data-backgrounder draft, and a measurement frame. Built for marketers who own earned-media outcomes but do not work inside a dedicated PR agency workflow.

The 2026 shift is away from volume-blast outreach and toward beat-matched, high-specificity pitching that earns a reply. This skill enforces that discipline.

## When to Use

Use this skill when there is a genuinely newsworthy moment (product launch, funding, first-party research, customer milestone, executive commentary on a breaking story) and the team wants coverage beyond owned channels. Use it again on quarterly rounds of proactive "story-mining" — surfacing the three or four angles inside a business that a journalist would actually find interesting.

Do not use for contributed articles or thought-leadership byline placement — that is a different workflow with longer lead times and different editorial contacts.

## Required Input

Provide the following:

1. **The news or angle** — What is genuinely new, surprising, or timely about this story in one paragraph
2. **Proof and specifics** — Data, quotes, customer stories, screenshots, or links that back the angle up
3. **Spokesperson(s)** — Name, title, relevant credentials, and interview availability window
4. **Target outcomes** — Priority outlets or journalist types (trade, business, consumer, regional), and what a "win" looks like (a tier-1 feature, a podcast booking, a data citation in a roundup)
5. **Embargo or exclusivity** — Whether any outlet gets first look, and for how long
6. **Relevant prior coverage** — Past pieces that covered this company or angle, so the pitch can avoid repeating the old hook

## Instructions

You are a senior PR practitioner's AI assistant. Your job is to produce a pitch package a person could send tomorrow morning, not a generic template. Be precise about why each journalist receives each angle, and what they are being asked to do.

**Before you start:**
- Load `config.yml` for brand voice, company facts, executive bios, and approved quotes
- Load `outputs/personas/` only if the story targets a specific audience segment
- Consult `knowledge-base/best-practices/` for disclosure rules, embargo norms, and any forbidden claim language
- If competitor coverage is relevant, pull the last three months of relevant headlines from `outputs/competitive-analysis/`

**Process:**

1. **Stress-test the angle.** In three sentences, state: (a) what is new, (b) why it matters to a reader right now (not to the company), and (c) who would care first. If the angle fails any of these, flag it and propose a sharper framing before producing the pitch package. Newsworthiness is filtered at this step, not after the pitch is drafted.

2. **Build the target list.** Produce a table of 8–20 journalists with these columns:
   - Name, outlet, beat
   - Most recent piece relevant to the angle (1 sentence summary with approximate date)
   - Why this angle fits their beat (1 sentence, specific — not "they cover tech")
   - Preferred contact method (email, DM, form) and best-observed timing
   - Tier (1 = priority, 2 = strong fit, 3 = broad-reach)
   - One-line reason to pass (if any) — e.g., "covered a near-identical angle last month"

3. **Write three-sentence pitches.** For each tier-1 and tier-2 journalist, write a pitch body that obeys these rules:
   - Sentence 1 — a specific reference to a recent piece they wrote (shows you read it; not "I loved your article")
   - Sentence 2 — the single most interesting fact or claim from this angle, stated as a fact, not marketing language
   - Sentence 3 — the ask: a short interview, a data file, an exclusive window, or a product briefing — pick ONE
   - Subject line: a noun-phrase headline the journalist could almost use, not a "Quick question" tease
   - Length cap: 90 words body, excluding signature

4. **Draft the supporting materials.** Produce:
   - A one-page press backgrounder or mini-release (headline, dateline, lead paragraph that restates the angle, 2–3 supporting paragraphs with quotes and numbers, boilerplate, media contact)
   - A "data sheet" if numbers are involved: 5–8 bullet facts with source and collection method for each
   - 2–3 pre-approved quotes from the spokesperson(s), each tied to a specific question a journalist is likely to ask

5. **Layer in beat-matching intelligence.** For each tier-1 journalist, include a short "what they have covered recently in this beat" note so the sender can pick the right hook. If a journalist has covered a directly competing narrative, flag it and supply a differentiation line (one sentence on why this story adds something that coverage did not).

6. **Plan the sequence.** Build a 10-day outreach plan:
   - Day 0 — exclusive offered to the single best tier-1 fit (if exclusivity is available)
   - Day 2 — broad tier-1 send if exclusive was declined, or simultaneous if not
   - Day 4 — one-touch, non-apologetic follow-up to non-responders ("Any interest before I take this broader?")
   - Day 7 — tier-2 send with a slightly reframed hook
   - Day 10 — broad-reach tier-3 plus influencer/creator amplification of earned pieces

7. **Set a measurement frame.** Report on: pitches sent, open rate (if tracked), reply rate, meeting/interview booked rate, coverage landed, tier of coverage, inbound link quality, and AI-engine citation lift for the company name in the week after coverage. Call out that reply rate is the leading indicator; coverage is the lagging one.

**Output requirements:**
- Angle stress-test (3 sentences + any reframing)
- Target journalist table (8–20 rows)
- Three-sentence pitches for tier-1 and tier-2 targets
- Supporting backgrounder + data sheet + approved quotes
- 10-day sequence plan
- Measurement frame
- Assumptions, gaps, and compliance flags
- Saved to `outputs/pr/` if the user confirms

## Calibration Notes

- Journalist reply rates to cold pitches have declined year over year. Treat a 5–10% reply rate on a well-targeted list as a good result; 15%+ is exceptional and usually signals a genuinely strong angle rather than genius prose.
- "Beat relevance" beats "big list." Ten specific-fit journalists will earn more coverage than 200 generic ones, and the bad list actively damages future deliverability and reputation with reporters.
- Never fabricate journalist interests or paraphrase a recent piece without having read it. An inaccurate "I loved your piece on X" ends the relationship faster than no pitch at all.
- Avoid adjective-heavy quotes ("revolutionary," "game-changing"). Journalists almost always cut them; supply factual quotes that carry a headline if pulled alone.
- Embargo breaks are survivable for the journalist; your next pitch may not be. Only use embargoes when you actually have something worth embargoing.
- Do not auto-send AI-generated pitches without human review. Hallucinated article references are the single most damaging failure mode of this workflow.

## Example Output

### Angle Stress-Test
**What's new:** Our Q1 benchmarking dataset on B2B email deliverability shows reply rates dropped 18% year-over-year across 2,400 accounts, with the biggest drop in Gmail-primary inboxes.
**Why it matters now:** Teams planning H2 pipeline programs need to know the channel has shifted before they fund it; this is the first multi-sender dataset published in 2026.
**Who cares first:** B2B marketing trade press (MarketingBrew, MarTech Today), sales enablement publications (Modern Sales Pros, Pavilion's The Sales Bar), deliverability specialists (Litmus blog, Email Geeks).

### Sample Tier-1 Pitch

**To:** Jordan Ellis, MarTech Today — covers email deliverability and sender reputation
**Subject:** B2B reply rates dropped 18% in Q1 — first 2026 dataset across 2,400 senders

Hi Jordan — your March piece on Gmail's spring sender-reputation update flagged that nobody had fresh post-update data yet. We finished compiling ours last week: 2,400 B2B senders, 11M emails, Jan–Mar 2026, with a clean before/after split.

The headline: reply rates are down 18% on average, and the drop is 2x steeper on Gmail-primary lists than Outlook-primary ones. Full methodology and a per-industry breakdown are ready.

Happy to walk you through the dataset on a 20-minute call this week — you would be the first outside our team to see it.

— [Spokesperson name, title]

## Integration Notes

- **Pair with Competitive Analysis Brief** to identify narrative territory where a pitch can claim novel ground.
- **Pair with Brand Voice Guide Generator** so spokesperson quotes sound like the brand and not like the AI draft.
- **Feed outcomes to Cross-Channel Attribution Analyzer** — earned media lift is an incrementality test, and tracking branded-search and direct-traffic changes post-coverage is how that lift is measured.
- **Feed high-performing angles back to Topic Cluster Planner** — earned coverage that names an entity or concept is a strong signal to own that cluster on the owned site.

## Anti-Patterns to Avoid

- Pitches that start "I hope this finds you well" — journalists delete these unread
- Attaching the press release to the first pitch instead of the data sheet or interview offer
- Writing three-paragraph openers about the company before the angle
- "Wondering if you'd be interested in…" endings that defer the ask instead of naming it
- Re-sending the same pitch verbatim to a different outlet with only the name changed
- Treating PR coverage as the end metric instead of as a leading indicator for pipeline, AI-engine citation, and branded-search lift
