# MuleSoft AI Chain (MAC) Connector

## Overview

MuleSoft AI Chain (MAC) Connector is an AI connector for MuleSoft that enables seamless integration with AI models.

## Key Features

- **AI Model Integration**: Connect to AI models (LLMs) like OpenAI, Gemini, and more
- **Native Mule Integration**: Use AI directly inside Mule flows, just like DB or HTTP connectors
- **Platform Support**: Runs inside Anypoint Platform

## Purpose

	• Make it easy to use AI in Mule applications
	• Build AI agents, chatbots, and RAG (Retrieval Augmented Generation) solutions
  	• Easily switch AI models or vector stores without changing much code.
	
## Key Features
	• LLM Access
		○ Chat, text generation, summarization, analysis
		○ Supports OpenAI, Azure OpenAI, Gemini, Anthropic, Mistral, Hugging Face, Ollama, Groq
	• Embeddings & RAG
		○ Create embeddings
		○ Store and search vectors
	• AI Tools
		○ Sentiment analysis
		○ Image generation & image analysis
		○ Tool / function calling (AI can call APIs or services)
## Supported Operations
MAC provides ~15 operations grouped as:

- **Chat** – ask prompts and get responses
- **Agents** – AI agents that reason and act
- **Embeddings** – generate and search vectors
- **RAG** – question answering over documents
- **Image** – text-to-image and image analysis
- **Sentiment** – analyze user sentiment
- **Tools** – let AI call APIs or functions

  How MAC Fits into Mule
	• Import MAC Connector from Anypoint Exchange
	• Configure it as a global element
	• Drag & drop MAC operations into Mule flows
	• Can be used with:
		○ APIs
		○ Databases
		○ Queues
		○ Salesforce
        ○ External REST services

