# Client Proposal Slide Generator

A Claude Code skill that creates polished, activation-focused HTML presentation slides from technical analysis results. Designed for data scientists and ML engineers who need to communicate findings to non-technical stakeholders — with a focus on what stakeholders can **do** with the results.

## What It Does

Starts with a **discovery phase** to understand your audience and their decision context, then takes your analysis results (JSON, markdown, BQ output, SQL capabilities, or conversation context) and produces **three self-contained HTML presentations** at 16:9 (1280x720px):

1. **Detailed** — Full evidence, multiple data points, comprehensive impact section, activation callout
2. **Minimal** — ~40% less text, simpler layout, same key message with inline activation
3. **Bullet-point** — Plain text for traditional-deck stakeholders, with separate activation section

Each file can be opened in a browser, screenshotted for PowerPoint, or printed to PDF.

## Key Features

### Discovery Phase (Brainstorming)
Before building anything, the skill asks clarifying questions to understand:
- **Who is in the room?** — Job titles, decision-making authority, technical literacy
- **What decision does this need to drive?** — Budget approval, prioritization, pilot buy-in
- **What can they actually do with this?** — Which teams act, what workflows change
- **What's the status quo cost?** — Quantify inaction
- **What has been tried before?** — Avoid proposing rejected ideas

Hard gate: won't proceed until audience, decision, and activation are clear.

### Business Activation — "So What? Now What?"
Every proposal item must answer **"What do I do Monday morning?"** for each stakeholder:
- **Who acts** — Named team/role (not "the organization")
- **What changes** — Concrete workflow shift (not "better predictions")
- **What triggers it** — Daily report, dashboard alert, CRM update
- **Expected behavioral change** — How actions differ from today
- **Success metric** — Observable business KPI (not model accuracy)

Common activation patterns: prioritized outreach lists, triggered interventions, resource allocation, campaign targeting, early warning dashboards.

### Jargon-Free Translation
Automatically converts technical language into client-friendly terms:
- "AUC improved from 0.50 to 0.96" → "The system can now clearly distinguish between different student groups"
- "features" → "signals" or "data points"
- "model" → "the system" or "the scoring system"

### Two-Tier Confidence Structure
Every proposal splits recommendations into:
- **"Model Optimisation"** — High-confidence items backed by diagnostic evidence, with estimated hours
- **"Areas We Could Explore"** — Directionally promising but needs validation, with hours + what validation is needed

This builds trust by showing analytical rigor rather than overselling.

### Adversarial Accuracy Review
When your deck makes verifiable claims against a codebase or data source, the skill can trigger a **multi-agent review panel** (via the `agent-review-panel` skill) to fact-check every claim before you present.

Common over-claim patterns it catches:
- Counting file variants as distinct capabilities (inflated headline numbers)
- Presenting multi-step pipelines as single capabilities
- Claiming causal inference when only observational comparison exists
- Using universal quantifiers ("every", "all") when coverage is partial
- Listing capabilities without backing implementation

### Design Quality (via `frontend-design` skill)
HTML generation is delegated to the `frontend-design` skill for distinctive visual quality:
- Distinctive Google Fonts pairings (no generic system fonts)
- Cohesive color schemes matched to audience tone
- CSS Grid layouts with generous padding
- `@media print` rules for PDF export
- Horizontal bar charts, stat cards, progress bars (pure CSS, no JS libraries)
- Visually distinct activation section (callout box, icon badges, different background)

## Installation

```bash
# Add the marketplace
/plugin marketplace add wan-huiyan/claude-client-proposal-slide

# Or install directly
/plugin install client-proposal-slide
```

## Usage

The skill activates automatically when you say things like:

- "Make a slide proposing the model improvements to the client"
- "Create a deck showcasing our AMC capabilities"
- "Design a presentation summarizing the analysis results"
- "Client proposal for the new feature expansion"

### Example Workflow

```
You: I have analysis results in analysis_results.json — can you make a client proposal slide?

Claude: Before I build the slide, I need to understand the context:
        1. Who will be in the room when this is presented?

You: VP of Enrollment and two admissions directors

Claude: 2. What decision should this drive? Budget approval, prioritization, or...?

You: We need them to approve 40 hours of implementation work

Claude: 3. What would change for their teams? How would admissions counselors use this day-to-day?

You: They'd get a daily prioritized call list instead of calling everyone alphabetically

Claude: [Reads the file, extracts narrative, translates jargon, builds activation framing,
         produces 3 HTML files via frontend-design, opens in browser]
```

## Process Overview

| Step | What Happens |
|------|-------------|
| 1. Discover | Ask clarifying questions about audience, decision, and activation (hard gate) |
| 2. Gather | Read all referenced analysis files, extract narrative elements |
| 3. Translate | Convert ML jargon to client-friendly language |
| 4. Categorize | Split into "Optimisation" vs "Explore" tiers |
| 5. Activate | Define who acts, what changes, and success metrics for each proposal item |
| 6. Design | Structure narrative flow (left-to-right story) |
| 7. Build | Generate three HTML versions via `frontend-design` skill |
| 8. Deliver | Open all three in browser for preview |
| 9. Review | *(Optional)* Run adversarial accuracy panel if claims are verifiable |
| 10. Iterate | Refine based on user feedback |

## Quality Checklist

The skill enforces these checks before delivery:

- Discovery questions answered — audience, decision, activation identified
- No ML jargon (AUC, entropy, precision, recall, F1, log-odds)
- No unvalidated accuracy claims
- All counts verified for deduplication
- Cautious attribution for data source disagreements
- Title tells a story (not a technical label)
- Proposed changes split into two confidence tiers
- Estimated hours included per item
- **Business activation defined** — each item has: who acts, what changes, success metric
- **No orphan proposals** — every item answers "what does the stakeholder do differently Monday morning?"
- All three versions produced
- HTML built via `frontend-design` skill
- If claims reference code/data: accuracy review panel run

## Narrative Framing Examples

**Bad (technical):**
> "Expanding application_stage from 4 to 7 categories improves proxy AUC from 0.50 to 0.96 with 62% entropy reduction."

**Good (client-friendly):**
> "Today, all submitted applications are scored identically. By connecting to Salesforce admissions data, the system can distinguish between students in review, accepted, and deposited — with dramatically different enrollment outcomes at each stage."

**Bad (no activation):**
> "The system will produce more accurate predictions by incorporating deposit status data."

**Good (activation-focused):**
> "Each morning, admissions counselors receive a prioritized outreach list — students who've been accepted but haven't deposited, ranked by risk of choosing another school. Instead of calling all 200 accepted students, your team focuses on the 40 most at-risk."

## Dependencies

- **Required:** None — the skill generates self-contained HTML files
- **Optional:** `agent-review-panel` skill for Step 9 accuracy verification
- **Optional:** `frontend-design` skill for Step 7 HTML generation (recommended for visual quality)
- **Optional:** `brainstorming` skill (Step 1 discovery phase embeds its mindset inline)

## Version History

| Version | Changes |
|---------|---------|
| 3.0.0 | Added brainstorming discovery phase (Step 1), business activation section (Step 5), delegated HTML to frontend-design skill (Step 7) |
| 2.1.0 | Added adversarial accuracy review step via agent-review-panel |
| 2.0.0 | Initial release with 8-step process, three output versions, quality checklist |

## License

MIT
