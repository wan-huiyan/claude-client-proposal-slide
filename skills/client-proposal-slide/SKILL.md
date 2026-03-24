---
name: client-proposal-slide
description: |
  Create polished, activation-focused HTML presentation slides for proposing ML/data science
  enhancements to non-technical clients. Starts with a brainstorming discovery phase to
  understand audience, decision context, and stakeholder workflows before building anything.
  Use this skill whenever the user asks to create a presentation, slide, deck, or proposal
  for a client based on analysis results, model improvements, or data project findings. Also
  trigger when the user says "design a slide", "make a PPT", "client presentation", "propose
  to the client", "present findings to stakeholders", "turn analysis into a deck",
  "summarize for the VP", "build a proposal deck", "translate technical results for the client",
  "create a one-pager for the client", "make an HTML slide", "present findings to the VP",
  "present to the admissions team", or wants to summarize technical analysis for stakeholder
  buy-in. Produces three HTML versions (detailed, minimal, bullet-point)
  plus a PDF with proper page breaks. Translates technical ML jargon into client-friendly language.
  Splits proposed changes into "Model Optimisation" (high-confidence) and "Areas We Could Explore"
  (needs validation) with estimated hours. Every proposal item includes business activation — who
  acts, what changes in their workflow, and how success is measured.
  NOT for: internal documentation, code review, data analysis, building dashboards, writing READMEs,
  CI/CD setup, model debugging, unit testing, or any non-client-facing deliverable.
  Do not use for conference talks, internal retros, or wiki pages.
version: 3.2.0
dependencies:
  required:
    - frontend-design skill (for HTML generation)
  optional:
    - brainstorming skill (for discovery phase)
    - agent-review-panel skill (for accuracy review)
    - Google Chrome or puppeteer (for PDF generation)
compatible_with: "Claude Code v1.0+"
namespace: client-proposal-slide
---

# Client Proposal Slide Generator

Create compelling, single-slide HTML presentations that translate technical ML/data analysis
into client-friendly proposals. The output is a self-contained HTML file at 16:9 aspect ratio
(1280x720px) that can be opened in a browser, screenshotted for PowerPoint, or printed to PDF.

## Process

### Step 1: Discovery & Context (Brainstorming Phase)

Ask clarifying questions **one at a time** before building. Required context:

1. **Who is in the room?** — Job titles, decision authority, technical literacy
2. **What decision does this drive?** — Budget approval, prioritization, pilot buy-in ("informational" is not valid)
3. **What can they do with this?** — Which teams act, what workflows change
4. **Status quo cost?** — Quantify what happens if they do nothing
5. **What's been tried before?** — Avoids proposing rejected ideas

Optional: timeline/budget cycles, competing priorities, first vs follow-up, format preference.

**HARD GATE:** Minimum questions 1-3 answered before Step 2. Push back once if user says "just make it". If they insist, use defaults and flag assumptions.

### Step 2: Gather Source Material

Read all referenced analysis files (JSON, markdown, BQ output, or conversation context). Extract these narrative elements because they form the slide's story arc:
- **The problem**: What gap or limitation exists today?
- **The evidence**: What data validates the solution?
- **The solution**: What specific changes are proposed?
- **The impact**: What measurable improvement is expected?
- **The ask**: What does the client need to approve or fund?

Verify all extracted numbers against the source data since misquoted metrics damage credibility.

### Step 3: Translate for the Audience

Apply the language rules from `references/language-rules.md`. Remove all ML jargon (AUC, entropy, F1) because clients cannot act on abstract metrics. Replace "features" with "signals". Use directional language instead of accuracy numbers since unvalidated numbers erode trust. Verify all counts are deduplicated and prefer rates over raw counts.

### Step 4: Categorize Proposed Changes

Split proposed changes into two confidence tiers:

**"Model Optimisation"** — High-confidence improvements backed by diagnostic evidence:
- Items where analysis has already demonstrated clear value (e.g., enrollment gradient, coverage gaps quantified)
- Include estimated implementation hours for each item
- These are the "we know this will help" items

**"Areas We Could Explore"** — Directionally promising but with unknowns that need validation:
- Items where the signal looks good but has confounders, limited data, or needs further investigation
- Include estimated hours AND what validation is needed
- These are the "worth investigating" items — be honest about uncertainty

Use this two-tier structure because it builds trust — clients see analytical rigor rather than overselling. Verify each item's tier: "Optimisation" requires quantified diagnostic evidence; "Explore" is for confounded data, small samples, or unclear causal mechanisms.

### Step 5: Business Activation — "So What? Now What?"

Define activation for every proposal item because without it, even the best analysis becomes shelf-ware. Every item must answer: **"What do I do Monday morning?"** for each stakeholder.

**For each proposed improvement, define:**

1. **Who acts on this?** — Name the team/role (e.g., "Admissions counselors", "IT/CRM admin"). Specify a role because if nobody specific acts, the proposal is too abstract.
2. **What changes in their workflow?** — Concrete operational shift. Not "better predictions"
   but "counselors receive a prioritized call list each morning sorted by enrollment likelihood,
   replacing the current alphabetical queue."
3. **What's the trigger?** — When does this kick in? Daily report? Dashboard alert? CRM field
   update? Automated email? Be specific about the delivery mechanism.
4. **What's the expected behavioral change?** — How will the stakeholder's actions differ from
   today? "Instead of calling all 500 admitted students equally, focus on the 120 flagged as
   at-risk of not enrolling."
5. **How will we know it's working?** — Observable success metric the stakeholder can track
   themselves (not model accuracy — business KPIs). E.g., "yield rate for contacted at-risk
   students vs. control group."

See `references/activation-patterns.md` for common activation patterns, anti-patterns,
and placement guidance per version (detailed/minimal/bullet-point).

### Step 6: Design the Narrative Structure

Organize content into a left-to-right story flow. Use this layout because it maps to how decision-makers scan proposals:

**Detailed version (3-column layout):**
- Left: The problem/opportunity (what's broken or missing)
- Center: The evidence + proposed signals/changes (using the two-tier structure)
- Right: The recommended action + expected impact

**Minimal version (2-column layout):**
- Left: The opportunity (problem + evidence together)
- Right: Proposed changes (using the two-tier structure)

**Bullet-point version (plain text layout):**
- Clean, simple slide with minimal styling — for stakeholders who prefer traditional decks
- White/light background, standard fonts acceptable, no charts or bars
- Organized as: brief context at top, then "Model Optimisation" bullets, then "Areas We Could Explore" bullets
- Each bullet includes the item name, a one-line description, and estimated hours
- Footer with implementation reassurances

All versions must include:
- A clear, non-technical title that captures the narrative (e.g., "Unlocking Untapped Admissions Data" not "Salesforce Feature Expansion")
- Company/client branding in the header
- A footer with implementation reassurances (single release, data validated, etc.)
- Key statistics as large, bold callouts (detailed/minimal) or inline numbers (bullet-point)
- A visually prominent callout for the primary recommendation
- Estimated hours per item in the proposed changes section

### Step 7: Build the HTML (via `frontend-design` skill)

Invoke `frontend-design` with constraints from `references/html-build-specs.md`. Delegate typography and visual design since this ensures consistent quality. Do not re-implement styling — call `frontend-design` because it produces distinctive, non-generic outputs.

### Step 8: Deliver Four Outputs

Generate all four files:
1. `[name]_slide.html` — Detailed 3-column version with full evidence and activation
2. `[name]_slide_minimal.html` — 2-column version with ~40% less text
3. `[name]_slide_bullets.html` — Plain bullet-point version, minimal styling
4. `[name]_slide.pdf` — Print-ready PDF from detailed HTML

See `references/html-build-specs.md` for PDF generation commands (Chrome headless or puppeteer)
and `@media print` rules. Open all HTML versions in the browser for preview.

### Step 9: Accuracy Review (Optional but Recommended)

Run `agent-review-panel` when the deck makes verifiable claims, because over-claims in client decks destroy credibility. Apply fixes across all three versions. See `references/accuracy-review.md` for trigger criteria.

### Step 10: Iterate on Feedback

Expect iteration on client-facing materials. Apply these common fixes:
- "Too technical" → rewrite using the language rules above
- "Can we add X section" → restructure the layout to accommodate
- "Numbers don't look right" → verify deduplication and units
- "Too busy" → move details to the minimal version, simplify the detailed one
- "Make X more prominent" → use accent colors, larger fonts, or a callout box

## Quality Checklist

Before delivering, verify:
- [ ] Discovery questions answered (Step 1) — audience, decision, activation identified
- [ ] No ML jargon (AUC, entropy, precision, recall, F1, log-odds, calibration)
- [ ] No unvalidated accuracy claims
- [ ] All counts verified for deduplication
- [ ] Cautious attribution for data source disagreements
- [ ] Title tells a story (not a technical label)
- [ ] Primary recommendation is visually prominent
- [ ] Proposed changes split into "Model Optimisation" and "Areas We Could Explore"
- [ ] Estimated hours included for each proposed item
- [ ] **Business activation defined** — each proposal item has: who acts, what changes, success metric
- [ ] **No orphan proposals** — every item answers "what does the stakeholder do differently Monday morning?"
- [ ] All three HTML versions produced (detailed, minimal, bullet-point)
- [ ] PDF version generated with proper page breaks (no content cut off mid-page)
- [ ] Footer includes implementation reassurances
- [ ] HTML built via `frontend-design` skill (not generic templates)
- [ ] Renders cleanly at 1280x720
- [ ] If deck references verifiable code/data: accuracy review panel run (Step 9)

## Input / Output Contract

**Input:** Takes as input one or more of: JSON analysis results, markdown reports, BQ query output,
conversation context describing findings, or file paths to analysis artifacts.

**Output:** Produces four files scoped to the `client-proposal-slide` namespace:
- `[name]_slide.html` — detailed 3-column version (1280x720px)
- `[name]_slide_minimal.html` — minimal 2-column version
- `[name]_slide_bullets.html` — plain bullet-point version
- `[name]_slide.pdf` — print-ready PDF from Chrome headless

All outputs are self-contained HTML with inline styles. No external dependencies at runtime.

## Error Handling

- If source data is empty or missing, ask the user to provide data. Do not generate slides with fabricated content because this erodes client trust.
- If `frontend-design` is unavailable, fall back to inline CSS. Log a warning since the output will be less polished.
- If Chrome headless fails for PDF, skip PDF and inform user. The HTML files are the primary deliverables.
- If discovery is skipped, use reasonable defaults and flag assumptions explicitly.

## Safety & Idempotency

Safe to re-run because each invocation creates new output files without modifying existing ones. No side effects beyond file creation. This means running again with updated data produces a fresh set without losing previous versions.

## Composability & Handoff

- **Before this skill:** Use the `brainstorming` skill for discovery if context is unclear.
- **After this skill:** Use `agent-review-panel` to verify accuracy of claims in the deck.
- **Depends on:** `frontend-design` skill for HTML generation quality. Requires Google Chrome
  for PDF export (if not available, use puppeteer as alternative, or skip PDF).
- **For internal documentation** instead of client proposals, use a different approach —
  suggest using standard markdown docs or wiki tools instead.
- Works with Claude Code compatible with version >= 1.0. Supported versions: Claude Code v1.x+.
