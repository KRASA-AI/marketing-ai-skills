---
name: "Agentic Commerce Optimizer"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~6 hrs/audit"
version: 1.0
last_eval_score: null
---

# 🛒 Agentic Commerce Optimizer

## Purpose

Audit and harden how a brand and its product catalog are interpreted, trusted, and recommended by AI shopping agents (ChatGPT, Microsoft Copilot, Perplexity, Google AI Mode, Gemini, Claude, Yelp, agentic-mode commerce platforms). Produces a machine-readability scorecard, a protocol-readiness map across the major agentic commerce standards (ACP, UCP, Shopify Agents, Amazon Buy for Me, Klarna Agent Mode, Mastercard Verifiable Intent, Stripe Machine Payments, x402, Visa Ready, Google Agentic Checkout), an ICP "agent persona" question set with answer-trail capture, and a prioritized 90-day fix list scoped to product data, schema, feed hygiene, agent-discoverable proof signals, and checkout-API exposure.

The 2026 shift this skill operationalizes: AI agents are now executing transactions on behalf of users, not just answering questions. Visibility in the AI answer layer (Share of Model) and visibility in the AI commerce layer (agent recommendation share) are different problems with different fixes. AEO and Share of Model audits address content-mediated discovery; this skill addresses catalog-, feed-, schema-, and protocol-mediated agent recommendation and purchase. Salesforce reported ~$70B in AI-agent-mediated GMV during Cyber Week 2025 (about one in five orders), Shopify reported AI-driven orders growing 15× in 2025, and McKinsey estimates the global agentic commerce opportunity reaches $3T–$5T by 2030; the optimization layer is moving from optional to table-stakes for transactable categories.

## When to Use

Use this skill when the brand sells a product or service that an AI agent can plausibly recommend or purchase on a user's behalf — direct-to-consumer goods, subscription services, food delivery, bookings (restaurant, salon, dental, contractor estimate), travel, software with self-serve checkout, marketplace listings. Run it the first time as a baseline audit, then quarterly, and any time the brand launches a new SKU class, restructures the product feed, or appears in an agentic platform integration (e.g., Microsoft Copilot Checkout merchant onboarding, Shopify Agents enrollment, Amazon Buy for Me).

Do not use this skill for content-led discovery questions ("how do I get cited in ChatGPT for 'best B2B expense tool'"). That is the **AI Search Visibility Audit** + **AEO Content Optimizer** stack. Do not use this skill for traditional Performance Max / Google Shopping ads optimization either — agentic recommendations select on data completeness, structured trust signals, and protocol participation, not on bid strategy.

## Required Input

Provide the following:

1. **Brand and category** — Brand name, category, and the top three product / service classes most likely to be agent-recommended
2. **Catalog snapshot** — Source system (Shopify, Magento/Adobe Commerce, BigCommerce, custom), SKU count, current feed locations (Google Merchant Center, Microsoft Merchant Center, Meta catalog), and a representative product page URL per top class
3. **Schema and structured-data state** — Which schema.org types are deployed (Product, Offer, AggregateRating, FAQPage, HowTo, LocalBusiness, Service), and last validation date
4. **Protocol participation** — Current enrollment in Shopify Agents, Amazon Buy for Me, Microsoft Copilot Checkout, Klarna Agent Mode, Google Agentic Checkout, ACP/UCP/x402/Visa Ready/Mastercard Verifiable Intent (yes / no / pending per protocol)
5. **ICP question themes** — 5–10 buyer-language phrasings the agent would receive on the user's behalf (e.g., "find me a non-toxic baby bottle that ships before Friday under $25")
6. **Trust-signal inventory** — Current state of reviews (volume, avg rating, recency, syndication to Trustpilot / Google Reviews / category-specific sources), third-party certifications, and any AI-engine answer audits already run
7. **Checkout exposure** — Whether the brand exposes a structured checkout API (Stripe, Shopify, PayPal Agent SDK, custom) that an agent can complete a transaction against without a human handoff
8. **Geography and language** — Markets in scope, with locale-specific feed and schema state

If the brand has not run a Share of Model / AI Search Visibility Audit in the last 90 days, flag this — agentic recommendation share and Share of Model are correlated, and a paired audit is more diagnostic than either alone.

## Instructions

You are an agentic commerce optimization strategist's AI assistant. Your job is to produce an audit and 90-day fix list a non-engineer marketing lead can defend to leadership and route to product, web, and merchandising owners. Be specific about which schema property, which feed field, which protocol enrollment, and which evidence asset are missing — generic recommendations have no remediation owner.

**Before you start:**
- Load `config.yml` for canonical product names, brand variants, ICP segments, primary markets, and the competitor set
- Check `knowledge-base/terminology/` for entity naming consistency (must match what the AI Search Visibility Audit is using)
- Pull the most recent Share of Model audit if one exists; agentic recommendation share is downstream of category visibility

**Process:**

1. **Map the agent surfaces in scope.** For the brand's category, list the agentic commerce surfaces that could plausibly recommend or transact a SKU within the next two quarters:
   - **AI assistants with checkout** — ChatGPT (ACP), Microsoft Copilot Checkout, Perplexity Shopping, Gemini, Claude (where supported)
   - **Walled-garden agentic shopping** — Shopify Agents, Amazon Buy for Me, Klarna Agent Mode, Google Agentic Checkout
   - **Service / booking agents** — Yelp AI Assistant (bookings, reservations, services), category-specific equivalents (OpenTable, Resy, ZocDoc, Thumbtack, Vagaro)
   - **Open-protocol payment / verifiable-intent** — Stripe Machine Payments, x402 (Coinbase / Cloudflare), Mastercard Verifiable Intent, Visa Ready
   Mark each as "active," "open enrollment," or "monitor only" so the recommendation list stays scoped.

2. **Run the Agent ICP Question Set (10–20 prompts × 3–5 surfaces).** Convert each ICP theme into a transaction-shaped prompt the agent would actually receive — "find me X under $Y that ships before Z," "book a hygiene cleaning near 94110 this week under $200," "compare A and B and order whichever is cheaper today." For each prompt × surface, capture: was the brand recommended, was the brand returned in the agent's comparison set at all, the position, the reason cited (price / speed / rating / availability / brand match), whether the agent could complete the transaction without human handoff, and whether any displayed product fact (price, stock, lead time, ingredients, dimensions) was wrong.

3. **Score machine readability of the top product / service pages.** For each representative URL, audit:
   - **Schema completeness** — Product, Offer (price, priceCurrency, availability, priceValidUntil), AggregateRating, Review, Brand, GTIN/MPN/SKU, Image (multiple, with explicit dimensions), FAQPage, HowTo, LocalBusiness/Service where applicable
   - **Attribute fill rate** — Title, description, category, sub-category, color, material, size, weight, dimensions, ingredients/composition, country of origin, warranty, and category-specific attributes (e.g., battery life, allergens, accessibility)
   - **Inventory and price freshness** — Real-time availability, last-updated stamp on price feed, stock-level granularity (in stock / low stock / backorder)
   - **Trust signals an agent can parse** — Review volume + recency + average + distribution; named third-party certifications (organic, fair-trade, ISO, etc.); shipping speed and cost, return policy, and warranty in structured form
   - **Image and media** — Multiple high-res images per SKU, alt text with full product context, video where the category warrants, all referenced via schema
   Score each on a 0–4 rubric per dimension and compute an overall machine-readability index per page.

4. **Score feed hygiene at the catalog level.** Across the merchant feed(s) audit:
   - **Fill rate** — Percentage of SKUs with each required and recommended attribute populated (Google Merchant Center disapproval and warning rates are a leading indicator)
   - **Freshness** — Time-since-last-update distribution; flag any SKU stale > 24 hours for inventory and 7 days for price
   - **Title and description specificity** — How well titles include category + brand + key attributes; avoid marketing copy in title fields
   - **GTIN / MPN coverage** — GTIN coverage is a major agentic recommendation differentiator
   - **Image-per-SKU coverage** — Minimum two distinct images per SKU; primary image without watermark or text overlay
   - **Variant handling** — Are color / size / material exposed as variants with their own structured offers, or buried in a single page
   Catalog data quality is the single largest non-protocol agentic visibility lever — merchants with 95%+ fill rates on core attributes consistently appear in agent comparison sets where 70%-fill peers do not.

5. **Build the protocol-readiness map.** For each of the 10 protocols listed in step 1, mark current state, blocker (if any), and the cost / effort / window to enable. Highlight the top three to enable next quarter on the basis of (a) agent surface where the brand is most likely to be recommended for this category, (b) effort to enable, and (c) whether the protocol is open or walled-garden. As of Q2 2026, walled-garden protocols (Shopify Agents, Amazon Buy for Me, Google Agentic Checkout, Klarna Agent Mode) generally compound faster than open protocols inside their host platform, while open protocols (ACP, UCP, x402) compound across multiple agent surfaces but require more in-house implementation.

6. **Diagnose the recommendation-share gap.** For each prompt where the brand failed to surface, classify the cause:
   - **Catalog gap** — SKU not in merchant feed, missing GTIN, missing required attribute
   - **Schema gap** — Page exists but agent can't parse offer, price, availability, or rating
   - **Trust gap** — Review volume / recency / certifications below the agent's apparent threshold for the category
   - **Protocol gap** — Brand not enrolled in the surface that returned the result
   - **Price / speed gap** — Brand is in the comparison set but loses on price, ship speed, or availability — escalate to merchandising and operations, not to marketing
   - **Hallucination** — Agent returned wrong information about the brand (route to **Brand Safety & Crisis Response Planner**)

7. **Build the prioritized 90-day fix list.** Rank 8–15 interventions by expected agentic recommendation lift × effort. Each intervention has:
   - The gap it addresses (catalog / schema / trust / protocol / price-speed)
   - The owner (merchandising, web, product, ops)
   - The metric it moves (recommendation appearance rate, position, accuracy, transaction completion without handoff)
   - The effort window (this sprint / this quarter / next quarter)
   - The dependency on adjacent skills (route schema work to AEO Content Optimizer, route messaging gaps to Topic Cluster Planner, route review-volume gaps to Customer Review & Insight Miner, route hallucinations to Brand Safety & Crisis Response Planner)

8. **Set up the recurring program.** If this is not a one-off:
   - Cadence (quarterly default; monthly for high-velocity categories like fashion, electronics, food)
   - 8–12 "tracker prompts" held constant across audits for time-series comparability
   - Reporting frame: agent recommendation rate, agent recommendation position, transaction-completion rate without human handoff, accuracy rate, protocol enrollment delta, top three gains, top three losses
   - Owner per intervention, standing review meeting, and an escalation rule when the agent recommendation rate falls below the floor for a tracker prompt

**Output requirements:**
- Agent surface map (which surfaces are in scope and why)
- Agent ICP prompt set with answer-trail captures (10–20 prompts × 3–5 surfaces)
- Page machine-readability scorecard (rubric per dimension per representative page)
- Catalog feed hygiene scorecard (fill rate, freshness, GTIN coverage, variant handling)
- Protocol-readiness map (10 protocols, current state, top three to enable next quarter)
- Recommendation-share gap diagnosis
- Prioritized 90-day fix list (8–15 interventions, owner, metric, effort, dependencies)
- Recurring program design (if applicable)
- Assumptions, sampling-bias notes, and known unstable surfaces (agentic platforms change weekly in 2026)
- Saved to `outputs/agentic-commerce/` if the user confirms

## Calibration Notes

- **Agent recommendation share is not the same as Share of Model.** SoM measures whether an AI engine names your brand in an answer. Agent recommendation share measures whether an AI agent puts your SKU in its comparison set when it is buying on a user's behalf. They are correlated but rarely 1:1 — many brands have strong SoM and weak agent recommendation share because content discovery does not require a clean feed and agents do.
- **Catalog data quality dominates protocol participation.** A brand with 95% feed fill rate and no protocol enrollment will often outperform a brand at 60% fill with three protocol enrollments. Fix the data first.
- **Walled-garden vs. open-protocol trade-off.** Walled gardens compound inside their host platform faster but lock you to that surface; open protocols (ACP, UCP, x402) compound across many surfaces but require more implementation work. The right mix depends on where the category's agent traffic is concentrated; for most consumer categories in 2026, two walled gardens + one open protocol is a defensible starting point.
- **Hallucinations propagate slowly.** Like AI-engine answers, agent recommendations correct on the order of weeks, not hours. Plan multi-quarter lift curves; the only short-term correction path goes through the Brand Safety & Crisis Response playbook.
- **Don't conflate transactable and pre-transactable categories.** B2B SaaS with a sales-led motion does not need the same protocol surface coverage as DTC consumer goods; for B2B the focus is on agentic-discoverable proof signals, structured pricing where exposed, and integrations with research-style agent surfaces (Perplexity, ChatGPT, Claude). Tailor the audit accordingly.
- **Agent-recommendation cause attribution is noisy in 2026.** Agents rarely expose why they chose one brand over another in machine-readable form. Score the answer text to extract reasoning patterns, but treat reasoning attribution as a working hypothesis, not a verified cause.
- **Don't stretch one prompt set across categories.** Service and booking categories (dental, salon, contractor) score on availability and proximity; consumer goods score on price, speed, and ratings; SaaS scores on integration and pricing transparency. Use category-appropriate prompts per audit.
- **The agent layer is changing weekly.** Mark the surface map with a "verified-on" date and re-verify before any quarterly readout — protocol terms, walled-garden inclusion criteria, and surface availability shift faster than any other layer in marketing technology in 2026.

## Example Output

### Sample Agent Surface Map (DTC personal care brand, US-only, Q2 2026)

| Surface | Status | Why in scope |
|---|---|---|
| ChatGPT (ACP) | Active | Brand category surfaces in 60%+ of "best non-toxic" prompts |
| Microsoft Copilot Checkout | Open enrollment | 500K+ merchants live; brand SKU class qualifies |
| Perplexity Shopping | Active | Comparison-shopping prompts dominant |
| Shopify Agents | Active | Brand on Shopify Plus; native enrollment |
| Amazon Buy for Me | Open enrollment | Brand has Amazon storefront |
| Google Agentic Checkout | Open enrollment | Active in Google Merchant Center |
| Klarna Agent Mode | Monitor only | Klarna penetration low in category |
| Yelp AI Assistant | Out of scope | Not a service category |
| ACP / UCP / x402 / Visa Ready / Mastercard Verifiable Intent | Open / monitor | Stripe Machine Payments via existing Stripe stack |

### Sample Page Machine-Readability Scorecard (representative SKU)

| Dimension | Score (0–4) | Top fix |
|---|---|---|
| Product schema | 3 | Add `priceValidUntil` and `gtin13` |
| Offer schema | 2 | Expose variants as separate Offer entities; add `shippingDetails` |
| AggregateRating + Review | 4 | Maintain |
| Image schema | 2 | Add 3 more SKU images, structured per variant |
| Attribute fill | 2 | Add ingredients, country of origin, warranty (currently 60% of category-relevant attributes) |
| Inventory freshness | 4 | Maintain |
| Third-party trust | 2 | No structured certifications exposed; brand has two unlinked certifications |
| **Overall index** | **2.7** | Schema + attribute completeness are the top levers |

### Sample Top-of-List Intervention

**Intervention:** Bring representative SKU class machine-readability index from 2.7 → 3.7 by expanding Offer schema (variants, shippingDetails, priceValidUntil), structuring two existing certifications via schema, and adding three category-required attributes (ingredients, country of origin, warranty) across the catalog.
**Gap addressed:** Schema + attribute fill (causes recommendation appearance failure on 60% of agent prompts where SKU class loses to better-attributed peers).
**Owner:** Web engineering + merchandising.
**Effort:** 6 weeks (web schema lift) + 4 weeks (catalog attribute backfill, in parallel).
**Metric movement target:** Agent recommendation appearance rate from 32% → 55% across tracker prompts on ChatGPT, Perplexity, and Copilot Checkout; transaction-completion-without-handoff rate from 70% → 88%.
**Dependencies:** Route schema work to **AEO Content Optimizer** for the Q&A and HowTo blocks; route the 18 SKUs with review volume below category threshold to the **Customer Review & Insight Miner** lift program.

## Integration Notes

- **Pair with AI Search Visibility Audit** — Visibility (SoM) and recommendation share are different layers. Run both; gaps that appear in both layers route to a coordinated content-and-catalog plan.
- **Pair with AEO Content Optimizer** — Schema and Q&A schema work for product/service pages route through AEO; this skill identifies which pages, AEO fixes them.
- **Pair with Customer Review & Insight Miner** — Review-volume and recency gaps that suppress agent recommendations route through the review program.
- **Pair with Brand Safety & Crisis Response Planner** — Hallucinated agent recommendations or factual errors above a severity threshold escalate into the crisis playbook.
- **Pair with Cross-Channel Attribution Analyzer** — As agent-mediated transactions grow, attribution treatment shifts; surface this audit's findings into the next attribution review.
- **Pair with Competitive Analysis Brief** — When a competitor consistently outranks the brand in agent comparison sets, run a teardown of their feed, schema, and protocol footprint, not just their messaging.
- **Hand off to product / engineering** — Most fixes from this skill belong outside marketing. Marketing's job is to detect, scope, and route; product and engineering own the implementation.

## Anti-Patterns to Avoid

- Treating agentic commerce as "Performance Max but newer" — it is feed, schema, and protocol work, not bid strategy
- Enrolling in every protocol before the catalog is clean — protocol participation amplifies your data quality, good or bad
- Optimizing only the top 10 SKUs — agent comparison sets surface long-tail SKUs more than human shoppers do; comprehensive feed hygiene beats top-SKU obsession
- Reporting one number ("agent recommendation rate = 42%") without surface and prompt breakdown — agent surfaces vary so widely that the average hides the real gap
- Conflating SoM and agent recommendation share — they require different fixes, and quoting them as a single visibility metric obscures action
- Chasing every new protocol — pick the two or three concentrated where your category's agent traffic actually lives
- Ignoring the ops / merchandising side of the gap — when the cause is price, ship speed, or stock, marketing cannot fix it; route it
- Failing to re-verify the surface map quarterly — the agent layer in 2026 changes faster than any other marketing surface, and stale audits silently misallocate work
