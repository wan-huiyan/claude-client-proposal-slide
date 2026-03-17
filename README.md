# Client Proposal Slide Generator

A Claude Code skill that creates polished, data-driven HTML presentation slides from technical analysis results. Designed for data scientists and ML engineers who need to communicate findings to non-technical stakeholders.

## What It Does

Takes your analysis results (JSON, markdown, BQ output, SQL capabilities, or conversation context) and produces **three self-contained HTML presentations** at 16:9 (1280x720px):

1. **Detailed** — Full evidence, multiple data points, comprehensive impact section
2. **Minimal** — ~40% less text, simpler layout, same key message
3. **Bullet-point** — Plain text for traditional-deck stakeholders, white background

Each file can be opened in a browser, screenshotted for PowerPoint, or printed to PDF.

## Key Features

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

### Adversarial Accuracy Review (v2.1)
When your deck makes verifiable claims against a codebase or data source, the skill can trigger a **multi-agent review panel** (via the `agent-review-panel` skill) to fact-check every claim before you present.

Common over-claim patterns it catches:
- Counting file variants as distinct capabilities (inflated headline numbers)
- Presenting multi-step pipelines as single capabilities
- Claiming causal inference when only observational comparison exists
- Using universal quantifiers ("every", "all") when coverage is partial
- Listing capabilities without backing implementation

### Design Quality
- Google Fonts (Fraunces + DM Sans or similar pairings)
- Dark/light themes with strategic accent colors
- CSS Grid layouts with generous padding
- `@media print` rules for PDF export
- Horizontal bar charts, stat cards, progress bars (pure CSS, no JS libraries)

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

Claude: [Reads the file, extracts narrative, translates jargon, produces 3 HTML files, opens in browser]

You: The numbers look inflated — can you verify against the codebase?

Claude: [Triggers agent-review-panel to adversarially verify every claim, fixes issues]
```

## Process Overview

| Step | What Happens |
|------|-------------|
| 1. Gather | Read all referenced analysis files, extract narrative elements |
| 2. Translate | Convert ML jargon to client-friendly language |
| 3. Categorize | Split into "Optimisation" vs "Explore" tiers |
| 4. Design | Structure narrative flow (left-to-right story) |
| 5. Build | Generate three HTML versions with production-grade design |
| 6. Deliver | Open all three in browser for preview |
| 7. Review | *(Optional)* Run adversarial accuracy panel if claims are verifiable |
| 8. Iterate | Refine based on user feedback |

## Quality Checklist

The skill enforces these checks before delivery:

- No ML jargon (AUC, entropy, precision, recall, F1, log-odds)
- No unvalidated accuracy claims
- All counts verified for deduplication
- Cautious attribution for data source disagreements
- Title tells a story (not a technical label)
- Proposed changes split into two confidence tiers
- Estimated hours included per item
- All three versions produced
- If claims reference code/data: accuracy review panel run

## Narrative Framing Examples

**Bad (technical):**
> "Expanding application_stage from 4 to 7 categories improves proxy AUC from 0.50 to 0.96 with 62% entropy reduction."

**Good (client-friendly):**
> "Today, all submitted applications are scored identically. By connecting to Salesforce admissions data, the system can distinguish between students in review, accepted, and deposited — with dramatically different enrollment outcomes at each stage."

**Bad (overconfident):**
> "Most students progress without triggering digital events."

**Good (cautious):**
> "Some students progress through the admissions funnel without triggering these digital events — Salesforce holds the authoritative record."

## Dependencies

- **Required:** None — the skill generates self-contained HTML files
- **Optional:** `agent-review-panel` skill for Step 7 accuracy verification
- **Optional:** `frontend-design` skill (referenced for visual quality principles)

## Version History

| Version | Changes |
|---------|---------|
| 2.1.0 | Added adversarial accuracy review step (Step 7) via agent-review-panel |
| 2.0.0 | Initial release with 8-step process, three output versions, quality checklist |

## License

MIT
