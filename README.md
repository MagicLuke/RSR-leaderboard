# RSR ASR Leaderboard

Shared evaluation notes and leaderboard tables for ASR performance on RSR.

Use this as a cross-team view of aggregate results for `MagicLuke/Redmond-Sentence-Recall`
(`sentence` subset, `manifest_test.jsonl`).

- Primary scoring view: `whisper_english` normalization.
- Full leaderboard with all normalizations: [redmond_sentence_test_leaderboard.md](redmond_sentence_test_leaderboard.md).
- Normalization operations:
  - [`none`](normalization.md#none)
  - [`simple`](normalization.md#simple)
  - [`whisper_english`](normalization.md#whisper_english)
- Metrics and formulas: [evaluation-metrics.md](evaluation-metrics.md).

## Primary view: `whisper_english`

| Rank | Model | Utterances | Corpus WER Bounded | Corpus WER | Avg WER Bounded | Avg WER | Reference Cleanup |
| ---: | --- | ---: | ---: | ---: | ---: | ---: | --- |
| 1 | Qwen/Qwen3-ASR-1.7B (Qwen FT: segmented-latest v3 (best)) | 2065 | 8.73% | 8.82% | 10.22% | 10.33% | none |
| 2 | Qwen/Qwen3-ASR-1.7B | 2065 | 16.36% | 16.62% | 17.73% | 18.35% | none |
| 3 | microsoft/Phi-4-multimodal-instruct | 2065 | 19.53% | 20.47% | 21.14% | 22.59% | none |
| 4 | openai/whisper-large-v3 | 2065 | 21.11% | 23.27% | 22.39% | 26.97% | none |
| 5 | openai/whisper-large-v3-turbo | 2065 | 21.93% | 22.88% | 23.04% | 24.68% | none |
| 6 | nyrahealth/CrisperWhisper | 2065 | 22.60% | 23.49% | 24.07% | 25.51% | none |
| 7 | nvidia/canary-qwen-2.5b | 2065 | 23.82% | 24.62% | 25.49% | 26.93% | none |
| 8 | openai/whisper-medium | 2065 | 23.92% | 25.67% | 25.07% | 28.32% | none |
| 9 | nvidia/parakeet-tdt-0.6b-v2 | 2065 | 24.46% | 24.79% | 26.04% | 26.64% | none |
| 10 | ibm-granite/granite-4.0-1b-speech | 2065 | 28.28% | 31.79% | 29.55% | 34.34% | none |

Run ids and backend identifiers are excluded for clarity. See the detailed
leaderboard page for reused-prediction flags and all rows.
