# Redmond Sentence Recall Baseline Leaderboard

- Dataset: `MagicLuke/Redmond-Sentence-Recall`, config `sentence`, split `manifest_test.jsonl`.
- Primary metric: `corpus_wer_bounded`; lower is better.
- Public table contains aggregate metrics only; predictions and training details are not exported.
- Evaluation metrics: [evaluation-metrics.md](evaluation-metrics.md)
- Normalization details: [normalization.md](normalization.md)

## Normalization: `none` ([details](normalization.md#none))

| Rank | Model | Utterances | Corpus WER Bounded | Corpus WER | Avg WER Bounded | Avg WER | Reference Cleanup |
| ---: | --- | ---: | ---: | ---: | ---: | ---: | --- |
| 1 | microsoft/Phi-4-multimodal-instruct | 2065 | 34.71% | 35.48% | 36.14% | 37.13% | none |
| 2 | nvidia/canary-qwen-2.5b | 2065 | 38.68% | 39.26% | 40.40% | 41.23% | none |
| 3 | ibm-granite/granite-4.0-1b-speech | 2065 | 40.07% | 42.86% | 41.21% | 44.68% | none |
| 4 | Qwen/Qwen3-ASR-1.7B | 2065 | 42.20% | 42.41% | 43.95% | 44.30% | none |
| 5 | openai/whisper-large-v3 | 2065 | 44.97% | 46.66% | 46.42% | 49.13% | none |
| 6 | openai/whisper-large-v3-turbo | 2065 | 45.59% | 46.35% | 46.97% | 47.99% | none |
| 7 | nyrahealth/CrisperWhisper | 2065 | 45.76% | 46.47% | 47.51% | 48.49% | none |
| 8 | nvidia/parakeet-tdt-0.6b-v2 | 2065 | 45.99% | 46.24% | 47.78% | 48.14% | none |
| 9 | openai/whisper-medium | 2065 | 46.81% | 48.29% | 48.21% | 50.54% | none |

## Normalization: `simple` ([details](normalization.md#simple))

| Rank | Model | Utterances | Corpus WER Bounded | Corpus WER | Avg WER Bounded | Avg WER | Reference Cleanup |
| ---: | --- | ---: | ---: | ---: | ---: | ---: | --- |
| 1 | Qwen/Qwen3-ASR-1.7B | 2065 | 16.46% | 16.72% | 17.67% | 18.30% | none |
| 2 | microsoft/Phi-4-multimodal-instruct | 2065 | 19.70% | 20.64% | 21.18% | 22.65% | none |
| 3 | openai/whisper-large-v3 | 2065 | 21.43% | 23.56% | 22.61% | 27.22% | none |
| 4 | openai/whisper-large-v3-turbo | 2065 | 22.23% | 23.25% | 23.23% | 25.08% | none |
| 5 | nyrahealth/CrisperWhisper | 2065 | 22.96% | 23.84% | 24.32% | 25.82% | none |
| 6 | nvidia/canary-qwen-2.5b | 2065 | 23.85% | 24.64% | 25.42% | 26.91% | none |
| 7 | openai/whisper-medium | 2065 | 24.27% | 26.11% | 25.32% | 28.78% | none |
| 8 | nvidia/parakeet-tdt-0.6b-v2 | 2065 | 24.56% | 24.88% | 26.01% | 26.62% | none |
| 9 | ibm-granite/granite-4.0-1b-speech | 2065 | 28.35% | 31.80% | 29.42% | 34.13% | none |

## Normalization: `whisper_english` ([details](normalization.md#whisper_english))

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

## Note

All rows in each table are ranked by the same metric shown by `Primary metric` above.
Run ids and backend identifiers are excluded from this report for clarity.
