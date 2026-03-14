# Turtle Framework Data-Pack Requirements v0.15

Use this file when building or validating the staged inputs for analysis.

## Contents

1. Market data pack
2. PDF data pack
3. Required source fields
4. Downgrade behavior

## 1. Market Data Pack

`data_pack_market.md` should contain, at minimum:

- Basic company info, market, listing structure, holding channel, dividend-tax assumption, report currency, and FX rate when needed
- Latest price, market cap, shares outstanding, dividend yield, 52-week range, and industry classification
- Five years of income statement, balance sheet, and cash-flow statement data
- Full dividend history and buyback history
- Ten-year weekly price context
- Risk-free rate and source
- Governance and management facts
- Industry and competition notes
- Listed subsidiary data when the company is a holding structure
- MD&A summary when available

Collection discipline:

- Missing items must be marked explicitly, not guessed
- Use a consistent currency and state the unit at the top of the file
- Keep raw facts only; no investment conclusion language

## 2. PDF Data Pack

`data_pack_report.md` should extract filing-only details when a PDF exists:

- Parent-only balance sheet
- Restricted cash detail
- Receivable aging
- Related-party transactions
- Capitalized interest
- Contingent liabilities and commitments
- Deposit and wealth-management-product detail
- Lease obligations
- MD&A key excerpts
- Segment data
- Dividend policy and payout history

If a section cannot be found, mark it explicitly and record the searched location or limitation.

## 3. Required Source Fields

Data packs should make it possible to cite:

- Section or page location
- Currency and unit
- Date or fiscal year
- Source type such as MCP, filing, or web search

The final report should be able to reference values with patterns like:

`参数名 = X（data_pack_market §3 / data_pack_report P1）`

## 4. Downgrade Behavior

If `data_pack_report.md` is missing:

- Continue with market-pack-only analysis
- Mark note-dependent checks as downgraded or data-limited
- Do not invent parent-only numbers, receivable aging, or note detail
- Push all such gaps into the final risk and manual-verification sections
