---
name: "Email Sequence Builder"
category: sales
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~30 min/sequence"
version: 2.1
last_eval_score: null
---

# ✉️ Email Sequence Builder

## Purpose

Draft a complete multi-email nurture sequence with subject lines, preview text, body copy, CTAs, and send timing — designed to move leads through a specific stage of your marketing or sales funnel.

## When to Use

Use this skill when building automated email sequences for lead nurturing, onboarding, re-engagement, post-purchase follow-up, event promotion, or abandoned cart recovery. Works best when you know the entry trigger and desired end action.

## Required Input

Provide the following:

1. **Sequence type** — What kind of sequence? (e.g., welcome/onboarding, lead nurture, re-engagement, post-purchase, event promotion, abandoned cart)
2. **Entry trigger** — What action puts someone into this sequence? (e.g., downloaded a guide, signed up for newsletter, requested a quote, attended a webinar)
3. **Desired outcome** — What should the recipient do by the end? (e.g., book a demo, make a purchase, leave a review, refer a friend)
4. **Audience** — Who is receiving these emails? (role, awareness level, relationship to your brand). Ideally a named persona from `outputs/personas/`
5. **Number of emails** — How many emails in the sequence? (default: 5)
6. **Key selling points** — Top 3–5 benefits, proof points, or objections to address
7. **Existing assets** (optional) — Case studies, testimonials, blog posts, or landing pages to link to
8. **Sender identity** — From-name + from-address (a person beats a brand for nurture; brand beats a person for transactional)
9. **Sending domain & deliverability state** — Is the sending domain warmed (>30 days, SPF/DKIM/DMARC aligned)? If new, the skill will route the first 4 weeks to a "warming-safe" version with shorter HTML, no link shorteners, and one CTA per email
10. **Holdout policy** — Will a 5–10% control group be held out to measure incremental lift? Default: yes. If no, the measurement frame switches to "directional only" with that flag surfaced in the summary

### Minimum Viable Input

If only fields 1, 2, 3, 4 are present, the skill will produce a `confidence: medium` sequence with placeholder proof points marked `[PROOF NEEDED]` and a checklist of inputs that would lift it to `confidence: high`.

## Instructions

You are a skilled email marketing strategist's AI assistant. Your job is to architect and write email sequences that guide recipients toward a specific action through a logical, persuasive progression.

**Before you start:**
- Load `config.yml` from the repo root for company name, services, brand voice, and follow-up style
- Reference `knowledge-base/terminology/` for correct industry terms
- Use the company's communication tone from `config.yml` → `voice`
- Note the follow-up style preference from `config.yml` → `voice.followup_style`

**Process:**

1. Design the sequence architecture:
   - Map the emotional and logical journey from trigger to conversion
   - Assign a strategic purpose to each email:
     - Email 1: Welcome + set expectations + quick win
     - Email 2: Educate + address primary objection
     - Email 3: Social proof + credibility building
     - Email 4: Overcome secondary objection + urgency
     - Email 5: Final CTA + alternative next step
   - Define optimal send timing between emails (e.g., Day 0, Day 2, Day 5, Day 8, Day 12)
   - Identify exit conditions (when to remove someone from the sequence)

2. For each email, write:

   **Subject Line (3 options per email):**
   - Keep under 50 characters for mobile optimization
   - Vary approaches: curiosity, benefit, urgency, personalization, question
   - Avoid spam trigger words (free, act now, limited time, etc.)

   **Preview Text:**
   - 40-90 characters that complement (not repeat) the subject line
   - Should make sense on its own in mobile inbox view

   **Body Copy:**
   - Open with a hook relevant to where they are in the journey
   - One core message per email — don't overload
   - Use short paragraphs (2-3 sentences max)
   - Include personalization tokens where appropriate (e.g., {first_name}, {company})
   - Write in second person ("you") for direct engagement
   - Keep total length between 100-200 words for nurture emails

   **Call-to-Action:**
   - One primary CTA per email (clear button or link text)
   - CTA text should describe the outcome, not the action (e.g., "See How It Works" not "Click Here")
   - Include a soft secondary CTA for emails 3+ (e.g., "Reply to this email with questions")

3. Add sequence metadata:
   - Recommended send times (day of week + time of day per email)
   - Segment/tag recommendations for the email platform
   - Branch logic suggestions (e.g., "If they click CTA in email 2, skip to email 4")
   - Metrics to track per email (open rate, click rate, reply rate, conversion rate)
   - Industry benchmark targets for each metric

4. **Add the AI-assist layer.** For each email, recommend one concrete AI-assisted tactic the team can turn on now:
   - LLM-generated subject-line variants per recipient cluster (5–8 clusters max, no per-recipient generation — you'll exceed your model spend without lifting outcomes)
   - Send-time personalization (only worth turning on once list is >5K and >30 days warm)
   - Dynamic body insertion blocks (3–4 modular paragraphs swapped by persona; not full-email regen)
   - Reply detection routing (inbound replies that look like questions → SDR; that look like unsubscribes → suppression list)

5. **Define the measurement frame.**
   - **Primary KPI:** sequence completion → desired outcome conversion rate (not open rate)
   - **Holdout:** 5–10% control if field 10 = yes; results read at sequence end + 14 days
   - **Apple Mail Privacy Protection adjustment:** open rates inflated 30–60% post-MPP; treat opens as directional only and key on click + reply + conversion
   - **Sequence-level review:** at 30 days, compute conversion rate by email position (which email is doing the work?), reply rate (is anyone responding?), and unsubscribe rate per email (>0.5% per email = the email is the problem, not the audience)

6. **Build the deliverability + compliance checklist.**
   - SPF, DKIM, DMARC alignment confirmed before send
   - From-name consistency with prior sends (changing from-name resets sender reputation)
   - Plain-text version included for every HTML email
   - One-click unsubscribe in header (Gmail/Yahoo bulk-sender requirement, in force since Feb 2024)
   - List-Unsubscribe-Post header set
   - Spam complaint rate target < 0.1%; pause sequence if rate > 0.3% at any inflection point
   - Subject lines tested against "Mail Tester" or equivalent before launch
   - GDPR / CAN-SPAM / CASL footer with physical address + opt-out

**Output requirements:**
- Complete sequence with all emails written in full
- Subject line options and preview text for each
- Send timing schedule in a clear table format
- Branch logic and exit conditions documented
- One-page sequence overview diagram (text-based flow)
- AI-assist layer with one named tactic per email
- Measurement frame (primary KPI, holdout plan, MPP adjustment, sequence-level review)
- Deliverability + compliance checklist
- Confidence flag (high / medium / low) based on input completeness
- Uses company name, voice, and follow-up style from config
- Professional formatting ready for import to email platforms
- Saved to `outputs/sequences/` if the user confirms

## Calibration Notes

- **Open rate is largely vanity in 2026.** Apple Mail Privacy Protection inflates reported opens; bot-prefetch in some ESPs adds another 5–20% noise. Treat opens as directional only. Key on **clicks, replies, and downstream conversions.**
- **Reply rate is the truest engagement signal.** A 1–3% reply rate on a B2B nurture is a strong sequence; >3% is exceptional. Build at least one email designed to provoke a reply (a real question with no link).
- **Unsubscribe rate per email is the diagnostic.** Industry-acceptable range: 0.1–0.3% per send. >0.5% on a single email = the email is the problem. >1% across the sequence = the audience-trigger fit is wrong, not the copy.
- **Sales-cycle calibration:** for a 90-day enterprise sale, a 5-email sequence over 12 days is too compressed. Match sequence cadence to typical sales-cycle length (rule of thumb: sequence duration = 15–25% of typical cycle).
- **Subject-line spam triggers in 2026:** the historic list (FREE, ACT NOW, $$$) is largely solved by spam filters. The current killers are over-personalized first-name-in-subject ("Hey {first_name}, are you free Tuesday?"), excessive emoji density, and any sense of fake urgency. Filters now also penalize "RE:" or "FW:" on cold outbound.
- **AI-generated copy is detectable to humans by week 2.** Sequences fully generated by AI without editing collapse to a sing-song cadence and abstract claims. Recommend AI-draft-then-human-edit, not AI-only.
- **B2C transactional vs. B2B nurture have different rhythms.** B2C abandoned-cart: 3 emails over 7 days, urgency rising. B2B nurture: 5–8 emails over 4–8 weeks, education compounding.
- **Holdout > A/B for sequence-level decisions.** A/B tests answer "which email is better." Holdout answers "is the sequence worth running at all." Run a 5–10% holdout before celebrating a 12% conversion lift.
- **Refresh cadence:** Re-validate every 90 days. Sequences degrade as audience composition shifts and as the team's case studies / proof points age.

## Anti-Patterns

- **The 9-email epic** — Most B2B nurture sequences past email 5 see exponential unsubscribe lift with negligible conversion lift. Default to 5; require justification for 7+.
- **Day 0, Day 1, Day 2 carpet-bomb** — sender reputation tanks fast under daily cadence. Minimum 48-hour gap for nurture; 24-hour gap acceptable for transactional with clear triggering action.
- **First-name-in-subject** — "Hey {first_name}, quick question" reads like a fake friend in 2026. Use it sparingly; never as the dominant pattern.
- **Recycled CTA across all emails** — if every email ends with "Book a demo" the team is begging, not persuading. Reserve "Book a demo" for emails 4+ and earn it with prior emails that gave value.
- **Open-rate optimization as the goal** — optimizing for opens optimizes for clickbait subject lines and gets the sequence flagged. Optimize for replies and conversions.
- **No exit conditions** — if a recipient converts in email 2, they should not receive emails 3–5. Branch logic + suppression on the conversion event is mandatory.
- **No holdout** — claiming "30% lift in pipeline from this sequence" without a control group is reporting fiction. Either run the holdout or label results as directional.
- **Brand-from-address for cold/nurture** — "noreply@company.com" or "marketing@company.com" gets filtered. Send nurture from a person.

## Integration Notes

- **Persona & ICP Builder** (`outputs/personas/`) — Persona's hidden motivation, verbatim language, and channel attention budget feed every email's hook + body. The named persona should appear in the sequence file frontmatter so future runs can re-target.
- **Brand Voice Style Guide Generator** — Voice attributes + AI prompt preamble are embedded in the AI-assist layer. Banned-phrase list runs as a final-pass filter.
- **Synthetic Persona Simulator** — Run the full sequence through the simulator before launch. The simulator's SHIP / ITERATE / REWORK verdict is a required gate at email 3 (the educate + objection email — the highest-failure-rate slot).
- **Cross-Channel Attribution Analyzer** — Sequence-level conversion data feeds the attribution analyzer's email-channel input. Holdout results overwrite last-click for incremental measurement.
- **Campaign Performance Narrator** — Sequence-level KPIs (reply rate, unsubscribe rate per email, downstream conversion) feed the narrator's email-channel diagnostic.
- **Multi-Channel Content Repurposer** — Email body sections often become LinkedIn newsletter posts and short-form social; this skill's output is upstream content for the repurposer.
- **AI Search Visibility Audit** — When sequences cite proof points or stats, mirror them in the website knowledge base so AI answer engines surface the same numbers buyers see in inbox.

## Example Output

### Input Recap
- Sequence type: B2B nurture for a "downloaded the State of RevOps 2026 report" lead
- Entry trigger: form fill on report landing page
- Desired outcome: book a 30-min demo with an AE
- Audience: Persona "Priya, the Pragmatic Head of RevOps" (`outputs/personas/priya-revops.md`)
- 5 emails, sender = "Maya Chen, Head of Customer at Threadline" (person, not brand)
- Domain warmed > 6 months; holdout 8% control
- Confidence: `high`

---

### Sequence Architecture

| # | Day | Purpose | Primary CTA | Secondary CTA |
|---|-----|---------|-------------|---------------|
| 1 | Day 0 | Welcome + deliver report + set expectations | Read the report | (none — let value land) |
| 2 | Day 3 | Educate on the #1 finding | Read companion piece | Reply with your top blocker |
| 3 | Day 7 | Address the primary objection ("another tool to maintain") | Watch 6-min admin walkthrough | Reply with your stack |
| 4 | Day 11 | Social proof + named-peer reference | Read ScaleHQ case study | Book a 30-min demo |
| 5 | Day 16 | Soft close + alternative path | Book a 30-min demo | Stay on the list |

**Exit conditions:** demo booked → exit + route to AE workflow; reply with question → SDR routing; unsubscribe → full suppression; no opens by Day 11 → suppress emails 4–5, route to retargeting.

---

### Email 1 — Day 0

**Subject options:**
1. "The State of RevOps 2026 — your copy"
2. "Here's the report (and one finding I keep thinking about)"
3. "Your RevOps benchmark report"

**Preview:** "Plus the one chart that surprised even our analysts."

**From:** Maya Chen <maya@threadline.com>

**Body:**

Hi {first_name},

Thanks for grabbing the State of RevOps 2026. Here's the [PDF link].

One finding the team keeps circling back to: 64% of RevOps leaders said the bottleneck wasn't tooling — it was the handoff between tools. We expected a clean tooling-gap story. We got a "it's the seams" story instead.

I'll send a couple more emails over the next two weeks pulling apart the most useful sections. If they're not useful, hit unsubscribe — I won't take it personally.

— Maya
Head of Customer, Threadline

**[CTA button]** Read the report

---

### Email 2 — Day 3

**Subject options:**
1. "The handoff problem (and a 6-minute fix)"
2. "Why ops keeps getting paged at 11pm"
3. "The seam between Salesforce and everything else"

**Preview:** "We mapped the broken handoff in 4 customer stacks. Here's what we found."

**Body:**

{first_name},

The State of RevOps report flagged broken handoffs as the #1 source of ops pain. We dug deeper. In four customer stacks we audited last quarter, the same pattern showed up: a deal exits one tool, sits in nobody's queue for 6–48 hours, and re-enters the next stage with stale data.

The fix usually isn't a new tool. It's an observability layer between the tools you already have.

Quick read: [companion blog post — "The Seam Between Salesforce and Everything Else"].

Curious — what's the handoff that breaks first in your stack? Hit reply, even one word works.

— Maya

**[CTA button]** Read the companion piece
**[Soft CTA]** Reply with your top blocker

---

### Email 3 — Day 7 (highest-failure-rate slot — passes through Synthetic Persona Simulator before launch)

**Subject options:**
1. "'Another tool to maintain' (the honest answer)"
2. "What we tell Salesforce admins on the demo call"
3. "The 6-minute admin walkthrough"

**Preview:** "Skip the deck. This is the part most demos hide."

**Body:**

{first_name},

The most common pushback we hear: "I don't need another tool to maintain."

Fair. So instead of a sales-deck answer, here's the 6-minute video of our solutions engineer walking through the admin config — including the rollback plan, the namespace, and where it can break.

If you watch and decide it's not for you, that's a clean no. We'd rather you know the rough edges in 6 minutes than 6 weeks.

— Maya

**[CTA button]** Watch the 6-minute admin walkthrough
**[Soft CTA]** Reply with your stack and I'll flag specific integration gotchas

---

### Email 4 — Day 11

**Subject options:**
1. "How ScaleHQ cut ops cycle time 31%"
2. "The case study most like your stack"
3. "ScaleHQ's RevOps team (their words, not ours)"

**Preview:** "Series C, 240 FTE, Salesforce + HubSpot + 4 integrations. Sound familiar?"

**Body:**

{first_name},

The case study most like the stacks I see in the report data: ScaleHQ. Series C, 240 FTE, Salesforce as system of record, HubSpot for marketing, four other tools wired in.

Their RevOps lead wrote the case study herself — including the part where our first onboarding session uncovered a config conflict that delayed go-live by a week. We left it in.

Read: [ScaleHQ case study link].

If you want to talk to her directly — we offer peer reference calls on demos. Just hit the button below and pick a 30-min slot.

— Maya

**[CTA button]** Book a 30-min demo
**[Soft CTA]** Read the ScaleHQ case study

---

### Email 5 — Day 16

**Subject options:**
1. "Last note from me — and a way to stay in the loop"
2. "Closing the loop on the State of RevOps"
3. "Two paths from here"

**Preview:** "30 min demo, or a monthly RevOps memo. Both fine."

**Body:**

{first_name},

This is the last sequence email — I won't keep tapping the same shoulder.

Two ways to keep going:

1. **30-min demo** — we'll show your stack specifically, including the one thing we won't fix
2. **The monthly RevOps memo** — one email a month, no demos, no pitches, just the patterns we see

Either's good. Or unsubscribe — really, no hard feelings.

— Maya

**[CTA button]** Book a 30-min demo
**[Soft CTA]** Stay on the monthly memo list

---

### AI-Assist Layer

| Email | AI tactic | Implementation note |
|-------|-----------|---------------------|
| 1 | Subject-line variants by industry cluster (SaaS, Marketplace, Fintech) | 3 clusters × 3 variants = 9 subjects, A/B/C in ESP |
| 2 | Dynamic body insert block (which "one finding" to lead with based on report-section-clicked) | Single modular block; do not regen full email |
| 3 | Reply-routing classifier on inbound replies (question / objection / unsubscribe-intent) | Route to SDR / AE / suppression respectively |
| 4 | Case-study selection by persona's industry (default ScaleHQ for SaaS, Brightline for logistics) | Persona file in `outputs/personas/` resolves selection |
| 5 | Predictive send-time per recipient (only if list >5K) | Skip for now if list is smaller; window 9–11am recipient TZ |

---

### Measurement Frame

- **Primary KPI:** demo-booked rate by sequence end + 14 days
- **Holdout:** 8% control held out from sequence; primary KPI compared at sequence end + 14 days; lift required > 1.5x to declare incremental win
- **MPP adjustment:** treat open rate as directional only; report click + reply + conversion as decision metrics
- **Per-email diagnostics:** unsubscribe % per send (alert if >0.5%), reply rate (target 1–3%), CTR (target 4–8% for nurture)
- **30-day review:** which email is doing the conversion work? (Almost always email 3 or 4 in this template — if it's email 1, the audience is too warm; if it's email 5, the early emails aren't pulling weight.)

---

### Deliverability + Compliance Checklist
- [x] SPF, DKIM, DMARC aligned on threadline.com (verified 2026-04-20)
- [x] From-name "Maya Chen" consistent with prior sends from this address
- [x] Plain-text version generated for all 5 emails
- [x] List-Unsubscribe + List-Unsubscribe-Post headers set
- [x] One-click unsubscribe in footer
- [x] CAN-SPAM physical address in footer
- [x] Spam complaint rate alarm at 0.3% (auto-pause)
- [ ] Mail Tester score > 9/10 for all 5 emails (run before launch)

---

### Refresh Date
Sequence: re-validate 2026-07-24 (90 days). Subject-line variants: re-test monthly against sender reputation and ESP filters.
