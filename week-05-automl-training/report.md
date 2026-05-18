# Week 5 Report: AutoML Training & Fine-Tuned Model Evaluation

**Name:** Hala Elhanafy
**Capstone Project:** Security Event Classification  
**My Component:** Emergency Detection

---

## Part A: Teachable Machine Training

### Training Setup

- Task: Emergency vs Routine Security Event Classification
- Training images per class: 25
- Test images per class: 5
- Total training time: ~45 seconds

---

### Confusion Matrix

| | Predicted Emergency | Predicted Routine |
|---|---|---|
| Actual Emergency | TP = 4 | FN = 1 |
| Actual Routine | FP = 0 | TN = 5 |

---

### Calculated Metrics

- Accuracy: 90%
- Precision: 100%
- Recall: 80%
- F1 Score: 88.9%

---

### Interpretation

The model demonstrated strong classification performance.

Precision was perfect, meaning all predicted emergencies were correctly identified.

Recall was lower because one actual emergency was missed.

Since missed emergencies pose greater operational risk than false alarms, improving recall would be a priority.

More diverse emergency training images would likely improve performance.

---

## Part B: Generic vs Fine-Tuned Model Comparison

### Models Tested

1. Generic: distilbert-base-uncased-finetuned-sst-2-english
2. Fine-Tuned A: cardiffnlp/twitter-roberta-base-sentiment-latest
3. Fine-Tuned B: j-hartmann/emotion-english-distilroberta-base

### Analysis

**Generic model strengths:**  
Reliable basic sentiment classification.

**Generic model weaknesses:**  
Unable to distinguish operational urgency from ordinary negative language.

**Fine-tuned model advantage:**  
The emotion-based classifier detected fear and concern signals strongly associated with emergency scenarios.

**Biggest surprise:**  
The emotion classifier consistently identified emergency events with high confidence while maintaining neutral classifications for routine operational updates.

### Recommended Model for My Capstone Component

**Primary Model:** j-hartmann/emotion-english-distilroberta-base

**Why:**  
Its outputs align more closely with emergency escalation logic than sentiment-based models.

**Confidence Threshold:** 0.85

**Priority Metric:** Recall

Missing emergencies presents greater operational risk than false alerts.
