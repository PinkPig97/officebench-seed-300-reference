# Task Card: Seed 300

## Overview

- Task ID: `seed_300`
- Title: `Debt Schedule + Covenant Test`
- Modality: spreadsheet completion
- Primary app surface: Excel-compatible workbook editing
- Public inputs:
  - `input/description.md`
  - `input/template.xlsx`
  - `input/financing_memo.pdf`
  - `input/operating_support.xlsx`
- Final artifact: one completed `.xlsx` workbook

## What the solver must do

The solver must complete a starter workbook that:

- builds a quarterly debt roll-forward
- computes quarterly cash interest expense
- computes net debt and net leverage
- maps covenant status to `PASS`, `WARN`, or `BREACH`
- pulls final-quarter outputs into a summary sheet

This is not a presentation-only task. The workbook must contain the required formulas and sheet-to-sheet linkages.

## Core skills tested

- extracting financing terms from a memo
- reading a support workbook and locating the correct source series
- filling reserved input cells accurately
- building linked spreadsheet formulas across multiple tabs
- handling rolling LTM logic correctly
- preserving spreadsheet structure instead of rebuilding a custom layout

## Why this task is useful

Seed 300 is a compact finance-modeling task. It is small enough to run quickly, but it still exposes meaningful failure modes:

- wrong quarter roll-forward logic
- wrong LTM window
- wrong final summary linkage
- confusing label rows with value rows
- protocol-compatible submission that still fails business logic

## Deliverable contract

The submission must:

- keep the four required sheet names:
  - `Inputs`
  - `Debt_Schedule`
  - `Covenant_Test`
  - `Summary`
- use values in reserved input cells
- use formulas in modeled rows
- keep the visible layout already provided by `template.xlsx`
- produce explicit text status outputs, not color-only signaling

## Scoring / verification behavior

The released checker validates:

- required sheets
- key period headers
- key numeric outputs
- key label outputs
- canonical formula/linkage cells
- value-only input cells
- formula-only modeled cells

The checker also supports cache-missing workbooks by evaluating supported formula families directly from the workbook formula layer.

## Validation status

Release readiness evidence for this task:

- gold submission: pass
- blank template: fail
- external baselines:
  - `gpt-5.4` / Codex subagent: pass
  - `claude-opus-4-6` / Claude Code CLI: pass
  - `DeepSeek-V3.2`: pass under the released verifier
  - `GLM-5`: pass under the released verifier
  - multiple weaker or less aligned models: partial fail or protocol fail

## Common failure modes observed during validation

- using the wrong rolling 4-quarter EBITDA window
- pulling final closing debt from the wrong sheet
- reading the period-label row instead of the EBITDA value row
- emitting a valid workbook with logically correct but non-canonical linkage in one monitored summary cell
- failing the execution protocol before submission is produced

## Recommended use

Use Seed 300 when you want a benchmark item that is:

- more logic-heavy than formatting-only spreadsheet tasks
- still short enough for MVP benchmark packages
- sensitive to both business reasoning and spreadsheet execution quality
