# Environment

This benchmark is an agent task, not a bundled agent runtime.

You can use any scaffold, runner, or model API as long as your agent can:

- read `input/description.md`
- read the financing memo PDF
- open and edit the Excel template
- inspect the operating support workbook
- produce one final `.xlsx` submission

## Minimum Environment

- OS: macOS, Linux, or Windows
- Python: `3.10+`
- Verifier dependency:
  - `openpyxl>=3.1.0`

Install the verifier dependency with:

```bash
pip install -r requirements.txt
```

## Solver Environment

No official scaffold is required.

Your own agent/runtime should provide whatever it needs to:

- inspect PDF content
- edit Excel workbooks while preserving formulas and formatting
- save a final workbook artifact

Typical choices include:

- Python + `openpyxl`
- Excel / LibreOffice driven by automation
- a desktop agent with spreadsheet editing tools

## Submission Convention

The verifier does not require a fixed output path.

It only requires a final workbook file:

- filename: any `.xlsx`
- content: must satisfy the released task spec and the checks implemented in `verifier/checker.py`

## What Is Not Included

This package intentionally does not include:

- an official agent scaffold
- a benchmark orchestrator
- model-calling scripts
- task scheduling or batch evaluation code

Those are user-side runtime choices, not part of the benchmark task release itself.
