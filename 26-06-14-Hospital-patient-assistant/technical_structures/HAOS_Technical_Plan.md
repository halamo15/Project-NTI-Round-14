# 🏥 Healthcare Autonomous Operating System (HAOS) - Technical & Tools Specification

## 1. Executive Summary & Core Topology
HAOS operates as a stateful Multi-Agent network built on top of LangGraph. By managing asynchronous data streaming and deterministic safety thresholds, HAOS automates medical onboarding, minimizes handling latency, and preserves absolute administrative accountability via Human-in-the-Loop validation.

---

## 2. The Exact Technology Stack Grid

| Component Layer | Chosen Tool / Framework | Exact Technical Role & Responsibility |
| :--- | :--- | :--- |
| **Orchestration Core** | `LangGraph` (Python) | Manages cyclic states, node handovers, and conditional edge routing between the 4 Specialized Agents. |
| **API Gateway** | `FastAPI` + WebSockets | Asynchronously handles live text/voice traffic from WhatsApp and pushes live alarms to the ER console. |
| **Clinical Reasoning Engine** | `Claude 3.5 Sonnet` / `GPT-4o` | Extract deep medical schemas, processes vision-based medical files, and builds structured SOAP notes. |
| **Routing Classifier Engine** | `gpt-4o-mini` | Executes ultra-fast intent parsing and handles administrative RAG questions with low-token pricing. |
| **Data Knowledge Base** | `Neo4j` (GraphRAG) | Constructs the family medical genogram network to screen for inheritable risk factors. |
| **Vector Search Database** | `ChromaDB` / `Pinecone` | Hosts embedded hospital policy data and insurance parameters for semantic FAQ matching. |
| **Peripherals & Multimodal** | `OpenAI Whisper API` | Transcribes voice memos submitted by patients into clean, actionable data streams. |

---

## 3. Production Python Project Directory Tree

```text
HAOS_PROJECT/
│
├── app/
│   ├── __init__.py
│   ├── main.py                 # FastAPI Application entry point & Webhook listeners
│   │
│   ├── core/                   # System-wide architecture configurations
│   │   ├── config.py           # Environment secrets management (API Keys, DB URIs)
│   │   └── security.py         # HIPAA-compliant data masking & encryption rules
│   │
│   ├── agents/                 # The LangGraph State Machine Architecture Layer
│   │   ├── __init__.py
│   │   ├── graph.py            # Compiles nodes, conditional edges, and memory state flow
│   │   ├── state.py            # Defines the Unified State Object (TypedDict/Pydantic)
│   │   ├── router_agent.py     # Code for the Call Optimization & Routing Engine
│   │   ├── history_agent.py    # Code for the Patient History & Intake Extraction Engine
│   │   ├── emergency_agent.py  # Code for the Hard-coded Red-Flag Emergency Guardrail
│   │   └── scheduling_agent.py # Code for the Predictive Waitlist Optimization Engine
│   │
│   ├── tools/                  # Callable Functions executed autonomously by Agents
│   │   ├── __init__.py
│   │   ├── medical_ocr.py      # Vision LLM tool for handwriting & lab report processing
│   │   ├── voice_transcribe.py # Whisper wrapper for audio stream translation
│   │   ├── hospital_rag.py     # Administrative vector similarity lookup function
│   │   └── neo4j_client.py     # Cypher query builder for the Family Medical Graph
│   │
│   └── database/               # Permanent Ledger Persistence
│       ├── postgres_db.py      # PostgreSQL Connection pools for Audit Trails & User Logs
│       └── schemas.py          # Relational Data Models (SQLAlchemy definitions)
│
├── requirements.txt            # Explicit dependency pinning configurations
└── README.md                   # Implementation deployment steps and environment guide