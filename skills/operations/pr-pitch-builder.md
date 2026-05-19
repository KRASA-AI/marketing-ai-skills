---
name: "PR Pitch & Journalist Outreach Builder"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~2 hrs/pitch cycle"
version: 2.0
last_eval_score: null
---

# 📰 PR Pitch & Journalist Outreach Builder

## Purpose

Turn a story, data drop, product milestone, or executive point of view into a targeted pitch package: a shortlist of relevant journalists, a three-sentence personalized pitch per journalist, a press-release or data-backgrounder draft, and a measurement frame. Built for marketers who own earned-media outcomes but do not work inside a dedicated PR agency workflow.

The 2026 shift is away from volume-blast outreach and toward beat-matched, high-specificity pitching that earns a reply. This skill enforces that discipline, and adds an AI-citation lift measurement loop: earned coverage in 2026 is no longer measured only in impressions — it is measured in whether the named entity appears in AI-engine answers the week after coverage runs (which Conductor's 2026 data shows is 2.4× more likely when the cited source is fresh).

## When to Use

Use this skill when there is a genuinely newsworthy moment (product launch, funding, first-party research, customer milestone, executive commentary on a breaking story) and the team wants coverage beyond owned channels. Use it again on quarterly rounds of proactive "story-mining" — surfacing the three or four angles inside a business that a journalist would actually find interesting. Use it reactively when the AI Search Visibility Audit flags a low citation-share cluster — earned coverage is the external-credibility lever for citation-share gaps.

Do not use for contributed articles or thought-leadership byline placement — that is a different workflow with longer lead times and different editorial contacts. Do not use it for SEO-link-building outreach — that is a separate workflow with different success criteria and different deliverability rules.

## Minimum Viable Input

If the user provides only the three fields below, proceed immediately and tag every assumption `[ASSUMED]` or `[INFERRED]`:

1. **The news or angle** — One paragraph describing what is genuinely new, surprising, or timely
2. **Spokesperson** — Name + title of who is available for an interview (one is enough)
3. **One proof point** — A specific number, customer name, or data point that backs the angle (a screenshot link or single sentence is sufficient)

When running in MVI mode: infer target outlets from the angle's category; assume no embargo and no prior coverage history; generate a tier-1 list of 6 named journalists (instead of the full 8–20 tier-1/2/3 set); skip the data sheet (use a single-paragraph proof block); compress the 10-day sequence into a 5-day default; flag at the bottom the top 2 inputs that would most improve pitch performance if the user can supply them (typically: prior coverage history + data sheet with methodology).

MVI mode produces a sendable pitch package in ~30 minutes vs. ~2 hours for the full workflow. The MVI output is sufficient for an opportunistic news-of-the-day pitch; it is not sufficient for a major launch announcement, a research-paper drop, or a funding round.

## Full Required Input

Provide the following for the highest-fidelity pitch package:

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
- If `outputs/ai-visibility/` exists, check whether this angle maps to a low citation-share cluster — that should sharpen the target outlet selection

**Process:**

1. **Stress-test the angle.** In three sentences, state: (a) what is new, (b) why it matters to a reader right now (not to the company), and (c) who would care first. If the angle fails any of these, flag it and propose a sharper framing before producing the pitch package. Newsworthiness is filtered at this step, not after the pitch is drafted.

2. **Build the target list.** Produce a table of 8–20 journalists (6 in MVI mode) with these columns:
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

6. **Plan the sequence.** Build a 10-day outreach plan (5-day in MVI mode):
   - Day 0 — exclusive offered to the single best tier-1 fit (if exclusivity is available)
   - Day 2 — broad tier-1 send if exclusive was declined, or simultaneous if not
   - Day 4 — one-touch, non-apologetic follow-up to non-responders ("Any interest before I take this broader?")
   - Day 7 — tier-2 send with a slightly reframed hook
   - Day 10 — broad-reach tier-3 plus influencer/creator amplification of earned pieces

7. **Set a measurement frame.** Report on: pitches sent, open rate (if tracked), reply rate, meeting/interview booked rate, coverage landed, tier of coverage, inbound link quality, **AI-engine citation lift for the company name in the week after coverage** (re-query the top 5 AI engines for the angle's keyword cluster and compare to a pre-coverage baseline), and **branded-search trend in the 14 days after coverage**. Call out that reply rate is the leading indicator; coverage is mid-stream; AI-engine citation lift and branded-search are the pipeline-relevant lagging indicators.

**Output requirements:**
- Angle stress-test (3 sentences + any reframing)
- Target journalist table (8–20 rows, or 6 in MVI mode)
- Three-sentence pitches for tier-1 and tier-2 targets
- Supporting backgrounder + data sheet + approved quotes
- 10-day sequence plan (5-day in MVI mode)
- Measurement frame including AI-citation lift loop
- Assumptions, gaps, and compliance flags
- Saved to `outputs/pr/` if the user confirms

## Calibration Notes

- **Reply rates are declining year over year.** Treat a 5–10% reply rate on a well-targeted list as a good result; 15%+ is exceptional and usually signals a genuinely strong angle rather than genius prose. A 25%+ reply rate is implausible and usually a sign the list is over-curated to friendlies who would reply regardless.
- **"Beat relevance" beats "big list."** Ten specific-fit journalists will earn more coverage than 200 generic ones, and the bad list actively damages future deliverability and reputation with reporters. The mid-2020s "spray and pray" model is now a deliverability anti-pattern.
- **Never fabricate journalist interests or paraphrase a recent piece without having read it.** An inaccurate "I loved your piece on X" ends the relationship faster than no pitch at all. Hallucinated article references are the single most damaging failure mode of an AI-assisted PR workflow.
- **Avoid adjective-heavy quotes** ("revolutionary," "game-changing"). Journalists almost always cut them; supply factual quotes that carry a headline if pulled alone.
- **Embargo breaks are survivable for the journalist; your next pitch may not be.** Only use embargoes when you actually have something worth embargoing (proprietary data, real news, or a coordinated multi-outlet drop). Manufacturing embargoes for a routine product update destroys credibility for future real embargoes.
- **Do not auto-send AI-generated pitches without human review.** The hallucinated-recent-piece risk is the dealbreaker; a single fabricated article reference can blacklist a sender from a beat for years.
- **The angle stress-test is the most-skipped step and the highest-leverage one.** Half of low-reply-rate pitch cycles trace back to an angle that failed (b) — "why it matters to a reader right now" — at the stress-test gate, but the team skipped the gate and went straight to drafting. Hold the gate.
- **Tier 1 pitch personalization is not optional.** A tier-1 journalist gets a hand-personalized pitch; a tier-2 gets a templated-with-named-detail pitch; a tier-3 gets a structured pitch with the angle and data. Inverting this is the most common reason a generally-strong list underperforms.
- **AI-engine citation lift is now a load-bearing PR metric.** Earned coverage that names the company or product in a fresh article makes that source 2.4× more likely to be cited by AI engines (Conductor 2026 freshness data). Re-query the top 5 engines for the angle's keyword cluster in the 7–14 days after coverage; the citation-share delta is the pipeline-relevant lagging indicator.
- **Branded-search lift is the second pipeline indicator.** Earned coverage that triggers branded-search lookups shows up in Google Search Console / Bing branded-query trend 1–14 days post-coverage. Pair this with AI-engine citation lift for a defensible attribution narrative.
- **Newsroom-to-newsletter substack handoff is now standard.** Many top-tier B2B journalists run a Substack newsletter alongside their staff role. Pitch the staff role; if rejected, the Substack is a credible second-touch with a different editorial threshold.
- **Day-of-week and time-of-day matter less than freshness.** Send when the angle is freshest, not when "Tuesday 10am" rules say. Stale-by-six-hours angles outperform fresh-by-one-hour angles delivered "at the right time."
- **Exclusive offers should be measured in hours, not days.** A 4–24-hour exclusive window respects the journalist's deadline pressure and reduces the risk of leaks; a 48–72-hour exclusive often loses the news cycle.
- **Internal sign-off latency kills more pitches than external rejection.** Pre-clear quotes, statistics, and approved messaging *before* the angle is pitchable, not after a journalist replies asking for them. The "we need legal to approve" delay between reply and follow-up is the most common reason booked interviews evaporate.
- **One-touch follow-up beats two-touch.** A single, non-apologetic follow-up at Day 4 outperforms a Day 4 + Day 8 double-tap; the second touch is read as harassment and damages future deliverability.

## Anti-Patterns to Avoid

- **Pitches that start "I hope this finds you well"** — journalists delete these unread
- **Attaching the press release to the first pitch** — the first email should offer the data sheet or an interview, not push the polished release at a cold contact
- **Three-paragraph openers about the company before the angle** — the angle goes in sentence 2 at latest
- **"Wondering if you'd be interested in…" endings** — defer the ask instead of naming it; specify the ask (interview / data / exclusive / briefing) and pick exactly one
- **Re-sending the same pitch verbatim to a different outlet with only the name changed** — journalists notice and share examples publicly; the deliverability damage is permanent
- **Treating PR coverage as the end metric** — coverage is mid-stream; AI-engine citation lift and branded-search are the pipeline-relevant lagging indicators
- **Pitching tier-1 outlets first with a half-developed angle** — the angle dies at the first tier-1 rejection; develop and stress-test before the highest-leverage send
- **Manufacturing exclusivity for routine news** — burns the embargo norm for future real embargoes
- **Auto-sending AI-generated pitches without human review of the recent-piece reference** — the hallucinated-article-reference risk is the dealbreaker for AI-assisted PR workflows
- **Following up more than once on a single pitch** — a single Day-4 follow-up is the ceiling; the second touch is read as harassment
- **Pitching the news without an AI-citation lift measurement plan** — the lift is the modern pipeline-relevant indicator and skipping it loses the strongest 2026 ROI narrative
- **Pitching without confirming the spokesperson's interview window** — booking an interview the spokesperson can't attend is a relationship-ender that takes 12+ months to recover

## Integration Notes

- **Pair with Competitive Analysis Brief** to identify narrative territory where a pitch can claim novel ground; the brief's "language signatures" cell highlights phrase moats competitors own that the pitch should avoid or reframe.
- **Pair with Brand Voice Guide Generator** so spokesperson quotes sound like the brand and not like the AI draft.
- **Pair with AI Search Visibility Audit** — low citation-share clusters from the audit map directly to PR pitch angles; an audit-driven PR pitch is the structural answer to a citation-share gap.
- **Pair with Cross-Channel Attribution Analyzer** — earned media lift is an incrementality test; the analyzer closes the loop by measuring branded-search and direct-traffic changes post-coverage.
- **Pair with Topic Cluster Planner** — earned coverage that names an entity or concept is a strong signal to own that cluster on the owned site; high-performing angles feed back as cluster pillar topics.
- **Pair with Persona & ICP Builder** — pitch outlet selection is downstream of which persona segment the coverage should reach; the persona roster names which trade press matters.
- **Pair with Campaign Performance Narrator** — PR cycles produce earned-media metrics that belong in the executive narrative; the narrator skill aggregates pitch outcomes alongside paid and owned channel metrics.
- **Pair with Brand Safety & Crisis Response Planner** — if the angle is reactive to a sensitive event, route through the crisis planner's holding-statement frame first to ensure spokesperson availability and approved messaging are pre-cleared.
- **Pair with Creative Brief Generator** — major launch announcements share inputs with creative briefs; the brief and the pitch package should share the same proof points and spokesperson quotes.
- **Pair with Multi-Channel Repurposer** — earned coverage is a content asset; the repurposer skill turns landed coverage into owned-channel posts (LinkedIn, X, newsletter, internal narrative).

## Example Output

### Threadline RevOps Cycle Time Benchmark — Q2 2026 Pitch Package (excerpt)

**Angle:** Threadline's Q1 2026 dataset (n=312 Series B–D SaaS companies) shows RevOps cycle time dropped 22% YoY for AI-instrumented companies and **rose** 8% for non-AI-instrumented companies. First multi-company AI-vs-non-AI benchmark published in 2026.

**Spokesperson:** Priya Shah, VP of Revenue Strategy, Threadline (ex-Clari, ex-Gong, 12 years RevOps). Available May 19–22 for 20-minute interviews.

**Embargo:** Tier-1 exclusive offered to MarTech Today for 24 hours (May 19 9am ET → May 20 9am ET).

#### Angle Stress-Test

**What's new:** First multi-company benchmark dataset that splits RevOps performance by AI instrumentation status — 30 percentage-point delta between AI-instrumented and non-AI-instrumented companies, opposing-direction movement (one down, one up), published with full methodology and segment cuts.

**Why it matters now:** H2 2026 budget planning is starting at Series B–D SaaS companies; CFOs are asking RevOps leaders to justify AI tool spend with measurable cycle-time impact. This dataset is the first defensible answer at the category level.

**Who cares first:** B2B RevOps trade press (MarTech Today, MarTech.org, Modern Sales Pros), the Pavilion + GTM Partners analyst circuit, sales-tech newsletter operators (Sales Hacker, Sales Engagement Weekly, RevOps Reviewed), and the CFO trade press (CFO Dive, CFO Brew).

#### Target Journalist Table (excerpt — top 5 shown)

| # | Name / Outlet | Beat | Most recent piece (1 sentence) | Why this angle fits | Tier | Contact / timing |
|---|---|---|---|---|---|---|
| 1 | Jordan Ellis / MarTech Today | RevOps + sales tech | "Why RevOps cycle time matters more than rep ramp" (Apr 28, 2026) — argued the field lacks benchmark data | Direct answer to the gap Jordan flagged in the April piece — first 2026 dataset with the cut they asked for | 1 | Email (replies within 4h); send Tues 9am ET |
| 2 | Sara Okada / MarTech.org | Marketing-and-sales platform analysis | "The state of sales-tech consolidation in 2026" (May 2, 2026) — referenced "no industry-level data on AI ROI yet" | Provides the AI-ROI data point Sara called out as missing two weeks ago | 1 | Email (replies within 24h); send Wed 10am ET |
| 3 | Sam Bahnsen / Modern Sales Pros newsletter | RevOps practitioner trends | "What's actually working in 2026 RevOps stacks" (May 5, 2026) — surveyed 47 ops leaders | Adds n=312 quantitative depth to Sam's qualitative survey; possible co-byline framing | 1 | DM via newsletter; send Mon 8am ET |
| 4 | Maya Patel / CFO Dive | CFO budget + spend analysis | "How CFOs are scoring AI tool ROI in 2026" (May 12, 2026) — argued AI spend justification needs cycle-time data | Direct match — the cycle-time data this piece said CFOs need | 1 | Email; send Tues 9am ET |
| 5 | Tom Reynolds / Sales Hacker | Sales tech for B2B SaaS | "Cycle time as the new pipeline metric" (Apr 14, 2026) | Beat-fit; tier-2 because Tom's newsletter has lower deliverability than MarTech / MarTech.org | 2 | Email; send Thu 10am ET |

#### Sample Tier-1 Pitch

**To:** Jordan Ellis, MarTech Today
**Subject:** RevOps cycle time dropped 22% for AI-instrumented Series B–D SaaS — first 2026 dataset, n=312

Hi Jordan — your April 28 piece on RevOps cycle time flagged that the field lacks multi-company benchmark data, especially with an AI cut. We just finished compiling ours: 312 Series B–D SaaS companies, Q1 2025 vs. Q1 2026, with a clean AI-instrumented vs. non-AI-instrumented split.

The headline: cycle time dropped 22% YoY for AI-instrumented companies and **rose** 8% for non-AI-instrumented ones — a 30-point delta with full methodology, segment cuts by ARR band, and named (anonymized) cohort composition.

I'd like to offer you a 24-hour exclusive starting Tuesday May 19 9am ET. Priya Shah (VP Revenue Strategy, ex-Clari) is open for a 20-minute call this week. Want the methodology + dataset preview?

— [Sender name, Threadline Comms]

#### Backgrounder (1-page mini-release excerpt)

**HEADLINE:** RevOps cycle time dropped 22% YoY for AI-instrumented Series B–D SaaS companies — and rose 8% for non-AI-instrumented peers — per Threadline's Q1 2026 RevOps Cycle Time Benchmark (n=312)

**DATELINE:** SAN FRANCISCO — May 19, 2026

**LEAD:** Threadline today released the first multi-company benchmark dataset to segment RevOps cycle-time performance by AI instrumentation status. The Q1 2026 RevOps Cycle Time Benchmark, drawn from 312 Series B–D SaaS companies across Q1 2025 and Q1 2026, finds that AI-instrumented teams cut cycle time by 22% year-over-year while non-AI-instrumented peers added 8%.

[2–3 supporting paragraphs with named methodology, segment cuts, and Priya Shah quotes]

**BOILERPLATE:** [Standard Threadline boilerplate from `config.yml`]

**MEDIA CONTACT:** [From `config.yml`]

#### Data Sheet (excerpt — 5 of 8 facts)

| # | Fact | Source | Collection method |
|---|---|---|---|
| 1 | n=312 Series B–D SaaS companies | Threadline 2026 RevOps Cycle Time Benchmark | Voluntary cohort with consent + anonymization; ARR-band balanced |
| 2 | Cycle time dropped 22% YoY for AI-instrumented cohort | Q1 2025 vs. Q1 2026 cycle-time medians, AI-instrumented subset (n=178) | Self-reported instrumentation status verified against tool stack audit |
| 3 | Cycle time rose 8% YoY for non-AI-instrumented cohort | Q1 2025 vs. Q1 2026 cycle-time medians, non-AI-instrumented subset (n=134) | Same methodology |
| 4 | 30-percentage-point delta is consistent across ARR bands $5M–$50M | Segment cut by ARR band | Sub-cohort medians |
| 5 | Methodology: "cycle time" = days from MQL to closed-won | Threadline benchmark definition | Standardized across all 312 cohort companies |

#### Approved Quotes (excerpt — 2 of 3 shown)

> "The 22-percent drop isn't surprising — what's surprising is the opposite-direction movement on the non-AI-instrumented side. RevOps teams that didn't adopt AI tooling in 2025 are now measurably falling behind, not just standing still." — Priya Shah, VP Revenue Strategy, Threadline

> "Series B–D SaaS CFOs have been asking RevOps leaders to defend AI tool spend with cycle-time data since Q4 2025. This is the first dataset that lets them have that conversation at the category level instead of the anecdote level." — Priya Shah

#### 10-Day Sequence

- **Day 0 (May 19, 9am ET):** Tier-1 exclusive sent to Jordan Ellis / MarTech Today
- **Day 1 (May 20, 9am ET):** Exclusive window closes; tier-1 broad send to Sara Okada (MarTech.org), Sam Bahnsen (Modern Sales Pros), Maya Patel (CFO Dive)
- **Day 4 (May 23):** Single-touch follow-up to non-responders; reframe with one new data point
- **Day 7 (May 26):** Tier-2 send to 8 named journalists; reframe headline to lead with the CFO/budget angle
- **Day 10 (May 29):** Tier-3 broad-reach send; activate creator/influencer amplification of any landed coverage; submit to Pavilion + GTM Partners analyst circuit

#### Measurement Frame

- **Leading indicator (Day 1–4):** Pitches sent (n), open rate (if tracked), reply rate (target 8–12%); interviews booked (target 3)
- **Mid-stream (Day 5–14):** Coverage landed (target 4 tier-1/2 placements); tier distribution; inbound link quality (Domain Rating, follow vs. nofollow)
- **Lagging — AI-engine citation lift (Day 7 + Day 14):** Re-query top 5 AI engines (ChatGPT, Perplexity, Gemini, AI Overviews, Claude) for keywords {"RevOps cycle time benchmark," "AI RevOps ROI," "Threadline RevOps benchmark"} and compare citation-share to pre-coverage baseline. Target: +12pp citation share on at least 3 of 5 engines.
- **Lagging — Branded-search lift (Day 7 + Day 14):** Threadline branded-query trend in Google Search Console + Bing. Target: +15% week-over-week.
- **Lagging — Pipeline assist (Day 30 + Day 60):** Direct-traffic uptick on Threadline benchmark page; first-touch and assisted MQL trend; named-account engagement on benchmark page (from intent platform)

#### Assumptions, Gaps, Compliance Flags

- `[ASSUMED]` Tier-1 exclusive to MarTech Today is the right pick — verify against the most recent Jordan Ellis coverage to ensure no near-identical angle in the prior 30 days
- `[ASSUMED]` Priya Shah's interview window (May 19–22) is confirmed in calendar; re-confirm before send
- **Gap:** No prior coverage history loaded — recommend pulling the last 90 days of Threadline coverage before send to avoid stale-hook reuse
- **Compliance flag:** Cohort anonymization disclosed in methodology; do not name customer companies unless explicit consent on file (check `config.yml` approved-customer-mentions list)
