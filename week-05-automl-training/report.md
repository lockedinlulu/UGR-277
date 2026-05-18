# Week 5 Report: AutoML Training & Fine-Tuned Model Evaluation

**Name:** Hala Elhanafy 
**Date:** May 2026  
**Capstone Project:** Emergency Security Monitoring System  
**My Component:** Image classification for emergency vs routine system events  

---

## Part A: Teachable Machine Training

### Training Setup
- Task: Emergency vs Routine security event classification
- Training images per class: 25
- Test images per class: 5 (10 total test images)
- Tool: Google Teachable Machine

---

## Test Results

| # | Actual Class | Predicted Class | Confidence | Correct? |
|---|-------------|----------------|------------|----------|
| 1 | Routine | Routine | 100% | Yes |
| 2 | Routine | Routine | 100% | Yes |
| 3 | Routine | Routine | 100% | Yes |
| 4 | Routine | Routine | 100% | Yes |
| 5 | Routine | Routine | 100% | Yes |
| 6 | Emergency | Emergency | 100% | Yes |
| 7 | Emergency | Emergency | 54% | Yes |
| 8 | Emergency | Routine | 46% | No |
| 9 | Emergency | Emergency | 100% | Yes |
| 10 | Emergency | Emergency | 82% | Yes |

---

## Confusion Matrix

| | Predicted Emergency | Predicted Routine |
|---|---|---|
| Actual Emergency | TP = 4 | FN = 1 |
| Actual Routine | FP = 0 | TN = 5 |

---

## Metrics

- Accuracy: **90%**
- Precision (Emergency): **100%**
- Recall (Emergency): **80%**
- F1 Score: **88.9%**

---

## Interpretation

The model performs very well on routine cases, correctly identifying all normal events. However, it misses some emergency cases when confidence is low, indicating that recall is weaker than precision. This means the model is conservative and prefers to avoid false alarms, but it can miss real threats.

Improving performance would require more diverse emergency training data and additional edge-case examples.

---

## Part B: Generic vs Fine-Tuned Model Comparison

### Models Tested
- Generic: distilbert-base-uncased-sst-2 (sentiment model)
- Fine-Tuned A: j-hartmann/emotion-english-distilroberta-base
- Fine-Tuned B: cardiffnlp/twitter-roberta-base-sentiment-latest

---

## Results Summary

Across test inputs, the fine-tuned models provided more meaningful classifications than the generic sentiment model. The generic model sometimes labeled security alerts as “positive” or “neutral,” showing lack of domain awareness.

The emotion-based model performed better at detecting fear and concern signals in emergency-related text.

---

## Analysis

**Generic model strengths:**
- Fast and stable
- Works well on clear positive/negative language

**Generic model weaknesses:**
- Misclassifies security alerts as positive/neutral
- No domain understanding of emergencies

**Fine-tuned model advantage:**
- Better detection of emotional tone (fear, anger, threat)
- More aligned with real-world security interpretation

**Biggest surprise:**
A fire suppression alarm event was classified as “positive,” showing that sentiment models do not understand operational risk.

---

## Recommended Model

**Component:** Emergency detection system  
**Best model:** Fine-tuned emotion model (j-hartmann/emotion-english-distilroberta-base)

**Reason:** It better captures threat-related emotional signals such as fear and urgency.

**Priority metric:** Recall — missing emergencies is more costly than false alarms.

---

## Limitations & Next Steps

- Small dataset (10 test samples) limits reliability
- More training data would improve recall
- Future improvement: train a domain-specific classifier for security alerts
