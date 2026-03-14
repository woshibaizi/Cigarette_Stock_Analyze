# Turtle Framework Coordinator Workflow v0.15

Use this file to preserve the staged orchestration model from the original prompt.

## Contents

1. Inputs
2. Staged flow
3. PDF handling
4. Unit discipline
5. Output discipline

## 1. Inputs

Possible user inputs:

- Stock code or company name
- Holding channel such as `港股通`, `直接持有`, or `W-8BEN`
- Optional annual-report PDF

If only a company name is given, resolve the ticker before analysis.

## 2. Staged Flow

Use this sequence:

1. Confirm the target symbol, market, holding channel, and working directory.
2. Ensure there is a usable annual-report PDF when the task requires note-level verification.
3. Build `data_pack_market.md`.
4. Build `data_pack_report.md` if a PDF exists.
5. Run the analysis only from the prepared data packs.
6. Write the final report after the factor work is complete.

The analysis stage must not fetch new external data. If a required datapoint is missing, flag the gap instead of backfilling ad hoc during the report-writing stage.

## 3. PDF Handling

Preferred rule:

- If the user already provided a recent full-year annual-report PDF, use it.
- If the user did not provide one, attempt to obtain the latest full-year annual report before the PDF stage when the environment supports that workflow.
- If no PDF can be obtained, skip the PDF pack and use the downgrade path in the analysis framework.

When the PDF pack is missing, state:

`⚠️ 无年报PDF数据包，以下分析基于市场数据包`

## 4. Unit Discipline

Default unit expectations:

- `data_pack_market.md`: usually report-currency `百万元`
- `data_pack_report.md`: original filing units, often `千元`, `百万元`, or `万元`
- Final report: `人民币亿元`

Conversion rules:

- `百万元 -> 亿元`: divide by `100`
- `千元 -> 亿元`: divide by `100000`
- `万元 -> 亿元`: divide by `10000`
- Non-RMB values: convert using the analysis-date spot FX rate first

Never assume the PDF pack uses `千元`; read the file header.

## 5. Output Discipline

- Separate data collection, PDF extraction, and analysis logic.
- Preserve citations back to the data packs.
- Append conclusions factor by factor if the task is long so the report survives context loss.
- Do not write into strategy reference folders; write only into the task workspace.
