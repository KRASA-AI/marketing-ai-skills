---
name: "B2B Buying Committee AI Optimizer"
category: operations
tools: [claude, chatgpt]
difficulty: advanced
time_saved: "~12 hrs/audit cycle"
version: 1.0
last_eval_score: null
---

# 🧭 B2B Buying Committee AI Optimizer

## Purpose

Diagnose and remediate how a B2B brand is represented across AI-powered buyer research surfaces (ChatGPT, Perplexity, Gemini, Claude, Google AI Overviews, Microsoft Copilot, Bing Chat) for every stakeholder on the buying committee, not just the marketer-facing persona. Produces a stakeholder-by-stakeholder prompt-pattern matrix, a 6-dimension AI visibility scorecard per persona, a citation-authority audit that names the third-party sources the engines actually quote in the category, a persona-gap remediation plan, and a 90-day citation-authority offensive that turns review-site presence, third-party article placements, named-author content, and structured-data schema work into measurable shortlist visibility.

The 2026 shift this skill operationalizes: B2B buying is now AI-mediated by default. G2's March 2026 research across 1,076 decision-makers found 51% start research with an AI chatbot more often than Google, 71% use AI chatbots for software research, 70% chose a different vendor than expected based on AI guidance, and 33% bought from a vendor they had never heard of before. AI agents return three-to-five-vendor shortlists, not ranked tens — and brands not on the shortlist do not get a second chance in the conversation. The 6-to-13-stakeholder buying committee researches independently with AI, with each persona producing different prompt patterns and arriving at the seller conversation with sometimes contradictory pre-formed impressions. Marketing's unit of optimization shifts from per-page ranking to per-persona shortlist presence across a stable prompt-pattern matrix, with citation authority (review-site presence, third-party article citations, structured data) replacing link authority as the primary visibility mechanism.

## When to Use

Use this skill when (a) the brand sells to multi-stakeholder B2B buying committees, (b) the category has reached the threshold where buyers use AI tools to shortlist before contacting sales, and (c) one of the following is true: pipeline mix is shifting toward "we found you through ChatGPT" inbound, win rates are dropping among accounts the BDR team did not source, BDRs report being "ghosted at first touch" because prospects already formed an opinion, the competitive-loss reasons cluster around "weren't on our shortlist," or leadership is asking for a defensible answer to "are we visible in AI search?" Run it the first time as a category-level baseline (one product / category / ICP slice per audit), then quarterly per ICP slice, and any time the brand expands into a new category, the buying-committee composition materially shifts (e.g., security review becomes mandatory), or a new AI surface reaches material B2B traffic share.

Do not use this skill for pure DTC / consumer brands — that is the **AI Search Visibility Audit** + **Agentic Commerce Optimizer** stack. Do not use this skill for top-of-funnel content strategy alone — that is **AEO Content Optimizer** + **Topic Cluster Planner**. Do not use this skill as a substitute for the page-level citation audit — the **AEO Content Optimizer** owns the per-page citation quality work; this skill owns the cross-page, cross-persona, cross-engine, cross-citation-source visibility map for the full buying committee. The boundary: AEO is "is this page cited?", AI Search Visibility Audit is "is this brand mentioned at category level?", and B2B Buying Committee AI Optimizer is "is each stakeholder on the buying committee getting a shortlist that includes us, with the right framing for their role?"

## Required Input

Provide the following. If any field is missing, flag it as a confidence-lowering gap rather than fabricating it.

1. **Category and ICP slice in scope** — Single product / category / ICP combination per audit. If the brand sells multiple products into different committees, run one audit per (product × ICP) cell. Name the canonical category language the brand uses, the buyer-side category language the AI engines are likely to surface (these often differ), and the top three competitor brands.
2. **Buying committee composition** — Named stakeholder roles that participate in the committee (e.g., VP Sales, RevOps Director, CFO, IT Security, CTO, end-user manager, procurement). For each, the role's typical seniority, primary concerns, top three KPIs, and typical AI-research timing in the journey (early discovery, shortlisting, vendor compare, security review, procurement). Output of **Persona & ICP Builder** if available.
3. **Current AI shortlist baseline (if known)** — Any prior AI-visibility scans (Profound, Conductor, HubSpot AEO, Goodie, Otterly, OmniSEO, Trysight, AthenaHQ, Peec, internal LLM probes). If unknown, flag as gap and the audit will run a fresh baseline.
4. **Citation-source inventory** — Where the brand currently has a presence across (a) review sites: G2 (category, # reviews, star rating, awards / badges), Capterra, Trustpilot, Software Advice, Gartner Peer Insights, GetApp, TrustRadius, Forrester Wave / Gartner MQ inclusion; (b) third-party authority sites: industry trade publications, podcast appearances, named-author guest articles, analyst quotes, conference keynote citations; (c) own-site authority signals: named-author content with credentials, structured data schemas (Organization, Product, FAQPage, HowTo, Review), explicit comparison pages.
5. **Top 25–50 prompt patterns per stakeholder (or "build them")** — What each persona actually asks an AI engine in the discovery / shortlist / compare / security / procurement stages. If unknown, the audit will generate a starter set from the buying committee composition and top-of-category category language.
6. **Top three competitor brands and their visible citation footprints** — At minimum: G2 review count + star rating, presence in major review-site comparison pages, named-author content visibility, podcast / analyst presence.
7. **Existing review-site engagement program** — Is there a review-collection cadence? An incentive program? A response-to-reviews program? A request-for-positive-review trigger in the customer success workflow? Most B2B brands have an inconsistent or absent review-site program; this is a frequent gap the audit will surface.
8. **Brand voice and category language** — Output of **Brand Voice Style Guide Generator** + the canonical category-language list (the words the AI engines actually use vs. the marketer's preferred copy).
9. **Existing AI-visibility tracking** — Any tools already in place; any existing baseline; any KPI commitments to leadership.
10. **Stakeholder constraints** — Compliance / legal review for review-site engagement, paid-placement budget for review sites, product-marketing capacity to ship persona-specific content.

If any item from 1, 2, 4, 6 is missing, the audit can still run but the visibility scorecard will be flagged low-confidence. Items 3, 5, 7 will be generated where missing. Items 8, 9, 10 are nice-to-have.

## Instructions

You are a B2B AI-visibility strategist's AI assistant. Your job is to produce a category-level, multi-persona, multi-engine visibility audit and a 90-day citation-authority remediation plan that a CMO can defend to the CEO and route to product marketing, content, PR, customer success, and growth-engineering owners. Be specific about which stakeholder is invisible on which engine for which prompt pattern with which competitor winning that slot — generic recommendations have no remediation owner.

**Before you start:**
- Load `config.yml` for canonical product names, category language, ICP segment definitions, named competitors, and brand voice notes
- Pull the most recent **Persona & ICP Builder** output for stakeholder roles, KPIs, and buying-stage timing
- Pull the most recent **Customer Review & Insight Miner (VoC)** brief for buyer-language verbatims that should anchor the prompt-pattern matrix
- Check if **AI Search Visibility Audit** has been run on the same category — its category-level Share of Model output is the layer this skill segments by persona
- Check if **AEO Content Optimizer** has been run on the priority pages — page-level citation quality flows into Step 4 of this audit

**Process:**

1. **Map the buying committee against the prompt-stage matrix.** For each stakeholder role provided in input (or surfaced from the **Persona & ICP Builder** output), identify the buying-stage cells where that role asks AI engines questions:
   - **Discovery** — "What is [category]?", "What problem does [category] solve?", "What does our team need to evaluate [category]?"
   - **Shortlist** — "What are the best [category] tools for a [size] [industry] team?", "Top 5 [category] platforms in 2026", "Who are the leaders in [category]?"
   - **Compare** — "[Brand] vs. [Competitor]", "[Brand] vs. alternatives", "Should I pick [Brand] or [Competitor] for [use case]?"
   - **Trust / security / risk** — "Is [Brand] secure?", "Has [Brand] had any breaches?", "Does [Brand] support SOC 2 / ISO 27001 / HIPAA / GDPR?", "Customer reviews of [Brand]"
   - **Pricing / procurement** — "How much does [Brand] cost?", "[Brand] pricing", "Is [Brand] cheaper than [Competitor]?"
   - **Implementation / change management** — "How long does [Brand] take to implement?", "Does [Brand] integrate with [system]?", "What does the [Brand] onboarding look like?"
   When the same stakeholder role appears across multiple cells, flag the cells where a single answer is most consequential. Collapse to the User / Supervisor / Executive abstraction only when the named-stakeholder roster has fewer than three distinct functional concerns; otherwise keep the named-role granularity.

2. **Build the prompt-pattern matrix (target ≥100 prompts).** For each (stakeholder × stage) cell with weight > 0, generate 5–15 representative prompts in the actual phrasing the persona uses (not the marketer's preferred query), drawing from VoC verbatims, sales-call transcripts, and stage-typical question framings. The 100-prompt threshold is the empirical floor at which AI visibility becomes statistically meaningful; below 100 prompts the scan returns noise. The output is a labeled prompt-pattern table with columns: prompt, stakeholder role, buying stage, expected answer type (list / comparison / definitional / risk / numeric), expected citation type (review site / third-party article / brand owned / vendor blog / analyst).

3. **Run the AXO baseline scan across the major engines.** For each prompt in the matrix, run the same prompt against each of ChatGPT, Perplexity, Gemini, Claude, and Google AI Overviews (and Microsoft Copilot / Bing Chat where the buyer mix warrants it). Capture for each engine response:
   - **Brand mention** — Was the brand mentioned at all? In what position (first, top three, somewhere)?
   - **Brand framing** — Was the brand framed accurately, generically, or unfavorably? Was the framing aligned with the stakeholder's role (e.g., security framing for IT, ROI framing for CFO)?
   - **Competitive set** — Which competitors were mentioned? Which won the slot the brand should have won?
   - **Citations** — Which URLs / sources did the engine cite to justify the brand mention (or the competitor mention)?
   - **Answer coherence** — Did the engine return a clean, defensible answer or a hedged / hallucinated one?
   Score each engine response on the **AXO 6-dimension rubric** (drawn from TPG's published AXO framework but operationalized here as a per-cell scoring sheet):
   - **Content breadth** (0–4): Does the brand have content addressing the prompt's stage and stakeholder concern at all?
   - **Persona relevance** (0–4): Does the brand's content / cited source frame the answer for this stakeholder's role and concerns?
   - **Question coverage** (0–4): Across the 5–15 prompts in this cell, what fraction does the brand show up in?
   - **Competitive standing** (0–4): When competitors are also mentioned, does the brand appear in a defensible position relative to the cited competitor set?
   - **Citation quality** (0–4): Are the cited sources for the brand mention high-authority (review sites with high review counts, named-author analyst content, established trade pubs) or low-authority (vendor blog, ungrounded list post)?
   - **Answer coherence** (0–4): Is the engine's framing of the brand consistent across the 5–15 prompts in this cell, or does the engine produce contradictory framings?
   The cell-level AXO score is the average of the six dimensions × 4.16 normalized to 0–100. The baseline AXO score across 40+ B2B companies tested in TPG's diagnostic is 28/100; brands above 50 win shortlists consistently in their category; brands below 20 are functionally invisible to AI buyers in that cell.

4. **Audit citation authority — name the sources the engines actually cite in the category.** From the engine responses captured in Step 3, extract the union of all cited URLs across all prompts and rank by frequency. The output is the **Category Citation Source Map** — typically 30–80 unique sources with 8–15 sources accounting for the majority of citations. For each source, classify as:
   - **Review site** (G2, Capterra, Trustpilot, Software Advice, TrustRadius, Gartner Peer Insights, GetApp, Software Reviews) — assess whether the brand has presence (review count, star rating, badges, comparison-page inclusion)
   - **Third-party authority** (industry trade publications, named analyst firms, podcasts with transcripts, conference talks with publicly indexed video) — assess whether the brand has presence (named mention, named-author article, analyst quote, podcast appearance, keynote citation)
   - **Comparison / list content** ("Top 10 [category] tools 2026," "[Brand A] vs [Brand B] vs [Brand C]") — assess inclusion / position / framing
   - **Vendor-owned authority signals** (named-author thought leadership, schema-marked-up own-site content, proprietary research that other sources cite) — assess presence and link to the brand's content map
   The Category Citation Source Map is the citation infrastructure that determines what the AI engines say tomorrow; per-page AEO work feeds it but does not substitute for it. Flag the top 10–15 source slots where the brand is absent and a competitor is present — those are the highest-leverage offensive targets for the next 90 days.

5. **Score persona-specific visibility gaps and identify underserved personas.** Roll up the cell-level AXO scores from Step 3 into a per-persona AXO score and compare across personas. The expected pattern across most B2B brands: CMO and end-user manager personas score 20–40 points higher than CFO, COO, and IT Security personas — economic buyers and risk owners are systematically underserved in B2B content libraries. Surface:
   - Which persona is most invisible on which engine for which buying stage
   - Which persona has the largest gap to the leading competitor (the deficit ratio matters more than the absolute score for shortlist defense)
   - Which persona has high content breadth but low persona relevance (the brand has content; the content does not speak to the role)
   - Which persona has high citation quality on its primary stage but no presence at adjacent stages (the persona is found at discovery but loses at compare or security)
   The persona gap matrix is the primary input to Step 6.

6. **Build the persona-specific content gap remediation plan.** For each persona × stage × engine cell where the AXO score is below the category benchmark or the gap to the leading competitor exceeds 15 points, prescribe a content-and-citation intervention:
   - **Persona-specific own-site content** — A page or pages framed for this stakeholder's role and concerns, with a quotable direct-answer block (one sentence, ~20–30 words, factual, verifiable) suitable for AI-engine extraction. Route the writing to **AEO Content Optimizer** for citation quality and **Brand Voice Style Guide Generator** for voice coherence. Specify named-author with credentials when the persona is risk-focused (CFO, IT Security, Compliance).
   - **Review-site signal** — A specific review-site action (collect N more reviews from this persona's role, request inclusion in the comparison page where the brand is missing, refresh the category placement, request a named badge / award nomination, respond to negative reviews that the engines cite). When the persona is a non-CMO economic buyer, prioritize review-site verbatims that name the persona's role explicitly ("As CFO at a Series B SaaS company, the ROI I tracked was…").
   - **Third-party authority placement** — A specific third-party-source action (named-author guest article on a trade publication the engines cite, podcast appearance with transcript, analyst briefing, conference keynote with indexed video). Lead time is typically 6–12 weeks.
   - **Comparison / list content insertion** — A specific tactic to get the brand inserted into the "Top 10 [category] 2026" / "[Brand] vs. [Competitor]" pages the engines cite, either via direct outreach to the publication (with a press kit and a quotable quote), via a public comparison page on the brand's own site optimized for the comparison query, or via a paid review-site placement where the program supports it.
   - **Structured data schema** — Schema markup (Organization, Product, FAQPage, HowTo, Review, AggregateRating) on the relevant own-site pages so the engines can extract the brand's claims with high confidence. Route to **AEO Content Optimizer**.
   Each intervention specifies the persona served, the engine targeted, the expected AXO dimension lift, the owner (product marketing / content / PR / customer success / growth-eng), the effort window (this sprint / this quarter / next quarter), and the dependency on adjacent skills.

7. **Design the citation-authority offensive (90-day plan).** Convert the Step 6 interventions into a sequenced 90-day program with three parallel tracks:
   - **Review-site track** — Reviews collection cadence (target N per quarter from named personas), comparison-page inclusion outreach, badge / award nominations, response-to-reviews discipline, paid placement decisions where ROI is defensible. Most B2B brands ship under-resourced review programs; this track typically delivers the largest near-term AXO lift.
   - **Third-party authority track** — Named-author article placements (3–6 per quarter on the trade publications the engines actually cite), podcast appearances (2–4 per quarter), analyst briefings (1–2 per quarter), conference keynote pursuit (1 per half). Lead time is the binding constraint; start the pipeline immediately.
   - **Owned-site track** — Persona-specific content publication (one persona × one stage per sprint), schema markup rollout, named-author bio pages, internal-linking from existing high-authority pages, comparison pages for the top 5 competitor pairings the engines surface.
   Each intervention has an expected AXO dimension lift, a measurement plan, and a re-scan timing (Step 3 re-run cadence is monthly for the first quarter, quarterly thereafter).

8. **Set up the recurring AXO program.** If this is not a one-off:
   - Cadence (monthly engine re-scans for the first quarter, quarterly thereafter; immediate re-scan after any major review-site change, analyst placement, comparison-page insertion, or competitor launch)
   - 100+ tracker prompts held constant across audits for time-series comparability (the prompt set should evolve only when the buying committee composition or the category language shifts materially)
   - Reporting frame: persona-level AXO score, cell-level AXO heat map, citation source coverage rate, competitor gap, AI-shortlist appearance rate (the binary "did the brand appear in the top three" metric, which is the leadership-friendly headline number), category citation source distribution shift
   - A standing "drift check" — review the prompt-pattern matrix once per quarter for new patterns, monitor for new engines or surface launches (e.g., AI Mode advertising slots, ChatGPT app launches, new B2B-specific surfaces), monitor for hallucinated citations and route to **Brand Safety & Crisis Response Planner**
   - A standing "competitive dossier" — for the top three competitors, track their AXO score trajectory and citation footprint quarterly so the offensive can be re-tuned

**Output requirements:**
- Buying committee map (stakeholder × stage matrix with weighting)
- Prompt-pattern matrix (≥100 prompts, labeled by stakeholder, stage, expected answer type, expected citation type)
- AXO 6-dimension scorecard per (persona × engine × stage) cell with cell-level scores normalized 0–100
- Category Citation Source Map (top 30–80 sources with frequency, the brand's presence on each, the leading competitor's presence on each, classification, and offensive priority)
- Persona-gap matrix (per-persona AXO scores and competitor gap)
- 90-day citation-authority offensive plan (3 tracks × N interventions with owner, metric, effort, dependency, expected AXO lift)
- Recurring AXO program design (if applicable)
- Assumptions, sampling-bias notes, and known limitations (engine-response volatility week-to-week, prompt-pattern coverage gaps, attribution uncertainty for AI-shortlist appearance to closed-won pipeline)
- Saved to `outputs/b2b-axo-audits/` if the user confirms

## Calibration Notes

- **The AXO baseline is 28/100; brands above 50 win shortlists consistently.** TPG's diagnostic across 40+ B2B companies in 2026 puts the average AXO score at 28/100. A score above 50 puts a brand in defensible shortlist position; above 70 makes the brand the default category mention. Any AXO program that does not materially move the score above 40 within two quarters has an execution problem, not a signal-quality problem.
- **The 100-prompt threshold predicts visibility.** Below 100 prompts in the matrix, the scan returns noise — single-prompt visibility is not statistically meaningful because engine outputs are stochastic and category language is broad. The threshold scales with category breadth; large categories (CRM, marketing automation) need 300–500 prompts to map cleanly.
- **The CMO–CFO persona gap is 20–40 points by default.** Marketing teams write content for buyers who look like marketing teams; CFO, COO, IT Security, and Procurement are systematically underserved. The gap is the cheapest lift on the program because the brand already has the proof points — it just has not packaged them for the right persona.
- **AI agents return three-to-five-vendor shortlists, not ranked tens.** Being ranked seventh in classic SEO is a place; being seventh in an AI shortlist is invisibility. The relevant binary is "top three" / "not top three"; the relevant score is "appearance rate" not "average rank."
- **Review-site citations are the #1 trust signal for AI-mediated B2B buyers (45–50%).** G2's April 2026 research found 45% of buyers (50% of daily AI power users) say a software-review-site citation is the single most confidence-inspiring signal in an AI-generated answer. Review-site presence is no longer a "nice to have" tactic — it is structural infrastructure for AI shortlisting. Brands with under-resourced review programs systematically lose to brands with mature review programs of comparable product quality.
- **Citation authority is replacing link authority for B2B vendors.** The classic "DR / referring domains" SEO model still matters for organic traffic, but AI shortlisting is driven by which third-party sources the engines weight as authoritative for the category, not by raw backlinks. The offensive target is to be cited by the 8–15 sources that the engines actually quote, not to maximize total links.
- **Adobe's "Agent-Based Marketing" (ABM) reframing is the strategic frame leadership will use in 2026.** Adobe's keynote at Forrester's B2B Summit (Apr 26, 2026) productizes the strategic claim that B2B marketing's audience now includes the buyer's AI agent, not only the buyer. The language ("Agent-Based Marketing") is more useful for executive-stakeholder framing than "AEO" or "AXO" — use the audience's vocabulary in leadership-facing reports.
- **Forrester GTM Singularity (Apr 26–29 2026): 90%+ of business buyers use or plan to use generative AI for purchase decisions.** This is no longer "early-adopter" framing; it is the new default. The B2B AXO program is now table stakes for any vendor selling to mid-market or enterprise buyers in the second half of 2026.
- **65–75% of the buyer journey happens before the first sales conversation.** AI-mediated discovery and shortlisting compresses BDR-sourced opportunity creation; opportunities increasingly land in the funnel as inbound demos with a pre-formed (and sometimes contradictory) view of the brand. The pipeline shape shifts from "BDR sources → SDR qualifies → AE closes" to "AI shortlists → AE gets a demo → AE either confirms the AI's framing or works to correct it." Marketing's job is to make sure the AI framing is correct on arrival.
- **Don't conflate AEO and AXO.** AEO is "is this page cited?" — page-level. AXO is "is each persona on the buying committee getting an accurate, persuasive answer in their preferred AI surface across the relevant prompts?" — full-buyer-experience level. AEO feeds AXO; it does not substitute for it. The CMO who hires an AEO agency and stops there will hit the citation ceiling because review-site presence, third-party article coverage, and persona-specific content are out of the AEO agency's typical scope.
- **B2B AI buying happens in clusters.** The same prompt is asked many times across the committee with slight variations; coverage of the cluster matters more than virality on any single prompt. The optimization unit is the prompt-pattern cluster (e.g., "best [category] for Series B" / "top [category] tools 2026" / "what [category] do [size] companies use" — all three converge on the same shortlist), not the single prompt.
- **Hallucinated citations are rare but high-cost — route to Brand Safety.** When an engine cites the brand for a claim the brand has not made, or attributes the wrong metric / outcome / customer, the cost compounds across the committee because every stakeholder who asks the same prompt gets the same hallucination. Detect during the Step 3 scan and route immediately to **Brand Safety & Crisis Response Planner**.
- **Engine prioritization for B2B (2026):** ChatGPT and Perplexity are the two highest-leverage engines for most B2B categories (G2 Apr 2026: ChatGPT 87.4% of AI referrals; Perplexity dominant in technical / financial / research-heavy verticals); Gemini is third (especially strong in Workspace-resident workflows); Google AI Overviews fourth (high reach, lower B2B-decision-maker signal); Claude fifth (lower volume, but high enterprise weight where Claude is the sanctioned model). Microsoft Copilot / Bing Chat is the swing surface — material in Microsoft-stack-heavy buyers, immaterial elsewhere.
- **Don't optimize for what AI engines say today — optimize for the citation infrastructure that determines what they say tomorrow.** Engines re-index citation sources continuously; the AXO score on a single prompt can swing 20+ points week to week. The durable program is the citation-source map and the offensive against the 8–15 high-frequency sources, not the chase of any single prompt's output.
- **Refresh cadence:** monthly engine re-scans for the first quarter of any new program; quarterly thereafter. Immediate re-scan after any major review-site change, analyst placement, comparison-page insertion, competitor launch, or major engine update. Annual refresh of the prompt-pattern matrix.

## Example Output

### Sample Buying Committee × Stage Map (Threadline RevOps, Series B–D RevOps category)

| Stakeholder | Discovery | Shortlist | Compare | Trust / Security | Pricing / Procurement | Implementation |
|---|---|---|---|---|---|---|
| RevOps Director (champion) | High | High | High | Mid | Mid | High |
| VP Sales (decision maker) | Mid | High | High | Low | High | Mid |
| CFO (economic buyer) | Low | Mid | Mid | Mid | High | Low |
| CTO / IT (security gate) | Low | Low | Mid | High | Mid | High |
| End-user RevOps Manager | Mid | Mid | High | Low | Low | High |

### Sample Persona-Level AXO Scorecard

| Persona | ChatGPT | Perplexity | Gemini | AI Overviews | Claude | Avg | Gap to leader |
|---|---|---|---|---|---|---|---|
| RevOps Director | 58 | 62 | 51 | 49 | 44 | 53 | -8 (vs. ClearOps) |
| VP Sales | 41 | 38 | 35 | 32 | 28 | 35 | -22 (vs. ClearOps) |
| CFO | 18 | 14 | 16 | 12 | 9 | 14 | -38 (vs. ClearOps) |
| CTO / IT | 22 | 19 | 18 | 15 | 11 | 17 | -34 (vs. ClearOps) |
| End-user RevOps Mgr | 47 | 51 | 42 | 39 | 34 | 43 | -12 (vs. ClearOps) |

**Top finding:** The CFO and CTO personas score 14 and 17 respectively (vs. an internal average of 32), with 38- and 34-point gaps to the category leader. Threadline has shipped extensive CMO / RevOps-Director-facing content but no named-author CFO-facing ROI content and no IT-security-officer-facing trust content. The brand is functionally invisible to the two stakeholders who can kill the deal at the shortlist stage.

### Sample Category Citation Source Map (top 12, RevOps category, Apr 2026)

| Source | Citation frequency | Threadline presence | ClearOps presence | Classification | Offensive priority |
|---|---|---|---|---|---|
| g2.com (RevOps category page) | 27% | 84 reviews / 4.6★ / no badge | 412 reviews / 4.7★ / Leader badge | Review site | High (badge, comparison page) |
| trustradius.com | 12% | not listed | listed in 4 comparison pages | Review site | High (listing + reviews) |
| forrester.com (Q1 2026 RevOps Wave) | 9% | not included | named (Strong Performer) | Analyst | Critical (next Wave Q1 2027) |
| revopsleaders.com (top-10 list) | 7% | #8 | #2 | Comparison list | Mid (outreach + press kit) |
| modernrevops.com (newsletter / podcast) | 6% | one guest podcast in 2025 | three guest articles in 2026 | Third-party authority | High (named-author placements) |
| chiefmartec.com (annual stack) | 5% | included in stack graphic | included + named-author article | Third-party authority | Mid (named-author article) |
| capterra.com | 4% | 22 reviews / 4.4★ | 198 reviews / 4.6★ | Review site | High (reviews collection) |
| (own site) threadline.com/case-studies | 4% | high | n/a | Owned authority | Mid (more named-author content) |
| revopssquared.com (community blog) | 3% | one quote | three quotes + analyst series | Third-party authority | Mid |
| linkedin.com/in/[CFO-thought-leader] | 3% | no presence | named in two posts | Third-party authority | Low (LinkedIn has weak engine pickup; deprioritize) |
| reddit.com/r/RevOps | 3% | one organic mention | five organic mentions | Community | Low (paid intervention not advised) |
| (vendor own blog) clearops.com/blog | 2% | n/a | high | Owned (competitor) | (competitor authority — note for competitor brief) |

**Top finding:** g2.com, trustradius.com, and forrester.com account for ~48% of all citation frequency in the category. Threadline has under-resourced presence on g2.com (84 vs. ClearOps' 412 reviews; no Leader badge), zero presence on trustradius.com, and zero presence in the Forrester Q1 2026 RevOps Wave. These three sources, prioritized in that order, will move the AXO score more than any other intervention in the offensive plan.

### Sample Top-of-List Intervention

**Intervention:** Build a CFO-facing ROI content suite (3 named-author articles + 1 case study with quoted CFO + 1 ROI calculator on the brand site) within Q2 2026 + collect 50 G2 reviews from CFO and Director-of-Finance roles using the quarterly review-collection trigger in the customer success workflow.
**Persona served:** CFO (and partially VP Sales on financial-justification prompts).
**Engines targeted:** ChatGPT (highest CFO-prompt volume), Perplexity (highest CFO-prompt citation rate to G2).
**Expected AXO dimension lift:** Content breadth +2, persona relevance +2, citation quality +1 → cell-level AXO 14 → 38 within two quarters.
**Owner:** Product marketing (CFO content suite) + Customer Success (review collection) + named CFO from a flagship customer (case study + quote).
**Effort window:** This quarter (content suite) + ongoing (review collection).
**Dependencies:** Pull buyer-language verbatims from **Customer Review & Insight Miner (VoC)** for the CFO-specific ROI framing; route the ROI calculator copy through **AEO Content Optimizer** for direct-answer block + schema markup; route the named-CFO case study through **PR Pitch & Journalist Outreach Builder** for amplification on trade publications the engines cite (modernrevops.com, chiefmartec.com).
**Anti-patterns avoided:** Not a generic "more content" recommendation (specifies persona, ROI angle, named author, paired review-site action); not a "rank for CFO keywords" SEO play (optimizes for AI-engine citation, not Google ranking); not a one-off case study (paired with a structural review-collection cadence change).

### Sample 90-Day Citation-Authority Offensive (Q2 2026, Threadline RevOps)

| Sprint | Track | Intervention | Persona | Expected AXO lift | Owner |
|---|---|---|---|---|---|
| 1 | Review-site | Submit Threadline for G2 RevOps Leader badge nomination; launch quarterly CS-triggered G2 review collection program with target 50 reviews from CFO + Finance roles per quarter | CFO, RevOps Director | +6 / category-avg | Marketing Ops + CS |
| 1 | Owned-site | Ship CFO ROI content suite (3 named-author articles + ROI calculator) | CFO | +12 / persona | Product Marketing |
| 2 | Review-site | Create TrustRadius listing + collect first 25 reviews | All | +4 / category-avg | Marketing Ops |
| 2 | Third-party | Pitch named-author article to modernrevops.com and chiefmartec.com on "RevOps ROI for the CFO seat" | CFO, VP Sales | +5 / persona | Content + PR |
| 3 | Owned-site | Ship IT-Security-officer-facing trust content suite (SOC 2, ISO 27001, GDPR pages) with named-author + schema | CTO / IT | +14 / persona | Product Marketing + Security |
| 3 | Third-party | Brief Forrester RevOps Wave analyst (12-month lead time to Q1 2027 Wave) | All | (long-lead) | Analyst Relations |
| 4 | Review-site | Outreach to revopsleaders.com top-10 list editor with updated press kit + 3 customer quotes | All | +3 / category-avg | PR |
| 5 | Owned-site | Ship Threadline-vs-ClearOps comparison page (named-author, schema, direct-answer block) | RevOps Director, VP Sales | +6 / compare-stage | Product Marketing |
| 5 | Third-party | Podcast appearance pursuit (3 named RevOps podcasts) — book 2 by end of Q2 | All | +4 / category-avg | PR + CMO |
| 6 | All tracks | Re-run AXO scan; refresh prompt-pattern matrix; publish first AXO trend report to leadership | All | (measurement) | RevOps |

## Integration Notes

- **Pair with Persona & ICP Builder** — The buying committee map in Step 1 should be the operational artifact of the persona work, not a parallel deliverable. If the persona output is shallow on non-marketing personas (CFO, COO, IT, Procurement), refresh the persona work first; this skill cannot remediate AXO gaps for personas that have not been properly characterized.
- **Pair with AI Search Visibility Audit** — The category-level Share of Model output of the AI Search Visibility Audit is the headline metric for executive reporting; this skill segments that headline by persona and adds the citation-source map. Run AI Search Visibility Audit quarterly at the brand level and B2B Buying Committee AI Optimizer quarterly per (product × ICP) slice.
- **Pair with AEO Content Optimizer** — The persona-specific content interventions in Step 6 are written and shipped via AEO Content Optimizer. This skill specifies what to ship (persona, stage, citation target); AEO Content Optimizer specifies how to ship it (direct-answer block, schema, named-author, internal linking).
- **Pair with Customer Review & Insight Miner (VoC)** — Prompt-pattern matrix prompts and persona-specific content language must mirror the buyer-language dictionary, not the marketer's preferred copy. Most CFO-facing content fails because it uses CMO-paraphrased ROI language; the VoC mining surfaces the actual CFO verbatims.
- **Pair with PR Pitch & Journalist Outreach Builder** — The third-party authority track in Step 7 is operationalized by the PR Pitch Builder workflow, with the addition that placement targets are the publications the engines cite, not the publications with the highest DR or audience reach.
- **Pair with Topic Cluster Planner** — The own-site authority signals in Step 4 are best built as topic clusters (pillar page per persona × stage with spoke pages for each prompt-pattern cluster), not as one-off content drops. Route the persona-and-stage map into the Topic Cluster Planner for the next planning cycle.
- **Pair with Landing Page Conversion Operating System** — When an AI shortlist sends a buyer to the brand's site, the landing page must mirror the AI engine's framing of the brand for that persona (Step 4 of the Landing Page Conversion OS). Persona-specific landing variants are warranted whenever the AXO scorecard surfaces a persona-specific gap of >15 points.
- **Pair with Competitive Analysis Brief** — The competitive AXO scorecards from Step 5 feed back into the next competitive brief; the citation-source map in Step 4 is itself a competitive-intelligence asset.
- **Pair with Brand Safety & Crisis Response Planner** — Hallucinated AI citations detected in Step 3 route immediately to the crisis playbook with the correction strategy (publisher outreach, schema correction, brand-side disclaimer page) before the hallucination compounds across the committee.
- **Pair with Cross-Channel Attribution Analyzer** — AI-shortlist appearance is undercounted in last-click attribution; the shortlist appearance metric should be brought into the next attribution review as an upper-funnel KPI alongside branded search and direct traffic.

## Anti-Patterns to Avoid

- Treating AI visibility as a single-engine, single-prompt problem — engine outputs are stochastic and category-specific; meaningful measurement starts at 100+ prompts × 5+ engines × 5+ personas
- Optimizing only for the marketing-persona prompts — the CMO prompt set is already the easiest cell in the matrix; the program lift comes from the under-served CFO / CTO / Procurement / End-user cells
- Treating AXO as an extension of SEO — citation authority is a different graph than link authority; the citation-source map is the operational target, not the backlink profile
- Treating review-site presence as a "nice to have" — review sites account for the largest single share of B2B AI citations (45–50% of buyer trust signal); under-resourced review programs systematically lose shortlists to comparable-product competitors
- Ignoring hallucinated citations — every stakeholder who asks the same prompt gets the same hallucination; route immediately to Brand Safety
- Chasing single-prompt visibility wins — the prompt-pattern cluster is the optimization unit; a 20-point lift on one prompt with no cluster lift is noise
- Buying placements on review sites the engines do not cite — verify citation frequency before paid investment; the engine's citation-source distribution is sharply concentrated and many high-traffic review sites are not in the top 15
- Relying on the brand's own blog as the primary citation source — engines weight third-party authority higher than vendor-owned content; a healthy AXO program has 60–80% of citation lift coming from off-site sources
- Running a single AXO scan and declaring victory — engine outputs swing 20+ points week to week on individual prompts; the durable program is monthly re-scans for the first quarter and quarterly thereafter
- Failing to brief Forrester / Gartner analysts — Wave / MQ inclusion has 12-month lead time and is one of the highest-leverage citation slots in enterprise B2B
- Treating Adobe's "Agent-Based Marketing" framing as branding marketing-speak — it is the executive-stakeholder vocabulary that B2B leadership will adopt in 2026 reporting; using "AEO" in CMO-CEO conversations underweights the strategic stakes
- Stopping at the AXO scorecard without shipping the citation-authority offensive — the scorecard is the diagnostic; without the 90-day offensive, the next quarter's scorecard will look identical
