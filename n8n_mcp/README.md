# Research Agent Workflow with MCP Server in n8n

This project demonstrates how to build a research assistant in n8n using the Model Context Protocol (MCP) and a live web search tool. The workflow connects an AI agent to an MCP server that exposes a SerpAPI-powered Google search tool, allowing the agent to perform research before answering a user query.

The implementation is based on the demo titled: "Demo_02: Building a Research Agent Workflow with MCP Server in n8n".

## Overview

The project includes two complementary n8n workflows:

1. An MCP server workflow that exposes a Google search capability through SerpAPI.
2. A client workflow that connects an AI agent to that MCP server and uses the tool as part of a research workflow.

Together they show how tools can be exposed as reusable capabilities and consumed by an agent in a modular, extensible way.

## What this project demonstrates

- Building an MCP server in n8n
- Exposing an external tool through the MCP protocol
- Connecting a chat-based AI agent to MCP tools
- Using web search to ground research answers
- Combining LLM reasoning with tool execution in a workflow
- Integrating Google Gemini with a search tool and memory

## Architecture

The setup is structured as follows:

- Chat trigger starts the workflow when a user message arrives.
- Research Agent performs reasoning and chooses tools when needed.
- MCP Client connects to a remote MCP server endpoint.
- MCP Server hosts the search tool for the agent.
- SerpAPI performs live Google search requests.
- Optional memory keeps the conversation context.

This pattern allows an agent to use a dedicated research tool rather than relying only on the model's built-in knowledge.

## Project files

- `mcp_server_serpapi.json` - n8n workflow for the MCP server exposing SerpAPI search
- `mcp_client-research_agent.json` - n8n workflow for the research agent client
- `mcp_server_serpapi.jpg` - screenshot of the MCP server setup
- `research_agent_mcp_client.jpg` - screenshot of the research agent client setup
- `Demo_02_Building a_Research_Agent_Workflow_with_MCP_Server_in_n8n.pdf` - demo/reference PDF

## Workflow details

### 1) MCP Server workflow

The file `mcp_server_serpapi.json` defines a workflow with:

- `MCP Server Trigger`
- `Google search in SerpApi`

This workflow exposes a tool to the outside world through an MCP endpoint. The tool uses SerpAPI to run live Google searches and return relevant search results that can be used by the agent.

### 2) Research Agent workflow

The file `mcp_client-research_agent.json` defines a workflow with:

- `When chat message received`
- `Research Agent`
- `Google Gemini Chat Model1`
- `Simple Memory`
- `MCP Client`

The MCP Client connects to the server URL:

`https://subhroy.app.n8n.cloud/mcp/b95ec77b-7049-434f-bc12-e6d17cb8a782`

The agent is configured with a system prompt:

> You are a helpful research assistant and use the MarketIntel tool to conduct research.

This makes the agent perform structured research using MCP tools rather than answering from memory alone.

## Prerequisites

Before importing and running these workflows, make sure you have:

- An n8n instance (cloud or self-hosted)
- A valid Google Gemini API credential in n8n
- A SerpAPI account and API key
- Access to the MCP endpoint created by the server workflow

## Setup instructions

### Step 1: Import the server workflow

1. Open your n8n instance.
2. Import `mcp_server_serpapi.json`.
3. Configure the SerpAPI credentials.
4. Activate the MCP Server Trigger.
5. Copy the generated MCP endpoint URL for use in the client workflow.

### Step 2: Import the client workflow

1. Import `mcp_client-research_agent.json`.
2. Connect the `Google Gemini Chat Model1` node to your Gemini credentials.
3. Set the `MCP Client` endpoint to the MCP server URL created in Step 1.
4. Save and activate the workflow.

### Step 3: Run the research agent

1. Trigger the chat workflow with a question such as:
   - "Research the latest trends in AI agents."
   - "Find the top news on MCP and n8n."
   - "Compare the latest product updates in AI tooling."
2. The agent calls the MCP tool to search the web.
3. Results are used to produce a more grounded, research-based answer.

## Example use cases

- Market and competitor research
- Trend monitoring in AI and automation
- News-based research assistant
- Product discovery and information gathering
- Research assistance for business or academic projects

## Notes

This project is a practical example of combining agentic AI with external tools. It highlights how tools can be exposed through MCP and then reused by AI workflows in a clean, modular manner.

The workflows provide a strong foundation for extending the project with additional tools, memory, databases, or specialized business data sources.

## Related concept

This project fits within the broader area of agentic AI, where LLM-powered agents interact with tools, APIs, and external systems to perform tasks beyond static text generation.

---

For a full walkthrough, refer to the included PDF in this folder: `Demo_02_Building a_Research_Agent_Workflow_with_MCP_Server_in_n8n.pdf`.

