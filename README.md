# OfficeBench Seed 300

This repository is a minimal benchmark task package for a single Office agent task.

Important scope note:

- this repository publishes the task package, environment note, gold answer, and verifier
- it does not publish an official runner or agent scaffold
- any model result tables kept under `docs/` are reference-only archival material and are not part of the benchmark specification

It contains only four release components:

1. `input/`
   Solver-facing task materials:
   - `description.md`
   - `template.xlsx`
   - `financing_memo.pdf`
   - `operating_support.xlsx`
2. `ENVIRONMENT.md`
   Environment guidance for running the task with any agent/runtime.
3. `answer/gold_submission.xlsx`
   The reference workbook.
4. `verifier/checker.py`
   A deterministic checker that validates a submission workbook against the released task contract.

## Quick Start

Install verifier dependency:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Run the checker:

```bash
python3 verifier/checker.py --submission /path/to/submission.xlsx
```

The checker prints JSON with:

- `task_pass`
- `score`
- `failures_count`
- `failures`
- `check_results`

## Repository Layout

```text
input/
  description.md
  template.xlsx
  financing_memo.pdf
  operating_support.xlsx
answer/
  gold_submission.xlsx
verifier/
  checker.py
ENVIRONMENT.md
requirements.txt
```

## Reference-Only Archive

For internal comparison and historical record only:

- [Task card](docs/TASK_CARD.md)
- [Human instructions](docs/HUMAN_INSTRUCTIONS.md)
- [Reference leaderboard (2026-04-23)](docs/REFERENCE_LEADERBOARD_2026-04-23.md)

This file is intentionally non-normative:

- it is not part of the benchmark definition
- it is not an official evaluation harness
- it mixes multiple execution setups and is kept only as a result archive
