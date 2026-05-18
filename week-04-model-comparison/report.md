# Model Comparison Report — Week 4

**Name:** Hala Elhanafy
**Date:** May 18, 2026
**Capstone Project:** Emergency Response Protocol System
**My Component:** Component 1 — Emergency Protocol Knowledge Base (Airtable)

---

## Test Setup

**Input dataset:** 5 cybersecurity text samples covering:
- 2 clearly concerning/high-severity records (unauthorized login, multiple failed SSH attempts)
- 1 ambiguous/edge case record (phishing email)
- 2 routine/benign records (firewall update, normal system utilization)

**Models tested:**
1. distilbert-base-uncased-finetuned-sst-2-english (sentiment analysis)
2. facebook/bart-large-mnli (zero-shot classification)
3. dslim/bert-large-NER (named entity recognition)
4. Groq Llama 3 8B (LLM classification)

**Evaluation criteria:** label accuracy, confidence score, speed, ease of integration in n8n

---

## Results Summary

| Record | Sentiment | Zero-Shot Label | Zero-Shot Score | NER Entities | Groq Classification |
|--------|-----------|-----------------|-----------------|--------------|---------------------|
| 1 — Unauthorized login from IP (Moscow, John Miller, 3:47 AM) | NEGATIVE (0.9961) | possible anomaly | 0.9961 | Person, Location entities | CRITICAL |
| 2 — Routine firewall rule update (fw-01, maintenance window) | NEGATIVE (0.9986) | routine activity | 0.9986 | Organization entities | LOW |
| 3 — Phishing email targeting finance @ acmecorp.com | NEGATIVE (0.9959) | possible anomaly | 0.9959 | Organization entities | CRITICAL |
| 4 — Multiple failed SSH attempts from Beijing IP (47 in 5 min) | NEGATIVE (0.9994) | possible anomaly | 0.9994 | Location entities | CRITICAL |
| 5 — System resource utilization normal, no anomalies | NEGATIVE (0.9880) | routine activity | 0.9880 | No entities | LOW / INFORMATIONAL |

---

## Analysis

**Where models agreed:**
Records 2 and 5 (the benign/routine records) were consistently classified as low-risk by both Zero-Shot and Groq. Records 1, 3, and 4 (the concerning records) were flagged as anomalies or critical by both models. There was strong agreement between Zero-Shot and Groq on severity direction across all 5 records.

**Where models disagreed:**
The Sentiment model classified every single record as NEGATIVE, including the routine firewall update (Record 2) and the normal system utilization report (Record 5). This is a clear disagreement with Zero-Shot and Groq, which correctly identified those records as low-risk. The Sentiment model failed to distinguish between threat severity and linguistic negativity.

**Most accurate model overall:**
Groq Llama 3 8B gave the most sensible and nuanced results. It correctly classified Records 2 and 5 as LOW, and Records 1, 3, and 4 as CRITICAL, with one sentence of reasoning that was contextually accurate for each record. Zero-Shot also performed well but returned only a label without explanation.

**Fastest/most practical:**
Zero-Shot (bart-large-mnli) is the most practical for scale — it is fast, free, requires no prompt engineering, and returns structured confidence scores that can be used for routing logic. Groq is slightly slower due to API latency but provides richer output.

---

## Recommended Models for My Capstone Component

**Component:** Emergency Protocol Knowledge Base (Component 1)

**Primary model:** Groq Llama 3 8B — it can generate structured, natural language summaries of emergency protocols (the `ai_summary` field in the Airtable schema) and classify incoming incidents against stored protocols with contextual reasoning.

**Secondary model:** facebook/bart-large-mnli (Zero-Shot) — useful for quickly tagging incoming emergency incidents against the `trigger_keywords` and `emergency_type` fields in the knowledge base without requiring additional training.

**Rejected models and why:**
- distilbert-sst-2 (Sentiment): This model is trained on movie reviews and social media text. It classified every security record as NEGATIVE regardless of actual threat level, making it useless for emergency classification. It has no understanding of domain-specific language.
- dslim/bert-large-NER: While NER is useful for extracting names, locations, and organizations from incident reports, it does not help with protocol classification or knowledge base population. It would only be relevant as a preprocessing step, not a primary model for this component.

---

## Failure Cases and Limitations

The most significant failure was the Sentiment model classifying Record 2 ("Routine firewall rule update completed on fw-01 during scheduled maintenance window") as NEGATIVE with 99.86% confidence. This is factually wrong — the record describes a routine, benign maintenance event. The model has no understanding of security or emergency context; it simply detects negative-sounding words like "firewall" and "update" and assigns a negative sentiment. In a production emergency response system, this model would generate constant false positives and would be completely unusable as a triage tool. This demonstrates that general-purpose NLP models trained on consumer text data cannot be applied directly to domain-specific emergency management without fine-tuning or replacement with a more appropriate model.

Additionally, the NER model returned empty entity arrays for Record 5, which is expected behavior since that record contains no proper nouns. However, this means NER is unreliable for records that describe system states rather than events involving people or places.

---

## Next Steps

With more time, I would test a fine-tuned emergency/safety classification model from Hugging Face, such as a model trained on incident reports or public safety data, to see if domain-specific training improves accuracy over the general-purpose models tested here. I would also test with a larger set of records (20+) covering edge cases like partial information, ambiguous language, and multi-type emergencies (e.g., a fire during a medical emergency). Finally, I would explore using Groq with a larger model like mixtral-8x7b to see if reasoning quality improves for complex protocol matching.

---

## Reflection

The most surprising finding was how confidently wrong the Sentiment model was. It assigned 99%+ confidence scores to every record, including clearly benign ones, as NEGATIVE. This was a good reminder that confidence score does not equal accuracy; a model can be very confident and completely wrong when applied outside its training domain. Groq's performance was the most impressive, it not only got the classifications right but provided reasoning that would actually be useful in a real emergency response context. The difference between a model that says "CRITICAL" and one that says "CRITICAL: An unauthorized login from an unknown location at 3:47 AM suggests a potential security breach" is enormous for practical use.
