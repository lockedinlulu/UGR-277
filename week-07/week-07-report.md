# Week 7: RAG Security Knowledge Assistant — Evaluation Report

## 1. Setup Summary
- **LLM:** llama-3.3-70b-versatile via Groq
- **Embeddings:** sentence-transformers/all-MiniLM-L6-v2 via HuggingFace Inference API
- **Vector Store:** In-Memory Vector Store
- **Documents loaded:**
  - `input-capture-credential-access.txt` (~2 pages)
  - `brute-force-credential-access.txt` (~2 pages)
  - `mitre-credential-access.txt` (~2 pages)

## 2. Test Results

| # | Question | Used Documents? | Quality | Notes |
|---|----------|----------------|---------|-------|
| 1 | What are common techniques for credential access according to MITRE? | Yes | Good | Referenced specific MITRE technique IDs such as T1110 and described brute force and credential dumping methods |
| 2 | How does phishing relate to initial access in the ATT&CK framework? | Yes | Partial | Provided relevant context from uploaded documents but lacked deeper detail on spearphishing variants |
| 3 | What is lateral movement and what techniques do attackers use? | Yes | Good | Pulled relevant content from documents and described attacker movement across systems |
| 4 | What are some examples of brute force attacks? | Yes | Good | Directly referenced brute force techniques from the uploaded document including password spraying and credential stuffing |
| 5 | What is MITRE ATT&CK? | Yes | Good | Correctly identified it as a framework listing adversary tactics and techniques, referencing technique IDs from the documents |

## 3. Edge Case Observations
- **Unrelated question (weather):** The chatbot responded with "Hmm, I'm not sure" and did not attempt to make up an answer. This shows the RAG system is correctly limiting responses to the knowledge base.
- **Topic not in documents (latest CVEs from 2026):** The chatbot again responded with "Hmm, I'm not sure" rather than hallucinating an answer. This confirms the system is grounded in the uploaded documents only.

## 4. Settings Experiments
- No additional settings experiments were conducted beyond the default configuration. Default chunk size of 1000 and chunk overlap of 200 were used, along with a temperature of 0.3 for more factual responses.

## 5. Reflection
- **What surprised you about how RAG works?** It was surprising how the chatbot strictly limited its answers to the uploaded documents. When asked about something not in the documents, it simply said it didn't know rather than making something up. This shows how RAG grounds the LLM in real source material.
- **How could you improve this chatbot for real-world use?** Adding more documents would improve the depth and accuracy of answers. Using a persistent vector store instead of in-memory storage would also make the system more reliable and scalable. Better document formatting and chunking strategies could improve retrieval quality.
- **How might you use RAG in your capstone project?** RAG could be used to build a domain-specific knowledge assistant that answers questions based on official guidelines, procedures, or case studies relevant to the capstone topic. This would make the assistant much more accurate and trustworthy than a general-purpose LLM.
