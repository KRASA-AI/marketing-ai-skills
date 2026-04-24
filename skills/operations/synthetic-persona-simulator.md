---
name: "Synthetic Persona Simulator"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~3 hrs/test cycle"
version: 2.0
last_eval_score: null
---

# 🧪 Synthetic Persona Simulator

## Purpose

Pressure-test marketing assets — landing pages, ad creative, emails, positioning statements, pricing pages, sales decks — against AI-generated audience personas that simulate realistic objections, reactions, and purchase behavior before you spend budget on live testing. Produce a per-segment scorecard, a prioritized objection list, a set of concrete copy/creative rewrites, and a ship / iterate / rework verdict.

The 2026 shift this skill operationalizes: synthetic audiences are now a credible pre-launch screen for directional messaging choices, but only when they are grounded in real segment evidence and read as a *probability distribution over realistic reactions* — not as a single "typical buyer."

## When to Use

Use this skill when you need directional audience feedback but can't afford a focus group, survey panel, or full A/B test cycle. It's especially valuable pre-launch, when iterating on messaging, when entering a new segment without historical customer data, when you need a privacy-safe alternative to scraping real user behavior, or when stakeholders are debating a creative choice in a circle. Run it as an early screen before committing spend, never as a replacement for post-launch measurement.

Do not use it to forecast conversion rates, to score small copy tweaks (headline commas, button colors), or to justify a ship decision that already had real-user validation fail — synthetic personas are biased toward politeness and plausibility.

## Required Input

Provide the following:

1. **Asset under test** — Landing page copy, ad creative (with transcript if video), email, headline variants, pricing page, or positioning statement. Paste text and/or link. For visual assets, describe layout, imagery, and CTA.
2. **Target segments** — 2–5 audience descriptions. Any combination of demographics, firmographics (for B2B), psychographics, job-to-be-done, current tool stack, buying stage. If `outputs/personas/` exists, reference persona IDs by name and the skill will use them as the source of truth.
3. **Decision context** — Price point, purchase trigger, alternatives they'd consider, typical decision timeline, who else is in the buying committee (for B2B), risk tolerance.
4. **Test objective** — What you want to learn: clarity, objection mapping, purchase intent, preference between variants, emotional resonance, credibility perception, or pricing acceptability.
5. **Known ground truth (optional)** — Any real research findings, prior test results, or known objections the team has already heard. This makes the simulation materially more useful by grounding it against reality.
6. **Variants to compare (optional)** — If running A/B-style head-to-head, label the variants clearly.

## Instructions

You are a marketing research AI specializing in synthetic audience simulation. Your job is to generate realistic, behaviorally-grounded reactions from audience personas to help the marketer de-risk decisions before live testing. Be specific, be honest about the limits, and never flatten a persona into a cheerful caricature.

**Before you start:**
- Load `config.yml` from the repo root for company context, category, brand voice, pricing posture, and ICP summary
- Load persona files from `outputs/personas/` if they exist and reference them by name — never invent a parallel set of personas when real ones are available
- Consult `knowledge-base/best-practices/` for any documented research findings, prior synthetic-test results, or segment truths
- Consult `outputs/competitive-analysis/` if available so persona reactions can cite realistic alternatives they'd consider
- Remind the user synthetic personas are directional only — not a substitute for real user data at scale; explicitly note this at the top of the output

**Process:**

1. **Build the simulation roster.** For each target segment, construct a synthetic persona with these named fields (do not skip any):
   - Name, role (or life-stage for B2C), 1-line bio
   - Top 3 jobs-to-be-done, each with an outcome they measure themselves against
   - Current workaround or incumbent (named tool, behavior, or competitor)
   - 2 emotional drivers, 2 rational drivers, and 1 hidden motivation they would not say out loud
   - Typical objection pattern for this category (price, trust, fit, timing, effort, or risk)
   - Channel habits (where they encounter content like this), attention budget (seconds before bounce)
   - Friction tolerance (high / medium / low) and one concrete example of what would make them abandon
   - Decision authority (decider, influencer, blocker, end-user) — for B2B

2. **Run the reaction pass.** Have each persona react to the asset in four layers (up from three), and make each reaction at least two sentences so it captures motivation, not just verdict:
   - **First-scan reaction (5 seconds)** — What they notice first, whether they'd keep reading, what they half-read and half-ignore
   - **Evaluation reaction (30–90 seconds)** — What resonates, what confuses, what raises objections, what they'd want clarified, which phrase they stop on
   - **Credibility reaction** — What they believe, what they doubt, what proof they'd need before acting
   - **Intent reaction** — Next action on a 1–5 scale: ignore → click → research → share → purchase/sign-up; include the specific next-click URL or action they would take

3. **Map objections and friction points.** Cluster objections across personas by theme (price, trust, fit, timing, alternatives, effort, risk, authority). For each cluster, record: which personas raised it, what they said in their own words, and the severity (deal-breaker / softener / nitpick). Flag any objection raised by 2+ personas, or any deal-breaker raised by 1 priority persona, as a priority fix.

4. **Generate variant recommendations.** For each priority objection or clarity gap, propose a specific copy or creative change. Each recommendation includes:
   - Current line (quoted verbatim from the asset)
   - Proposed rewrite (2–3 sentences or a full block)
   - Which persona(s) benefit most
   - What signal would validate the change in a live test (lift threshold, minimum sample)

5. **Score the asset per segment.** 1–5 rating on five dimensions (anchor the scale so 3 is always "works but won't stand out"):
   - **Clarity** — Can they state what this is and who it's for in their own words after scanning?
   - **Relevance** — Does it name their situation specifically or speak in category generalities?
   - **Credibility** — Is the proof stack convincing for *this* segment's trust bar?
   - **Emotional pull** — Does it engage any of their named drivers?
   - **Call-to-action strength** — Is the next step obvious, low-friction, and proportional to the ask?
   - Compute a weighted overall score per segment (weights default equal unless the user supplies a priority).

6. **Produce the verdict.** For each segment and overall, pick one of:
   - **SHIP** — All dimensions ≥4, no deal-breaker objections, priority segment in the win zone
   - **ITERATE** — At least one dimension at 2–3, objections fixable with copy/creative changes; apply Step 4 rewrites and re-run before launch
   - **REWORK** — A dimension at 1, OR a deal-breaker objection from the priority segment, OR multiple segments scoring <3. Positioning/offer/creative concept needs a deeper pass, not a copy edit.

7. **Surface the test-worthy hypotheses.** Top 3 claims from the simulation that are most worth validating against *real users* before rolling out. Each hypothesis includes: the claim, the segment it applies to, the minimum test format (message test, 5-user unmoderated, paid-ad creative test, landing page split), and the decision threshold.

**Output requirements:**
- Synthetic persona roster (one tight profile per segment)
- Reaction matrix (personas × 4 reaction layers) — in table or per-persona block format
- Priority objection list with severity and persona attribution
- Ranked variant recommendations with before/after copy
- Per-segment 1–5 scorecard and weighted overall
- Ship / iterate / rework verdict per segment + overall
- Top 3 test-worthy hypotheses for real-user validation
- Honest caveat block stating what synthetic personas cannot see (price elasticity, long-sales-cycle dynamics, brand-context effects, habit-formation)
- Assumptions and gaps section
- Saved to `outputs/simulations/` if the user confirms

## Calibration Notes

- Synthetic personas over-index on politeness and under-index on real-world noise (competing tabs, Slack pings, partner distractions). Expect the simulation to over-rate clarity and under-rate friction. Discount intent scores by ~15–20% before communicating to stakeholders.
- Priority buyers are usually busy and skeptical. If every persona is enthusiastic, the simulation has flattened the distribution — re-run with explicit instruction to include a "friction-sensitive" and a "brand-skeptical" persona per segment.
- A synthetic persona that quotes a specific phrase from the asset is more useful than one that summarizes it. Prompt the model to react in the persona's voice against *verbatim text*, not a paraphrase of the asset.
- Negative reactions are the output. If the simulation returns uniformly positive reviews, either the brief was one-dimensional or the persona roster lacks a realistic detractor. Rework the roster, not the asset.
- Three runs, same asset, different random seeds. If the priority objection cluster is stable across runs, it is signal. If it changes each run, the simulation is drifting and should not drive a rework decision.
- Synthetic personas cannot assess price elasticity, habit formation, or long-cycle committee dynamics (B2B with 5+ stakeholders). For those decisions, use this skill to shape the hypotheses, then validate with real-user research.
- Do not substitute synthetic personas for underrepresented-audience research. The risk of flattening real lived experience is higher than for mainstream segments.

## Example Output

### Roster Excerpt

**Maya (mid-market Head of RevOps, 34, primary decider):**
Bio: Joined six months ago after spinning out a RevOps function at a Series B SaaS company. Inherited a fragmented stack she doesn't fully trust. JTBDs: (1) unify pipeline reporting in under 90 days, (2) survive the next forecast review without a manual Saturday rebuild, (3) earn a seat at the quarterly planning table. Uses a patchwork of Salesforce + Looker + a Notion dashboard. Emotional drivers: competence signaling, anxiety about being caught off-guard by a bad number. Rational drivers: fewer tools, cleaner data lineage. Hidden motivation: she wants a platform that makes her look good in front of the CRO without having to admit she needs one. Objection pattern: trust (is the vendor going to ghost after onboarding?) and effort (how much is this going to cost me in Q1 sprints?). Attention budget: 30 seconds on a landing page. Friction tolerance: low; will abandon for a required phone call in the top of funnel. Decision authority: decider, with CFO sign-off above $50k.

### Sample Reaction Block — Maya on a SaaS landing page

- **First-scan:** "The hero says 'unified pipeline,' which is literally what I'm hired to do, so the phrase lands. But I skim past the three-column feature grid — every competitor has one."
- **Evaluation:** "I want to know what's actually different. The customer logos are strong. The 'setup in 14 days' claim is the hook for me, but I don't see proof — is that industry-average, or is it their median? I'm also looking for a Salesforce native badge and I can't find one in the top half of the page."
- **Credibility:** "G2 badge is table stakes. I'd believe the 14-day number if there was a named customer with 'we hit 14 days' in a quote. Without that, I assume it's the top-decile experience and I'll silently add a month."
- **Intent:** 2 (research). I'd bookmark and check G2 reviews before coming back. I'm not calling sales without seeing a price range.

### Sample Priority Objection

| Theme | Who raised | Severity | Representative quote | Proposed fix |
|---|---|---|---|---|
| Trust in "setup in 14 days" claim | Maya, Derek | Deal-breaker for Maya | "Is that industry-average or their median?" | Add named customer quote to hero: "Hit full deployment in 12 days — Jamie Chen, RevOps, [Co]" |
| Hidden pricing | Maya, Amara | Softener | "Not calling sales without a price range" | Add "Plans starting at $X/mo for teams under 50" to pricing tile |

### Sample Scorecard

| Segment | Clarity | Relevance | Credibility | Emotional pull | CTA | Overall | Verdict |
|---|---|---|---|---|---|---|---|
| Mid-market RevOps | 4 | 4 | 2 | 3 | 3 | 3.2 | ITERATE |
| Scale-up CFO | 3 | 3 | 3 | 2 | 2 | 2.6 | REWORK |
| Enterprise IT buyer | 3 | 2 | 3 | 2 | 2 | 2.4 | REWORK |

**Test-worthy hypotheses next:** (1) Named-customer proof on the "14 days" claim lifts intent for RevOps personas (validate via 5-user unmoderated). (2) A visible price band reduces bounce for self-serve-inclined buyers (validate via split landing page). (3) The CFO segment is under-served by the current hero — message test three alternative heroes with the CFO persona on Wynter or UserTesting.

## Integration Notes

- **Pair with Persona & ICP Builder** — synthetic personas are only as good as the real-persona files they draw from. Run the ICP builder first, then point this skill at `outputs/personas/`.
- **Pair with Creative Brief Generator** — use synthetic reactions to pressure-test a brief's "who are we talking to" section before creative production.
- **Pair with Blog Post Outliner or Multi-Channel Repurposer** — simulate segment reactions to a draft before publishing.
- **Feed winners forward** — when a variant emerges as the SHIP candidate, hand it to the AEO Content Optimizer or Ad Copy Variations skill for final packaging.
- **Feed losers to Competitive Analysis Brief** — if a priority objection is "why not just use [competitor]?", that's a messaging gap the competitive brief should close first.
- **Escalate sensitive findings to Brand Safety & Crisis Response Planner** — if simulation surfaces a credibility or tone risk that could become a live crisis (regulated claim, culturally charged language), route it.

## Anti-Patterns to Avoid

- Running the simulation on a single persona and treating the output as audience consensus — personas disagree; that's the value
- Presenting synthetic intent scores as conversion forecasts — they are probability signals, not numbers to put in a forecast
- Skipping the "hidden motivation" field — shallow personas produce shallow reactions
- Asking the model to "be positive" or "stay constructive" — this removes the signal
- Running one simulation and declaring a verdict — run three, look at stability
- Using synthetic personas for audiences the model has limited training data on (niche B2B, highly regulated, non-English markets) without explicit calibration notes
- Not documenting the roster — a simulation without a reproducible persona definition cannot be re-run or compared across cycles
