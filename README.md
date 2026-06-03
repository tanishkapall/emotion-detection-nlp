# Emotion Detection from Text

An NLP project that goes beyond basic sentiment analysis — predicts fine-grained emotions from text with confidence scores, word-level explainability (LIME + SHAP), and multi-sentence emotion trend visualisation.

Built in Google Colab using only free, open-source tools.

---

## Features

| Feature                         | Detail                                                                                 |
| ------------------------------- | -------------------------------------------------------------------------------------- |
| 28-class emotion classification | `SamLowe/roberta-base-go_emotions` — RoBERTa fine-tuned on Google's GoEmotions dataset |
| Full confidence distribution    | Bar chart of all 28 emotion scores per input                                           |
| Ambiguity detection             | Flags prediction as "ambiguous" if top score < 35%                                     |
| Language guard                  | Warns before inference if input is not English                                         |
| LIME explainability             | Word highlights showing contribution to prediction                                     |
| SHAP explainability             | Shapley-value-based word attribution (more stable than LIME)                           |
| Emotion trend graph             | Stacked area chart of emotion landscape across a conversation                          |
| Failure case analysis           | 6 documented edge cases with real model outputs                                        |
| Dataset evaluation              | F1 / accuracy against `dair-ai/emotion` test split (200 samples)                       |

---

## Model

### `SamLowe/roberta-base-go_emotions`

* **Architecture:** RoBERTa-base (~125M parameters)
* **Fine-tuned on:** GoEmotions (Google, ~58k Reddit comments, 28 emotion labels)
* **Hosted on:** Hugging Face Hub — downloaded automatically on first run (~500 MB)
* **Training:** No additional training or fine-tuning is performed; pretrained weights are used as-is

### Output Classes (28)

* admiration
* amusement
* anger
* annoyance
* approval
* caring
* confusion
* curiosity
* desire
* disappointment
* disapproval
* disgust
* embarrassment
* excitement
* fear
* gratitude
* grief
* joy
* love
* nervousness
* optimism
* pride
* realization
* relief
* remorse
* sadness
* surprise
* neutral

---

## Evaluation Results

**Cell 9 output (200 samples)**

Evaluated by mapping the 28 GoEmotions classes to the 6 classes used in the `dair-ai/emotion` dataset.

See `docs/emotion_map.md` for the full mapping and reasoning.

```text
              precision    recall  f1-score   support

anger             0.53      0.33      0.41        30
fear              0.75      0.21      0.33        28
joy               0.71      0.56      0.63        62
love              0.17      0.27      0.21        15
sadness           0.50      0.74      0.60        61
surprise          0.20      0.50      0.29         4

accuracy                               0.51       200
macro avg         0.48      0.44      0.41       200
weighted avg      0.57      0.51      0.51       200
```

**Overall accuracy:** 51% on 200 samples.

Note that this reflects both model quality and mapping quality. Compressing 28 emotion categories into 6 classes inevitably loses information.

See `docs/failure_analysis.md` for qualitative failure analysis.

---

## How to Run

1. Open `emotion_detection.ipynb` in Google Colab.
2. Run **Cell 1** to install dependencies (one-time per session).
3. Run notebook cells in order.
4. **Cell 9** is optional and takes approximately 5 minutes on CPU.

### Notes

* No dataset is required for Cells 1–8.
* Model weights download automatically in Cell 3.

---

## Repository Structure

```text
emotion-detection-nlp/
│
├── emotion_detection.ipynb     
├── requirements.txt
├── README.md
│
├── docs/
│   ├── failure_analysis.md      
│   └── emotion_map.md           # 28→6 class mapping with reasoning
│
└── assets/
    └── sample_outputs/
    └── failure_cases/
      
```

---

## Tech Stack

```text
transformers==4.40.0
torch==2.2.0
lime==0.2.0.1
shap==0.45.0
langdetect==1.0.9
datasets==2.19.0
matplotlib==3.8.4
numpy==1.26.4
scikit-learn==1.4.2
```

---

## References

* Demszky et al. (2020). *GoEmotions: A Dataset of Fine-Grained Emotions*. ACL 2020.
* Ribeiro et al. (2016). *"Why Should I Trust You?" Explaining the Predictions of Any Classifier (LIME)*.
* Lundberg & Lee (2017). *A Unified Approach to Interpreting Model Predictions (SHAP)*.
* Hugging Face model: `SamLowe/roberta-base-go_emotions`

---

## Author

**Tanishka Pal**
B.Tech AI/ML
Symbiosis Institute of Technology, Pune
