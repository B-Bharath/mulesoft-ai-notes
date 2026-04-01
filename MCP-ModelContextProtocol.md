# 🤖 MCP – Model Context Protocol

## What is MCP?
MCP (Model Context Protocol) is an open standard developed by Anthropic that enables AI models (like Claude) to securely connect to external tools, data sources, and services. It acts as a universal interface between AI assistants and the systems they need to interact with.

---

## Why MCP Matters
- Standardizes how AI connects to tools and data
- Replaces custom one-off integrations with a unified protocol
- Enables AI agents to take real actions (read files, call APIs, query databases)
- Works across different AI models and platforms

---

## Core Concepts

### 1. MCP Server
- A lightweight service that exposes tools, resources, or prompts
- Can be local (running on your machine) or remote
- Examples: filesystem server, GitHub server, database server

### 2. MCP Client
- The AI host application (e.g., Claude Desktop, Cursor, custom app)
- Connects to one or more MCP servers
- Sends requests and receives responses

### 3. Tools
- Functions the AI can call via MCP
- Example: `read_file`, `search_web`, `query_database`
- Defined with name, description, and input schema (JSON Schema)

### 4. Resources
- Data exposed by the MCP server to provide context
- Example: file contents, database records, API responses
- Read-only by nature

### 5. Prompts
- Reusable prompt templates defined by the MCP server
- Can include dynamic arguments

---

## MCP Architecture

```
+------------------+         MCP Protocol        +------------------+
|   MCP Client     | <-------------------------> |   MCP Server     |
| (Claude Desktop, |    JSON-RPC over stdio/SSE   | (filesystem,     |
|  Cursor, etc.)   |                             |  GitHub, DB...)  |
+------------------+                             +------------------+
```

**Transport Options:**
- `stdio` – Local process communication (most common for local servers)
- `SSE (Server-Sent Events)` – HTTP-based, used for remote servers

---
### REST vs MCP

REST is like the language of the internet: it's a set of rules for how one computer asks another for a specific piece of data (like a weather report or a user profile).MCP, on the other hand, is like a universal adapter designed specifically for AI "brains."

**REST**  
REST is the standard way applications communicate over the web using HTTP endpoints and methods to request or update specific data, such as a weather report or a customer profile.

**MCP**  
MCP is a protocol designed specifically for AI assistants, acting like a universal adapter that lets them discover tools, understand their schemas, and call them in a consistent way across different systems.


## MCP in MuleSoft Context
MuleSoft can act as an **MCP Server**, exposing Anypoint Platform APIs and integrations as tools that AI agents can invoke.

### Use Cases:
- AI agent triggers a MuleSoft flow to fetch customer data
- Claude uses MCP to call a MuleSoft API for order processing
- RAG pipelines pulling data via MuleSoft connectors through MCP

### MuleSoft + MCP Integration Pattern:
```
AI Agent (Claude)
     |
   MCP Client
     |
   MCP Server (MuleSoft Anypoint)
     |
   Anypoint Connectors (Salesforce, SAP, DBs...)
```

---

## MCP vs Traditional API Integration

| Feature | Traditional API | MCP |
|---|---|---|
| Discovery | Manual docs | Auto via tool schema |
| Auth | Per-API setup | Handled by MCP server |
| AI Awareness | None | Native |
| Standardization | Varies | Unified protocol |
| Reusability | Low | High |

---

## Key MCP Servers (Community / Official)
- **Filesystem** – Read/write local files
- **GitHub** – Interact with repos, PRs, issues
- **Brave Search** – Web search
- **PostgreSQL** – Query databases
- **Slack** – Send/read messages
- **Anypoint MuleSoft** – Integration platform APIs

---

## Setting Up an MCP Server (Basic Example)

```json
// claude_desktop_config.json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/dir"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<your-token>"
      }
    }
  }
}
```

---

## MCP Tool Definition Structure

```json
{
  "name": "get_customer_data",
  "description": "Fetches customer details by customer ID from the CRM",
  "inputSchema": {
    "type": "object",
    "properties": {
      "customerId": {
        "type": "string",
        "description": "The unique customer identifier"
      }
    },
    "required": ["customerId"]
  }
}
```

---

## Benefits for AI Agents
- **Discoverability** – AI can query available tools dynamically
- **Safety** – Servers control what AI can and cannot access
- **Composability** – Chain multiple MCP servers together
- **Portability** – Same server works with any MCP-compatible AI client

---

## References
- [MCP Official Docs](https://modelcontextprotocol.io)
- [Anthropic MCP Announcement](https://www.anthropic.com/news/model-context-protocol)
- [MCP GitHub Repository](https://github.com/modelcontextprotocol)
- [MuleSoft AI Chain (MAC) Project](https://mac-project.ai)
