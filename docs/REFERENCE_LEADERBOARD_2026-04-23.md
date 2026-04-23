# Reference Leaderboard Archive (2026-04-23)

This document is included for reference and internal archival purposes only.

It is not part of the benchmark specification.

Specifically:

- it does not define the task
- it does not define the verifier
- it does not define the official execution environment
- it does not imply that all rows are directly apples-to-apples comparable

The benchmark itself is defined only by:

1. `input/`
2. `ENVIRONMENT.md`
3. `answer/gold_submission.xlsx`
4. `verifier/checker.py`

This file is kept only to preserve a snapshot of model results observed during task development and validation.

---

## Task

- `seed_300`
- task type: debt schedule + covenant test spreadsheet completion

## Reference Results

`setup` indicates how the result was produced:

- `external baseline`: same released checker, but not the same external-model compare harness
- `official compare`: released task materials routed through the OfficeBench external-model compare flow
- `official compare (regraded)`: original run artifact rechecked with the final released verifier

| rank | model / agent | underlying model | setup | failures | task_pass | exec | note |
|---|---|---|---|---:|---|---|---|
| 1 | `Codex subagent` | `gpt-5.4` | `external baseline` | `0` | `true` | `submitted` | pass |
| 2 | `Claude Code CLI` | `claude-opus-4-6` | `external baseline` | `0` | `true` | `submitted` | pass |
| 3 | `Pro/deepseek-ai/DeepSeek-V3.2` | `Pro/deepseek-ai/DeepSeek-V3.2` | `official compare (regraded)` | `0` | `true` | `submitted` | original stored run used an older stricter checker on `Covenant_Test!B8:E8` |
| 4 | `Pro/zai-org/GLM-5` | `Pro/zai-org/GLM-5` | `official compare` | `0` | `true` | `submitted` | pass |
| 5 | `Pro/moonshotai/Kimi-K2.6` | `Pro/moonshotai/Kimi-K2.6` | `official compare` | `1` | `false` | `submitted` | only wrong `Summary!B5` linkage |
| 6 | `Pro/MiniMaxAI/MiniMax-M2.5` | `Pro/MiniMaxAI/MiniMax-M2.5` | `official compare` | `8` | `false` | `submitted` | used the period-label row instead of the EBITDA-value row |
| 7 | `Pro/moonshotai/Kimi-K2.5` | `Pro/moonshotai/Kimi-K2.5` | `official compare` | `14` | `false` | `submitted` | wrong rolling LTM window |

## Non-Ranked Hard-Blocked Models

These models did not reach a stable, valid submitted artifact under the same compare scaffold.

| model | outcome pattern | note |
|---|---|---|
| `Pro/zai-org/GLM-5.1` | `protocol_fail` | did not follow the required one-JSON-action response protocol |

## Reading Notes

- `task_pass=false` means the submitted workbook failed verification.
- `failures` is the most useful distance-to-gold signal for this archive because the public release checker is task-specific rather than a generic workbook diff.
- The table intentionally preserves historical validation evidence; it should be read as an archive, not as part of the benchmark spec.
