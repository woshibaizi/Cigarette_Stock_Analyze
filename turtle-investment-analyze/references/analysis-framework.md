# Turtle Framework Analysis Framework v0.15

Use this file to run the four-factor analysis in the original order.

## Contents

1. Factor 1A
2. Factor 1B
3. Factor 2
4. Factor 3
5. Factor 4
6. Final decision gates

## 1. Factor 1A: Five-Minute Quick Screen

Check all six items:

1. Abnormal audit opinion
2. Frequent auditor changes
3. Fraud or major regulatory history
4. Cannot explain the business model simply
5. Business model not validated across a full cycle
6. Major controlling-shareholder red flags

Any `是` is a veto and stops the later factor work.

If all pass, record the initial profile:

- Capital consumption: `capital-light` or `capital-hungry`
- Collection model
- Cyclicality
- Moat intuition

## 2. Factor 1B: Deep Qualitative Work

Cover these blocks:

- `3.0 三大报表基础数据与关键指标`
- Capital consumption intensity
- Collection model
- Competition and moat
- Cyclicality
- Human-capital dependence
- Management and governance
- Regulatory and policy risk
- MD&A interpretation
- Holding-company discount analysis when applicable

Rules:

- Anchor the parameter set once in the financial-summary block and reuse it later
- Separate reported profit from adjusted profit when one-off non-cash items distort the year
- If the company is a holding structure, run SOTP and stress cases
- End with a factor-1 conclusion of `通过` or `否决`

## 3. Factor 2: Rough Through-Look Return

Required steps:

1. Derive attributable profit
2. Estimate `Owner Earnings`
3. Verify distribution capacity
4. Check upstream cash obstacles when relevant
5. Judge payout willingness
6. Judge predictability
7. Adjust for tax leakage
8. Compute rough through-look return `R`
9. Apply the rough-return veto gate

Hard gate:

- If `R < Rf` or `R < II x 0.5`, reject and stop before factor 3

## 4. Factor 3: Precise Through-Look Return and Cash-Quality Audit

Required steps:

1. Rebuild real cash income
2. Check receivables when collection quality is weak
3. Classify non-recurring cash inflows
4. Rebuild operating cash outflows
5. Treat capex and investments conservatively
6. Check accounting-standard differences
7. Derive true distributable cash balance
8. Audit cash-reserve quality
9. Compute post-dividend cash change
10. Compute precise through-look return `GG`
11. Cross-check factor 1 conclusions and assign confidence

Output must include:

- `GG`
- Sensitivity analysis where the prompt requires it
- Confidence grading
- Cash-protection commentary

## 5. Factor 4: Valuation and Margin of Safety

Required steps:

1. Compute hurdle `II`
2. Run value-trap checks
3. Derive margin of safety and position size
4. Evaluate current price position and trigger price

Factor 4 is a decision layer. It must yield a clear invest / observe / reject style output with explicit position sizing.

## 6. Final Decision Gates

Respect these rules:

- A veto in factor 1A, factor 1B, or factor 2 stops the framework
- Factor 3 refines valuation; it does not rescue a name that factor 2 already vetoed
- Factor 4 can reject a company even if earlier factors passed
- Final recommendation must be consistent with the factor outputs, not softer than them
