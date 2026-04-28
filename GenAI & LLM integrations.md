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
