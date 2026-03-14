---
name: cigarette-stock-analyze
description: "Analyze static-value cigarette-butt stocks from company filings and the latest market data. Use when the user provides a stock name/code plus at least two reporting periods of financial statements or PDFs, and wants a full Markdown report that strictly follows the cigarette-butt framework: latest-data market refresh, T0/T1/T2 asset cushion, subtype A/B/C classification, Fact Check 22 validation, and the exact report template."
---

# Cigarette Stock Analyze

Use this skill to generate a cigarette-butt stock report that matches the v1.8 prompt structure exactly. Do not improvise section order, headings, tables, or pass criteria.

## Required Reads

Read these files before writing the report:

1. [references/strategy-framework.md](references/strategy-framework.md)
2. [references/report-template.md](references/report-template.md)

The framework file defines execution order, hard gates, formulas, warning taxonomy, and subtype rules. The template file defines the exact Markdown structure that must appear in the final answer.

## Execution Contract

1. Confirm the minimum input set.
   Require a stock name or ticker and at least two reporting periods of financial data. Accept PDF filings or pasted tables.

2. Refresh all time-sensitive market data.
   Always fetch the latest price, date, market cap, shares outstanding, PB, dividend yield, controller data, buybacks, risk-free rate, and other current datapoints during the task. Prefer structured MCP tools first and fall back to web only when structured data is unavailable or clearly wrong.

3. Build the data pack before judging anything.
   Normalize the accounting standard, map line items, separate latest period versus prior period, identify narrow/broad/super-broad cash, and mark every missing item explicitly as `⚠️ 数据缺失：<科目名>`.

4. Use latest-period priority without period mixing.
   Main calculations must use the newest balance-sheet period. Show the previous period only as comparison. Never mix numbers from different filing periods inside one formula.

5. Run the framework in fixed order.
   Complete business model and governance work first, then pillar one, pillar two, pillar three, subtype-specific analysis, Fact Check 22, and only then the investment plan.

6. Treat subtype gates and vetoes as hard rules.
   A subtype exists only if every core condition passes. Do not write "接近满足", "边缘成立", or similar softening language.

7. Keep the final report template exact.
   Use the exact headings, subsection labels, and table structure from [references/report-template.md](references/report-template.md). Do not delete sections even for negative cases.

## Mandatory Output Rules

- Write the narrative in Chinese and preserve financial terms in English where useful.
- Show formulas, substituted numbers, and results for every material calculation.
- Label each figure with its period and source context when relevant.
- Separate `WARNING-Data` from `WARNING-Risk`; only risk warnings affect the base rating.
- Apply the payout-path integrity cap and the asset-structure health cap exactly as defined in the framework.
- End with the source table required by the template, including MCP calls or URLs and collection dates.

## Non-Negotiable Checks Before Finalizing

- `报告元信息` includes latest price date, market-cap source, holding channel, tax rate, risk-free rate, accounting standard, and filing periods.
- `五、支柱一` shows latest-period main calculation plus prior-period comparison for `T0/T1/T2`.
- `七、支柱三` explicitly lists pass/fail for A, B, and C hard gates before choosing the final subtype.
- `九、Fact Check 22项验证` includes items 1-19 and 22 with `PASS/WARNING/VETO` plus `Data/Risk/--`.
- `十、操作建议` includes entry, staging, take-profit, stop-loss, and scenario return math.
- `十一、风险提示` repeats all `WARNING-Data` items inside `11.3 需要人工验证的内容`.

If any of these checks fail, revise the report instead of submitting it.
