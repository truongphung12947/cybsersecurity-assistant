# 03. Agent Development

This module teaches you how to create and deploy AI agents with diverse capabilities and functionalities.

## 📋 Table of Contents

- [Agent Overview](#agent-overview)
- [Create Cybersecurity Assistant](#create-cybersecurity-assistant)
- [Deploy and Invoke Agents](#deploy-and-invoke-agents)
- [Next Steps](#next-steps)

## 🎯 Learning Objectives

- Understand core concepts of Microsoft Foundry agents
- Create MCP Connection to external services (Microsoft Sentinel)

## ⏱️ Estimated Time

Approximately 10 minutes

---

## Agent Overview

### What is a Microsoft Foundry Agent?

A Microsoft Foundry Agent is an intelligent system that understands user requests and performs tasks using appropriate tools and knowledge.

### Key Components

```
Agent = Model + Instructions + Tools + Knowledge
```

- **Model**: Base language model (GPT-5.1, Claude, etc.)
- **Instructions**: Agent behavior guidelines and persona
- **Tools**: File Search, Web Search, Function Calling, etc.
- **Knowledge**: Connected knowledge base (Foundry IQ)

### Agent Types

| Type | Description | Use Cases |
|------|-------------|-----------|
| **Conversational** | Dialogue-oriented agent | Chatbots, customer support |
| **Task-oriented** | Task-focused agent | Data analysis, document generation |
| **Retrieval-augmented** | Search-based agent | Knowledge base QA |
| **Multi-agent** | Multi-agent collaboration | Complex workflows |

---

## Create Cybersecurity Assistant

Create an agent that assist security analyst on alert triage and reporting.

### Step-by-Step Guide

1. **Navigate to Agents Section**
   - Select **Build** from the top right menu in the Foundry portal.
   - Click the **Agents** menu.
   
   ![Build > Agents menu](assets/4_1.png)

2. **Create New Agent**
   - Click the **+ Create agent** or **New agent** button.
   
   ![Create agent button](assets/4_2.png)

   ![Create agent button](assets/4_3.png)

3. **Agent Configuration**
   ```
   Agent name: cybsersecurity-assistant
   Model: gpt-5.2
   ```

   **Instructions Configuration**:
   ```
   You are a Cybersecurity Agent tasked with coordinating the end‑to‑end investigation of security alerts using the tools and data provided to you.
   Your responsibilities include:
      - Designing an investigation plan
      - Delegating subtasks
      - Executing tool commands
      - Synthesizing findings
      - Delivering clear, actionable outcomes. 
   Follow the guidelines below to ensure a thorough, efficient, and repeatable investigation process.
   ```
   
   **Tools**:
    - Click the **Add** button to save.

    ![Create agent button](assets/4_4.png)

    - Click the **Custom** button to save.

    ![Create agent button](assets/4_5.png)

    - Click the **Model Context Protocol (MCP)** button to save.

    ![Create agent button](assets/4_6.png)

   ```
   Name: SentinelMCP
   Remote MCP Server Endpoint: https://fpt-sentinel-mcp.fastmcp.app/mcp
   Authentication: Unauthenticated (Moving to API key -> TruongPQ3)
   ```

   - Click the **Connect** button to save.

    ![Create agent button](assets/4_7.png)

    ![Create agent button](assets/4_8.png)

3. **Save Agent**
   - Click the **Save** button.

4. **Test Agent**

   **Test current information questions in Chat tab:**

   ```
   User: Who has logged in during the last 3 days?
   ```
   → Search user loggin log in Sentinel

   ```
   User: How many endpoint devices do we have in our tenant?

   ```
   → Search device information in Sentinel, require Sentinel connector from Intune and Microsoft Defender for Endpoint
   
   ![Create agent button](assets/4_9.png)
