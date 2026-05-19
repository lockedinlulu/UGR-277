# Prompt Log — Hala Elhanafy

**Project:** Emergency Response Coordinator
**Team:** Farida S, Astra S, MD M.
**My Component:** Component 1 — Protocol Knowledge Base
**AI Tools Used:** Claude (claude.ai)

---

## How to Use This Log
Each entry documents a significant AI interaction — when I asked AI to generate, explain, or debug something meaningful for the project.

---

## 2026-05-18 — Built 3 Flowise LLM chains for incident classification

**Context:** Week 8 homework. Building 3 separate LLM chains in Flowise — a classifier, analyzer, and recommender — for emergency incident processing. Hit the free tier limit of 2 chatflows so had to fit all 3 chains on one canvas.

**Prompt:**
> I need a system prompt for a Flowise LLM chain that classifies emergency incidents as Fire, Medical, or Lockdown with a severity of HIGH, MEDIUM, or LOW and returns only a JSON object with severity, confidence, incident_type, and reasoning fields.

**Result:** AI generated a detailed system prompt with clear severity definitions, output format constraints, and a rule to return nothing outside the JSON object. The prompt worked on the first test — returned clean JSON with no extra text.

**Evaluation:** Accurate and immediately usable. The constraint "do not include any text outside the JSON object" was the key line — without it the model kept adding explanations before or after the JSON which broke parsing.

**What I changed:** Added the specific emergency types (Fire, Medical, Lockdown) to match our project's protocol IDs rather than using generic severity categories.

**What I learned:** Constraints matter as much as instructions. Telling the model what NOT to do is just as important as telling it what to do.

---

## 2026-05-18 — Connected Flowise chains to n8n via HTTP Request

**Context:** Week 8 homework. Building an n8n workflow that calls all 3 Flowise chains in sequence. Getting a "bad control character" JSON error on the second HTTP Request node.

**Prompt:**
> I'm getting a bad control character error in n8n when I put this in the JSON body field: {"question": "{{ $json.text }}"}. How do I fix this?

**Result:** AI explained that n8n's JSON body field doesn't handle template expressions well when typed manually. Suggested switching the "Specify Body" setting to "Using Fields Below" and using the expression editor (fx button) to reference $json.text as a field value instead of embedding it in raw JSON.

**Evaluation:** Fix worked immediately. The "Using Fields Below" approach is cleaner than raw JSON anyway since it validates field types properly.

**What I changed:** Applied the same fix to all 3 HTTP Request nodes instead of just the one that was erroring.

**What I learned:** n8n has two ways to specify a request body and they behave differently with dynamic expressions. Always use "Using Fields Below" when passing expressions to avoid encoding issues.

---

## 2026-05-18 — Generated capstone audit for Checkpoint 2 readiness

**Context:** Week 8 homework. Running a pre-checkpoint audit to find gaps before Checkpoint 2. Provided full project context including Airtable schema, component status, and known issues.

**Prompt:**
> Act as a capstone project advisor. Review the Emergency Response Coordinator project. Components 1-3 are built and tested. Component 4 has not been started. Identify gaps and produce a readiness assessment with a prioritized fix list.

**Result:** AI produced a structured readiness report marking the project AT RISK due to Component 4 not being built. It also flagged a field naming inconsistency between protocol_id and Protocol_Id that could break n8n lookups, and noted that the Incidents and Tasks tables didn't exist in the shared Airtable base.

**Evaluation:** The field naming issue was a real gap we hadn't noticed. The audit was more useful than a manual review because it checked every handoff point systematically.

**What I changed:** Added the field naming fix to the team task list and flagged the missing shared tables as a blocker for the Component 4 team member.

**What I learned:** Giving AI the actual field names instead of describing the schema generally produces specific, actionable feedback.

---

## 2026-05-18 — Generated Component 1 README

**Context:** Week 8 homework. Component 1 had no formal README. Used AI to generate one based on the project context file.

**Prompt:**
> Write a complete README for Component 1 (Emergency Protocol Knowledge Base). Include what it does, how it connects to other components, the full Airtable schema as a table, setup instructions, testing steps, and known limitations.

**Result:** AI generated a complete README with accurate schema table, setup steps, connection descriptions for all 4 components, and a limitations section that correctly identified the in-memory vector store reload issue.

**Evaluation:** Mostly accurate. Had to edit the setup instructions slightly to match our actual Airtable base name. The vector store limitation note was something we hadn't formally documented before.

**What I changed:** Updated the base name in setup instructions and added a note about required vs optional fields.

**What I learned:** AI documentation generation works best when you give it the actual schema — it produces a formatted table automatically which would have taken significantly longer to write manually.

---

## 2026-05-18 — Checkpoint 2 end-to-end test documentation

**Context:** Week 9 lab. Documenting the Checkpoint 2 end-to-end test results. Component 4 was not delivered by the responsible team member so the pipeline could not complete the full flow.

**Prompt:**
> Help me write a checkpoint2-results.md for a capstone project. Components 1, 2, and 3 are working. Component 4 was not built. The test record was a fire incident. Write an honest component-by-component assessment and a prioritized fix plan.

**Result:** AI generated a complete results document with PARTIAL status, detailed descriptions of what each component did, a gap list identifying the missing shared Airtable tables and the absent Component 4, and a fix plan with owners and effort estimates.

**Evaluation:** The document was accurate and honest about the project state. The gap list caught the missing Incidents and Tasks tables in the shared base as a separate issue from the Component 4 absence — two different problems that need different owners.

**What I changed:** Added specific teammate names as owners for each fix item and adjusted the effort estimates.

**What I learned:** Using AI to write failure documentation is just as valuable as using it to write success documentation. A structured gap list is more actionable than a vague note about what needs fixing.
