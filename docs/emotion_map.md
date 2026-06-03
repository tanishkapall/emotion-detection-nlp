# 28-class → 6-class emotion mapping

Cell 9 evaluates the model against `dair-ai/emotion`, which uses 6 classes.
Since the model outputs 28 classes (go_emotions), a manual mapping is required.
This document records the mapping and the reasoning behind non-obvious choices.

The 6 target classes are: sadness, joy, love, anger, fear, surprise.

---

## Mapping table

| go_emotions label | Mapped to | Reasoning |
|---|---|---|
| sadness | sadness | direct |
| grief | sadness | grief is intense sadness |
| remorse | sadness | regret with sadness component |
| disappointment | sadness | unmet expectation, negative valence |
| disapproval | sadness | judgment with negative valence; debatable |
| joy | joy | direct |
| amusement | joy | positive, lighthearted |
| excitement | joy | high-arousal positive |
| optimism | joy | positive future-orientation |
| relief | joy | positive resolution |
| pride | joy | positive self-directed emotion |
| love | love | direct |
| caring | love | other-directed warmth |
| admiration | love | strong positive regard |
| desire | love | wanting, attachment |
| gratitude | love | appreciative positive emotion |
| anger | anger | direct |
| annoyance | anger | low-intensity anger |
| disgust | anger | negative rejection; fear also possible |
| fear | fear | direct |
| nervousness | fear | anticipatory fear |
| surprise | surprise | direct |
| realization | surprise | sudden understanding |
| confusion | surprise | cognitive disruption |
| approval | joy | positive judgment; debatable |
| curiosity | surprise | exploratory, open |
| embarrassment | sadness | social discomfort with negative valence |
| neutral | sadness | fallback — introduces noise |

---

## Notes on judgment calls

"disapproval" → sadness: could equally map to anger. Mapped to sadness
because the training data context (Reddit) tends to use disapproval in
disappointed rather than actively angry contexts.

"disgust" → anger: the dair-ai dataset does not have a disgust class.
Anger is the closest negative-action emotion.

"neutral" → sadness: this is a lossy fallback. Any neutral sentence the
model sees will pull sadness precision down. The 51% overall accuracy
reflects this noise.

"approval" → joy: positive judgment, but lower arousal than joy proper.
An argument could be made for a separate class.

---

## Effect on evaluation

The mapping compresses 28 classes into 6, which means:
- Precision suffers because multiple different go_emotions labels all
  land in the same bucket, increasing false positives within each class.
- The 51% accuracy and 0.41 macro F1 reflect mapping loss as much as
  model quality. A proper evaluation would use the GoEmotions test set
  with the original 28 labels.
