# Language Translation Rules for Client-Facing Slides

## ML Jargon to Client Language

| Never use | Instead use |
|-----------|-------------|
| AUC, entropy, precision, recall, F1 | "clear differentiation", "significantly better ranking", "strong signal" |
| features | signals, data points |
| model | the system, the scoring system |
| training window | historical data available for learning |
| false positive rate | (omit or use "reliability of the flagging") |
| log-odds, calibration | (omit entirely) |

## Attribution Rules

- When two data sources disagree, use cautious language ("some students" not "most students")
- Do not assert behavioral explanations for data gaps — could be tracking, integration, or genuine differences
- Do not quote specific accuracy percentages unless from a validated, deployed model

## Number Rules

- Verify whether counts are unique entities or duplicated observations
- Use the correct unit: "applications" vs "students" vs "observations"
- Prefer percentages and rates over raw counts (less deduplication ambiguity)
- When showing rates, always note the baseline comparison
