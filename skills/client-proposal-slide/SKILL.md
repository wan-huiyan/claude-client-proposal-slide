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
  "create a one-pager for the client", "make an HTML slide", or wants to summarize technical
  analysis for stakeholder buy-in. Produces three HTML versions (detailed, minimal, bullet-point)
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

## When This Skill Activates

- User wants to propose model improvements or new features to a client
- User has analysis results (JSON, markdown, BQ output, or conversation context) to visualize
- User needs to communicate technical findings to non-technical stakeholders
- User asks for a "slide", "deck", "presentation", or "proposal"

## Process

### Step 1: Discovery & Context (Brainstorming Phase)

Before building anything, invoke the `brainstorming` skill mindset to understand what the user
actually needs. Ask clarifying questions **one at a time** to fill in gaps. Do NOT proceed to
slide creation until you have clear answers on these dimensions:

**Required context (ask if not provided):**
1. **Who is in the room?** — Job titles, decision-making authority, technical literacy level.
   A VP of Enrollment thinks differently than a CIO. Tailor language and emphasis accordingly.
2. **What decision does this need to drive?** — Budget approval? Prioritization? Buy-in for
   a pilot? "Informational" is not a valid answer — every proposal needs an ask.
3. **What can they actually do with this?** — Which teams will act on the insights? What
   existing workflows or tools will change? If you can't name concrete actions, the proposal
   is too abstract.
4. **What's the status quo cost?** — What happens if they do nothing? Lost revenue, missed
   students, operational blind spots? Quantify inaction.
5. **What has been tried before?** — Prior initiatives, vendor tools, or internal projects
   in this space. Avoids proposing something they've already rejected.

**Optional context (ask if relevant):**
- Timeline constraints or budget cycles
- Competing priorities or organizational politics
- Whether this is a first proposal or a follow-up to prior work
- Preferred presentation format (screen share, printed, emailed)

**HARD GATE:** Do not proceed to Step 2 until the user has answered at minimum questions 1-3.
If the user says "just make it", push back once — the activation framing requires knowing the
audience and the desired action. If they insist, use reasonable defaults and flag assumptions.

### Step 2: Gather Source Material

Read all referenced analysis files. These might be:
- **JSON results** from analytical queries (enrollment rates, feature evaluations, etc.)
- **Markdown docs** (analysis reports, implementation plans, benefit assessments)
- **Conversation context** (the user may describe findings verbally)
- **BQ query results** or data summaries

Extract the key narrative elements:
- **The problem**: What gap, blind spot, or limitation exists today?
- **The evidence**: What data proves the problem and validates the solution?
- **The solution**: What specific changes are proposed?
- **The impact**: What measurable improvement is expected?
- **The ask**: What does the client need to approve or fund?

### Step 3: Translate for the Audience

Apply the language, attribution, and number rules from `references/language-rules.md`.
Key principles: never use ML jargon (AUC, entropy, F1), replace "features" with "signals",
use directional language instead of unvalidated accuracy numbers, and prefer rates over raw counts.

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

This two-tier structure builds trust with the client: it shows analytical rigor rather than
overselling everything as a sure thing. Items that clearly belong in "Optimisation" are those
with quantified diagnostic evidence (e.g., enrollment gradients, coverage gap analysis). Items
where the raw data is confounded, the sample is small, or the causal mechanism is unclear
belong in "Explore."

### Step 5: Business Activation — "So What? Now What?"

Every proposal must answer: **"What do I do Monday morning?"** for each stakeholder in the room.
This is the most important differentiator from a generic technical report. Without activation
framing, even the best analysis becomes shelf-ware.

**For each proposed improvement, define:**

1. **Who acts on this?** — Name the team/role (e.g., "Admissions counselors", "IT/CRM admin",
   "Enrollment marketing"). If nobody specific acts, the proposal is too abstract.
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

Organize content into a left-to-right story flow:

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

Invoke the `frontend-design` skill for HTML generation. Pass it the constraints and layout
specs from `references/html-build-specs.md`. Do not re-implement typography or visual
design decisions — delegate those to `frontend-design`.

### Step 8: Deliver Four Outputs

Generate all four files:
1. `[name]_slide.html` — Detailed 3-column version with full evidence and activation
2. `[name]_slide_minimal.html` — 2-column version with ~40% less text
3. `[name]_slide_bullets.html` — Plain bullet-point version, minimal styling
4. `[name]_slide.pdf` — Print-ready PDF from detailed HTML

See `references/html-build-specs.md` for PDF generation commands (Chrome headless or puppeteer)
and `@media print` rules. Open all HTML versions in the browser for preview.

### Step 9: Accuracy Review (Optional but Recommended)

When the deck makes verifiable claims against a codebase or data source, run the
`agent-review-panel` skill to adversarially verify accuracy. Apply fixes across all
three versions. See `references/accuracy-review.md` for trigger criteria and common
over-claim patterns.

### Step 10: Iterate on Feedback

Client-facing materials require iteration. Common feedback patterns:
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

## Examples

See `references/language-rules.md` for narrative framing examples (bad technical vs good client-friendly).
See `references/activation-patterns.md` for activation framing examples.

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

- If source data files are empty or missing, ask the user to provide data before proceeding.
  Do not generate slides with fabricated content.
- If the `frontend-design` skill is unavailable, fall back to inline CSS styling. The output
  will be functional but less visually polished. Log a warning.
- If Chrome headless fails for PDF generation, skip the PDF and inform the user. The three
  HTML files are the primary deliverables.
- If discovery questions are skipped, proceed with reasonable defaults and flag all assumptions
  explicitly in the output.

## Safety & Idempotency

This skill is safe to re-run multiple times. Each run produces new output files without
modifying existing files. Running again with the same input produces equivalent output.
No side effects beyond file creation.

## Composability & Handoff

- **Before this skill:** Use the `brainstorming` skill for discovery if context is unclear.
- **After this skill:** Use `agent-review-panel` to verify accuracy of claims in the deck.
- **Depends on:** `frontend-design` skill for HTML generation quality. Requires Google Chrome
  for PDF export (if not available, use puppeteer as alternative, or skip PDF).
- **For internal documentation** instead of client proposals, use a different approach —
  suggest using standard markdown docs or wiki tools instead.
- Works with Claude Code compatible with version >= 1.0. Supported versions: Claude Code v1.x+.
