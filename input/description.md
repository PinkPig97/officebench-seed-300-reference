# Seed 300: Debt Schedule + Covenant Test

## Task

You are given:

1. a financing memo with one term loan and one covenant definition
2. an operating support workbook with historical and forecast EBITDA plus forecast unrestricted cash
3. a starter workbook

Build `submission.xlsx` by completing the workbook so that it:

- calculates a quarterly debt schedule
- calculates quarterly cash interest expense
- calculates quarterly net leverage
- returns a quarterly `PASS` / `WARN` / `BREACH` status
- shows the final-quarter status on the `Summary` sheet

## Required workbook tabs

Keep these sheet names exactly:

- `Inputs`
- `Debt_Schedule`
- `Covenant_Test`
- `Summary`

## Public input materials

- `financing_memo.pdf`
- `operating_support.xlsx`
- `template.xlsx`

## Explicit rules

### Debt schedule

- The opening debt balance for `2026Q1` is given explicitly in the financing memo.
- Scheduled amortization is a quarter-specific amount from the financing memo.
- Interest expense for each quarter is calculated on the opening debt balance of that quarter.
- Scheduled amortization occurs at quarter end, after interest accrues.
- Closing debt = Opening debt - Scheduled amortization.
- The next quarter's opening debt equals the previous quarter's closing debt.

### Covenant definition

- `Net Debt = max(Closing Debt - Unrestricted Cash, 0)`
- `Net Leverage = Net Debt / LTM EBITDA`
- `LTM EBITDA` for a tested quarter equals the sum of EBITDA for:
  - that quarter
  - the prior three quarters
- As forecast quarters roll forward, forecast EBITDA replaces historical EBITDA where applicable.

### Status mapping

- `PASS`: Net Leverage <= `3.25x`
- `WARN`: Net Leverage > `3.25x` and <= `3.50x`
- `BREACH`: Net Leverage > `3.50x`

## Workbook constraints

- Do not create a substitute layout. Complete the reserved cells already present in the starter workbook.
- Use the reserved input cells exactly as laid out:
  - `Inputs!C5` for opening debt
  - `Inputs!C6` for annual cash interest rate
  - `Inputs!B10:E10` for scheduled amortization by quarter
  - `Inputs!B11:E11` for unrestricted cash by quarter
  - `Inputs!B12:E12` for forecast EBITDA by quarter
  - `Inputs!B16:I16` for the full LTM EBITDA source series
- Input cells must remain values, not formulas.
- Modeled rows must use formulas, not hardcoded outputs.
- Summary outputs must pull from modeled sheets rather than retype results.
- Status must be represented by explicit text labels, not color alone.
- Keep period headers aligned across modeled sheets.

## Required visible outputs

### `Debt_Schedule`

By quarter, show:

- Opening Debt
- Scheduled Amortization
- Interest Expense
- Closing Debt

### `Covenant_Test`

By quarter, show:

- Unrestricted Cash
- Closing Debt
- Net Debt
- LTM EBITDA
- Net Leverage
- Status

### `Summary`

Show:

- final-quarter Closing Debt
- final-quarter Net Leverage
- final-quarter Status
- quarterly Status by period
- quarterly Net Leverage by period

## What is intentionally not part of this task

Do not introduce any unsupported logic for:

- revolvers
- optional prepayments
- cash sweeps
- multiple covenant types
- PIK interest

Use only the explicit public rules above.
