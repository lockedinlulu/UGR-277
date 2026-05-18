# Week 4: Model Comparison

Tested 4 AI models on 5 cybersecurity text samples to evaluate their suitability for the Emergency Protocol Knowledge Base component of our Emergency Response Protocol System.

## Models Tested
- HF Sentiment (distilbert-sst-2)
- HF Zero-Shot (bart-large-mnli)
- HF NER (bert-large-NER)
- Groq Llama 3 8B

## Finding
Recommended Groq Llama 3 8B for the Emergency Protocol Knowledge Base component because it produced accurate, context-aware severity classifications with natural language reasoning that can directly populate the `ai_summary` field in the Airtable schema.

See `report.md` for full analysis.

## Files
- `workflow.json` — n8n workflow export
- `results/comparison-table.csv` — Exported Airtable results
- `report.md` — Full model comparison report
