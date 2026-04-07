# Accuracy Review via agent-review-panel

## When to Trigger

- Deck references specific counts derived from code (e.g., "17 analysis types")
- Deck claims technical capabilities backed by SQL, scripts, or models
- Audience is technically sophisticated and will fact-check claims
- Deck describes methodology that could be over-stated

## What the Panel Checks

- Do headline numbers match verifiable counts in the codebase?
- Does each claimed capability have backing code/SQL?
- Are methodological claims accurate?
- Are there unbacked claims that could embarrass you?
- Are real capabilities missing from the deck?

## How to Use the Output

- Fix claims rated CRITICAL or HIGH
- Soften language where panel flags over-statement
- Reduce counts to match items with direct backing evidence
- Add qualifiers where methodology spans multiple tools

## Common Over-Claim Patterns

- Counting file variants as distinct capabilities (inflated numbers)
- Presenting multi-step pipeline as single capability
- Claiming causal inference when only observational comparison exists
- Using universal quantifiers ("every", "all") when coverage is partial
- Listing capabilities without backing implementation
