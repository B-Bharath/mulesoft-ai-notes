## What is GenAI & LLM integration?

- Wiring Large Language Models (LLMs) into applications so they can read, generate, or reason over text and structured data.  
- Typically involves: calling hosted LLM APIs, bringing in your own data (RAG), and letting models call tools/APIs to act on the world.  

---
## Why it matters

- Moves from static apps to **context‑aware** assistants that use real business data instead of generic training data.  
- Reuses existing systems (APIs, DBs, services) as tools the model can call, instead of rebuilding everything “inside” the LLM.  

---
## Core Integration Patterns

- **Direct LLM calls**  
  - App → LLM API (prompt, model, params) → generated answer (summarize, classify, translate, reason).  

- **RAG (Retrieval Augmented Generation)**  
  - App retrieves relevant documents/snippets from a vector store and injects them into the prompt so the LLM answers with fresh, domain‑specific context.  

- **Tool‑using agents**  
  - LLM decides when to call tools (functions/APIs) to fetch data or perform actions, then uses their results in its reasoning and responses.  

---

## RAG – Short Overview

- **Indexing (offline / batch)**  
  - Take documents → chunk into small passages → generate embeddings → store in a vector database.  

- **Querying (online)**  
  - User query → embed → similarity search (top‑k chunks) → build prompt: “context + question” → send to LLM → grounded answer.  

- Effect: higher accuracy, less hallucination, and the ability to use private, up‑to‑date data without retraining the model.  

---
## Tools & MCP‑style Integrations

- **Tools (functions/APIs)**  
  - Structured operations the LLM can call, such as `get_user_profile`, `search_tickets`, or `create_order`.  
  - The host app executes the tool and returns JSON; the model uses that result in the next reasoning step.  

- **MCP (Model Context Protocol) perspective**  
  - MCP defines a standard way for LLM *clients* to discover servers, list tools, call them, and stream results.  
  - Tools and resources are exposed via MCP servers; LLM agents can use them without custom per‑provider wiring.  

---
## Concrete examples of tools an LLM can call

- `getCustomerByEmail(email)` – look up a customer in CRM before answering.  
- `listOpenTickets(customerId)` – fetch current support issues for context.  
- `searchDocs(query)` – run a keyword or vector search in a document store (often combined with RAG).  
- `createSupportTicket(payload)` – turn a conversation into an actual ticket in the system.  
- `getExchangeRate(from, to)` – fetch real‑time FX data for calculations.  

---
## AI Gateways / LLM Proxies (high level)

- Single “front door” API that routes to multiple LLM providers and models, often via an OpenAI‑compatible interface.  
- Central place for auth, routing, quotas, logging, and policies for all GenAI traffic. 
