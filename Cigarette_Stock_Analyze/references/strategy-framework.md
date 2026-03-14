# Static-Value Cigarette-Butt Framework v1.8

Use this reference to enforce the cigarette-butt workflow. It is a distilled execution spec, not optional background.

## Contents

1. Input and data-priority rules
2. Period and accounting rules
3. Execution workflow
4. Pillar one
5. Pillar two
6. Pillar three and subtype gates
7. Fact Check 22 and rating
8. Investment-plan defaults
9. Final-output gates

## 1. Input and Data-Priority Rules

Minimum input:

- Stock name or ticker
- At least two reporting periods of financial data
- PDF filings or pasted tables are both acceptable

Refresh these items during the task:

- Latest close price and date
- Latest market cap
- Latest shares outstanding
- Latest TTM dividend yield
- Latest MRQ PB
- Controlling shareholder and actual controller
- SOE level when relevant
- Listed subsidiary market values when subtype B or bonus item 20 applies
- Buyback records in the last 12 months when subtype C1b applies
- Full annual statements and dividend history if user-provided files are incomplete
- Local risk-free rate used for hurdle checks

Data-source priority:

1. Structured MCP or other structured market-data tools
2. Web search only when structured data is unavailable, incomplete, or clearly abnormal

Always preserve the source for every external datapoint for the final source table.

## 2. Period and Accounting Rules

- Main quantitative calculations use the newest available period.
- Show the prior period immediately after as `对比参考`.
- Never mix periods within one formula.
- Interim balance-sheet data can be used directly.
- Interim income-statement or cash-flow data must be labeled `年化数据（基于中报×2）` if annualized.
- Identify the accounting standard first: `HKFRS/IFRS`, `US-GAAP`, or `CN-GAAP`.

Core line-item mapping:

- Cash equivalents: `Cash and cash equivalents` / `货币资金`
- Short-term securities: `Financial assets at FVTPL` / `Trading investments` / `交易性金融资产`
- Time deposits: deposit items or other financial assets explicitly disclosed as liquidity reserves
- Receivables: `Trade receivables` / `Accounts receivable` / `应收账款`
- Inventory: `Inventories` / `存货`
- Interest-bearing debt: short-term + long-term debt, including lease liabilities where relevant
- Total liabilities: `Total liabilities` / `负债合计`

Cash-layer definitions:

- `narrow_cash = cash + short_term_securities`
- `broad_cash = narrow_cash + time_deposits_or_liquidity_reserves`
- `super_broad_cash = broad_cash + qualifying_contract_liabilities`

Special treatment:

- Contract liabilities may be added only to `super_broad_cash` when the business is clearly prepaid, delivery certainty is very high, and the balance is stable.
- Restricted cash above 5% must be removed from the T0/T1 cash pool; above 20% is a veto.
- Negative equity makes PB unusable; use `market cap / total assets` as the valuation anchor and call it out.
- For multi-market or cross-currency groups, use the analysis-date spot FX rate and state it.

## 3. Execution Workflow

Run these steps in order:

1. Normalize company code/name, filing periods, accounting standard, market, and holding channel.
2. Collect the market data pack and governance facts.
3. Parse filing line items and note-level items.
4. Complete business model and governance analysis.
5. Compute pillar one.
6. Compute pillar two.
7. Evaluate pillar three, subtype hard gates, and payout-path integrity.
8. Run Fact Check 22 and derive the rating.
9. Produce the investment plan, monitoring list, sources, and disclaimer.

Do not write the final report until steps 1-8 are complete.

## 4. Pillar One: Asset Cushion

Formulas:

`T0_NAV = (cash + short_term_securities + time_deposits - total_liabilities) / shares`

`T1_NAV = (cash + short_term_securities + time_deposits - interest_bearing_debt) / shares`

`T2_NAV = ((cash + short_term_securities + time_deposits) * 1.0 + receivables * 0.85 + inventory * inventory_discount + other_current_assets * 0.5 - total_liabilities) / shares`

Inventory discount guidance:

- `0.8` low-obsolescence consumer goods
- `0.7` general manufacturing
- `0.5` electronics or high-obsolescence categories

Grade logic:

- `T0`: cash pool minus total liabilities exceeds market cap
- `T1`: cash pool minus interest-bearing debt exceeds market cap
- `T2`: adjusted current assets minus total liabilities exceeds market cap

Final asset-cushion grade is the highest passing grade in order `T0 -> T1 -> T2`.

## 5. Pillar Two: Low Maintenance Cost

Core metrics:

- `FCF = operating_cash_flow - capex`
- `asset_burn_rate = FCF / asset_cushion_value`
- `FCF_conversion = FCF / net_profit`
- `SG&A ratio trend = SG&A / revenue`

Thresholds:

| Grade | Pass | Warning | Veto |
|:--|:--|:--|:--|
| T0 | `>= 0%` | `-5% to 0%` | `< -5%` |
| T1 | `>= 5%` | `0% to 5%` | `< 0%` |
| T2 | `>= 10%` | `5% to 10%` | `< 5%` |

Three-choose-two rule:

1. Latest full-year FCF is positive
2. Asset burn rate meets the chosen T-grade threshold
3. Operating cash flow is positive for three consecutive years

Pillar two passes only if at least two items pass.

## 6. Pillar Three and Subtype Gates

Subtype A hard gates, all required:

1. Dividend yield meets the market threshold
   - HK `>= 6%`
   - A-share `>= 4%`
   - US `>= 5%`
2. `PB <= 0.5`
3. Continuous dividends for at least 5 years

Subtype B hard gates, all required:

1. Holding-company discount `>= 30%`
2. At least one listed subsidiary holding `>= 10%`
3. Visible holding-value coverage `>= 30%`
4. Parent has net cash

Subtype C rules:

- `C1a`: disposal or spin-off catalyst with timing evidence
- `C1b`: actual buyback execution, not only authorization
- `C1c`: liquidation, delisting, or privatization
- `C2`: official policy-repair path plus healthy fundamentals and cheap valuation

Subtype C2 hard gates, all required:

1. Positive policy direction is officially signaled
2. At least one precedent exists, or an official timetable substitutes for precedent
3. Fundamentals are healthy: positive operating cash flow, core revenue trend not worse than `-5%`, and no Fact Check veto
4. Valuation already prices in pessimism: `PB <= 0.6` or adjusted `PE <= 6x`, and drawdown from pre-shock high `>= 60%`

Cross-type rule:

- A type is valid only if every hard gate passes.
- Mixed labels such as `A+B` or `C+B` are allowed only when both component types fully pass.
- Never soften failures with "borderline" wording.

Payout-path integrity:

- Count A only if all three A hard gates pass.
- Count B only if all four B hard gates pass.
- Count C only if the catalyst has substantive progress.
- If valid paths = 0, cap the final rating at `C`.
- If TTM dividend yield is below the local risk-free rate and there is no valid B or C path, add `WARNING-Risk`.

Dividend-cut normalization test:

If the latest dividend drops by more than 30% year over year:

1. Compute the prior-3-year average annual dividend or the longest available run
2. Compare the latest dividend to both the prior year and the normalized base
3. Interpret:
   - Latest `< 0.85 x normalized base`: substantive cut
   - Latest `>= 0.85 x normalized base` but `< 0.70 x prior year`: high-base fallback
   - Latest `>= normalized base`: not a true cut

## 7. Fact Check 22 and Rating

Checks 1-19 and 22 must show:

- Check name
- Key data or finding
- Result: `PASS`, `WARNING`, or `VETO`
- Warning type: `Data`, `Risk`, or `--`

Grouping:

- `1-7` asset quality
- `8-13` liability risks
- `14-19` operating quality
- `20-21` bonus items
- `22` asset-structure health

Check 22 formula:

`non_current_fin_assets_ratio = non_current_fin_assets / total_assets`

Bands:

- `<= 15%`: pass
- `15% to 30%`: `WARNING-Risk`
- `30% to 50%`: severe `WARNING-Risk`, then compute core cash coverage
- `> 50%`: `VETO`

For the `30%-50%` band:

- `core_cash_pool = cash + listed liquid securities + bank wealth products/deposits - interest_bearing_debt`
- `core_t_grade = core_cash_pool / market_cap`
- If `< 1.3`, cap the final rating at `B`

Rating rules:

- `A`: no `WARNING-Risk`
- `B`: up to 3 `WARNING-Risk`
- `C`: more than 3 `WARNING-Risk`, near-veto conditions, or payout-path cap
- `D`: any veto

Bonus rules:

- Bonus items `20-21` can upgrade `B -> B+` or `C -> B`
- Bonus items never reverse a veto
- `WARNING-Data` does not change the rating, but all such items must reappear in `11.3 需要人工验证的内容`

## 8. Investment-Plan Defaults

Entry thresholds:

- `T0`: price `< T0_NAV x 0.85`
- `T1`: price `< T1_NAV x 0.80`
- `T2`: price `< T2_NAV x 0.70`

Position caps:

- `T0`: `10%`
- `T1`: `8%`
- `T2`: `5%`
- `C1`: `5-8%`
- `C2`: `2-5%`, up to `5-8%` for top-quality cases

Hard stops:

- Default `-25%`
- `C1` tighter at `-20%`

Immediate exit conditions:

- Asset burn rate falls below the veto line
- Large goodwill impairment
- Related-party risk worsens materially
- Audit opinion turns non-standard
- Management integrity breaks

## 9. Final-Output Gates

Before finalizing, confirm:

- Exact section order from the report template
- Latest-period main calculation plus prior-period comparison for `T0/T1/T2`
- Full A/B/C hard-gate pass-fail listing
- Fact Check 22 tables with warning taxonomy
- Entry, staging, take-profit, stop-loss, and IRR scenario math
- Complete source table with `数据项 / 来源 / URL / 获取日期`
