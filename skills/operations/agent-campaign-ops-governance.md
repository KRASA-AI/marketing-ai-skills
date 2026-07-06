---
name: "Agent-Controlled Campaign Ops & MCP Governance"
category: operations
tools: [claude, chatgpt]
difficulty: advanced
time_saved: "~5 hrs/setup + ongoing risk avoidance"
version: 1.4
last_eval_score: 9.5
---

# 🎛️ Agent-Controlled Campaign Ops & MCP Governance

## Purpose

Produce a governance-and-operations playbook for running paid-media campaigns through AI agents connected to ad platforms over MCP (Model Context Protocol). The deliverable covers connector selection (official vs. third-party), permission scoping, a graduated read-only → human-in-the-loop → autonomous rollout, spend guardrails, an approval matrix, an audit trail standard, an incident kill-switch, and a natural-language campaign-brief template that turns a structured brief into agent-executable instructions across one or more platforms.

The 2026 shift this skill absorbs: as of mid-2026, the campaign-management interface is no longer only the platform UI. Inside roughly four months, the count of major ad platforms with platform-official MCP servers went from zero to seven — Amazon (February 2026, open beta), Google (April 28, open-source, read-only by design), Meta (April 29, open beta, read/write), TikTok (May 13, TikTok World, read/write across the full campaign lifecycle), Yahoo DSP (early 2026, read-oriented, programmatic-buying surface), and then a clustered set of June debuts one week before Cannes Lions: Pinterest and Microsoft Advertising both shipped official read-only servers on June 17, 2026, and Snap announced its own ad-platform MCP server on June 18. Each made a deliberately different architectural choice (see the connector-architecture table below). On top of the official servers, third-party cross-platform routers (Google / Meta / TikTok / LinkedIn / Amazon / Microsoft) stitch several platforms into one agent connection and add write capability where an official server is read-only. The optimization unit moves from "navigate the Ads Manager UI" to "write a brief the agent executes," which makes the brief, the brand code, and the structured offer attributes the load-bearing inputs — and makes connector governance a first-class marketing risk, not an IT afterthought.

The single most useful pattern across these seven launches: **read-only-first is now the de facto standard for first-party servers.** The earliest servers (Google, Amazon, Yahoo) and the three June debuts (Pinterest, Microsoft, Snap) all launched read-only or read-oriented — agents read live campaign data and draft recommendations, but a human applies every mutation. Only Meta and TikTok ship full read/write. For most accounts on most platforms, the broadly-supported safe pattern today is therefore **read-and-recommend with a human in the loop**, not autonomous editing — which is exactly the posture this skill's Phase 1/2 rollout already encodes. Two of the June launches (Pinterest alpha, Microsoft open pilot) are also gated behind named-partner lists with no general-availability date, so "official server exists" does not yet mean "broadly available" — confirm access tier before planning a rollout around it.

A structural fact that shapes the whole plan: the official servers are **single-platform by design** — each keeps query patterns, conversion signals, and audience data inside its own platform's perimeter, so an agent that manages Google, Meta, and TikTok in one conversation cannot do it on official rails alone. That makes a unified cross-platform agent *harder*, not easier, to build safely: the only cross-platform path is a third-party router, which is exactly the higher-risk, broader-blast-radius option this skill treats with extra scope discipline. "Prefer official" and "want one agent across all platforms" are in genuine tension; this plan resolves it in favor of official-per-platform unless the team explicitly accepts the router risk.

#### Official ad-platform MCP architecture (as of June 2026)

| Platform | Launch | Read | Write | Notable guardrail / shape |
|----------|--------|------|-------|---------------------------|
| Amazon Ads | Feb 2026 (open beta) | Yes | Yes (campaigns + billing) | Platform auth; bundled tool packs; invite-gated |
| Google Ads | Apr 28, 2026 (open source) | Yes | **No — read-only by design** | 3 tools + 4 resources; mutations stay in REST/gRPC; self-hosted; Google has signaled future mutation tools |
| Yahoo DSP | Early 2026 | Yes | Read-oriented | Programmatic-buying / DSP surface rather than search/social |
| Meta Ads | Apr 29, 2026 (open beta) | Yes | Yes | **Everything created lands paused by default** — a campaign only goes live after a human activates it; 29 tools (+10 catalog), hosted, Business OAuth with 3 scope tiers |
| TikTok Ads | May 13, 2026 (TikTok World) | Yes | Yes (full lifecycle) | Plan / launch / bid / budget / targeting / optimization; tool inventory not yet publicly documented |
| Pinterest Ads | Jun 17, 2026 | Yes | **No — read-only at alpha** | Performance + analytics + keyword + Taste Graph signals; alpha, named partners only, no GA date; shipped alongside a wider AI suite (Business Assistant, Performance+) |
| Microsoft Advertising | Jun 17, 2026 | Yes | **No — read-only (open pilot)** | Live campaign data readable inside M365 Copilot, Claude, ChatGPT and other agents; pilot-gated, no GA date |
| Snap Ads | Jun 18, 2026 (announced) | Yes | Read-oriented (shape TBD) | Opens Snap's ads platform to third-party agents; bundled with Snap Smart Assistant + Creator Network; specifics not yet documented |

The two-speed pattern is the operating takeaway: only **Meta and TikTok** offer full read/write; **every other official server is read-only or read-oriented** at this writing. Treat write as a per-platform capability you confirm, not a default you assume.

This skill is the governance answer to that shift. It does not replace the brief-writing skills (Creative Brief Generator) or the measurement skills (Cross-Channel Attribution Analyzer); it sits between them and the live ad account, defining who is allowed to let an agent touch spend, under what scope, with what controls, and how an incident gets stopped in under five minutes.

#### The plan at a glance

The full deliverable is eight linked controls. Read the table top-to-bottom as the rollout sequence — each row's gate is what lets the next one exist:

| # | Control | One-line job | Owner | The number / trigger that makes it real |
|---|---------|--------------|-------|------------------------------------------|
| 1 | Connector selection | Pick official vs. verified vs. router, per platform | Connector-authorization owner | Read/write shape confirmed before a phase is assigned |
| 2 | Permission scope | Grant the minimum tool set, deny-list the rest | Connector-authorization owner | Default read-only; write only when the phase justifies it |
| 3 | Three-phase rollout | Read-only → human-in-the-loop → bounded autonomy | Brief owner + approver | Phase-exit criteria met (e.g., 20+ clean approvals) |
| 4 | Spend guardrails | Hard limits independent of agent judgment | Approver | Per-action cap + daily cap + anomaly auto-pause, scaled to config |
| 5 | Approval matrix | Map action class → approver → phase | Approver (primary + backup) | Above-cap / new-surface actions need a named human, every phase |
| 6 | Audit trail | Log prompt, decision rationale, and action for every mutation | Independent reviewer | Reviewed weekly for Phase 2/3 accounts |
| 7 | Kill-switch | Stop spend in under five minutes | Any named owner | Drilled quarterly, not just documented |
| 8 | Campaign-brief template | Turn intent into auditable agent instructions | Brief owner | Mandatory for any Phase 2/3 write action |

The operating spine in one sentence: **read-only-first by default, write only behind a per-action cap and a named approver, and a drilled kill-switch under everything.**

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

**Before you start — load `config.yml` and let it set the actual guardrail numbers, not just the voice (this is what makes the plan *this* team's risk posture instead of a generic template):**
- `pricing` / spend-authority levels — the human approval thresholds the team already uses for spend become the default for the agent's per-action and daily caps. The agent should never be allowed a larger unilateral move than a human at the same seniority. If config declares a per-approval spend authority (e.g., "Growth Lead approves up to $2K, VP above"), derive the per-action cap *from it* rather than inventing a round number.
- `risk_tier` (or risk profile) — a config-declared risk tier sets the cap math directly: **conservative** → per-action cap ≈ 5% of daily account spend, daily cumulative cap ≈ 15%, Phase 3 disabled; **standard** → ≈ 10% / 30%, Phase 3 only within an approved campaign set; **aggressive** → ≈ 15% / 40% with the same hard billing ceiling. If config has no risk-tier field, derive a conservative tier from the stated monthly spend, state `[ASSUMED] conservative tier`, and flag adding a `risk_tier` field to config as the single highest-value personalization upgrade.
- `team.roles` + leadership contacts — populate the approval matrix's named primary/backup per approver directly from config; do not leave the matrix with role placeholders when config names real people.
- `tools` — name the team's actual billing surface and incident channel in the guardrail and kill-switch steps (e.g., where the budget cap is set, where the incident alert fires).
- `voice` (`always_use` / `never_use`) — these are the "never say" constraints that flow into the campaign-brief template's messaging-guidelines field, so agent-generated creative inherits the brand's banned-claim list as a hard filter.
- Consult `knowledge-base/regulations/` for any category-specific advertising disclosure rules that constrain autonomous creative generation
- Consult `knowledge-base/best-practices/` for prior connector-governance decisions and any logged incidents
- Establish the read/write capability of each connector under consideration before recommending a rollout phase — an official read-only MCP and a write-capable third-party wrapper carry very different risk

**Process:**

1. **Select the connector per platform.** For each platform, classify the available connectors and recommend one:
   - **Official platform MCP** — published by the ad platform, platform-hosted auth, no credential paste. Lowest account-suspension risk. Establish its read/write shape first: it may be read-only by design (Google), read/write with a paused-by-default safety guardrail (Meta — created entities stay paused until a human activates them), or read/write across the full lifecycle (TikTok, Amazon). The guardrail shape changes which rollout phase the platform can safely enter — a read-only official server is permanently safe in Phase 1; a paused-by-default writer can move to Phase 2 with the platform's own guardrail reinforcing the human-approval step.
   - **Verified third-party connector** — an app that passed the platform's app review with scoped permissions. Moderate risk; adds write capability the official MCP may lack.
   - **Unverified / community connector** — convenient and often broad-scoped, but the highest account-suspension and data-exposure risk; community connectors have triggered account bans. Default recommendation: do not connect a spend-capable account through an unverified connector.
   - **Cross-platform router** — a single connector exposing several platforms' tools at once. Convenient for multi-platform teams but concentrates risk; if it is compromised or mis-scoped, every connected account is exposed. Recommend extra scope discipline and a separate audit cadence.

2. **Scope the permissions.** Build a permission-scope table: for each connector, the minimum tool set required for the job, and an explicit deny-list of tools that are not needed (and so should not be granted). Default to read-only scopes wherever the job is reporting or diagnostics; grant write scopes (budget edits, campaign creation, bid changes) only when the rollout phase justifies them and the guardrails below are live.

3. **Design the three-phase rollout.** Do not start agents in autonomous-write mode:
   - **Phase 1 — Read-only.** Agent reads and reports only (performance pulls, anomaly flags, recommendation drafts). No mutation tools granted. Run for a defined window to build trust in the agent's judgment against known-good human decisions.
   - **Phase 2 — Human-in-the-loop write.** Agent proposes changes (budget shifts, new ad sets, bid adjustments) but a named human approves each before it goes live. Mutation tools are granted but a human-approval step gates every spend-affecting action.
   - **Phase 3 — Bounded autonomy.** Agent executes a defined class of low-risk changes within hard limits (e.g., budget moves under a fixed dollar / percentage cap, within an approved campaign set) without per-action approval; everything outside the bounds reverts to Phase 2 approval. Most teams should keep high-stakes actions (new campaign launch, budget increases above the cap, audience expansion, creative changes) in Phase 2 indefinitely.

4. **Set the spend guardrails.** Hard limits that exist independent of the agent's judgment. Derive the dollar/percentage numbers from the config risk tier and spend-authority levels loaded above — do not default to round numbers when config implies a specific posture:
   - Account-level budget cap configured at the platform billing layer (the agent cannot exceed it even if instructed to)
   - Per-action change cap (max dollar / percentage budget move the agent can make without escalation) — set from the config risk tier (conservative ≈ 5% of daily spend, standard ≈ 10%, aggressive ≈ 15%) and never above the spend authority a human at the agent's "seniority" would hold per config
   - Daily cumulative-change cap (max total change across all actions in 24 hours before a freeze)
   - New-spend-surface gate (any new platform, new campaign type, or new audience requires human authorization regardless of phase)
   - Anomaly auto-pause threshold (spend velocity or CPA drift beyond a band triggers an automatic pause + alert)

5. **Build the approval matrix.** A one-page table mapping action class → required approver → phase:
   - Reporting / analysis: no approval (any phase)
   - Budget change within per-action cap: Phase 2 named approver; Phase 3 no approval if within bounds
   - Budget change above cap, new campaign, audience expansion, creative change: named approver in every phase
   - Connector authorization / scope change: connector-authorization owner (a deliberately small list)
   - The matrix names a primary and backup for each approver so no action is blocked by one person's absence

6. **Define the audit-trail standard.** Every agent action against a live account is logged with: timestamp, connector, account, tool called, parameters (before / after values for any mutation), the brief or prompt that triggered it, the **agent's stated rationale for the decision** (why this change, what signal or expected impact drove it), the approver (if Phase 2), and the outcome. The rationale field is what turns the log from a record of *what* changed into an explanation of *why* — and it is the single control that closes the "decision-visibility" gap named as the top adoption barrier for agentic buying (see the decision-transparency calibration note). Where a platform agent optimizes bids or budgets on its own logic and cannot expose a rationale, treat that opacity itself as a governance flag, not a neutral default. The log is reviewable by someone other than the person who ran the agent. Specify where the log lives and the review cadence (recommend weekly for Phase 2/3 accounts).

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

- **Official-first, write-second.** Prefer the official platform MCP for any account that touches spend; it carries the lowest account-suspension risk because the platform hosts the auth and scopes the tools. Where the official MCP is read-only (Google's server exposes only account-listing and GAQL query tools — reporting and diagnostics, no mutation — and that posture is a deliberate design choice, not a technical limit, with Google signaling future mutation tools), keep the agent in reporting mode on that platform and do not reach for an unverified write-capable connector just to get mutation; the convenience is not worth the ban risk on a spend account. Note that some third-party Google Ads MCP builds expose mutation behind an opt-in flag — treat enabling it on a live spend account as a deliberate, governed decision, not a default.
- **Lean on the platform's own guardrail where it exists.** Meta's official server creates every entity **paused by default** — a hard-coded safety guardrail that means nothing the agent builds goes live until a human activates it in Ads Manager. Where a platform ships this behavior, it reinforces your Phase 2 human-approval step and is the backbone of a safe staged rollout. Two cautions: (a) a companion CLI may not share the MCP's safe default (Meta's CLI creates *active* by default — scripts need an explicit paused-status override to match), so verify the default on every surface the team uses; (b) TikTok and Amazon ship read/write without a documented paused-by-default equivalent, so on those platforms the human-approval gate has to be supplied entirely by your own governance, not the platform's.
- **Read-only-first is the de facto first-party standard — lean into it, don't fight it.** Six of the seven official ad-platform servers (Google, Amazon, Yahoo, Pinterest, Microsoft, Snap) launched read-only or read-oriented; only Meta and TikTok ship full read/write. This is a deliberate trust-then-write industry posture, not a temporary shortfall, and it means the broadly-supported, low-liability pattern for most platforms today is read-and-recommend with a human applying the change — exactly your Phase 1/2. Build the read-and-recommend muscle on the read-only platforms now so you are positioned to flip on write the day each platform ships it, rather than scrambling under deadline; expect the same read-to-write progression Meta and TikTok went through to reach Pinterest, Microsoft, and Snap over the coming cycles.
- **Prefer OAuth over static keys, and never assume a server is broadly available because it shipped.** Independent security review of the wider MCP ecosystem (Astrix Security, surveyed across 68 packages) found ~88% require credentials, roughly half rely on static keys, and only ~8.5% use OAuth — a real credential-handling gap that is part of why first-party platforms launch read-only and gate access behind named-partner pilots. Two governance consequences: (a) where a connector offers OAuth 2.1 / platform-hosted auth, prefer it over any static-key or token-paste setup, and treat a stale or over-broad write credential on a live account as a top-tier risk; (b) several official servers are pilot- or alpha-gated with no GA date (Pinterest, Microsoft as of June 2026), so confirm the actual access tier before designing a rollout around a server that may not be available to your accounts yet.
- **Official servers are single-platform by design — cross-platform is the higher-risk path.** No official server spans platforms; each keeps signals inside its own perimeter. The only way to get one agent across Meta + Google + TikTok is a third-party router, which concentrates blast radius and earns the stricter scope discipline and separate audit cadence below. Resist the pull to adopt a router purely for the convenience of one conversation when official-per-platform connections meet the actual need.
- **Specify every query to avoid hallucinated metrics.** Underspecified prompts ("how did we do last week?") can make an agent invent confident-but-fabricated numbers rather than ask for clarification, and the output reads identical whether the figure is verified or invented. Make it a standing rule that every reporting query names the **date range, metric definition, campaign ID, and attribution window**, and that a human spot-checks key figures against the platform UI during Phases 1–2. This is the single biggest reason to keep a human reviewing agent output early.
- **Rate-limit mutations to protect the learning phase.** On Meta, editing budgets or audiences more than roughly once per day can reset the campaign learning phase regardless of whether a human or an agent made the change — so an over-eager agent making frequent "optimizations" can degrade performance on its own. Pair the Phase 3 autonomy bounds with a mutation rate limit (batch changes; cap edits per campaign per day), not just a dollar cap. Treat the exact threshold as practitioner lore and the principle as real.
- **Read-only is a destination, not just a phase.** Many high-value agent use cases (anomaly detection, daily performance narration, budget-pacing alerts, AEO-citation-adjacent reporting) never need write access at all. Do not grant mutation scopes the job does not require; the most defensible governance posture for a large share of accounts is permanent Phase 1.
- **The per-action cap is the single most important number — and it should come from config, not a guess.** A budget cap at the billing layer prevents catastrophe; the per-action change cap prevents the slow bleed of many small agent mistakes. Derive it from the team's declared risk tier and existing human spend-authority levels in `config.yml` (the agent should never hold more unilateral authority than a human at the same seniority), scaled to the account's daily spend, before any write scope is granted. A team that has set a `risk_tier` in config gets caps that match its actual appetite; a team that hasn't should add one — it is the single highest-leverage personalization field for this skill.
- **Cross-platform routers concentrate risk.** A single connector exposing Google + Meta + TikTok + LinkedIn at once is operationally convenient and a larger blast radius if mis-scoped or compromised. If a team adopts one, the scope discipline and audit cadence should be stricter than for single-platform official MCPs, not looser.
- **No-developer-credentials is a feature and a risk.** Platform-hosted auth with no token paste lowers the setup barrier — which is exactly why the connection should still pass through the connector-authorization owner, not be self-serve for any team member. Ease of connection is not a reason to skip the authorization gate.
- **Briefs are the new load-bearing input.** When campaign execution moves to natural-language briefs, the brand code, structured offer attributes, and "never say" constraints do more work than the Ads Manager click path ever did. A vague brief produces a vague (or wrong) campaign faster than a human would have made the same mistake. The brief template is a control, not paperwork.
- **Carry the agent-shopping-surface copy calibration into the brief.** Briefs that generate ads for agent-mediated or AI-conversation surfaces should drop scarcity badges, countdown timers, and strikethrough framing as the default (these are penalized on the agent-completes-the-purchase surface per the May 2026 HBR shopping-agent research) and lead with star-rating prominence, price clarity, and verified-review density instead. The brief's messaging-guidelines field is where this rule lives.
- **The kill-switch is worthless undrilled.** A documented incident-stop that no one has executed has roughly the response-time performance of no plan at all. The quarterly drill (revoke the connector, confirm spend actually stops, confirm the named owner could do it without help) is the discipline that makes the rest of the plan real.
- **Agency multi-account isolation is a distinct problem.** One connector across many client accounts needs per-client scope isolation, per-client consent documentation, and a per-client kill-switch — a single compromised connector cannot be allowed to expose every client's budget. Agencies should treat each client account as its own governance instance.
- **Re-audit on every new platform MCP.** The MCP ad-surface landscape is expanding fast; each new platform that ships a connector should be brought into the same governance frame (connector selection → scope → phase → guardrails → audit → kill-switch) rather than improvised. The plan is a template to re-run, not a one-time document.
- **Log the prompt, not just the action.** When a mutation is logged, the brief or prompt that triggered it is the most useful field for the post-incident review — it is the difference between "the agent raised the budget" and "the agent raised the budget because the brief said 'scale aggressively' with no cap." The prompt-to-action link is the audit trail's highest-value column.
- **Decision-transparency is the real adoption gate — govern for it explicitly.** The barrier to agentic media-buying in 2026 is not capability, it's trust in the black box: mid-2026 surveys put marketer trust in autonomous agent execution around 55% with roughly one in five actively distrustful, and about 45% of executives name *lack of visibility into how the agent decides* as their top blocker (eMarketer / Yahoo DSP findings). The governance answer is not "trust more," it's "make the decision legible": require every delegated optimization to carry a rationale in the audit trail (why this bid/budget/audience move, on what signal, with what expected effect), review those rationales on the weekly Phase 2/3 cadence, and keep the human approval gate on anything above the per-action cap precisely so the agent's judgment is checkable, not just its spend. The IAB's AI Transparency & Disclosure Framework (January 2026) is a useful external reference point for what platform-side disclosure should cover; use it to pressure-test what each connector actually exposes about its decision logic, and treat a platform agent that optimizes on opaque logic it won't explain as a reason to stay in read-and-recommend on that surface, not to grant it write. Explainability you can't get from the platform, you supply with the human-in-the-loop phase.
- **A platform "agent" is not the same trust tier as a scoped MCP connector.** The wave of platform-native agents (Google's unified Gemini agent across Ads / Analytics / Merchant Center / Marketing Platform; Yahoo DSP's native agentic layer) bundles planning, activation, optimization, and measurement behind one assistant. Convenient, but it concentrates several action classes that this skill deliberately governs separately (reporting vs. budget vs. audience vs. creative vs. connector-scope). Map a platform agent's capabilities onto the same approval matrix you'd apply to discrete MCP tools — do not let "it's the platform's own agent" collapse five governed action classes into one ungoverned "just let it run."

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

#### Spend Guardrails (scaled to $120K/mo; `[ASSUMED] standard` risk tier — no `risk_tier` in config)

- Account-level budget cap at Meta billing: $5,000/day hard ceiling (agent cannot exceed regardless of instruction)
- Per-action change cap: $400 (≈10% of the ~$4K/day account spend, standard tier) or 15% of campaign daily budget, whichever is lower — capped below the Growth Lead's human spend authority
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
