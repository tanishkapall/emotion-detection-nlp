# Emotion Detection from Text — NLP Project

A beyond-basic emotion detection system built in Google Colab using
a pretrained HuggingFace transformer. Goes beyond a simple label predictor
to include full confidence distributions, two explainability methods,
multi-sentence emotion trend visualisation, and documented failure analysis.

---

## What this project does

| Feature | Description |
|---|---|
| 28-class emotion classification | Uses `SamLowe/roberta-base-go_emotions`, fine-tuned on Google's GoEmotions dataset |
| Full confidence distribution | Shows scores for all 28 emotions per input, not just the top prediction |
| Ambiguity detection | Flags predictions as "ambiguous" when top score < 35% instead of forcing a label |
| Language guard | Warns if input is not English before running inference |
| LIME explainability | Highlights which words pushed the model toward its prediction |
| SHAP explainability | More stable Shapley-value-based word attribution as a LIME alternative |
| Emotion trend graph | Stacked area chart of emotional landscape across a sequence of sentences |
| Failure case analysis | 6 documented edge cases where the model predictably fails and why |
| Dataset evaluation | Optional F1/accuracy evaluation against `dair-ai/emotion` test split |

---

## Tech stack

| Tool | Purpose |
|---|---|
| `transformers` | Load and run the HuggingFace model |
| `torch` | Backend for model inference |
| `lime` | LIME word-level explainability |
| `shap` | SHAP word-level explainability |
| `langdetect` | Detect non-English inputs |
| `datasets` | Load evaluation dataset (Cell 9 only) |
| `matplotlib` | All visualisations |

All tools are free and open source. No API keys or paid services required.

---

## Model

**`SamLowe/roberta-base-go_emotions`**

- Architecture: RoBERTa-base
- Fine-tuned on: [GoEmotions](https://huggingface.co/datasets/go_emotions)
  (Google dataset, ~58k Reddit comments)
- Output: 28 emotion classes
- Hosted on: HuggingFace Hub (downloaded automatically on first run)

The 28 classes are: admiration, amusement, anger, annoyance, approval,
caring, confusion, curiosity, desire, disappointment, disapproval, disgust,
embarrassment, excitement, fear, gratitude, grief, joy, love, nervousness,
optimism, pride, realization, relief, remorse, sadness, surprise, neutral.

---

## How to run

1. Open `emotion_detection.ipynb` in [Google Colab](https://colab.research.google.com/drive/1xb4fWkIUEBNunvWC4Z77-YPI6ZBGX_xa?usp=sharing)
2. Run Cell 1 to install dependencies (one-time per session)
3. Run cells in order — each cell is independent and copy-pasteable
4. Cell 9 (dataset evaluation) is optional and takes ~5 minutes on CPU

No dataset download is required for Cells 1–8. The model weights
download automatically (~500 MB) on first run of Cell 3.

---
