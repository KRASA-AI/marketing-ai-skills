---
name: "Brand Safety & Crisis Response Planner"
category: operations
tools: [claude, chatgpt]
difficulty: advanced
time_saved: "~6 hrs/plan + faster response"
version: 1.0
last_eval_score: null
---

# 🛡️ Brand Safety & Crisis Response Planner

## Purpose

Produce a tiered crisis-response plan that covers real-time monitoring signals, escalation triggers, decision roles, holding-statement templates, channel-specific response playbooks, and an AI-era risk addendum covering hallucinated AI-generated claims, model-citation errors, and synthetic-media incidents. Designed for marketing leaders who own external communications but do not have a dedicated crisis comms team.

The 2026 shift this plan absorbs: the window between "small incident" and "full reputation event" has compressed from days to hours, and AI answer engines now generate claims about brands that can be wrong in ways the brand did not create and cannot directly edit.

## When to Use

Use this skill proactively — before a crisis — to build a standing plan. Use it reactively during an incident to classify severity, assemble the response team, and draft holding statements against pre-approved templates. Use it quarterly to refresh scenarios, test the tiering, and audit which playbooks have been exercised in the last 12 months.

Do not use for ordinary customer-complaint handling; review-response playbooks live in the customer-service skill set. This is for incidents that could cross into earned-media, regulatory, or paid-media safety territory.

## Required Input

Provide the following:

1. **Brand context** — Company, category, geographies served, regulated or sensitive attributes (health, finance, children, political)
2. **Top five risk scenarios** — Historical near-misses, competitor incidents, and category-specific risks the team already worries about
3. **Current monitoring stack** — Social listening, review aggregators, media monitors, AI-answer-engine audit tools if any
4. **Response team** — Named decision makers for legal, comms, product, executive sponsorship, and a primary + backup for each
5. **Channel ownership** — Who posts on X, LinkedIn, TikTok, Instagram, the blog, the press page, and who handles inbound media
6. **Existing holding statements or playbooks** — If any, so we extend rather than replace

## Instructions

You are a crisis-communications strategist's AI assistant. Your job is to produce a plan that a non-expert team can actually execute under pressure. Use plain language. Every recommendation specifies a trigger, an owner, a channel, and a success measure.

**Before you start:**
- Load `config.yml` for brand voice, approved talking points, legal-sensitive topics, regulated phrasing, and leadership contacts
- Consult `knowledge-base/regulations/` for any industry-specific disclosure or notification rules (healthcare, finance, children's products)
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

3. **Assign the response team per tier.** A named primary and backup for each role:
   - Decision lead (who calls the escalation)
   - Communications lead (writes the statement)
   - Legal review (gates wording for regulatory or liability)
   - Product/operations lead (provides factual grounding)
   - Executive sponsor (public-facing spokesperson if needed)
   - Channel owners (who posts where, in what order)

4. **Draft holding-statement templates.** Write a template for each of the top five risk scenarios. Each holding statement follows this frame:
   - Acknowledgment of what happened in factual language (no defensiveness, no speculation)
   - What the brand is doing right now (investigating, pausing the campaign, notifying affected customers)
   - What the brand will share next and approximately when
   - Who to contact for more information
   - Explicit omissions: no blame, no legal admission, no promises beyond what can be kept
   - Approved by legal flag — who signs off before post

5. **Write an AI-era risk addendum.** Three categories to address:
   - **Hallucinated AI answers about the brand** — How the team monitors for factually wrong claims in AI Overviews, ChatGPT, Perplexity, Gemini, and Claude responses; correction workflow (owned-site canonical page, publisher corrections, structured-data updates, schema corrections, platform abuse reports)
   - **Synthetic media attacks** — Deepfake executive videos, cloned spokesperson voices, AI-generated fake customer reviews; detection tools, response sequence, legal escalation path
   - **AI-generated content missteps** — The brand's own AI-generated asset has an error or offensive artifact; retraction workflow, human-review gate going forward, post-incident audit

6. **Build the response playbooks.** For each top-five scenario, produce a one-page playbook:
   - Scenario name and early-warning signals
   - Tier classification and escalation path
   - First 60 minutes (tasks + owners)
   - First 4 hours (tasks + owners)
   - First 24 hours (tasks + owners)
   - 72-hour and 2-week follow-through
   - Metrics to track (volume, sentiment, share of voice, search trend, AI citation sentiment)
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
- Top-five scenario playbooks
- Five holding-statement templates (one per scenario)
- AI-era risk addendum (three categories)
- Quarterly exercise cadence
- Success metrics framework
- Assumptions, gaps, and regulatory flags
- Saved to `outputs/crisis/` if the user confirms

## Calibration Notes

- Speed matters, but factual accuracy matters more. A late, correct statement outperforms a fast, wrong one. Build the 90-minute holding-statement target around "acknowledgment + commitment to update," not around full factual explanation.
- Do not write the full statement before the facts are known. Holding statements exist precisely because the full picture takes time.
- Template language should sound like the brand, not like a legal notice. Load brand-voice rules before drafting; a statement that sounds like generic PR erodes trust in a moment when trust is already fragile.
- Silence is a choice with consequences. If the team decides to stay silent, document why, for how long, and what signal would change the decision. This prevents "paralysis by committee" drift.
- AI-engine corrections are slow. A factually wrong claim in an AI answer engine may take weeks to update even after the source is fixed. Plan for interim customer-facing correction content on owned channels.
- Avoid the "thoughts and prayers" tone for business incidents. Acknowledge, commit, update. Skip the rest.

## Example Output

### Sample Tier-2 Scenario — AI Answer Engine Hallucination

**Early-warning signals:** Support ticket referencing a feature the product doesn't have; a customer screenshot of ChatGPT or Perplexity recommending the brand based on wrong facts.

**Triggers:** Two confirmed hallucinated claims in a rolling 7-day window, OR one hallucination that caused a customer purchase decision we can attribute.

**First 60 minutes:**
- Community manager captures screenshots, timestamps, query prompts, and which engine produced it
- Marketing lead confirms the underlying on-site content is accurate and extractable
- Communications lead drafts a 120-word clarification post on the owned site's canonical page

**First 4 hours:**
- Canonical page is updated with a direct-answer paragraph that contradicts the hallucination explicitly
- Schema is validated (FAQPage / Article / Product)
- Publishers with citation-share are contacted via their correction forms
- If the hallucination mentions a competitor or third party falsely, they are notified

**First 24 hours:**
- Re-query the five major engines and log whether the correction has propagated
- Post a customer-facing LinkedIn note if the hallucination reached customers

**Metrics:** Time from signal to canonical-page update, re-query hallucination rate at 24h / 7d / 30d, customer-support ticket volume mentioning the wrong claim, Share of Model accuracy for the relevant query cluster.

### Sample Holding Statement — Product Safety Incident

> We are aware of reports regarding [issue] with [product]. We have paused [shipment / campaign / order flow] while we investigate. Customer safety is our first priority, and we will share a full update by [specific time, same business day if possible]. Customers with questions can reach us at [contact]. We will post updates at [URL].

*Approval required from: legal, operations, executive sponsor. Do not deviate without same approvers.*

## Integration Notes

- **Pair with Brand Voice Guide Generator** — every template must sound like the brand, not like a legal department.
- **Pair with Social Media Calendar** — during an active incident, the calendar pauses and is replaced by a coordinated issue-specific post schedule.
- **Pair with AI Search Visibility Audit** — monitor AI-engine citation accuracy as a leading indicator of hallucination-based risk.
- **Feed post-incident reviews to the Knowledge Base** — every closed incident adds a new scenario and a sharpened early-warning signal.

## Anti-Patterns to Avoid

- Escalating everything to tier 3 "just in case" — it burns the team and teaches them to ignore the classification next time
- Holding statements written in passive voice ("mistakes were made")
- Deleting negative posts or reviews — in most cases this accelerates the story
- Over-apologizing for something the team has not yet confirmed happened
- Firing off an executive tweet before the response team has seen the facts
- Letting the AI-answer correction workflow live in a single analyst's head — if they are on vacation when a hallucination spreads, there is no plan
