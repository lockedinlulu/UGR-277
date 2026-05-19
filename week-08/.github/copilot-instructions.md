# Capstone Project Context

## Project
- **Name:** Emergency Response Coordinator
- **What it does:** A system that receives free-text emergency incident reports, classifies them using AI, matches them to the correct response protocol, generates actionable tasks for responders, and displays everything on a live dashboard. The goal is to reduce human error and delays during emergencies.
- **Project type:** Emergency Response Automation System

## Architecture
- **Ingestion (Component 1):** Airtable knowledge base storing 5 structured emergency protocols with fields like protocol_id, emergency_type, severity, steps, trigger_keywords, and ai_summary
- **AI Core (Component 2):** n8n detects new incident reports in Airtable, sends them to Flowise via HTTP request, Flowise classifies the incident using RAG + Groq, n8n writes structured results back to Airtable Incidents table
- **Specialist (Component 3):** n8n reads classified incidents, matches to protocol, retrieves steps, auto-generates tasks with role assignments and due times, tracks via Kanban board
- **Integration (Component 4):** Dashboard connecting all components, visualizing active incidents and task progress

## Tech Stack
- n8n Cloud (workflow automation)
- Flowise Cloud (LLM chains and RAG)
- Groq API (llama-3.3-70b-versatile)
- HuggingFace Inference API (sentence-transformers/distilbert-base-nli-mean-tokens)
- Airtable (shared database)
- GitHub (repo and documentation)

## Airtable Schema

### Emergency_Protocols (Component 1)
| Field | Type | Description |
|-------|------|-------------|
| protocol_id | Single Line | Unique ID e.g. FIRE_001 |
| emergency_type | Single Select | Fire / Medical / Lockdown |
| description | Long Text | Short protocol explanation |
| trigger_keywords | Long Text | Keywords for AI classification |
| severity | Single Select | Low / Medium / High |
| roles_involved | Long Text | Personnel responsible |
| steps | Long Text | Step-by-step procedure |
| priority | Number | Response urgency ranking |
| ai_summary | Long Text | Natural language summary |

### Incident_Reports (Component 2 input)
| Field | Type | Description |
|-------|------|-------------|
| incident_text | Long Text | Raw free-text incident report |
| status | Single Select | new / classified / error |

### Incidents (Component 2 output)
| Field | Type | Description |
|-------|------|-------------|
| incident_text | Long Text | Original report |
| incident_type | Single Select | Fire / Medical / Lockdown |
| protocol_id | Single Line | Matched protocol |
| severity | Single Select | High / Medium / Low |
| matched_keywords | Long Text | Keywords that triggered match |
| recommended_steps | Long Text | First 3 steps from protocol |
| confidence | Single Select | High / Medium / Low |
| status | Single Select | classified / error |
| source | Single Line | n8n |

### Protocol_Steps (Component 3)
| Field | Type | Description |
|-------|------|-------------|
| Step_Id | Single Line | Unique step ID |
| Protocol_Id | Single Line | References protocol |
| Step_Order | Number | Order of the step |
| Task_Name | Single Line | Name of the task |
| Assigned_Role | Single Line | Who does this task |
| Due_Minutes | Number | Minutes to complete |
| Priority | Single Select | High / Medium / Low |

### Tasks (Component 3 output)
| Field | Type | Description |
|-------|------|-------------|
| Task_Id | Single Line | Unique task ID |
| Incident_Id | Single Line | References incident |
| Protocol_Id | Single Line | References protocol |
| Task_name | Single Line | Task description |
| Assigned_role | Single Line | Responsible person |
| Status | Single Select | Pending / In Progress / Completed / Overdue |
| due_time | DateTime | When task must be done |
| priority | Single Select | High / Medium / Low |
| Step_Order | Number | Order of step |

## Conventions
- Field names: snake_case (except Tasks table which uses mixed)
- Status values: lowercase for incidents, Title Case for tasks
- Protocol IDs follow format: TYPE_001

## Current State
- **Working:** Component 1 fully built, Component 2 fully built and tested with 20+ incidents, Component 3 built and tested
- **In progress:** Component 4 dashboard integration
- **Next milestone:** Checkpoint 2 — one record flowing end-to-end through all 4 components
