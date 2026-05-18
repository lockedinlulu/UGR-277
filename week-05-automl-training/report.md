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

---

### Analysis

**Generic model strengths:**  
Strong basic positive/negative sentiment detection.

**Generic model weaknesses:**  
Limited ability to identify operational urgency.

**Fine-tuned model advantage:**  
Better contextual understanding of emergency-related language.

**Biggest surprise:**  
Emotion-based classification was highly effective for security incident analysis.

---

## Recommended Model for My Capstone Component

**Component:** Emergency Detection

**Primary Model:** j-hartmann/emotion-english-distilroberta-base

**Confidence Threshold:** 0.85

**Priority Metric:** Recall

Recall is most important because missing emergencies creates higher operational risk than generating false alerts.

---

## Limitations & Next Steps

Future improvements would include:

- Larger training dataset
- More ambiguous edge-case examples
- Additional domain-specific fine-tuning
- Testing on live security dashboard feeds
