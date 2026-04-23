# Human Instructions

This note is for a human analyst who wants to solve the task manually in Excel.

## Goal

Complete `template.xlsx` so the workbook produces:

- a quarterly debt schedule
- a quarterly covenant test
- a final summary for `2026Q4`

Your finished file can be saved under any name, for example `submission.xlsx`.

## Files to open

1. `input/template.xlsx`
2. `input/financing_memo.pdf`
3. `input/operating_support.xlsx`

## Step 1: Read the financing memo

From the memo, collect:

- opening debt balance for `2026Q1`
- annual cash interest rate
- scheduled amortization for each quarter of `2026`
- covenant threshold logic:
  - `PASS` if leverage is at or below `3.25x`
  - `WARN` if leverage is above `3.25x` and at or below `3.50x`
  - `BREACH` if leverage is above `3.50x`

## Step 2: Read the operating support workbook

From `operating_support.xlsx`, collect:

- unrestricted cash forecast for `2026Q1` to `2026Q4`
- forecast EBITDA for `2026Q1` to `2026Q4`
- the full 8-quarter EBITDA source series used for LTM calculations:
  - `2025Q1`
  - `2025Q2`
  - `2025Q3`
  - `2025Q4`
  - `2026Q1`
  - `2026Q2`
  - `2026Q3`
  - `2026Q4`

Be careful not to confuse the row of quarter labels with the row of EBITDA values.

## Step 3: Fill the Inputs sheet

Enter values only, not formulas, in these reserved cells:

- `Inputs!C5`: opening debt
- `Inputs!C6`: annual cash interest rate
- `Inputs!B10:E10`: scheduled amortization by quarter
- `Inputs!B11:E11`: unrestricted cash by quarter
- `Inputs!B12:E12`: forecast EBITDA by quarter
- `Inputs!B16:I16`: full 8-quarter EBITDA source series

Do not change the layout.

## Step 4: Build the Debt_Schedule sheet

For each quarter:

- Opening Debt
- Scheduled Amortization
- Interest Expense
- Closing Debt

Use these mechanics:

- `Interest Expense = Opening Debt * annual cash interest rate / 4`
- amortization happens at quarter end
- `Closing Debt = Opening Debt - Scheduled Amortization`
- next quarter opening debt equals prior quarter closing debt

These modeled rows should be formulas, not hardcoded numbers.

## Step 5: Build the Covenant_Test sheet

For each quarter, calculate:

- Unrestricted Cash
- Closing Debt
- Net Debt
- LTM EBITDA
- Net Leverage
- Status

Use these rules:

- `Net Debt = max(Closing Debt - Unrestricted Cash, 0)`
- `LTM EBITDA = current quarter EBITDA + prior 3 quarters EBITDA`
- `Net Leverage = Net Debt / LTM EBITDA`

Example:

- for `2026Q1`, LTM EBITDA should include `2025Q2`, `2025Q3`, `2025Q4`, and `2026Q1`
- for `2026Q4`, LTM EBITDA should include `2026Q1` through `2026Q4`

Then map status:

- `PASS` if leverage `<= 3.25x`
- `WARN` if leverage `> 3.25x` and `<= 3.50x`
- `BREACH` if leverage `> 3.50x`

## Step 6: Build the Summary sheet

The summary should pull, not retype, the final outputs:

- final-quarter Closing Debt
- final-quarter Net Leverage
- final-quarter Status
- quarterly Status by period
- quarterly Net Leverage by period

In other words, link back to the modeled sheets.

## Step 7: Final self-check

Before running the verifier, check:

- sheet names are unchanged
- input cells are values, not formulas
- modeled cells are formulas
- the rolling 4-quarter EBITDA windows are aligned correctly
- the summary points to the final quarter outputs
- status labels are text, not just formatting

## Step 8: Run the checker

Install the dependency:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Run:

```bash
python3 verifier/checker.py --submission /path/to/your_submission.xlsx
```

If the checker returns `task_pass: true`, the workbook meets the released task contract.
