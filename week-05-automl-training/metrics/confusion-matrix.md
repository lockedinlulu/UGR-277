# Confusion Matrix

| | Predicted Emergency | Predicted Routine |
|---|---|---|
| Actual Emergency | TP = 4 | FN = 1 |
| Actual Routine | FP = 0 | TN = 5 |

## Metrics

Accuracy: 90%

Precision: 100%

Recall: 80%

F1 Score: 88.9%

## Interpretation

The classifier demonstrated perfect precision, meaning every predicted emergency was truly an emergency.

Recall was slightly lower because one real emergency was classified as routine.

For security management applications, minimizing false negatives is critical because missed emergencies may delay response and increase operational risk.
