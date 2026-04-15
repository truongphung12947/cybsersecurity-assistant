# Microsoft Foundry Workshop

A hands-on workshop that guides you through building an AI-powered cybersecurity assistant using Microsoft Foundry, Azure AI Search, and Microsoft Sentinel.

---

## 🧭 Workshop Overview

This workshop walks you through the end-to-end process of setting up a Microsoft Foundry environment, connecting security data sources, and building an intelligent cybersecurity agent capable of triaging alerts, querying logs, and generating investigation reports.

---

## 🎯 What You Will Build

By the end of this workshop, you will have:

- A fully configured **Microsoft Foundry** environment
- An **Azure AI Search**-powered knowledge base via **Foundry IQ**
- A **Microsoft Sentinel** workspace connected as a live data source
- An intelligent **Cybersecurity Assistant Agent** capable of:
  - Querying user login activity
  - Analyzing endpoint device inventory
  - Summarizing and triaging security alerts
  - Drafting structured investigation reports

---

## 🗂️ Workshop Modules

| # | Module | Description | Est. Time |
|---|---|---|---|
| 01 | [Environment Setup](1-environment.md) | Set up Azure Resource Group, deploy Microsoft Foundry resource, and enable the Foundry portal | 10 min |
| 02 | [Microsoft Sentinel *(Optional)*](2-sentinel-optional.md) | Create a Log Analytics Workspace and enable Microsoft Sentinel for security monitoring | 5–10 min |
| 03 | [Model Deployment](3-model.md) | Deploy and configure a base language model within Microsoft Foundry | 10 min |
| 04 | [Foundry IQ](4-foundry-iq.md) | Connect Azure AI Search, create a CosmosDB knowledge base, and index data for retrieval | 15 min |
| 05 | [Agent Development](5-agent.md) | Build and test a Cybersecurity Assistant agent with MCP tool connections and Foundry IQ knowledge base | 10 min |

**Total Estimated Time: ~50–55 minutes**

---

## 🧰 Prerequisites

Before starting this workshop, ensure you have the following:

- An active **Azure subscription** with sufficient permissions to create resources
- Access to the **Azure Portal** — [portal.azure.com](https://portal.azure.com)
- Access to the **Microsoft Foundry Portal** — [ai.azure.com](https://ai.azure.com)
- Basic familiarity with Azure resource management

---

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────────┐
│                  Microsoft Foundry                   │
│                                                      │
│   ┌─────────────┐        ┌──────────────────────┐   │
│   │   Model     │        │      Foundry IQ       │   │
│   │  (GPT-5.2)  │        │  (Knowledge Base)     │   │
│   └─────────────┘        └──────────────────────┘   │
│          │                          │                │
│          └──────────┬───────────────┘                │
│                     ▼                                │
│         ┌───────────────────────┐                    │
│         │  Cybersecurity Agent  │                    │
│         └───────────────────────┘                   │
│                     │                                │
│       ┌─────────────┼─────────────┐                 │
│       ▼             ▼             ▼                  │
│  SentinelMCP    EntraMCP       MDEMCP                │
│  (Sentinel)   (Entra ID)   (Defender)                │
└─────────────────────────────────────────────────────┘
         │
         ▼
┌─────────────────┐      ┌─────────────────┐
│ Azure AI Search │      │    CosmosDB      │
│    (Indexing)   │◄─────│  (Knowledge      │
│                 │      │    Base Data)    │
└─────────────────┘      └─────────────────┘

```

---

## 📚 Additional Resources

- [Microsoft Foundry Documentation](https://learn.microsoft.com/en-us/azure/ai-foundry/what-is-azure-ai-foundry?view=foundry)
- [Azure AI Search Documentation](https://learn.microsoft.com/en-us/azure/search/search-what-is-azure-search)
- [Microsoft Sentinel Documentation](https://learn.microsoft.com/en-us/azure/sentinel/overview)
- [Azure Cosmos DB Documentation](https://learn.microsoft.com/en-us/azure/cosmos-db/introduction)
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io)

---

## 📝 License

This workshop is provided for educational purposes as part of a Microsoft Foundry hands-on lab.