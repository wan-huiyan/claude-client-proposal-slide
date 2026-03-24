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

Ask clarifying questions **one at a time** before building. Required context:

1. **Who is in the room?** — Job titles, decision authority, technical literacy
2. **What decision does this drive?** — Budget approval, prioritization, pilot buy-in ("informational" is not valid)
3. **What can they do with this?** — Which teams act, what workflows change
4. **Status quo cost?** — Quantify what happens if they do nothing
5. **What's been tried before?** — Avoids proposing rejected ideas

Optional: timeline/budget cycles, competing priorities, first vs follow-up, format preference.

**HARD GATE:** Minimum questions 1-3 answered before Step 2. Push back once if user says "just make it". If they insist, use defaults and flag assumptions.

### Step 2: Gather Source Material

Read all referenced files (JSON, markdown, BQ output, or conversation context). Extract: **problem** (gap/limitation), **evidence** (data proving it), **solution** (proposed changes), **impact** (measurable improvement), **ask** (what to approve/fund).

### Step 3: Translate for the Audience

Apply rules from `references/language-rules.md`: no ML jargon (AUC, entropy, F1), replace "features" with "signals", use directional language instead of accuracy numbers, prefer rates over raw counts.

### Step 4: Categorize Proposed Changes

Split into two confidence tiers:

**"Model Optimisation"** — High-confidence, backed by diagnostic evidence. Include estimated hours. These are "we know this will help" items.

**"Areas We Could Explore"** — Directionally promising but needs validation. Include estimated hours AND what validation is needed. Be honest about uncertainty.

This two-tier structure builds trust by showing analytical rigor rather than overselling.

### Step 5: Business Activation — "So What? Now What?"

Every proposal must answer **"What do I do Monday morning?"** for each stakeholder. For each improvement, define:

1. **Who acts?** — Name the team/role
2. **What changes in their workflow?** — Concrete operational shift (not "better predictions" but "prioritized call list replacing alphabetical queue")
3. **Trigger** — When does it kick in? (daily report, dashboard alert, CRM update)
4. **Behavioral change** — How actions differ from today
5. **Success metric** — Observable business KPI (not model accuracy)

See `references/activation-patterns.md` for patterns, anti-patterns, and placement guidance.

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
- Minimal styling, white background, standard fonts. Context at top → "Model Optimisation" bullets → "Areas We Could Explore" bullets. Each bullet: item name, one-line description, estimated hours.

All versions require: narrative title (not technical label), client branding header, implementation reassurance footer, prominent primary recommendation callout, estimated hours per item.

### Step 7: Build the HTML (via `frontend-design` skill)

Invoke `frontend-design` for HTML generation with specs from `references/html-build-specs.md`. Delegate typography and visual design.

### Step 8: Deliver Four Outputs

1. `[name]_slide.html` — Detailed 3-column version
2. `[name]_slide_minimal.html` — 2-column version (~40% less text)
3. `[name]_slide_bullets.html` — Plain bullet-point version
4. `[name]_slide.pdf` — Print-ready PDF (see `references/html-build-specs.md` for Chrome/puppeteer commands)

### Step 9: Accuracy Review (Optional)

Run `agent-review-panel` when deck makes verifiable claims. See `references/accuracy-review.md`.

### Step 10: Iterate on Feedback

Common patterns: "Too technical" → apply language rules; "Numbers wrong" → verify deduplication; "Too busy" → simplify to minimal version; "Make X prominent" → accent colors/callout box.

## Quality Checklist

- [ ] Discovery questions 1-3 answered
- [ ] No ML jargon (AUC, entropy, F1, precision, recall, log-odds, calibration)
- [ ] No unvalidated accuracy claims; cautious attribution for disagreements
- [ ] Two-tier structure ("Model Optimisation" + "Areas We Could Explore") with hours
- [ ] Business activation defined per item (who acts, what changes, success metric)
- [ ] All three HTML versions + PDF produced; renders at 1280x720
- [ ] Narrative title, client branding, implementation reassurance footer
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
