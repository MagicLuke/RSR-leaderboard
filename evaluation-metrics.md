# RSR Evaluation Metrics

This document defines the four WER values used in shared leaderboard reporting.
The formulas apply after the per-row text pipeline in [normalization.md](normalization.md).

## Reported WER variants

For each utterance *i*, let:
- `d_i`: edit distance between normalized reference and hypothesis,
- `L_i`: number of tokens in the normalized reference.

Per-utterance WER is `d_i / L_i` with the convention that `L_i > 0` for valid rows.

| Metric | Formula | Interpretation |
| --- | --- | --- |
| `corpus_wer` | `sum(d_i) / sum(L_i)` | Corpus-weighted WER where long utterances contribute proportionally more. |
| `corpus_wer_bounded` | `sum(min(d_i, L_i)) / sum(L_i)` | Same as corpus WER with each utterance capped at 100% error. |
| `average_wer` | `mean(d_i / L_i)` | Per-utterance WER averaged equally across utterances. |
| `average_wer_bounded` | `mean(min(1, d_i / L_i))` | Same as average WER with each utterance capped at 100% error. |

## Why bounded versions are reported

- `corpus_wer` / `average_wer` are unbounded and can be driven by extreme long-form failures.
- Bounded variants cap each utterance at 100% before aggregation.
- Leaderboard ranking uses `corpus_wer_bounded` as the primary score for comparability across teams.
