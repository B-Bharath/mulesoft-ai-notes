# MuleSoft AI Chain (MAC) Connector

## Overview

MuleSoft AI Chain (MAC) Connector is an AI connector for MuleSoft that enables seamless integration with AI models.

## Key Features

- **AI Model Integration**: Connect to AI models (LLMs) like OpenAI, Gemini, and more
- **Native Mule Integration**: Use AI directly inside Mule flows, just like DB or HTTP connectors
- **Platform Support**: Runs inside Anypoint Platform

## Purpose

- Make it easy to use AI in Mule applications
- Build AI agents, chatbots, and RAG (Retrieval Augmented Generation) solutions
- Easily switch AI models or vector stores without changing much code.

## Key Features

- LLM Access
  - Chat, text generation, summarization, analysis
  - Supports OpenAI, Azure OpenAI, Gemini, Anthropic, Mistral, Hugging Face, Ollama, Groq
- Embeddings & RAG
  - Create embeddings
  - Store and search vectors
- AI Tools
  - Sentiment analysis
  - Image generation & image analysis
  - Tool / function calling (AI can call APIs or services)

## Supported Operations

MAC provides ~15 operations grouped as:

- **Chat** - ask prompts and get responses
- **Agents** - AI agents that reason and act
- **Embeddings** - generate and search vectors
- **RAG** - question answering over documents
- **Image** - text-to-image and image analysis
- **Sentiment** - analyze user sentiment
- **Tools** - let AI call APIs or functions

## How MAC Fits into Mule

- Import MAC Connector from Anypoint Exchange
- Configure it as a global element
- Drag & drop MAC operations into Mule flows
- Can be used with:
  - APIs
  - Databases
  - Queues
  - Salesforce
  - External REST services
 
## Best Practices & Use Case Patterns

### Performance Tips
- Keep prompts concise and specific — shorter, well-scoped prompts reduce token usage and latency
- Use **Chat** operations for simple Q&A; reserve **Agent** operations for multi-step reasoning tasks
- For RAG, pre-process and chunk documents before ingestion to improve embedding quality and retrieval accuracy
- Use a local file-based vector store for POCs/dev; switch to an external vector store (via Vector Store Connector) for production
- Avoid re-embedding the same documents on every run — store embeddings once, query many times
- Leverage Mule's built-in error handling (`on-error-propagate`, `on-error-continue`) around MAC operations to gracefully handle LLM timeouts or API errors

### Common Use Case Patterns

#### 1. Customer Service Agent
- Automatically classify and summarize incoming support cases
- Use **Agent** + **Tools** to look up order status or account info from CRM/DB in real time
- Maintain conversation history with **Chat** operations for multi-turn support bots

#### 2. Chatbot with Context
- Use **Chat** ops with a conversation memory object to keep context across turns
- Combine with Salesforce or DB connector to personalize responses based on user data

#### 3. Document Q&A (RAG)
- Ingest PDFs, Word docs, or web content → generate embeddings → store in vector store
- Use **RAG** operations to answer questions grounded in your own documents (e.g., HR policies, product manuals)

#### 4. Autonomous Agent with Tool Calling
- Define tools (REST endpoints) in `tools.config.json` or inline `tools` array
- Agent decides at runtime which tool to call based on the user prompt (e.g., inventory lookup, HR system query)
- Useful for: IT helpdesk bots, sales assistants, operations automation

#### 5. Content Generation Pipeline
- Use **Chat** ops to generate marketing copy, email drafts, or product descriptions at scale
- Combine with Anypoint MQ or Scheduler to run batch generation jobs asynchronously

#### 6. Sentiment & Triage
- Run **Sentiment** op on inbound messages (emails, tickets, forms) to score urgency
- Route high-priority negative sentiment cases to human agents via Salesforce or ServiceNow connector
