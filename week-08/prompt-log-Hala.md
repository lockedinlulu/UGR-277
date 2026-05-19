# Prompt Log

**Project:** Emergency Response Coordinator
**My Component:** Component 1 — Protocol Knowledge Base
**AI Tools Used:** Claude (claude.ai), GitHub Copilot

---

## How to Use This Log
Each entry documents a significant AI interaction — when I asked AI to generate, explain, or debug something meaningful for the project.

---

## 2026-05-18 — Capstone audit and readiness assessment for Checkpoint 2

**Context:** Working on Week 8 homework. Capstone repo open, all 4 components partially built. Checkpoint 2 is next week and requires one record flowing end-to-end through all components automatically.

**Prompt:**
> Act as a capstone project advisor. Based on my Emergency Response Coordinator project — which uses n8n, Flowise, Airtable, and Groq — review the current state of all 4 components and produce a Checkpoint 2 readiness assessment with critical gaps, schema issues, and a recommended fix order.

**Result:** AI produced a full readiness assessment marking the project as READY, identified a field naming inconsistency between Component 2 output (protocol_id) and Component 3 input (Protocol_Id), and flagged Component 4 dashboard integration as the main risk area. Recommended running a full end-to-end test before the checkpoint.

**Evaluation:** Accurate and useful. The field naming mismatch flagged by the AI is a real issue we hadn't noticed — protocol_id in the Incidents table uses lowercase while Protocol_Id in the Protocol_Steps table uses Title Case, which could cause lookup failures in n8n.

**What I changed:** Added the field naming fix to our team's pre-checkpoint task list. Will standardize to snake_case across all tables.

**What I learned:** Giving the AI detailed schema information (actual field names and types) produces much more specific and actionable feedback than describing the project at a high level. The more context you give, the more useful the output.

---

## 2026-05-18 — Generated Component 1 README using AI

**Context:** Week 8 homework required generating a capstone artifact using AI assistance. Component 1 had no formal README yet.

**Prompt:**
> Write a complete README for Component 1 (Protocol Knowledge Base) of the Emergency Response Coordinator project. Include what it does, how it connects to other components, setup instructions, how to test it, and known limitations.

**Result:** AI generated a complete, accurate README including the full Airtable schema table, setup steps, testing instructions, and a limitations section covering the manual curation requirement and vector store reload issue.

**Evaluation:** Mostly accurate. The schema table matched our actual Airtable fields. The limitations section correctly identified that the in-memory vector store needs to be reloaded when protocols are updated — something we hadn't formally documented before.

**What I changed:** Minor edits to the setup instructions to match our actual Airtable base name and sharing process.

**What I learned:** AI is most useful for generating structured documentation when you give it the actual schema and architecture details upfront. Generic prompts produce generic output — specific context produces specific, usable results.
