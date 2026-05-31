# RSR Text Normalization and WER Reporting

This note defines the text normalization used before computing RSR ASR scores.
It is intended for shared leaderboard reporting, so it describes evaluation
behavior without exposing model training details, checkpoint paths, or
per-utterance predictions.

## Scoring Pipeline

Each scored utterance goes through this pipeline:

1. The RSR reference transcript is cleaned with RSR-specific rules.
2. The selected text normalization is applied symmetrically to the cleaned
   reference and the model prediction.
3. Word-level edit distance is computed from the normalized text.
4. The edit distances are aggregated into the reported WER variants.

The RSR-specific cleanup is applied to references only. It removes transcript
annotation artifacts such as speaker markup, timing markers, CHAT-style bracket
codes, unintelligible-token markers, and non-lexical symbols. Model predictions
are not passed through this RSR cleanup step.

## Normalization Options

| Normalization | What It Does | Main Use |
| --- | --- | --- |
| `none` | Leaves text unchanged after RSR reference cleanup. Case, punctuation, and surface form all count. | Diagnostics when reference and prediction formats are already identical. |
| `simple` | Lowercases text, replaces punctuation and symbols with spaces, and collapses whitespace. Apostrophes are stripped, so contractions split into pieces. | Transparent internal comparison without extra dependencies. |
| `whisper_english` | Uses the Whisper English normalizer from the cached Whisper tokenizer. It lowercases, normalizes punctuation and symbols, expands common contractions, and removes some non-lexical English fillers. | Primary leaderboard normalization when comparing ASR systems. |

The same normalization must be applied to both reference and prediction. A
leaderboard table should not mix normalization settings across rows.

## none

This is the raw comparison mode after RSR reference cleanup:

- reference: cleaned only by RSR-specific cleanup.
- prediction: used as-is, after model post-processing.
- transformations: none (case/punctuation/whitespace are preserved).

Use this mode for strict diagnostics when outputs and references are already
formatted identically and you want surface-form mismatches to be counted.

## simple

`simple` applies a lightweight, deterministic normalization:

- lowercases both sides
- replaces punctuation and symbols with spaces
- collapses repeated whitespace
- strips apostrophe splits (for example, `don't` -> `don t`)

This mode is useful for transparent cross-system comparison without tokenizer
dependencies.

## whisper_english

`whisper_english` applies Whisper-style English normalization to both sides:

- lowercases
- normalizes punctuation and symbols
- expands common contractions (for example, `don't` -> `do not`)
- removes some non-lexical tokens/markers

This is the primary normalization for leaderboard ranking and external sharing.

## Examples

| Raw Text | `none` | `simple` | `whisper_english` |
| --- | --- | --- | --- |
| `The Big Cat.` | `The Big Cat.` | `the big cat` | `the big cat` |
| `She didn't go.` | `She didn't go.` | `she didn t go` | `she did not go` |
| `I've been waiting.` | `I've been waiting.` | `i ve been waiting` | `i have been waiting` |
| `That's 100% correct.` | `That's 100% correct.` | `that s 100 correct` | `that is 100% correct` |

## How Normalization Affects Scores

More normalization generally lowers absolute WER because it removes surface
mismatches that are not word-recognition errors. The effect is largest for
zero-shot systems whose output style differs from the RSR reference style.

The table below shows the effect on the same 2,053-utterance RSR test split.
The system labels are intentionally high level for external sharing.

| System | Normalization | `corpus_wer` | `corpus_wer_bounded` | `average_wer` | `average_wer_bounded` |
| --- | --- | ---: | ---: | ---: | ---: |
| Base ASR system | `none` | 0.2886 | 0.2835 | 0.3316 | 0.3145 |
| Base ASR system | `simple` | 0.1677 | 0.1631 | 0.2029 | 0.1858 |
| Base ASR system | `whisper_english` | 0.1656 | 0.1606 | 0.1975 | 0.1837 |
| Internal adapted system A | `none` | 0.1038 | 0.1021 | 0.1361 | 0.1273 |
| Internal adapted system A | `simple` | 0.0949 | 0.0934 | 0.1227 | 0.1138 |
| Internal adapted system A | `whisper_english` | 0.0944 | 0.0928 | 0.1191 | 0.1135 |
| Internal adapted system B | `none` | 0.1000 | 0.0986 | 0.1296 | 0.1223 |
| Internal adapted system B | `simple` | 0.0911 | 0.0898 | 0.1175 | 0.1102 |
| Internal adapted system B | `whisper_english` | 0.0910 | 0.0895 | 0.1148 | 0.1100 |

Key takeaways:

- `none` can inflate WER when a model omits punctuation or uses different
  capitalization from the references.
- `simple` removes most style-only mismatches and is easy to reproduce.
- `whisper_english` is slightly more forgiving than `simple` for contractions
  and selected English normalization rules.
- The relative ordering of these systems is stable across normalization
  settings, but the absolute WER values change substantially.

## Reported Metrics

For exact metric formulas, see [evaluation-metrics.md](evaluation-metrics.md).

## Reporting Rules

- Every leaderboard row should state the dataset split, utterance count,
  normalization, and the four WER metrics.
- The ranked table should use one normalization only, preferably
  `whisper_english`.
- Do not publish per-utterance references, predictions, checkpoint paths, or
  training hyperparameters in this shared leaderboard.
- If a table is intended to compare normalization choices, keep it separate
  from the ranked leaderboard.
