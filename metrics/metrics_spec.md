# Metrics specification (N1)

This repository publishes *ex ante* metrics for the N1 battery.

## Primary outcome
### M1 — Δ(A−B) by category and model family
For each model *m* and category *c*:
- Let `Acc_A(m,c)` be the mean human-annotated accuracy for A-items in category *c*.
- Let `Acc_B(m,c)` be the mean human-annotated accuracy for B-items in category *c*.
- Define `Δ(m,c) = Acc_A(m,c) − Acc_B(m,c)`.

Report:
- `Δ(m,c)` with 95% bootstrap CI (paired by `pair_id`).
- A pooled `Δ(m)` over all categories.

## Secondary outcomes
### M2 — Format adherence
`FormatOK = mean(format_ok)` where `format_ok` is derived by parsing the standardized response template.

### M3 — Calibration proxy (interface-level)
Compute accuracy by reported confidence bucket (0–3) and report:
- `Acc(conf=k)` for k in {0,1,2,3}
- Expected Calibration Error (ECE) on the 4-bucket scale (optional).

**Important:** Confidence is treated as an *interface signal*, not as ground-truth metacognition.

### M4 — Explanation-type distribution (a/b/c/d)
Using the annotation rubric, compute the distribution of explanation types for A vs B:
- `P(type=t | A)` and `P(type=t | B)` for t ∈ {a,b,c,d}.

### M5 — Robustness subset (optional, N2 hook)
For a predeclared subset, compute stability under paraphrase/self-consistency.

## Statistical notes
- Pair-level blocking: when possible, analyze deltas paired within `pair_id`.
- Multiple comparisons: report category-wise results; avoid over-claiming across 7 categories.
- Missingness: publish missing-rate for each field (answer, confidence, justification) and treat it as an outcome (M2).
