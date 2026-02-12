# N1 Epistemic Battery — Open Research Release

This repository publishes (1) **ex ante predictions**, (2) the **N1 test battery**, and (3) the **metrics specification** for an empirical study on the epistemic status of LLM outputs.

## What is included
- `data/batteries/` — N1 battery (CSV/JSONL), 7 categories × 30 pairs × A/B = 420 items.
- `predictions/` — pre-registered qualitative expectations (before analysis).
- `metrics/` — metric definitions and annotation rubric.
- `protocol/` — execution environment configuration (runner expectations).
- `data/schemas/` — JSON Schema for battery items.

## Reproducibility
- Battery IDs are stable (`CATx_nn_A|B`).
- Outputs should be logged line-by-line as JSONL runs under `data/runs/` (not included by default).

## Licensing (recommended)
- Code: MIT (`LICENSE_CODE`)
- Battery + protocol + metrics + predictions: CC BY 4.0 (`LICENSE_DATA`)

## Versioning
Release tags: `vMAJOR.MINOR.PATCH`.
Export generated on 2026-02-12 UTC.
