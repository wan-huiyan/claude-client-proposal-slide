---
name: client-proposal-slide
description: |
  Create polished, activation-focused HTML presentation slides for proposing ML/data science
  enhancements to non-technical clients. Starts with a brainstorming discovery phase to
  understand audience, decision context, and stakeholder workflows before building anything.
  Use this skill whenever the user asks to create a presentation, slide, deck, or proposal
  for a client based on analysis results, model improvements, or data project findings. Also
  trigger when the user says "design a slide", "make a PPT", "client presentation", "propose
  to the client", or wants to summarize technical analysis for stakeholder buy-in. Always
  produces three HTML versions (detailed, minimal, bullet-point) plus a PDF with proper
  page breaks. Automatically translates technical ML jargon into
  client-friendly language. Splits proposed changes into "Model Optimisation" (high-confidence)
  and "Areas We Could Explore" (needs validation) with estimated hours. Every proposal item
  includes business activation — who acts, what changes in their workflow, and how success is
  measured. Delegates HTML generation to the frontend-design skill for distinctive visual quality.
version: 3.1.0
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

**Activation section placement:**
- **Detailed version:** Dedicated right-column section or callout box titled "What This Means For Your Team"
- **Minimal version:** 2-3 bullet points under each proposed change showing the operational impact
- **Bullet-point version:** A separate "Activation" section after the two-tier proposed changes,
  listing stakeholder → action → expected outcome for each item

**Common activation patterns for ML/propensity projects:**
- **Prioritized outreach lists** — scores drive daily/weekly contact queues
- **Triggered interventions** — score drops below threshold → automated alert to counselor
- **Resource allocation** — shift budget/staffing toward segments with highest ROI
- **Campaign targeting** — marketing segments based on propensity tiers
- **Early warning dashboards** — leadership sees at-risk cohorts before it's too late
- **Process redesign** — eliminate low-value steps, add high-value touchpoints

**Anti-patterns to avoid:**
- "Improved predictions" without saying who uses them and how
- "Better insights" without naming the insight and the action it drives
- "Data-driven decisions" without specifying which decision changes
- Activation plans that require the client to build new infrastructure you haven't scoped

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

Invoke the `frontend-design` skill for HTML generation. This skill handles typography, color,
motion, spatial composition, and visual details — do NOT re-implement those decisions here.
Instead, pass the frontend-design skill the following constraints specific to proposal slides:

**Constraints to pass to frontend-design:**
- **Format:** Self-contained HTML at 1280x720px (16:9 aspect ratio)
- **Purpose:** Client-facing proposal slide — must feel premium, trustworthy, and actionable
- **Tone:** Match to audience (executive = refined/minimal, operational = data-rich/structured)
- **The "recommended" action should use a warm accent (amber/gold) to draw the eye**
- **Must include `@media print` rules for PDF export**
- **Self-contained (all styles inline, Google Fonts via CDN)**

**Content layout guidance (pass to frontend-design as structure requirements):**
- CSS Grid for the main layout
- Generous padding (44-56px edges)
- Clear section labels (uppercase, letter-spaced, colored)

**Data visualization:**
- Horizontal bar charts for rate comparisons (simple CSS, no JS libraries needed)
- Stat cards/pills for key numbers
- Progress bars for before/after comparisons
- Keep it simple — if a number tells the story, you don't need a chart

**Activation section styling:**
- The "What This Means For Your Team" / activation content from Step 5 should be visually
  distinct — use a different background shade, icon badges per stakeholder role, or a
  bordered callout box. This section is what makes the proposal actionable, not just informative.

### Step 8: Deliver Four Outputs

Always produce all four:

1. **`[name]_slide.html`** — Detailed version with full evidence, multiple data points, and comprehensive impact section
2. **`[name]_slide_minimal.html`** — Brief version with ~40% less text, simpler layout, same key message
3. **`[name]_slide_bullets.html`** — Plain bullet-point version for traditional-deck stakeholders. Clean white background, minimal styling, no charts. Just organized text with the two-tier structure and hours.
4. **`[name]_slide.pdf`** — Print-ready PDF generated from the detailed HTML version

**PDF generation:** Convert the detailed HTML to PDF using puppeteer or browser print.
The HTML must include these `@media print` rules to prevent content splitting across pages:

```css
@media print {
  .section, .card, .callout { break-inside: avoid; }
  p { break-inside: avoid; }
  h1, h2, h3 { break-after: avoid; }
  .activation-panel { break-inside: avoid; }
}
```

**Option A — puppeteer (if available):**
```javascript
await page.pdf({
  path: outputPath,
  format: 'A4',
  printBackground: true,
  margin: { top: '15mm', bottom: '15mm', left: '12mm', right: '12mm' },
});
```

**Option B — Chrome headless (fallback, no npm install needed):**
```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless --disable-gpu \
  --print-to-pdf="/absolute/path/to/output.pdf" \
  --no-pdf-header-footer \
  --print-to-pdf-no-header \
  "file:///absolute/path/to/input.html"
```

Key gotchas for Chrome headless:
- **Always use absolute paths** for both `--print-to-pdf` and the HTML URL — Chrome writes
  relative to its own CWD, not the HTML file location.
- **`--no-pdf-header-footer`** is critical — without it Chrome adds a date, page title, URL,
  and page numbers to every page, which looks unprofessional.
- **`--print-to-pdf-no-header`** is a separate flag that also helps suppress headers.
- CVDisplayLink errors on macOS are harmless — ignore them.
- Prefer Option B when puppeteer is not pre-installed, as `npx puppeteer` downloads ~300MB.

Open all HTML versions in the browser for the user to preview. Explain the key differences.
Note the PDF location for sharing via email or printing.

### Step 9: Accuracy Review (Optional but Recommended)

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

## Example: Activation Framing

**Bad (no activation):**
> "The system will produce more accurate predictions by incorporating deposit status data."

**Good (activation-focused):**
> "Each morning, admissions counselors receive a prioritized outreach list — students
> who've been accepted but haven't deposited, ranked by risk of choosing another school.
> Instead of calling all 200 accepted students, your team focuses on the 40 most at-risk.
> You'll know it's working when deposit rates for contacted students exceed the baseline."

**Bad (vague stakeholder):**
> "This improvement benefits the enrollment team."

**Good (specific stakeholder + action):**
> "Your enrollment marketing team adjusts email cadence by propensity tier — high-risk
> students get a personal outreach call within 48 hours of acceptance, while low-risk
> students continue the standard drip campaign."
