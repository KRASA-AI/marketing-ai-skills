# AI Content Disclosure & Provenance — Marketing Compliance Reference

*Maintained by the KRASA landscape monitor. Last updated 2026-06-29. This is a working reference for marketers, not legal advice; confirm specifics with counsel before relying on it for a launch.*

## Why this file exists

Through the first half of 2026 the question "do we have to tell people this ad was made with AI?" moved from a brand-judgment call to a hard compliance line, and it did so from three directions at once: binding regulation (the EU AI Act), a maturing technical provenance stack (C2PA Content Credentials plus model-level watermarking such as SynthID), and industry self-regulation that now carries real penalties (the Cannes Lions creative-integrity framework). For a marketing team that generates ads, social posts, images, video, or copy with AI — which by mid-2026 is most teams — these strands collapse into one operating requirement: **AI-generated and AI-manipulated marketing content must increasingly be disclosed, labeled, and provenance-marked, and the brand must be able to prove what it claims about its own work.** This file is the standing reference the Brand Safety & Crisis Response Planner and Creative Brief Generator consult for that requirement.

## 1. The EU AI Act — Article 50 transparency obligations

The EU AI Act is the binding instrument and the one with a near-term deadline.

- **What Article 50 requires.** Article 50 covers transparency for "certain AI systems." The two clauses that matter most for marketing are: (a) providers of generative AI must mark outputs in a machine-readable format detectable as artificially generated or manipulated; and (b) deployers — which includes a brand or agency publishing AI-generated content — must disclose AI generation/manipulation in defined cases, most importantly **deepfakes** (AI-generated or manipulated image, audio, or video resembling real people, places, or events) and AI-generated text published to inform the public on matters of public interest. The deployer-side disclosure must be clear and distinguishable, at the latest at first interaction/exposure.
- **The deadline.** The Act entered into force August 1, 2024, but the Article 50 transparency obligations become **enforceable on August 2, 2026** — roughly five weeks out as of this writing. A transitional carve-out from the May 2026 "AI Omnibus" provisional agreement gives generative systems already on the market before that date until **December 2, 2026** to meet the machine-readable marking requirement of Article 50(2); the deployer disclosure duties are not similarly extended.
- **The Code of Practice.** The European Commission published its **Code of Practice on Transparency of AI-Generated Content on June 10, 2026** — a voluntary-adherence guide that operationalizes Article 50 (marking techniques, labeling conventions, what counts as adequate disclosure). Signing it is not mandatory, but it is the clearest available signal of what regulators will treat as compliant, so it functions as the de facto implementation spec.
- **Who it reaches.** Extraterritorial by design: the obligations attach to any organization placing AI systems on the EU market or whose AI-generated content reaches people in the EU, regardless of where the company is headquartered. A US brand running AI-generated creative that EU users can see is in scope.
- **Penalties.** Non-compliance with the Article 50 transparency duties can draw fines up to **€15 million or 3% of total worldwide annual turnover, whichever is higher.** This applies to both providers and professional deployers.

**Marketing takeaway:** treat August 2, 2026 as a real launch gate. Any campaign with EU reach that uses AI-generated imagery, synthetic voice/video, AI-altered footage of real people, or AI-written public-interest text needs a disclosure decision documented before it ships, and the assets should carry machine-readable provenance marks.

## 2. The technical provenance stack — C2PA, Content Credentials, SynthID

Disclosure obligations presuppose a way to mark and detect AI content. By mid-2026 that infrastructure is in production, though imperfect.

- **C2PA / Content Credentials** is the cross-industry open standard for cryptographically signed provenance ("nutrition labels" for media — what made it, when, what edits were applied). Adoption is real but partial: Adobe (Content Credentials across Creative Cloud / Firefly), OpenAI (C2PA metadata on supported generated media), Google (Content Credentials verification rolling across Gemini, Search, and Chrome), Microsoft (C2PA metadata added to M365-generated content), and camera makers (Sony's PXW-Z300 as the first native-C2PA camcorder; Leica/Nikon/Canon/Fujifilm/Panasonic on the stills side).
- **Model-level watermarking (SynthID and peers)** embeds an imperceptible signal directly in generated pixels/audio rather than in detachable metadata. Google reports SynthID verification live for image, video, and audio in Gemini and expanding to Search and Chrome; OpenAI has signaled a layered approach combining C2PA metadata with watermarking and public verification.
- **The load-bearing caveat — metadata is fragile.** Social platform upload pipelines, screenshots, re-encodes, and exports routinely strip embedded C2PA manifests. A platform can "support" Content Credentials and still strip them in practice. So provenance metadata is a **signal, not proof**, and embedded watermarking (harder to strip) plus a visible on-asset label are the more durable belt-and-suspenders approach for marketing assets that will travel through social pipelines.

**Marketing takeaway:** to satisfy the EU machine-readable-marking duty *and* survive distribution, pair C2PA signing at export with model-level watermarking where the generator supports it, and don't rely on metadata alone for anything you legally need to be able to prove later — keep a visible label and an internal provenance record too.

## 3. US state law — the parallel track

The US has no federal AI-labeling statute, but state law is moving and is architecturally compatible with C2PA.

- **California SB 942 (AI Transparency Act)** — effective January 2026 — requires large generative-AI providers to offer detection tooling and provenance disclosure.
- **California AB 853** — effective January 2027 — extends transparency/labeling duties further (e.g., to large platforms and capture devices).
- Several other states have election-deepfake and disclosure statutes; the FTC's existing endorsement/deception authority already reaches undisclosed AI in advertising even without an AI-specific rule.

**Marketing takeaway:** a brand already engineering for EU Article 50 + C2PA will be substantially aligned with the emerging California regime; build once to the stricter (EU) bar.

## 4. Industry self-regulation — the Cannes Lions creative-integrity precedent

Regulation is not the only enforcement vector. In June 2026 the advertising industry's flagship awards body formalized its own AI-disclosure regime, triggered by a fraud case, and it now carries career-level penalties.

- **The trigger.** Brazilian agency DM9 had a 2025 Cannes **Creative Data Grand Prix** (plus additional Lions — twelve awards in total across the implicated entries) **revoked** after it emerged that case-study materials, including manipulated broadcast footage, had been AI-doctored; CNN Brasil's complaint precipitated the agency's own admission of "serious inconsistencies" and the withdrawal of three entries.
- **The new framework (for 2026 submissions onward).** Cannes Lions introduced a creative-integrity framework underpinned by an **AI Integrity Handbook**: **mandatory disclosure of AI use** in every entry (non-disclosure is itself grounds for disqualification/withdrawal); a **dual-layer verification system** combining AI-detection tooling with human review of case films; **executive sign-off** requiring both the agency business leader (CEO) and a senior brand-side marketer (CMO) to personally attest to each entry; an independent **Integrity Council** of legal/ethics experts to adjudicate disputes; and penalties up to **three-year bans** plus revocation of jury eligibility.
- **Why marketers should care beyond awards.** This is the most visible instance of the industry treating *undisclosed* AI and *unverifiable* claims as integrity violations rather than style choices, and of pushing accountability up to the executive who signs. It is a useful template for an internal content-integrity policy even for brands that never enter an award: disclose AI use, verify claims before publishing, and name an accountable signer.

## 5. Practical compliance checklist for marketing teams

Use this as a pre-publish gate; the Creative Brief Generator should capture the answers at kickoff and the Brand Safety planner should hold the standing policy.

1. **Reach test.** Will the asset be visible to EU users? If yes, Article 50 applies. (When unsure, assume yes for anything on open social or a public site.)
2. **Content-type test.** Does the asset contain AI-generated/altered depiction of real people, places, or events (deepfake territory), synthetic voice, or AI-written public-interest text? These carry the strongest deployer disclosure duty.
3. **Disclosure decision.** Decide and document the disclosure method (visible label/caption, in-platform AI tag, voiceover/footer) and the wording. Non-disclosure must be a deliberate, documented call, not an omission.
4. **Provenance marking.** Export with C2PA Content Credentials; enable model watermarking (e.g., SynthID) where the generator offers it; keep an internal provenance log (tool, model/version, prompt or edit summary, human reviewer).
5. **Claim verification.** Any performance/impact claim in the creative or in a case study must be backed by a named source and baseline before publish (the Cannes "proof over hype" + verification discipline applied internally).
6. **Accountable signer.** Name the person who attests the asset is disclosed, marked, and claim-verified — the internal analog of the Cannes CEO/CMO sign-off.
7. **Distribution durability.** For assets going through social pipelines, don't rely on metadata surviving; keep the visible label and the internal record.
8. **Refresh trigger.** Re-check when a new rule lands (Article 50 enforcement Aug 2 / marking extension Dec 2, 2026; California AB 853 Jan 2027; platform policy updates).

## Key dates at a glance

- **June 10, 2026** — EU Code of Practice on Transparency of AI-Generated Content published (implementation spec for Article 50).
- **June 2026** — Cannes Lions creative-integrity framework + AI Integrity Handbook announced (mandatory AI disclosure, dual-layer verification, CEO/CMO sign-off, Integrity Council, up to 3-year bans).
- **August 2, 2026** — EU AI Act Article 50 transparency obligations become enforceable.
- **December 2, 2026** — Extended deadline for pre-existing generative systems to meet the Article 50(2) machine-readable marking requirement.
- **January 2026 / January 2027** — California SB 942 in effect / AB 853 in effect.

## Sources scanned (for monitor traceability, not for verbatim reuse)

EU AI Act Article 50 text and transparency-rules guidance (artificialintelligenceact.eu); European Commission Code of Practice on AI-Generated Content (digital-strategy.ec.europa.eu) and law-firm analyses (Bird & Bird, Jones Day, Plesner, Bratby Law); C2PA / Content Credentials adoption reporting (contentauthenticity.org, eyesift, SoftwareSeni, Editors Weblog); Cannes Lions integrity-framework coverage (LBBOnline, Adweek, The Drum, Marketing Dive, Storyboard18, Campaign, DMNews). All prose above is original KRASA synthesis written in marketing-operations terms; dates, figures, statute names, and penalty amounts are factual references.
