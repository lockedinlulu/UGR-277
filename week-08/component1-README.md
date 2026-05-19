# Component 1: Emergency Protocol Knowledge Base

## What It Does
This component is the foundational data layer of the Emergency Response Coordinator system. It stores structured emergency response protocols in Airtable in a standardized, machine-readable format. All other components depend on this knowledge base to classify incidents, generate tasks, and visualize active emergencies.

## How It Connects to Other Components

**Inputs:** Manually curated emergency protocol documents (Fire, Medical, Lockdown procedures)

**Outputs:**
- → Component 2 (AI Core): Protocol data is loaded into the Flowise vector store for semantic search and incident classification
- → Component 3 (Task Assignment): Protocol steps are retrieved by n8n to auto-generate response tasks
- → Component 4 (Dashboard): Protocol metadata is used to label and visualize active incidents

## Airtable Schema

| Field | Type | Description |
|-------|------|-------------|
| protocol_id | Single Line | Unique identifier (e.g. FIRE_001) |
| emergency_type | Single Select | Fire / Medical / Lockdown |
| description | Long Text | Short explanation of the protocol |
| trigger_keywords | Long Text | Keywords used for AI classification |
| severity | Single Select | Low / Medium / High |
| roles_involved | Long Text | Personnel responsible for action |
| steps | Long Text | Step-by-step emergency response procedure |
| priority | Number | Response urgency ranking |
| ai_summary | Long Text | One-to-two sentence natural language summary |

## Current Protocols Loaded
| Protocol ID | Type | Severity |
|-------------|------|----------|
| FIRE_001 | Fire | High |
| FIRE_002 | Fire | Medium |
| MED_001 | Medical | High |
| MED_002 | Medical | Medium |
| LOCK_001 | Lockdown | High |

## Setup Instructions
1. Create a free Airtable account at https://airtable.com
2. Create a new base called `Emergency Response Coordinator`
3. Create a table called `Emergency_Protocols` with the fields listed in the schema above
4. Set field types exactly as specified — Single Select fields must have the correct options defined
5. Manually enter the 5 protocol records using the standardized format
6. Share the base with all team members so Components 2, 3, and 4 can access it

## How to Test It
1. Open the `Emergency_Protocols` table in Airtable
2. Verify all 5 records are present (FIRE_001, FIRE_002, MED_001, MED_002, LOCK_001)
3. Check that every record has all 9 fields filled in — no empty required fields
4. Verify that `trigger_keywords` contains relevant terms for each emergency type
5. Confirm that `steps` field contains numbered step-by-step procedures
6. Share the Airtable base URL with the Component 2 team and confirm they can read the records

## Known Limitations
- Protocols are manually curated — adding new emergency types requires manual data entry
- The in-memory vector store in Component 2 must be reloaded if protocols are updated in Airtable
- Currently supports only 3 emergency types (Fire, Medical, Lockdown) — expanding requires new protocol records and updated AI classification prompts
