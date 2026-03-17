---
name: client-proposal-slide
description: |
  Create polished, data-driven HTML presentation slides for proposing ML/data science
  enhancements to non-technical clients. Use this skill whenever the user asks to create
  a presentation, slide, deck, or proposal for a client based on analysis results, model
  improvements, or data project findings. Also trigger when the user says "design a slide",
  "make a PPT", "client presentation", "propose to the client", or wants to summarize
  technical analysis for stakeholder buy-in. Always produces three versions: one detailed,
  one minimal, and one plain bullet-point for traditional-deck stakeholders. Automatically
  translates technical ML jargon into client-friendly language. Splits proposed changes into
  "Model Optimisation" (high-confidence) and "Areas We Could Explore" (needs validation)
  with estimated hours.
version: 2.1.0
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

### Step 1: Gather Source Material

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

### Step 2: Translate for the Audience

The audience is non-technical. Apply these principles rigorously:

**Language rules:**
- Never use: AUC, entropy, proxy metrics, information gain, false positive rate, precision/recall, F1 score, log-odds, calibration, or any ML-specific metric name
- Instead of accuracy numbers from unvalidated analysis, use directional language: "clear differentiation", "significantly better ranking", "strong signal"
- Replace "features" with "signals" or "data points" when talking to clients
- Replace "model" with "the system" or "the scoring system" when appropriate
- Replace "training window" with "historical data available for learning" or similar
- Infrastructure details ("single model", "no architecture changes", "XGBoost") are internal — omit them unless the client specifically cares

**Attribution rules:**
- When two data sources disagree (e.g., CRM shows X but behavioral data shows Y), use cautious language ("some students" not "most students")
- Don't assert behavioral explanations for data gaps — the gap could be tracking issues, integration problems, or genuine behavior differences
- Don't quote specific accuracy percentages unless they come from a validated, deployed model

**Number rules:**
- Verify whether counts are unique entities or duplicated observations (e.g., per target_date in ML training data)
- Use the correct unit: "applications" vs "students" vs "observations"
- Percentages and rates are safer than raw counts for client communication (less ambiguity about deduplication)
- When showing enrollment/conversion rates, always note what the baseline comparison is

### Step 3: Categorize Proposed Changes

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

### Step 4: Design the Narrative Structure

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

### Step 5: Build the HTML

Use the `frontend-design` skill's principles for visual quality:

**Typography:** Use Google Fonts — pair a distinctive serif display font (e.g., Fraunces, Playfair Display) with a clean sans-serif body font (e.g., Outfit, DM Sans). Never use generic system fonts.

**Color:** Pick a cohesive scheme appropriate to the content:
- Dark themes work well for data-heavy, impressive slides
- Light themes work well for clean, simple proposals
- Use accent colors strategically for key numbers and callouts
- The "recommended" action should use a warm accent (amber/gold) to draw the eye

**Layout:**
- Fixed 1280x720px (16:9 aspect ratio)
- CSS Grid for the main layout
- Generous padding (44-56px edges)
- Thin accent line at top for visual polish
- Clear section labels (uppercase, letter-spaced, colored)

**Data visualization:**
- Horizontal bar charts for rate comparisons (simple CSS, no JS libraries needed)
- Stat cards/pills for key numbers
- Progress bars for before/after comparisons
- Keep it simple — if a number tells the story, you don't need a chart

**Responsive considerations:**
- Include `@media print` rules for PDF export
- Self-contained (all styles inline, Google Fonts via CDN)

### Step 6: Deliver Three Versions

Always produce all three:

1. **`[name]_slide.html`** — Detailed version with full evidence, multiple data points, and comprehensive impact section
2. **`[name]_slide_minimal.html`** — Brief version with ~40% less text, simpler layout, same key message
3. **`[name]_slide_bullets.html`** — Plain bullet-point version for traditional-deck stakeholders. Clean white background, minimal styling, no charts. Just organized text with the two-tier structure and hours.

Open all three in the browser for the user to preview. Explain the key differences.

### Step 7: Accuracy Review (Optional but Recommended)

When the deck makes **verifiable claims** against a codebase, data source, or analysis pipeline,
run the `agent-review-panel` skill to adversarially verify accuracy before presenting.

**When to trigger:**
- The deck references specific counts (e.g., "17 analysis types", "27 segments") derived from code
- The deck claims technical capabilities backed by SQL, scripts, or models
- The audience is technically sophisticated and will fact-check claims
- The deck describes methodology (e.g., "Markov attribution") that could be over-stated

**What the panel checks:**
- Do headline numbers match verifiable counts in the codebase?
- Does each claimed capability have backing code/SQL?
- Are methodological claims accurate (e.g., is "attribution" actually attribution, or just correlation)?
- Are there unbacked claims that could embarrass you if challenged?
- Are real capabilities missing from the deck (underselling)?

**How to use the output:**
- Fix any claims rated CRITICAL or HIGH by the panel
- Soften language where the panel flags over-statement (e.g., "every channel" → "key channels")
- Reduce counts to match only items with direct backing evidence
- Add qualifiers where methodology spans multiple tools (e.g., "AMC extraction + R modeling")

**Common over-claim patterns the panel catches:**
- Counting file variants as distinct capabilities (inflated numbers)
- Presenting a multi-step pipeline as a single capability (e.g., SQL + R as "SQL-based attribution")
- Claiming causal inference when only observational comparison exists ("incremental lift" vs "ad-exposed vs organic comparison")
- Using universal quantifiers ("every", "all", "unified") when coverage is partial
- Listing capabilities without backing implementation ("Custom rules" with no code)

After fixing panel findings, apply the same fixes across all three versions (detailed, minimal, bullets)
and any translations.

### Step 8: Iterate on Feedback

Client-facing materials require iteration. Common feedback patterns:
- "Too technical" → rewrite using the language rules above
- "Can we add X section" → restructure the layout to accommodate
- "Numbers don't look right" → verify deduplication and units
- "Too busy" → move details to the minimal version, simplify the detailed one
- "Make X more prominent" → use accent colors, larger fonts, or a callout box

## Quality Checklist

Before delivering, verify:
- [ ] No ML jargon (AUC, entropy, precision, recall, F1, log-odds, calibration)
- [ ] No unvalidated accuracy claims
- [ ] All counts verified for deduplication
- [ ] Cautious attribution for data source disagreements
- [ ] Title tells a story (not a technical label)
- [ ] Primary recommendation is visually prominent
- [ ] Proposed changes split into "Model Optimisation" and "Areas We Could Explore"
- [ ] Estimated hours included for each proposed item
- [ ] All three versions produced (detailed, minimal, bullet-point)
- [ ] Footer includes implementation reassurances
- [ ] Google Fonts load correctly (test in browser)
- [ ] Renders cleanly at 1280x720
- [ ] If deck references verifiable code/data: accuracy review panel run (Step 7)

## Example: Narrative Framing

**Bad (technical):**
> "Expanding application_stage from 4 to 7 categories improves proxy AUC from 0.50 to 0.96
> with 62% entropy reduction for submitted applications."

**Good (client-friendly):**
> "Today, all submitted applications are scored identically. By connecting directly to
> Salesforce admissions data, the system can distinguish between students still in review,
> those who've been accepted, and those who've deposited — with dramatically different
> enrollment outcomes at each stage."

**Bad (overconfident):**
> "Most students progress without triggering digital events."

**Good (cautious):**
> "Some students progress through the admissions funnel without triggering these
> digital events — Salesforce holds the authoritative record."
