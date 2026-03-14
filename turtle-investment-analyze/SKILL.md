---
name: turtle-investment-analyze
description: Generate Turtle Framework investment-analysis reports from a stock code/name, holding channel, and optional annual-report PDF. Use when the user wants the v0.15龟龟投资策略 workflow, including staged data-pack collection, optional PDF parsing, four-factor analysis, veto-gate logic, and a final Markdown report that strictly follows the framework template.
---

# Turtle Investment Analyze

Use this skill to produce a Turtle Framework report that matches the v0.15 prompt family. The workflow is staged and the final report format is fixed.

## Required Reads

Read these files before starting substantive work:

1. [references/coordinator-workflow.md](references/coordinator-workflow.md)
2. [references/data-pack-requirements.md](references/data-pack-requirements.md)
3. [references/analysis-framework.md](references/analysis-framework.md)
4. [references/report-template.md](references/report-template.md)

## Workflow Contract

1. Follow the staged architecture.
   Build or inspect the market data pack first, then the filing/PDF pack when available, then perform analysis from those prepared packs only.

2. Keep collection and analysis separated.
   Market-data gathering and PDF extraction are raw-data tasks. Do not mix them with valuation or recommendation language.

3. Respect veto gates.
   Factor `1A`, `1B`, and factor `2` contain hard veto conditions. Stop or downgrade exactly where the framework requires; do not continue as if the veto did not happen.

4. Use pre-extracted parameters consistently.
   Once a figure is anchored in the financial-summary module, reuse that value with explicit citations instead of silently recalculating with a different denominator or currency basis.

5. Keep units explicit.
   Data packs may arrive in `百万元`, `千元`, or `万元`, and may not be in RMB. Convert only after reading the file header and state the FX assumption used.

6. Keep the report template exact.
   Use the exact headings and section order from [references/report-template.md](references/report-template.md). Do not omit sections when the answer is negative.

## Mandatory Output Rules

- Write the report in Chinese with English financial terms preserved where useful.
- Show formulas, substituted values, and results for all material calculations.
- Cite data-pack locations inline, for example `参数名 = X（data_pack_market §3 / data_pack_report P1）`.
- If `data_pack_report.md` is unavailable, state the downgrade explicitly and use the reduced-scope path defined in the references.
- Preserve both reported and adjusted profit views when non-cash one-offs are material.
- Treat the final factor-4 conclusion as a decision rule, not a narrative preference.

## Final Checks Before Submission

- `报告元信息` contains holding channel, tax rate, risk-free rate, current price, market cap, and data periods.
- `因子1A` lists all six quick-screen items and stops if any veto applies.
- `因子1B` includes `3.0 三大报表基础数据与关键指标` and the module summary.
- `因子2` includes the rough-return veto-gate comparison against `Rf` and `II`.
- `因子3` includes cash-quality analysis and confidence grading.
- `因子4` includes hurdle, value-trap check, safety margin, position sizing, and trigger price.
- `最终综合输出` clearly states recommendation, expected return path, and position advice.

If any check is missing, revise the report instead of sending it.
