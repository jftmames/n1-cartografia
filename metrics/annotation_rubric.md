# Annotation rubric (N1)

## Fields
- `accuracy`: {0,1} or {0,0.5,1} if partial credit is enabled.
- `explanation_type`: one of {a,b,c,d}
  - (a) Correct with no principled justification (pattern/guess).
  - (b) Correct with principled justification tied to the task structure.
  - (c) Incorrect but shows partial principled reasoning / near miss.
  - (d) Evasive, non-answer, or policy/format collapse (meta-discourse without solving).

## Notes
- In CAT6 (normative), “accuracy” refers to meeting the task constraints (stance + trade-off + internal consistency), not moral truth.
- If the model violates required output format, set `format_ok=0` and annotate `explanation_type=d` unless a clear solution is present.
