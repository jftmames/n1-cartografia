# Ex ante predictions (N1)

These predictions are published *before* inspecting model outputs and human annotations.

## Global predictions
- **P1 (Primary):** For most model families, `Δ(A−B) > 0` in each category; the largest deltas will concentrate in categories requiring non-distributional verification.
- **P2:** Explanation types will shift from **(a)** in A toward **(c)/(d)** in B (template-like or evasive meta-answers).
- **P3:** Interface confidence will be weakly or negatively correlated with correctness in B for some categories (overconfidence / misplaced certainty).

## Category-level predictions (qualitative)
- **CAT1 Linguistic–formal:** small-to-moderate Δ; frequent “format-correct but principle-weak” responses in B.
- **CAT2 Empirical–propositional:** moderate Δ; reversal-direction items will show asymmetric degradation.
- **CAT3 Perceptual–corporeal:** large Δ; highest failure rate in B where embodied/metric constraints matter.
- **CAT4 Procedural–operational:** moderate Δ; degradation driven by step-tracking and intermediate-state consistency.
- **CAT5 Social–intentional:** large Δ in non-canonical belief-tracking; increased equivocation in B.
- **CAT6 Normative–evaluative:** smaller Δ in “reasonable arguments”, but increased avoidance of commitment in B (policy/stance).
- **CAT7 Metacognitive:** calibration degradation in B; confidence missingness increases when uncertainty is high.

## Model-family predictions
- Frontier closed models: higher A performance; B performance degrades but retains coherence.
- Open-weight fast inference: larger Δ and higher format missingness.
- Router/free models: highest variability across categories and runs.

## Falsification criteria (examples)
- If `Δ(A−B) ≈ 0` in CAT3 and CAT5 across families, the “referential/grounding frontier” claim is weakened.
- If confidence is well calibrated in B (ECE low) across families, the “interface epistemology” claim is weakened.
