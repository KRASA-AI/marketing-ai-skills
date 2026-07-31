---
name: "Brand Safety & Crisis Response Planner"
category: operations
tools: [claude, chatgpt]
difficulty: advanced
time_saved: "~6 hrs/plan + faster response"
version: 2.4
last_eval_score: 9.7
---

# 🛡️ Brand Safety & Crisis Response Planner

## Purpose

Produce a tiered crisis-response plan that covers real-time monitoring signals, escalation triggers, decision roles, holding-statement templates, channel-specific response playbooks, and an AI-era risk addendum covering hallucinated AI-generated claims, model-citation errors, and synthetic-media incidents. Designed for marketing leaders who own external communications but do not have a dedicated crisis comms team.

The 2026 shift this plan absorbs: the window between "small incident" and "full reputation event" has compressed from days to hours, and AI answer engines now generate claims about brands that can be wrong in ways the brand did not create and cannot directly edit. The brand-code framework from HBR's May 2026 agentic marketing org piece (Taite / Winsor / Fernandez) is the structural answer to the AI-misattribution risk — a machine-readable brand knowledge base that AI agents query — and the crisis plan must include a brand-code-correction workflow alongside the publisher-correction workflow.

#### The plan at a glance

The full deliverable is eight linked build steps. Read the table top-to-bottom as the run order — the roster (step 3) needs the tiers (step 1) to know who owns what, the statements (step 4) need the tiers to know the approval bar, and the drill (step 7) is the only thing that proves steps 1–6 actually work under pressure:

| # | Step | One-line job | Owner | The output that makes it real |
|---|------|--------------|-------|-------------------------------|
| 1 | Define the four tiers | Set testable severity definitions the team won't argue about mid-incident | Marketing lead | Tier 1–4 definitions, each with an owner and a response window |
| 2 | Map monitoring signals to tiers | Turn the tiers into thresholds the team's actual tools will show them | Marketing lead + monitoring owner | Signal map: volume / authority / sentiment / AI-specific / customer-impact triggers per tier |
| 3 | Assign the response team | Name a primary + backup per role, pre-filled from config | Marketing lead | Roster: decision lead, comms lead, legal, product, exec sponsor, channel owners — no `[placeholder]` seats |
| 4 | Draft holding-statement templates | Pre-approve the language before the pressure hits | Comms lead + legal | One template per top scenario, legal-approved, voice-constrained |
| 5 | Write the AI-era risk addendum | Cover the five categories that don't fit a traditional crisis plan | Comms lead + product | Hallucination / synthetic-media / AI-content-error / brand-code / disclosure workflows, each with a correction or rollback path |
| 6 | Build the response playbooks | One-page runbook per scenario, not a binder no one opens | Response team | 60-min / 4-hr / 24-hr / 72-hr-and-2-week task lists, each task owned |
| 7 | Design the exercise cadence | Rehearse before the real incident, not during it | Marketing lead | Quarterly drill calendar with time-to-first-response and gap tracking per drill |
| 8 | Define success metrics | Know whether the response — and the plan itself — worked | Marketing lead | Incident-level metrics (time-to-triage, sentiment recovery) + program-level metrics (drill-to-incident readiness) |

The operating spine in one sentence: **define the tiers, wire the signals that trigger them, staff and script the response before it's needed, cover the AI-era categories a traditional plan misses, build the one-page playbooks, drill them quarterly, then measure whether the drill and the real thing actually worked.**

## When to Use

Use this skill proactively — before a crisis — to build a standing plan. Use it reactively during an incident to classify severity, assemble the response team, and draft holding statements against pre-approved templates. Use it quarterly to refresh scenarios, test the tiering, and audit which playbooks have been exercised in the last 12 months. Use it on demand when the AI Search Visibility Audit flags hallucinated-claim or negative-sentiment patterns above the Tier 2 threshold.

Do not use for ordinary customer-complaint handling; review-response playbooks live in the customer-service skill set. This is for incidents that could cross into earned-media, regulatory, or paid-media safety territory.

## Minimum Viable Input

If the user provides only the three fields below, proceed immediately and tag every assumption `[ASSUMED]`:

1. **Brand context** — Company name + category (e.g., "Threadline, B2B RevOps SaaS")
2. **Top three risk scenarios** — The three incidents the team would lose sleep over (one sentence each)
3. **Decision lead and comms lead** — Named primary for "who calls the escalation" and "who writes the statement"

When running in MVI mode: infer geographies and regulated/sensitive attributes from the category; assume no existing monitoring stack and recommend a baseline configuration; produce the four tier definitions + three playbooks (one per scenario, one-page each) + three holding-statement templates + the AI-era risk addendum; skip the quarterly-exercise design and the full role roster (recommend a 30-minute follow-up to fill these); flag at the bottom the top 2 inputs that would most improve plan robustness if the user can supply them (typically: full response team roster + existing playbook materials).

MVI mode produces a deployable starter plan in ~45 minutes vs. ~6 hours for the full plan. The MVI output is sufficient for a small marketing team that needs a baseline standing plan before the first real incident; it is not sufficient for regulated industries (healthcare, finance, children, political) where the regulatory disclosure rules add an extra approval layer that must be fully mapped.

## Full Required Input

Provide the following for the highest-fidelity plan:

1. **Brand context** — Company, category, geographies served, regulated or sensitive attributes (health, finance, children, political)
2. **Top five risk scenarios** — Historical near-misses, competitor incidents, and category-specific risks the team already worries about
3. **Current monitoring stack** — Social listening, review aggregators, media monitors, AI-answer-engine audit tools if any
4. **Response team** — Named decision makers for legal, comms, product, executive sponsorship, and a primary + backup for each
5. **Channel ownership** — Who posts on X, LinkedIn, TikTok, Instagram, the blog, the press page, and who handles inbound media
6. **Existing holding statements or playbooks** — If any, so we extend rather than replace

## Instructions

You are a crisis-communications strategist's AI assistant. Your job is to produce a plan that a non-expert team can actually execute under pressure. Use plain language. Every recommendation specifies a trigger, an owner, a channel, and a success measure.

**Before you start — load `config.yml` and let it pre-fill the plan's named fields, not just the voice (a crisis plan with role placeholders where config already names real people is a plan that stalls at the moment it is needed most):**
- `team.roles` + leadership contacts — populate the response-team roster (Process Step 3) with the actual named primary + backup per role directly from config. Do not leave the roster with "[decision lead]" placeholders when config names the person; a plan the team has to fill in during the incident is a plan they will not finish in time. If config names fewer roles than the roster needs, carry the named ones through and flag only the genuinely-missing seats as `[ASSUMED]`.
- `risk_tier` / regulated-industry flags — a config-declared regulated or sensitive attribute (health, finance, children, political, or a named regulated customer segment) sets the plan's approval layer directly: add the mandatory legal + regulatory sign-off step to every Tier 2+ holding statement, raise the default classification floor for customer-data and disclosure incidents, and route the AI-disclosure category (Step 5, category 5) through the industry's specific notification rule. If config declares no regulated flag, state `[ASSUMED] general/unregulated profile` and note that adding the flag is the single highest-value personalization for this skill.
- `voice` (`always_use` / `never_use`) — the holding-statement templates (Step 4) must sound like the brand, so pass `voice` in as a hard prior: `never_use` phrases are a banned list the statements cannot contain even under time pressure, and `always_use` seeds the acknowledgment language. A statement that reads like generic PR erodes trust exactly when it is most fragile.
- `pricing` / product facts — where a scenario turns on a factual claim about the brand (a hallucinated-pricing or wrong-capability incident), config's canonical pricing and product facts are the ground truth the correction workflow asserts against; bind them so the canonical-page correction is written from the team's real numbers, not a placeholder.
- Consult `knowledge-base/regulations/` for any industry-specific disclosure or notification rules (healthcare, finance, children's products), and `knowledge-base/regulations/ai-content-disclosure.md` for the AI-provenance rules used in Step 5
- Consult `knowledge-base/best-practices/` for tone and escalation norms established in prior plans
- If the incident is live, note the timestamp and classify it before drafting — do not write a statement first and then reverse-engineer the severity

**Process:**

1. **Define the four tiers.** Write short, testable definitions for each:
   - **Tier 1 — Monitor.** Isolated negative mentions, within normal volume, no authority source, no legal exposure. Owner: community manager. Response: log + respond in channel if appropriate.
   - **Tier 2 — Elevated concern.** Cluster of 3+ negative mentions on the same issue in under 2 hours, OR one mention from a high-authority account (journalist, large creator, verified competitor employee), OR an AI-engine citation error about the brand. Owner: marketing lead + one deputy. Response: internal notice within 30 minutes; public channel post within 2 hours if warranted.
   - **Tier 3 — Active incident.** Issue is trending on at least one platform, local media is asking, customer impact is confirmed, OR a regulator has sent an inquiry. Owner: named response team per this plan. Response: holding statement within 90 minutes; full statement within 4 hours; executive sign-off required.
   - **Tier 4 — Crisis in progress.** National/international media coverage, viral social dynamics, potential safety or regulatory escalation, or synthetic-media attack. Owner: full response team + outside counsel if needed. Response: war-room cadence, pre-approved spokesperson, all channels coordinated.

2. **Map the monitoring signals to the tiers.** For each tier, list the specific triggers the team will actually see in their tools:
   - Mention-volume thresholds per platform (use last 90-day baseline as reference)
   - Authority thresholds (follower count, verified status, publication tier)
   - Sentiment-change thresholds (e.g., 15-point drop in rolling-7-day sentiment)
   - AI-specific signals: hallucinated claim in an AI answer engine, deepfake detection, competitor synthetic-audio attack, misattributed AI-generated content
   - Customer-impact signals: complaint volume, support ticket spike, refund requests, review-rating drop

3. **Assign the response team per tier.** A named primary and backup for each role — pre-filled from `config.yml` `team.roles` + leadership contacts wherever config names the person, so the roster ships populated rather than as a template the team completes mid-incident:
   - Decision lead (who calls the escalation)
   - Communications lead (writes the statement)
   - Legal review (gates wording for regulatory or liability)
   - Product/operations lead (provides factual grounding)
   - Executive sponsor (public-facing spokesperson if needed)
   - Channel owners (who posts where, in what order)

4. **Draft holding-statement templates.** Write a template for each of the top five risk scenarios (top three in MVI mode). Each holding statement follows this frame:
   - Acknowledgment of what happened in factual language (no defensiveness, no speculation)
   - What the brand is doing right now (investigating, pausing the campaign, notifying affected customers)
   - What the brand will share next and approximately when
   - Who to contact for more information
   - Explicit omissions: no blame, no legal admission, no promises beyond what can be kept
   - Approved by legal flag — who signs off before post

5. **Write an AI-era risk addendum.** Five categories to address (was four; the disclosure-compliance category added in v2.1):
   - **Hallucinated AI answers about the brand** — How the team monitors for factually wrong claims in AI Overviews, AI Mode, ChatGPT, Perplexity, Gemini, and Claude responses; correction workflow (owned-site canonical page direct-answer block, publisher corrections, structured-data updates, schema corrections, brand-code knowledge-base updates, platform abuse reports)
   - **Synthetic media attacks** — Deepfake executive videos, cloned spokesperson voices, AI-generated fake customer reviews; detection tools, response sequence, legal escalation path
   - **AI-generated content missteps** — The brand's own AI-generated asset has an error or offensive artifact; retraction workflow, human-review gate going forward, post-incident audit
   - **Brand-code corruption** — The brand's machine-readable knowledge base (per HBR May 2026 agentic marketing org framework) has been seeded with wrong claims, outdated pricing, or competitor-supplied data; the AI agents querying the brand code are now producing outputs based on bad inputs; rollback workflow, version-control discipline, brand-code-audit cadence
   - **AI-disclosure / provenance compliance failure** — The brand published AI-generated or AI-manipulated content without the disclosure or machine-readable provenance marking now required of it, OR an impact claim in a case study/ad turns out to be unverifiable or AI-doctored, OR **the ad platform rejected/paused the creative for undisclosed AI content or auto-applied an AI label the brand did not intend.** This is a *self-inflicted regulatory, delivery, and reputational* incident, distinct from the externally-driven attack categories above. Consult `knowledge-base/regulations/ai-content-disclosure.md` for the operative rules: EU AI Act Article 50 deployer disclosure duties + machine-readable marking (enforceable Aug 2, 2026; marking extension Dec 2, 2026; fines up to €15M / 3% of global turnover), the C2PA / SynthID provenance stack and its metadata-stripping fragility, California SB 942 / AB 853, the Cannes Lions creative-integrity precedent (mandatory AI disclosure + dual-layer verification + CEO/CMO sign-off as the template for an internal claim-verification and accountable-signer policy), and — the vector that bites first and hardest in practice — **platform-enforced disclosure** (Meta's mandatory AI-content labeling is live now, ahead of the Aug 2 regulation; the platform auto-labels from AI-tool telemetry and C2PA metadata, undisclosed AI content is a top-three ad-rejection reason, and Google/TikTok are moving the same direction). Workflow: identify the in-market assets out of compliance; for EU-reaching deepfake/synthetic-voice/public-interest-text assets, add the disclosure and re-export with provenance marks or pull the asset; for a platform rejection/mislabel, fix the disclosure at the creative level and re-submit, and confirm the corrected label after re-upload; for an unverifiable claim, correct or retract and publish the corrected source; document the gap and add the missing pre-publish gate (including the post-upload platform-label check) so it cannot recur

6. **Build the response playbooks.** For each top-five scenario (top three in MVI mode), produce a one-page playbook:
   - Scenario name and early-warning signals
   - Tier classification and escalation path
   - First 60 minutes (tasks + owners)
   - First 4 hours (tasks + owners)
   - First 24 hours (tasks + owners)
   - 72-hour and 2-week follow-through
   - Metrics to track (volume, sentiment, share of voice, search trend, AI citation sentiment, Share of Model)
   - Post-incident review prompts

7. **Design the exercise cadence.** Recommend a quarterly tabletop drill rotating through scenarios. Each drill produces:
   - Time-to-first-response metric
   - Decision-lead clarity (who called it, with what information)
   - Statement-approval latency
   - Gaps observed and owned follow-ups

8. **Define success metrics.** Per incident: time-to-triage, time-to-holding-statement, time-to-full-statement, sentiment recovery curve, share-of-voice return to baseline, Share of Model sentiment in AI engines, customer retention during and after, and whether the brand's correction was cited in coverage. Program-level: tier classification accuracy, drill-to-incident readiness, and percentage of scenarios with a tested playbook.

**Output requirements:**
- Tier definitions with specific triggers
- Monitoring signal map
- Named response team (primary + backup per role)
- Top-five scenario playbooks (top three in MVI mode)
- Five holding-statement templates (three in MVI mode)
- AI-era risk addendum (five categories)
- Quarterly exercise cadence
- Success metrics framework
- Assumptions, gaps, and regulatory flags
- Saved to `outputs/crisis/` if the user confirms

## Calibration Notes

- **Speed matters, but factual accuracy matters more.** A late, correct statement outperforms a fast, wrong one. Build the 90-minute holding-statement target around "acknowledgment + commitment to update," not around full factual explanation.
- **Do not write the full statement before the facts are known.** Holding statements exist precisely because the full picture takes time. Drafting a full statement on incomplete facts is the most common reason corrections are needed on the next news cycle.
- **Template language should sound like the brand, not like a legal notice.** Load brand-voice rules before drafting; a statement that sounds like generic PR erodes trust in a moment when trust is already fragile. Treat `config.yml` `voice.never_use` as a hard banned-phrase list the holding statements cannot contain even under deadline, and `voice.always_use` as the springboard for the acknowledgment line — the config is the voice prior, not a footnote.
- **The config is what makes this plan *this team's* plan.** A crisis plan's failure mode is being generic — a roster of placeholders, an approval layer that doesn't match the team's regulatory reality, statements in nobody's voice. Bind `config.yml` before drafting: `team.roles` + leadership contacts populate the roster so no seat is a `[decision lead]` placeholder the team scrambles to fill live; a config regulated/sensitive flag adds the mandatory legal + regulatory sign-off step and raises the classification floor for the incident classes that regulation touches; `voice` constrains the statement language. A plan the team has to personalize during the incident is a plan that arrives late.
- **Silence is a choice with consequences.** If the team decides to stay silent, document why, for how long, and what signal would change the decision. This prevents "paralysis by committee" drift.
- **AI-engine corrections are slow.** A factually wrong claim in an AI answer engine may take weeks to update even after the source is fixed. Plan for interim customer-facing correction content on owned channels.
- **Avoid the "thoughts and prayers" tone for business incidents.** Acknowledge, commit, update. Skip the rest.
- **The Tier 2 → Tier 3 jump is the most consequential classification decision.** Over-escalating Tier 2 to Tier 3 burns the response team and trains them to ignore the classification next time; under-escalating Tier 2 that should have been Tier 3 produces the catastrophic "we didn't see it coming" failure mode. The 90-day-baseline volume threshold + authority threshold + customer-impact-confirmed threshold are the three signals that resolve the Tier 2/3 ambiguity reliably.
- **Synthetic-media attacks are no longer theoretical.** Deepfake executive videos, cloned spokesperson voices, and AI-generated fake customer reviews are now mid-2026 production incidents in multiple industries. Detection tools (Reality Defender, Truepic, deepware, c2pa-validated provenance) must be in the monitoring stack, not an aspiration.
- **Brand-code corruption is the new Tier 2 category.** Per HBR May 2026, the machine-readable brand knowledge base that AI agents query is now central infrastructure; bad data in the brand code produces bad outputs across all AI-generated marketing assets. Version control + audit cadence + rollback workflow for the brand code must be in the plan.
- **AI-disclosure compliance is now a deadline-bound risk, not a brand-judgment call (added v2.1).** As of mid-2026 the requirement to disclose and provenance-mark AI-generated marketing content converged from three directions — EU AI Act Article 50 (enforceable Aug 2, 2026; machine-readable marking extension Dec 2, 2026; fines up to €15M / 3% of global turnover; extraterritorial, so any EU-reaching asset is in scope), the C2PA / SynthID provenance stack, and California SB 942 / AB 853 — plus the industry self-regulation precedent from Cannes Lions (mandatory AI disclosure + dual-layer verification + executive sign-off, with a Grand Prix revoked over an AI-doctored case study). Build the disclosure decision and provenance-marking step into the pre-publish gate now; the most preventable 2026 brand-safety incident is shipping unlabeled, unmarked AI content to an EU audience five weeks before the rule bites. Source of operative detail: `knowledge-base/regulations/ai-content-disclosure.md`.
- **The platform is now enforcing disclosure ahead of the regulation — so the disclosure gate is already live (added v2.3).** The most preventable mid-2026 disclosure incident is no longer "we shipped unlabeled AI content to an EU audience before Aug 2" — it is "the platform rejected our ad, or slapped an AI label on it we didn't choose, this week." Meta's mandatory AI-content labeling is live now: it auto-labels creative built with its own AI tools and reads C2PA metadata to detect third-party AI (Adobe generative fill, DALL·E, Canva AI), undisclosed AI content is a top-three ad-rejection reason, and Google/TikTok are tightening the same way. Two implications for the plan: (a) undisclosed AI is a *delivery* risk (rejected/paused campaign) that bites every advertiser on the platform regardless of EU reach, not only a regulatory-fine risk on the Aug 2 clock; (b) because the platform applies the label from tool telemetry and provenance metadata, add a **post-upload label check** to the pre-publish gate — confirm the applied label matches the brand's disclosure decision, because a surprise label or a missing label are both brand/delivery problems to catch before the campaign scales. Source of operative detail: `knowledge-base/regulations/ai-content-disclosure.md` §5.
- **Provenance metadata is fragile; don't rely on it alone.** Social upload pipelines, screenshots, and re-encodes routinely strip embedded C2PA manifests, so an asset can be "marked" at export and arrive unmarked at the audience. For anything you legally need to be able to prove later, pair C2PA signing with model-level watermarking (where supported) and a visible on-asset label, and keep an internal provenance log. Treat metadata as a signal, not proof.
- **Adopt the Cannes accountability model internally: disclose, verify, sign.** The festival's response to the AI-doctored-case-study fraud was to require AI-use disclosure, run dual-layer (AI-detection + human) verification, and put a named CEO/CMO signature on each entry. That is a clean internal template even for brands that never enter an award: every AI-touched asset and every impact claim should be disclosed, claim-verified against a named source/baseline before publish, and attested by a named accountable signer. An unverifiable performance claim is now an integrity incident, not a rounding error.
- **The first-60-minutes playbook is the most-rehearsed and most-skipped element.** Teams write the playbook, then forget to drill it. Quarterly tabletop drills are the discipline; the time-to-first-response metric is the gauge. A team with a great playbook and no drill is functionally a team with no playbook.
- **Pre-approved spokesperson list is non-negotiable for Tier 3+ incidents.** The "who speaks to media" question at Tier 3 must have been answered before the incident. Naming a spokesperson under crisis pressure for the first time guarantees a botched media interaction.
- **AI-engine citation accuracy is the new monitoring discipline.** A hallucinated claim that costs a customer a purchase decision is a Tier 2 trigger; two hallucinations in a rolling 7-day window is the escalation gate. Pair the AI Search Visibility Audit with this plan as the standing monitoring source.
- **Channel-pause discipline during active incident.** Social Media Calendar pauses at Tier 3+; pre-scheduled posts must be killable in under 15 minutes. A "looks tone-deaf next to the breaking news" social post is the most preventable Tier-3-becomes-Tier-4 amplifier.
- **Legal and comms must pre-negotiate the "acknowledgment vs. admission" line.** The most common Tier 3+ failure mode is comms wanting to acknowledge sooner than legal will allow, producing a 3–4 hour holding-statement delay that lets the news cycle define the brand's silence. Pre-negotiate the language template at quarterly drills, not in the live incident.
- **Post-incident reviews are the highest-ROI step.** Every closed incident adds a new scenario, a sharpened early-warning signal, and a refined holding-statement template. Teams that skip the review are paying the full cost of the incident without claiming the long-term learning value.
- **The at-a-glance table is the build order, not a menu (added v2.4).** Step 3's roster cannot name the right approval bar until step 1's tiers exist; step 6's playbooks are only as good as the step-2 signal map and the step-4 templates they route through. Building the AI-era addendum (step 5) before the tiers and roster exist produces a well-written document nobody can execute, because the escalation path it assumes doesn't exist yet. The single most common version of this error is a team that jumps straight to holding-statement templates because that feels like "the crisis plan" — and then discovers at the moment of the first real incident that nobody agreed who is allowed to approve one.
- **Tier 4 requires outside counsel involvement from the first hour.** Synthetic-media attacks, regulatory escalations, and viral viral-against-the-brand incidents have legal-exposure dimensions that internal counsel may be too close to the team to neutrally assess. The outside-counsel relationship must be on retainer or warm-contact basis before the first Tier 4 incident.

## Anti-Patterns to Avoid

- **Escalating everything to Tier 3 "just in case"** — burns the team and teaches them to ignore the classification next time
- **Holding statements written in passive voice** ("mistakes were made") — reads as evasion and amplifies the news cycle
- **Deleting negative posts or reviews** — in most cases this accelerates the story (Streisand effect is well-documented)
- **Over-apologizing for something the team has not yet confirmed happened** — locks in liability before the facts are established
- **Firing off an executive tweet before the response team has seen the facts** — the most common Tier-4-amplifier from inside the company
- **Letting the AI-answer correction workflow live in a single analyst's head** — if they are on vacation when a hallucination spreads, there is no plan; the workflow must be documented and a backup owner named
- **Writing playbooks but not drilling them** — a documented playbook with no rehearsal has roughly the same response-time performance as no playbook at all
- **Tier-1 monitoring without a named owner** — community-manager rotation gaps are the highest-frequency reason Tier 1 incidents incubate into Tier 3
- **Pre-scheduled social posts during active incidents** — Social Media Calendar pause at Tier 3+ is mandatory; pre-scheduled posts must be killable in under 15 minutes
- **Single-channel response when the incident is multi-channel** — if the issue is trending on X but only the LinkedIn response goes out, the silence on X is louder than the LinkedIn statement
- **Synthetic-media attacks treated as a theoretical risk** — deepfake executive videos and voice clones are now production incidents; the detection tool stack must be live, not on the roadmap
- **Brand-code corruption blind spot** — agentic marketing orgs (HBR May 2026) now have AI agents querying a machine-readable brand knowledge base; if the brand code is wrong, every AI-generated marketing asset is wrong; version control + audit cadence are mandatory
- **Shipping unlabeled, unmarked AI content to an EU audience** — treating AI disclosure as optional after EU AI Act Article 50 enforcement (Aug 2, 2026); the disclosure decision and C2PA/watermark provenance step must be in the pre-publish gate for any EU-reaching asset, with non-disclosure a documented deliberate call rather than an omission
- **Treating the Aug 2 deadline as the moment disclosure starts to matter** — the ad platforms are already enforcing it (Meta's mandatory labeling is live, undisclosed AI is a top-three ad-rejection reason, Google/TikTok tightening); a team waiting for the regulatory date is already behind its own platforms and risks rejected/paused campaigns now
- **Never checking the platform's applied AI label after upload** — Meta auto-labels from AI-tool telemetry and C2PA metadata, so an asset can be mislabeled (labeled on a trivial AI touch) or under-labeled (metadata stripped in the pipeline); a post-upload label check confirming the label matches the brand's disclosure decision belongs in the pre-publish gate
- **Publishing an unverifiable impact claim** — the Cannes case-study fraud showed an unbacked or AI-doctored performance claim is now an integrity incident; every claim needs a named source + baseline + accountable signer before publish

## Integration Notes

- **Pair with Brand Voice Guide Generator** — every template must sound like the brand, not like a legal department; the voice guide is the source of truth for tone calibration.
- **Pair with Social Media Calendar** — during an active incident, the calendar pauses at Tier 3+ and is replaced by a coordinated issue-specific post schedule; pre-scheduled posts must be killable in under 15 minutes.
- **Pair with AI Search Visibility Audit** — monitor AI-engine citation accuracy as a leading indicator of hallucination-based risk; two hallucinations in a rolling 7-day window is the Tier 2 escalation gate.
- **Pair with Competitive Analysis Brief** — competitor incidents are early-warning signals for the category; a competitor's Tier-3-becomes-Tier-4 incident is a free playbook stress-test for your team.
- **Pair with PR Pitch Builder** — Tier 3+ incidents require a coordinated proactive narrative; the pitch builder is the structural channel for the post-incident "what we learned and changed" story.
- **Pair with Persona & ICP Builder** — customer-impact signals are persona-specific; the persona roster identifies which segments are most exposed to which risks.
- **Pair with Multi-Channel Repurposer** — holding statements and full statements need channel-specific reformatting; the repurposer skill is the production line for the LinkedIn / X / blog / press-page variants.
- **Pair with Campaign Performance Narrator** — Tier 2+ incidents must be reflected in the executive performance narrative; the narrator skill incorporates incident-recovery metrics alongside campaign KPIs.
- **Feed post-incident reviews to the Knowledge Base** — every closed incident adds a new scenario and a sharpened early-warning signal; the knowledge base is the persistent learning loop.
- **Pair with Customer Review Insight Miner** — review-rating drops and complaint-keyword spikes are leading indicators of customer-impact severity; the insight miner is the data source for the customer-impact-confirmed gate.

## Example Output

### Threadline (B2B RevOps SaaS) Crisis Plan — Q2 2026 Baseline (excerpt)

**Brand context:** Threadline, B2B RevOps SaaS, US + EU primary markets, no regulated industry exposure (general enterprise software).
**Top five scenarios:** (1) AI-engine hallucinated claim about Threadline pricing or capabilities; (2) Customer data exposure incident; (3) Executive social-media post controversy; (4) Synthetic-audio deepfake of CEO during a quarterly investor call; (5) Brand-code corruption producing wrong-pricing claims across all AI-generated assets.

#### Tier Definitions with Specific Triggers (excerpt — Tier 2 shown)

**Tier 2 — Elevated concern.** Internal notice within 30 minutes; public channel post within 2 hours if warranted. Marketing lead + one deputy owns. Specific triggers:
- Cluster of 3+ negative mentions on the same issue within 2 hours on any single platform (90-day baseline: 0.4 negative mentions/2-hour window on X; 0.2 on LinkedIn)
- One mention from a high-authority account: journalist at a tier-1 trade press outlet (MarTech Today, MarTech.org, SaaStr), creator with >50K followers in the RevOps beat, or a verified competitor employee at director-level or above
- AI-engine citation error about Threadline: a hallucinated claim about pricing, capability, or customer outcome surfaced in any of the top 5 engines (ChatGPT, Perplexity, Gemini, AI Overviews, Claude)
- Sentiment-change threshold: 15-point drop in rolling-7-day sentiment score on social listening tool
- Customer-impact signal: 25%+ spike in support tickets referencing a single issue in a 24-hour window; review-rating drop of 0.3+ on G2 / TrustRadius in a 7-day window
- Brand-code corruption: any team member or external reviewer flags that the machine-readable brand knowledge base contains an outdated or wrong claim

#### Sample Tier-2 Scenario — AI Answer Engine Hallucination

**Early-warning signals:** Support ticket referencing a feature Threadline doesn't have; a customer screenshot of ChatGPT or Perplexity recommending Threadline based on wrong facts; the quarterly AI Search Visibility Audit flags a claim-accuracy issue.

**Triggers:** Two confirmed hallucinated claims in a rolling 7-day window, OR one hallucination that caused a customer purchase decision we can attribute, OR a hallucinated claim about pricing surfaced on AI Mode (highest-conversion AI surface per Seer 2026 data).

**First 60 minutes:**
- Community manager captures screenshots, timestamps, query prompts, engine, model version, and customer-impact evidence (if any)
- Marketing lead confirms the underlying on-site canonical content is accurate and extractable (entity clarity, direct-answer block, FAQ schema)
- Communications lead drafts a 120-word clarification post on the owned site's canonical page with an explicit contradiction of the hallucinated claim
- Product lead confirms which version of the brand-code knowledge base produced the corrupted output (if internally sourced)

**First 4 hours:**
- Canonical page is updated with a direct-answer paragraph that contradicts the hallucination explicitly (Conductor 2026: cited-source freshness 2.4× lift)
- Schema is validated (FAQPage / Article / Product); structured-data markup deployed
- Publishers with citation-share are contacted via their correction forms (and given the corrected source URL)
- Brand-code knowledge base is audited for the underlying source error; version increment + change-log entry; rollback to last known-good version if needed
- If the hallucination mentions a competitor or third party falsely, they are notified
- AI Search Visibility Audit re-query scheduled for 24h, 7d, 30d to track propagation

**First 24 hours:**
- Re-query the five major engines and log whether the correction has propagated; tier-2 metric: 60% propagation in 24h on Claude + ChatGPT; 30%+ on Perplexity + Gemini; AI Overviews + AI Mode tracked as slower-moving surfaces
- Post a customer-facing LinkedIn note if the hallucination reached customers (target audience: existing customers and prospects in active eval)
- Update the AI-era risk-addendum scenario log with the new instance for the quarterly review

**72-hour and 2-week follow-through:**
- Track re-query hallucination rate at 7d / 30d; if not propagated by 30d, escalate to platform abuse report (each engine has a different correction-form path; the workflow doc lists all five)
- Post-incident review prompts: which signal would have caught this earlier; was the brand-code version that produced the corruption flagged in the prior brand-code audit; is the 7-day rolling window the right detection cadence

**Metrics to track:**
- Time from signal to canonical-page update (target: <60 min)
- Re-query hallucination rate at 24h / 7d / 30d (target propagation: 60% / 80% / 95%)
- Customer-support ticket volume mentioning the wrong claim (target: zero new tickets after Day 7)
- Share of Model accuracy for the relevant query cluster (re-baselined at 30d via AI Search Visibility Audit)
- Brand-code version control: was the corrupted version caught by the brand-code audit cadence? (binary; informs cadence tuning)

#### Sample Holding Statement — Synthetic-Audio Deepfake of CEO (Tier 4 scenario template)

> We are aware that an audio recording purporting to be [CEO name] is circulating that does not reflect the views or statements of [CEO name] or Threadline. We have confirmed with our internal forensic review and an external authentication provider ([Reality Defender / Truepic / c2pa-validated tool]) that the audio is synthetic. We have notified the platforms where the audio is circulating and are working to have it removed. We will share a full update by [specific time, same business day]. Customers and partners with questions can reach us at [contact]. We will post updates at [URL].

*Approval required from: legal (primary + outside counsel), executive sponsor (CEO + Board chair). Do not deviate without same approvers. Use only after forensic authentication is complete; do not pre-publish a denial before the synthetic-audio confirmation is verified by an external provider.*

#### AI-Era Risk Addendum (excerpt — fourth category, brand-code corruption)

**Category 4 — Brand-code corruption.** The machine-readable brand knowledge base (per HBR May 2026 agentic marketing org framework) is now central infrastructure; AI agents query the brand code when generating any marketing asset. Corruption modes:

- Outdated pricing or packaging claims persist in the brand code after a product update
- A competitor-supplied data point was ingested without verification and is now being cited as a Threadline first-party claim
- A persona or ICP description in the brand code was updated but the named-customer references were not; AI-generated assets are now naming wrong customers as exemplars
- A regulatory or compliance-language update was applied to legal-page content but not to the brand-code template library; AI-generated assets are using stale compliance language

**Rollback workflow:**
- Brand-code knowledge base is version-controlled with semantic versioning (major.minor.patch) and a change log per version
- Audit cadence: monthly random-sample audit (10 fields/month); quarterly full-coverage audit; ad-hoc audit triggered by any Tier 2+ incident
- Rollback gate: any AI-generated asset citing the corrupted field is paused; rollback to last known-good version is one-click in the brand-code platform; re-generation of paused assets begins after the rollback is verified
- Detection tools: brand-code lint rules (pricing-claim format, customer-name allow-list, regulatory-language matchers); automated flagging of any AI-generated asset that cites a field flagged as "in audit"
- Owner roster: brand-code owner (primary + backup) named; brand-code audit owner (primary + backup) named; AI-generated-asset-pause owner named per channel

**Response sequence (Tier 2 brand-code corruption):**
- T+0: Brand-code owner version-rollbacks to last known-good version; affected AI-generated assets are paused
- T+1h: Communications lead drafts an internal-only note for the team explaining the rollback and the assets paused
- T+4h: Re-generation of paused assets begins; QA gate added to ensure the rolled-back version is being queried
- T+24h: Quarterly-audit-cycle accelerated for the affected field domain; root-cause analysis (which audit cadence failed; which lint rule was missing)
- T+72h: Post-incident review; brand-code audit cadence tuned; new lint rule added if the corruption mode was novel

#### Quarterly Exercise Cadence (excerpt)

- **Q2 2026 drill (June 12):** Tier 3 — Customer data exposure incident. Time-to-first-response target: 60 minutes from signal to internal incident commander assigned. Drill output: decision-lead clarity, statement-approval latency, gaps observed and owned follow-ups.
- **Q3 2026 drill (Sep 12):** Tier 4 — Synthetic-audio deepfake of CEO during an investor call. Includes outside-counsel-warm-contact rehearsal and forensic-authentication-tool live test.
- **Q4 2026 drill (Dec 12):** Tier 2 — Brand-code corruption with downstream AI-generated asset spread. Includes rollback workflow rehearsal and brand-code audit cadence stress-test.

#### Assumptions, Gaps, Regulatory Flags

- `[ASSUMED]` US + EU primary markets is the geography scope; if Threadline expands to APAC, the EU GDPR + UK DPA + APAC privacy regulatory frame must be re-mapped before that market launches
- `[ASSUMED]` General enterprise software regulatory profile (no healthcare, finance, children, political exposure); revisit if Threadline lands a regulated-industry customer that imposes its own disclosure rules
- **Gap:** Outside-counsel-warm-contact relationship not yet on retainer; recommend establishing before Q3 2026 drill
- **Gap:** Synthetic-media detection tool stack (Reality Defender / Truepic / c2pa-validated provenance) recommended for evaluation in Q2; not yet in monitoring stack
- **Regulatory flag:** No HIPAA / PCI / COPPA exposure currently; re-evaluate if Threadline's customer mix shifts to include healthcare / payments / under-13 user data
