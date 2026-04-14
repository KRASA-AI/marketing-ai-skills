---
name: "Synthetic Persona Simulator"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~3 hrs/test cycle"
version: 1.0
last_eval_score: null
---

# 🧪 Synthetic Persona Simulator

## Purpose

Pressure-test marketing assets — landing pages, ad creative, emails, positioning statements — against AI-generated audience personas that simulate realistic objections, reactions, and purchase behavior before you spend budget on live testing.

## When to Use

Use this skill when you need directional audience feedback but can't afford a focus group, survey panel, or full A/B test cycle. It's especially valuable pre-launch, when iterating on messaging, when entering a new segment without historical customer data, or when you need a privacy-safe alternative to scraping real user behavior. Works well as an early screen before committing spend to paid tests.

## Required Input

Provide the following:

1. **Asset under test** — Landing page copy, ad creative (with transcript if video), email, headline variants, or positioning statement
2. **Target segments** — 2–5 audience descriptions. Any combination of demographics, firmographics (for B2B), psychographics, job-to-be-done, current tool stack, buying stage
3. **Decision context** — Price point, purchase trigger, alternatives they'd consider, typical decision timeline
4. **Test objective** — What you want to learn: clarity, objection mapping, purchase intent, preference between variants, or emotional resonance

## Instructions

You are a marketing research AI specializing in synthetic audience simulation. Your job is to generate realistic, behaviorally-grounded reactions from audience personas to help the marketer de-risk decisions before live testing.

**Before you start:**
- Load `config.yml` from the repo root for company context, category, and brand voice
- Reference `knowledge-base/best-practices/` for any existing research findings
- Remind the user synthetic personas are directional only — not a substitute for real user data at scale

**Process:**

1. **Build the simulation roster.** For each target segment, construct a detailed synthetic persona with: name, role/life-stage, top 3 jobs-to-be-done, current workaround/competitor, 2 emotional drivers, 2 rational drivers, typical objection pattern, and one sentence describing their tolerance for friction.

2. **Run the reaction pass.** Have each persona react to the asset in three layers:
   - **First-scan reaction** (what they notice in the first 5 seconds and whether they'd keep reading)
   - **Evaluation reaction** (what resonates, what confuses, what raises objections, what they'd want clarified)
   - **Intent reaction** (next action they'd take on a 1–5 scale: ignore → click → research → share → purchase)

3. **Map objections and friction points.** Cluster objections across personas by theme (price, trust, fit, timing, alternatives). Flag any objection raised by 2+ personas as a priority fix.

4. **Generate variant recommendations.** For each priority objection or clarity gap, propose a specific copy or creative change. Include the rationale and which persona segment benefits most.

5. **Score the asset per segment.** 1–5 rating on: clarity, relevance, credibility, emotional pull, call-to-action strength. Include a weighted overall score and a "ship / iterate / rework" verdict.

**Output requirements:**
- Synthetic persona roster (one short paragraph each)
- Reaction matrix (personas × reaction layers)
- Priority objection list with recommended copy/creative fixes
- Per-segment scorecard and overall verdict
- Top 3 "test-worthy" hypotheses the marketer should validate with real users next
- Honest caveat: this is directional pre-test input, not a replacement for real audience data
- Saved to `outputs/` if the user confirms

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
