# Preregistration (Lite) — N1 Epistemic Battery

**Project:** Ontología epistémica del conocimiento maquínico (N1)  
**Version:** v0.1.0  
**Date (UTC):** 2026-02-12  
**Authors:** Jose Fernandez Tamames  
**Repository:** https://github.com/jftmames/n1-cartografia
**Contact:** jose.fernandezt@universidadunie.com

## 1. Research question and objective
This study tests whether Large Language Models (LLMs) exhibit a stable **epistemic profile** consistent with a “third epistemic type”: outputs that can be highly competent in distributional settings while exhibiting systematic fragility when tasks require non-distributional verification (referential/embodied/social/normative constraints).

**Primary objective:** Measure and compare performance degradation from **A → B** across seven epistemic categories, and across model families, using a fixed A/B battery (N=420 prompts).

## 2. Battery (frozen stimulus set)
The stimulus set is fixed and identified by stable IDs:
- 7 categories (CAT1–CAT7)
- 30 pairs per category
- 2 variants per pair: A and B  
Total = 7 × 30 × 2 = **420 items**

Files:
- `data/batteries/N1_pairs_catalog_*.csv` and `.jsonl`
- Schema: `data/schemas/battery_item.schema.json`

**Commitment:** No changes to prompts or IDs after preregistration. Any modification requires a new release tag (e.g., `v0.2.0`) and a new preregistration.

## 3. Models (planned sample)
We will run the full battery on **at least 4 models** spanning different families/providers.

For each model we will record:
- provider, model name, version/date (if available)
- temperature and max tokens
- run timestamp
- full raw output JSON
- parsed “clean” fields

**Minimum inclusion criterion:** ≥ 95% of items have a stored response (raw output present). Missingness will be reported.

## 4. Prompting and output format
Each item is sent to each model with a standardized wrapper requiring:

- `RESPUESTA:`
- `CONFIANZA (0-3):`
- `JUSTIFICACIÓN (máx 3 frases):`

**Format adherence** is treated as a measurable outcome (see M2). We will not manually edit model outputs.

## 5. Human annotation plan
A subset or the full set of outputs will be human-annotated using:
- `accuracy` (binary 0/1; optionally 0/0.5/1 if partial credit is enabled)
- `explanation_type` ∈ {a,b,c,d}

Rubric file: `metrics/annotation_rubric.md`

**Blinding:** Annotators will not see model identity (where operationally feasible).  
**Agreement:** We will report inter-annotator agreement (e.g., Cohen’s κ) and resolution rules for disagreements.

## 6. Outcomes and metrics (predeclared)

### Primary outcome (M1): Δ(A−B)
For each model m and category c:
- `Acc_A(m,c)` = mean annotated accuracy for A-items in category c
- `Acc_B(m,c)` = mean annotated accuracy for B-items in category c
- `Δ(m,c) = Acc_A(m,c) − Acc_B(m,c)`

We will report:
- `Δ(m,c)` with 95% bootstrap CI (paired by `pair_id`)
- pooled `Δ(m)` over all categories

### Secondary outcomes
**M2 — Format adherence:** `FormatOK = mean(format_ok)`  
**M3 — Calibration proxy:** accuracy by confidence bucket (0–3) + optional ECE  
**M4 — Explanation types:** distributions `P(type=t | A)` vs `P(type=t | B)`  
**M5 — Missingness as outcome:** missing rate for confidence/justification/answer

**Important:** “Confidence” is treated as an **interface-level signal**, not as ground-truth metacognition.

## 7. Statistical analysis plan
- Pair-level blocking: where possible, compute deltas paired within each `pair_id`.
- Bootstrap: 95% CI via bootstrap resampling of pairs within category.
- Multiple comparisons: category-wise reporting is primary; no global claims without appropriate caution.
- Missingness: reported explicitly and treated as a meaningful outcome; we will not impute missing confidence.

## 8. Ex ante predictions (summary)
Predictions are described in `predictions/predictions_N1.md`. Key priors:
- Δ(A−B) > 0 in most categories and models
- larger Δ in categories requiring non-distributional verification (e.g., perceptual/embodied, social-intentional)
- explanation types shift toward (c)/(d) in B
- confidence/calibration degrades in B and missingness increases when uncertainty rises

## 9. Stopping rules and deviations
- A model run is considered “complete” when ≥ 95% of items have raw outputs stored.
- Deviations (API outages, model deprecations, rate-limits) will be logged in a `DEVIATIONS.md` file with date and justification.
- Any post-hoc analysis not declared here will be labeled as exploratory.

## 10. Data management and openness
This repository publishes:
- battery, predictions, metrics specification, rubric, and protocol (open)
Model outputs may be published separately depending on provider TOS and privacy constraints; if not published, derived aggregates will be shared.

Licensing:
- Battery/protocol/metrics/predictions: CC BY 4.0 (`LICENSE_DATA`)
- Code: MIT (`LICENSE_CODE`)
