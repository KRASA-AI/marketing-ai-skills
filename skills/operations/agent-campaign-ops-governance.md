---
name: "Agent-Controlled Campaign Ops & MCP Governance"
category: operations
tools: [claude, chatgpt]
difficulty: advanced
time_saved: "~5 hrs/setup + ongoing risk avoidance"
version: 1.0
last_eval_score: null
---

# 🎛️ Agent-Controlled Campaign Ops & MCP Governance

## Purpose

Produce a governance-and-operations playbook for running paid-media campaigns through AI agents connected to ad platforms over MCP (Model Context Protocol). The deliverable covers connector selection (official vs. third-party), permission scoping, a graduated read-only → human-in-the-loop → autonomous rollout, spend guardrails, an approval matrix, an audit trail standard, an incident kill-switch, and a natural-language campaign-brief template that turns a structured brief into agent-executable instructions across one or more platforms.

The 2026 shift this skill absorbs: as of mid-2026, the campaign-management interface is no longer only the platform UI. Google shipped its official read-only Ads MCP (April 28, 2026); Meta shipped its official campaign-management MCP one day later (April 29); and within weeks the ecosystem filled in with cross-platform third-party connectors (Google / Meta / TikTok / LinkedIn / Amazon / Microsoft routers) that add write capability — campaign creation, budget edits, ad-set activation, bid changes — through a plain-English agent prompt. The optimization unit moves from "navigate the Ads Manager UI" to "write a brief the agent executes," which makes the brief, the brand code, and the structured offer attributes the load-bearing inputs — and makes connector governance a first-class marketing risk, not an IT afterthought.

This skill is the governance answer to that shift. It does not replace the brief-writing skills (Creative Brief Generator) or the measurement skills (Cross-Channel Attribution Analyzer); it sits between them and the live ad account, defining who is allowed to let an agent touch spend, under what scope, with what controls, and how an incident gets stopped in under five minutes.

## When to Use

Use this skill before connecting any ad account to an AI agent over MCP — the governance plan should exist before the first connector is authorized, not after the first incident. Use it when evaluating which connector to adopt (official platform MCP vs. third-party wrapper vs. cross-platform router). Use it when expanding an existing agent from read-only reporting to write-capable execution. Use it quarterly to re-audit scopes, rotate credentials, and confirm the kill-switch still works. Use it on demand when a new platform ships an MCP surface and the team wants to bring it into the same governance frame rather than improvising per-platform rules.

Do not use this skill to write the campaign creative or the offer strategy — that is the Creative Brief Generator and Ad Copy Variations. Do not use it as a substitute for the platform's own billing controls; it layers on top of them. This is for the operating discipline around agent-mediated campaign execution.

## Minimum Viable Input

If the user provides only the three fields below, proceed immediately and tag every assumption `[ASSUMED]`:

1. **Platforms + connector type** — Which ad platforms (e.g., "Google Ads + Meta") and whether using the official platform MCP, a named third-party connector, or undecided
2. **Monthly spend at risk** — Approximate total monthly spend on the accounts that would be agent-connected (sets the guardrail tier)
3. **Approver** — Who signs off on spend changes above a threshold (named primary)

When running in MVI mode: assume the official platform MCP where one exists and flag third-party alternatives only where official lacks write capability; recommend a conservative default guardrail set scaled to the stated spend; produce the connector-selection note + permission-scope table + three-phase rollout + spend-guardrail set + a one-page approval matrix + the kill-switch procedure + one natural-language campaign-brief template; skip the full audit-trail schema and the per-platform scope deep-dive (recommend a 30-minute follow-up); flag at the bottom the top 2 inputs that would most improve the plan (typically: the named connector vendor's permission model + the existing billing-control configuration).

MVI mode produces a deployable starter governance plan in ~45 minutes vs. ~5 hours for the full plan. The MVI output is sufficient for a small team connecting one or two accounts; it is not sufficient for an agency managing many client accounts under one connector, where per-client scope isolation and client-consent documentation add a layer that must be fully mapped.

## Full Required Input

Provide the following for the highest-fidelity plan:

1. **Platforms + accounts** — Every ad platform and account ID that would be agent-connected, with monthly spend per account
2. **Connector inventory** — Official platform MCPs, third-party connectors, and cross-platform routers under evaluation or already in use, with their stated permission models
3. **Team + roles** — Who writes briefs, who can authorize a connector, who approves spend changes, who owns the kill-switch, primary + backup for each
4. **Current billing controls** — Account-level budget caps, payment-method limits, alerting thresholds already configured at the platform
5. **Risk profile** — Regulated category, agency-vs-in-house, client-account isolation needs, prior connector incidents
6. **Existing SOPs** — Any current campaign-launch or change-approval process, so we extend rather than replace

## Instructions

You are a marketing-operations and risk strategist's AI assistant. Your job is to produce a governance plan a non-technical marketing team can actually run, that lets them capture the speed of agent-controlled campaign ops without exposing the budget to an un-gated agent. Use plain language. Every control specifies a trigger, an owner, a scope, and a recovery step.

**Before you start:**
- Load `config.yml` for brand voice, approved offer attributes, spend authority levels, and leadership contacts
- Consult `knowledge-base/regulations/` for any category-specific advertising disclosure rules that constrain autonomous creative generation
- Consult `knowledge-base/best-practices/` for prior connector-governance decisions and any logged incidents
- Establish the read/write capability of each connector under consideration before recommending a rollout phase — an official read-only MCP and a write-capable third-party wrapper carry very different risk

**Process:**

1. **Select the connector per platform.** For each platform, classify the available connectors and recommend one:
   - **Official platform MCP** — published by the ad platform, platform-hosted auth, no credential paste. Lowest account-suspension risk. May be read-only (reporting / diagnostics) in its first release.
   - **Verified third-party connector** — an app that passed the platform's app review with scoped permissions. Moderate risk; adds write capability the official MCP may lack.
   - **Unverified / community connector** — convenient and often broad-scoped, but the highest account-suspension and data-exposure risk; community connectors have triggered account bans. Default recommendation: do not connect a spend-capable account through an unverified connector.
   - **Cross-platform router** — a single connector exposing several platforms' tools at once. Convenient for multi-platform teams but concentrates risk; if it is compromised or mis-scoped, every connected account is exposed. Recommend extra scope discipline and a separate audit cadence.

2. **Scope the permissions.** Build a permission-scope table: for each connector, the minimum tool set required for the job, and an explicit deny-list of tools that are not needed (and so should not be granted). Default to read-only scopes wherever the job is reporting or diagnostics; grant write scopes (budget edits, campaign creation, bid changes) only when the rollout phase justifies them and the guardrails below are live.

3. **Design the three-phase rollout.** Do not start agents in autonomous-write mode:
   - **Phase 1 — Read-only.** Agent reads and reports only (performance pulls, anomaly flags, recommendation drafts). No mutation tools granted. Run for a defined window to build trust in the agent's judgment against known-good human decisions.
   - **Phase 2 — Human-in-the-loop write.** Agent proposes changes (budget shifts, new ad sets, bid adjustments) but a named human approves each before it goes live. Mutation tools are granted but a human-approval step gates every spend-affecting action.
   - **Phase 3 — Bounded autonomy.** Agent executes a defined class of low-risk changes within hard limits (e.g., budget moves under a fixed dollar / percentage cap, within an approved campaign set) without per-action approval; everything outside the bounds reverts to Phase 2 approval. Most teams should keep high-stakes actions (new campaign launch, budget increases above the cap, audience expansion, creative changes) in Phase 2 indefinitely.

4. **Set the spend guardrails.** Hard limits that exist independent of the agent's judgment:
   - Account-level budget cap configured at the platform billing layer (the agent cannot exceed it even if instructed to)
   - Per-action change cap (max dollar / percentage budget move the agent can make without escalation)
   - Daily cumulative-change cap (max total change across all actions in 24 hours before a freeze)
   - New-spend-surface gate (any new platform, new campaign type, or new audience requires human authorization regardless of phase)
   - Anomaly auto-pause threshold (spend velocity or CPA drift beyond a band triggers an automatic pause + alert)

5. **Build the approval matrix.** A one-page table mapping action class → required approver → phase:
   - Reporting / analysis: no approval (any phase)
   - Budget change within per-action cap: Phase 2 named approver; Phase 3 no approval if within bounds
   - Budget change above cap, new campaign, audience expansion, creative change: named approver in every phase
   - Connector authorization / scope change: connector-authorization owner (a deliberately small list)
   - The matrix names a primary and backup for each approver so no action is blocked by one person's absence

6. **Define the audit-trail standard.** Every agent action against a live account is logged with: timestamp, connector, account, tool called, parameters (before / after values for any mutation), the brief or prompt that triggered it, the approver (if Phase 2), and the outcome. The log is reviewable by someone other than the person who ran the agent. Specify where the log lives and the review cadence (recommend weekly for Phase 2/3 accounts).

7. **Write the kill-switch procedure.** A step-by-step incident-stop that any named owner can execute in under five minutes: deactivate the connector / revoke the MCP authorization at the platform, pause affected campaigns via the platform UI (independent of the agent), freeze the payment method if spend is runaway, notify the approval owners, and capture the audit log for the post-incident review. The kill-switch must be tested, not just documented — a quarterly drill confirms the named owner can actually execute it.

8. **Produce the natural-language campaign-brief template.** The structured brief that turns marketing intent into agent-executable instructions: objective + KPI, platforms + accounts in scope, budget + the hard cap, audience / matching guidance, messaging guidelines (including any "never say" constraints — e.g., no price claims, no scarcity / countdown framing per the agent-shopping-surface calibration), creative source (asset library location or generation instruction), the phase this brief runs under, and the approver. The template makes the brief auditable and repeatable rather than an ad-hoc chat message.

**Output requirements:**
- Connector-selection note (per platform, with the recommended connector and why)
- Permission-scope table (granted tools + deny-list per connector)
- Three-phase rollout plan with phase-exit criteria
- Spend-guardrail set (with specific numbers scaled to the account)
- One-page approval matrix (primary + backup per approver)
- Audit-trail standard (fields, location, review cadence)
- Kill-switch procedure (under-five-minute, testable)
- Natural-language campaign-brief template
- Assumptions, gaps, and risk flags
- Saved to `outputs/campaign-ops/` if the user confirms

## Calibration Notes

- **Official-first, write-second.** Prefer the official platform MCP for any account that touches spend; it carries the lowest account-suspension risk because the platform hosts the auth and scopes the tools. Where the official MCP is read-only (Google's first release exposed only account listing and query tools — reporting and diagnostics, no mutation), keep the agent in reporting mode on that platform and do not reach for an unverified write-capable connector just to get mutation; the convenience is not worth the ban risk on a spend account.
- **Read-only is a destination, not just a phase.** Many high-value agent use cases (anomaly detection, daily performance narration, budget-pacing alerts, AEO-citation-adjacent reporting) never need write access at all. Do not grant mutation scopes the job does not require; the most defensible governance posture for a large share of accounts is permanent Phase 1.
- **The per-action cap is the single most important number.** A budget cap at the billing layer prevents catastrophe; the per-action change cap prevents the slow bleed of many small agent mistakes. Set it deliberately, scaled to the account's daily spend, before any write scope is granted.
- **Cross-platform routers concentrate risk.** A single connector exposing Google + Meta + TikTok + LinkedIn at once is operationally convenient and a larger blast radius if mis-scoped or compromised. If a team adopts one, the scope discipline and audit cadence should be stricter than for single-platform official MCPs, not looser.
- **No-developer-credentials is a feature and a risk.** Platform-hosted auth with no token paste lowers the setup barrier — which is exactly why the connection should still pass through the connector-authorization owner, not be self-serve for any team member. Ease of connection is not a reason to skip the authorization gate.
- **Briefs are the new load-bearing input.** When campaign execution moves to natural-language briefs, the brand code, structured offer attributes, and "never say" constraints do more work than the Ads Manager click path ever did. A vague brief produces a vague (or wrong) campaign faster than a human would have made the same mistake. The brief template is a control, not paperwork.
- **Carry the agent-shopping-surface copy calibration into the brief.** Briefs that generate ads for agent-mediated or AI-conversation surfaces should drop scarcity badges, countdown timers, and strikethrough framing as the default (these are penalized on the agent-completes-the-purchase surface per the May 2026 HBR shopping-agent research) and lead with star-rating prominence, price clarity, and verified-review density instead. The brief's messaging-guidelines field is where this rule lives.
- **The kill-switch is worthless undrilled.** A documented incident-stop that no one has executed has roughly the response-time performance of no plan at all. The quarterly drill (revoke the connector, confirm spend actually stops, confirm the named owner could do it without help) is the discipline that makes the rest of the plan real.
- **Agency multi-account isolation is a distinct problem.** One connector across many client accounts needs per-client scope isolation, per-client consent documentation, and a per-client kill-switch — a single compromised connector cannot be allowed to expose every client's budget. Agencies should treat each client account as its own governance instance.
- **Re-audit on every new platform MCP.** The MCP ad-surface landscape is expanding fast; each new platform that ships a connector should be brought into the same governance frame (connector selection → scope → phase → guardrails → audit → kill-switch) rather than improvised. The plan is a template to re-run, not a one-time document.
- **Log the prompt, not just the action.** When a mutation is logged, the brief or prompt that triggered it is the most useful field for the post-incident review — it is the difference between "the agent raised the budget" and "the agent raised the budget because the brief said 'scale aggressively' with no cap." The prompt-to-action link is the audit trail's highest-value column.

## Anti-Patterns to Avoid

- **Connecting a spend account through an unverified community connector** — the convenience is real and so is the account-ban and data-exposure risk; spend accounts go through official or verified-scoped connectors only
- **Starting agents in autonomous-write mode** — skipping the read-only and human-in-the-loop phases to "move fast" is how the first runaway-budget incident happens; phases exist to build trust against known-good decisions first
- **Granting broad scopes "to be safe"** — over-scoping is the opposite of safe; grant the minimum tool set the job needs and deny-list the rest
- **Relying on the agent's judgment instead of a hard cap** — agent reasoning is not a budget control; the billing-layer cap and the per-action cap must exist independent of anything the agent decides
- **Self-serve connector authorization** — no-credential platform-hosted auth makes it tempting to let any team member connect an account; connector authorization belongs to a deliberately small named list
- **A kill-switch no one has tested** — documenting the incident-stop without drilling it is the most common reason it fails in the live incident
- **One connector across many client accounts with no isolation** — an agency that lets a single mis-scoped connector touch every client's budget has built a single point of catastrophic failure
- **Vague briefs into write-capable agents** — "scale this up" with no cap, no platform scope, and no messaging constraints is an instruction to make a fast expensive mistake; the structured brief template is mandatory for any Phase 2/3 action
- **Audit logs that only the operator can read** — if the person who ran the agent is the only one who can review what it did, there is no audit; the log must be reviewable by someone else on a set cadence
- **Treating each new platform MCP as a fresh improvisation** — every new connector goes through the same governance template; per-platform ad-hoc rules are how scopes and guardrails drift out of sync

## Integration Notes

- **Pair with Creative Brief Generator** — the campaign-brief template here is the execution wrapper; the Creative Brief Generator produces the messaging, audience, and offer content that fills the brief's fields, including the "never say" constraints that carry into agent-generated creative.
- **Pair with Brand Safety & Crisis Response Planner** — the kill-switch and incident-stop here are the operational counterpart to the crisis plan's agent-controlled-execution governance addendum; a runaway-spend or rogue-creative incident is a Tier 2/3 event that both skills should reference the same kill-switch for.
- **Pair with Cross-Channel Attribution Analyzer** — agent-executed budget moves change the spend mix faster than human cadence; the attribution analyzer should ingest the audit trail so reallocation analysis reflects what the agent actually did, and so agent-mediated changes are not analyzed on the same plane as deliberate human reallocations.
- **Pair with Campaign Performance Narrator** — the audit trail is a natural input to the executive performance narrative; "what the agent changed and why" belongs in the narration alongside the KPI movement.
- **Pair with Agentic Commerce Optimizer** — the structured offer attributes (feed completeness, schema, trust signals, price clarity) that the optimizer maintains are the inputs the campaign brief references; the same catalog hygiene now feeds both the agentic-commerce surface and the agent-executed paid campaign.
- **Pair with Ad Copy Variations** — variant copy generated for an agent-executed campaign should already reflect the agent-shopping-surface calibration (no scarcity / countdown default on agent-mediated surfaces); the two skills share the messaging-guidelines constraint set.
- **Pair with Brand Voice Guide Generator** — agent-generated creative is only as on-brand as the brand code it queries; the voice guide is the source of truth the brief points the agent at.
- **Feed connector incidents and drill results to the Knowledge Base** — every connector incident, scope mistake, and kill-switch drill adds a sharpened control; the knowledge base is the persistent learning loop for the governance template.

## Example Output

### Northbeam Outdoor (DTC apparel, ~$120K/mo paid) — Agent Campaign Ops Governance Plan (MVI excerpt)

**Inputs (MVI):** Platforms — Google Ads + Meta. Connector type — undecided. Monthly spend at risk — ~$120K. Approver — VP Growth (primary), Growth Lead (backup).

#### Connector-Selection Note

- **Google Ads:** Use the **official Google Ads MCP** (read-only in its current release — account listing + query tools only). Run Google in **Phase 1 reporting mode**: daily pacing pulls, CPA-drift flags, search-term anomaly reports. `[ASSUMED]` no mutation needed on Google this quarter; revisit when the official MCP adds write tools rather than adopting an unverified write connector on a $120K spend surface.
- **Meta:** Use the **official Meta Ads campaign-management MCP** (platform-hosted auth, no credential paste; includes campaign-management write tools). Eligible for Phase 2 human-in-the-loop write because the official connector carries write capability at acceptable risk.
- **Deny by default:** unverified community connectors and cross-platform routers for any spend-capable account this quarter.

#### Permission-Scope Table (excerpt)

| Connector | Granted (minimum) | Deny-list |
|-----------|-------------------|-----------|
| Google Ads MCP (official) | account listing, query/reporting | all mutation (not available; not sought) |
| Meta Ads MCP (official) | read insights, propose budget edits, propose ad-set status | autonomous campaign creation, autonomous audience expansion (Phase 2 approval only) |

#### Three-Phase Rollout

- **Phase 1 (weeks 1–3):** Both platforms read-only. Agent drafts daily performance narration + flags anomalies. Exit criterion: 3 weeks of agent flags reviewed against human judgment with <1 material miss/week.
- **Phase 2 (week 4+):** Meta human-in-the-loop write. Agent proposes budget shifts + ad-set pauses; VP Growth or Growth Lead approves each before it goes live. Google stays Phase 1. Exit criterion: 20+ approved actions with zero approver-overridden errors before considering any Phase 3 bound.
- **Phase 3 (deferred):** Bounded autonomy considered only for budget moves under the per-action cap within the existing campaign set; new campaigns, audience expansion, and creative changes stay in Phase 2 indefinitely.

#### Spend Guardrails (scaled to $120K/mo)

- Account-level budget cap at Meta billing: $5,000/day hard ceiling (agent cannot exceed regardless of instruction)
- Per-action change cap: $500 or 15% of campaign daily budget, whichever is lower
- Daily cumulative-change cap: $1,500 across all agent actions → freeze + alert
- New-spend-surface gate: any new campaign type, platform, or audience → VP Growth authorization, every phase
- Anomaly auto-pause: spend velocity >2× trailing-7-day average OR CPA >1.5× target → auto-pause + alert

#### Approval Matrix (one-page excerpt)

| Action class | Phase 1 | Phase 2 | Phase 3 |
|--------------|---------|---------|---------|
| Reporting / analysis | none | none | none |
| Budget change ≤ per-action cap | n/a | VP Growth / Growth Lead | none (within bounds) |
| Budget change > cap, new campaign, audience expansion, creative change | n/a | VP Growth / Growth Lead | VP Growth / Growth Lead |
| Connector authorization / scope change | Connector owner (VP Growth) | Connector owner | Connector owner |

#### Kill-Switch Procedure (under five minutes)

1. Revoke the Meta MCP authorization in Business Suite (deactivates the connector immediately)
2. Pause affected campaigns directly in Meta Ads Manager UI (independent of the agent)
3. If spend is runaway, freeze the payment method at the billing layer
4. Notify VP Growth + Growth Lead (incident channel)
5. Export the agent audit log for the post-incident review
- **Drill cadence:** quarterly; next drill confirms Growth Lead can execute steps 1–3 unaided.

#### Natural-Language Campaign-Brief Template (filled example)

> **Objective / KPI:** Scale prospecting on Meta toward CPA ≤ $32. **Scope:** Meta account [ID], Prospecting campaign set only. **Budget + hard cap:** raise daily budget up to but not beyond $4,000/day; per-action moves ≤ $500. **Audience:** existing lookalike + interest sets; no new audiences without approval. **Messaging guidelines:** lead with star ratings and verified-review density and clear price; do NOT use scarcity badges, countdown timers, or strikethrough framing. **Creative source:** approved asset library `/brand/assets/spring-prospecting/`. **Phase:** 2 (human-in-the-loop). **Approver:** VP Growth.

#### Assumptions, Gaps, Risk Flags

- `[ASSUMED]` No mutation needed on Google this quarter; plan revisits when the official Google Ads MCP ships write tools
- `[ASSUMED]` In-house single-brand account (no agency multi-client isolation needed); revisit if Northbeam adds managed sub-accounts
- **Gap:** Audit-log storage location + weekly reviewer not yet named — recommend a 30-minute follow-up to set the audit-trail standard
- **Risk flag:** apparel DTC is unregulated, but any "free shipping / limited time" promo copy must be checked against the no-scarcity messaging guideline before it enters an agent brief
