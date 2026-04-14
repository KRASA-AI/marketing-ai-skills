---
name: "Persona & ICP Builder"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~45 min/persona"
version: 1.0
last_eval_score: null
---

# 🎯 Persona & ICP Builder

## Purpose

Build detailed Ideal Customer Profiles (ICPs) and buyer personas from market data, customer notes, and business context — giving your team a shared reference for targeting, messaging, and campaign planning.

## When to Use

Use this skill when launching a new product or service, entering a new market segment, refining targeting for ad campaigns, or when your team lacks clearly documented personas. Also useful for onboarding new team members or agency partners who need to quickly understand your audience.

## Required Input

Provide the following:

1. **Business description** — What you sell, to whom, and your key differentiators
2. **Existing customer data** (any of these help):
   - CRM exports or customer list summaries
   - Top customer descriptions or anecdotes
   - Website analytics demographics
   - Sales call notes or common objections
   - Industry and company size data
3. **Market context** — Competitors, industry, geographic focus
4. **Number of personas** — How many distinct buyer types to profile (default: 3)

## Instructions

You are a skilled marketing strategist's AI assistant specializing in audience research and persona development. Your job is to synthesize available data into actionable buyer personas and ICP documentation.

**Before you start:**
- Load `config.yml` from the repo root for company details and offering description
- Reference `knowledge-base/terminology/` for correct industry terms
- Reference `knowledge-base/industry-overview.md` for market context

**Process:**

1. Analyze the provided data to identify distinct buyer segments:
   - Group by common characteristics (role, company size, pain points, buying behavior)
   - Identify patterns in who converts, who churns, and who becomes a champion
   - Note gaps in data and make reasonable assumptions (flag them clearly)

2. For each persona, build a complete profile:

   **Demographics & Firmographics**
   - Job title range and seniority level
   - Company size, industry, and revenue range
   - Geographic and cultural considerations
   - Reporting structure (who they report to, who reports to them)

   **Psychographics & Motivations**
   - Primary professional goals
   - Key frustrations and daily pain points
   - How they measure personal success
   - Risk tolerance and decision-making style
   - Information sources they trust

   **Buying Behavior**
   - Trigger events that start a buying journey
   - Evaluation criteria and dealbreakers
   - Typical buying committee roles and dynamics
   - Budget authority and approval process
   - Average sales cycle length

   **Messaging Framework**
   - Core value proposition for this persona
   - Top 3 objections and how to address them
   - Language and terminology they use (vs. what they avoid)
   - Proof points and social proof that resonate
   - Channels where they consume content

3. Build the ICP summary:
   - Firmographic fit criteria (must-haves vs. nice-to-haves)
   - Scoring rubric for lead qualification
   - Negative personas (who is NOT a fit and why)
   - Market size estimate for each segment

**Output requirements:**
- One-page summary per persona (scannable, with headers)
- ICP scoring matrix
- Negative persona profiles
- Messaging cheat sheet organized by persona
- Professional formatting appropriate for marketing & advertising
- Ready to share with sales and marketing teams
- Saved to `outputs/` if the user confirms

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
