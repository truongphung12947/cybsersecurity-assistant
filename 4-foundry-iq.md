# 04. Foundry IQ

This module teaches you how to build advanced knowledge bases using Microsoft Foundry IQ and seamlessly integrate them with agents.

---

## 📋 Table of Contents

- [Foundry IQ Overview](#foundry-iq-overview)
- [Connect AI Search](#connect-ai-search)
- [Create Knowledge Base (CosmosDB)](#create-knowledge-base-cosmosdb)
- [KnowledgeAgent Integration](#knowledgeagent-integration)
- [Next Steps](#next-steps)

---

## 🎯 Learning Objectives

- Understand Foundry IQ concepts and benefits
- Connect and configure Azure AI Search resources
- Create AI Search Index-based Knowledge Base
- Create CosmosDB Knowledge Base
- Learn how to integrate Knowledge Base with agents

---

## ⏱️ Estimated Time

Approximately **15 minutes**

---

## Foundry IQ Overview

### What is Foundry IQ?

Foundry IQ is Microsoft Foundry's intelligent knowledge management system that integrates various data sources to provide contextual knowledge to AI agents.

---

### Key Features

```
Foundry IQ = Retrieval + Reasoning + Ranking
```

| Pillar | Description |
|---|---|
| **Retrieval** | Efficiently search relevant information |
| **Reasoning** | Understand and interpret retrieved information |
| **Ranking** | Prioritize the most relevant information |

---

### Traditional RAG vs Foundry IQ

| Feature | Traditional RAG (Azure AI Search) | Foundry IQ |
|---|---|---|
| **Setup Complexity** | High — manual configuration required | Low — automated setup |
| **Vector Indexing** | Manual setup | Automatically managed |
| **Chunking Strategy** | Manual implementation | Optimized defaults included |
| **Retrieval Optimization** | Manual tuning required | AI-powered automatic optimization |
| **Multi-source Integration** | Complex implementation | Seamless integration |
| **Semantic Ranking** | Separate configuration | Included by default |

---

### Supported Data Sources

| Data Source | Description |
|---|---|
| **Azure AI Search Index** | Reuse existing indexes |
| **Azure Blob Storage** | Automatic document indexing |
| **Azure Data Lake Storage Gen2** | Large-scale data processing |
| **SharePoint** | Enterprise document integration |
| **OneDrive** | Personal and business documents |

---

## Connect AI Search

First, connect an Azure AI Search resource to use Foundry IQ.

### Create Azure AI Search Resource

**1. Create Search Service**

- Navigate to the **Foundry IQ** section in the Foundry portal.

![Foundry IQ section](assets/4_1.png)

- The message **"Connect to an AI Search resource to get started"** is displayed.

![Connect to AI Search resource message](assets/4_2.png)

- Click the **Create new resource** button.

---

**2. Search Service Configuration**

Navigate to the Azure Portal's search service creation page and enter the following:

```
Resource group: foundry-workshop-lab
Service name:   foundry-search-service-001  ⚠️ Remember to change this — name must be unique
Location:       East US
Pricing tier:   Basic
```

![Search Service creation settings](assets/4_3.png)

**Pricing Tier Selection Guide:**

| Tier | Best For | Storage | Indexes |
|---|---|---|---|
| **Free** | Testing | 50 MB | 3 (1 per subscription) |
| **Basic** | Development / Small-scale | 160 GB | 15 |
| **Standard** | Production | 512 GB+ | 50 |
| **Storage Optimized** | Large-scale data | 2 TB+ | — |

![Pricing tier selection screen](assets/4_4.png)

---

**3. Compute Settings**

```
Compute type: Default
Replicas:     1  (for development)
Partitions:   1  (for development)
```

---

**4. Complete Creation**

- Click **Review + create**.
- After validation, click the **Create** button.

> ⏳ Creation takes approximately **3–5 minutes**.

---

### Connect AI Search to Foundry

**1. Return to Foundry IQ**

- Return to the **Foundry IQ** section in the Foundry portal.

---

**2. Select Search Resource**

- Click the **Select a resource** or **Connect** button.
- Select the created Search Service from the dropdown.

![Connect AI Search](assets/4_5.png)

---

**3. Complete Connection**

- Click the **Connect** button.
- Once the connection is successful, the Foundry IQ dashboard is enabled.

![AI Search connection complete](assets/4_6.png)

---

### ✅ Verification Checklist

- [ ] AI Search resource is created and in **"Running"** state
- [ ] Connection to Foundry IQ is complete

---

## Create Knowledge Base (CosmosDB)

Create a Knowledge Base by uploading data into CosmosDB and indexing it with Azure AI Search.

### Step-by-Step Guide

**1. Create CosmosDB**

- Search for **"CosmosDB"** in the Azure Portal.

![Search for CosmosDB](assets/4_7.png)

- Click the **Create** button.

![CosmosDB create screen](assets/4_8.png)

- Click **Create** under **Azure Cosmos DB for NoSQL**.

![Azure Cosmos DB for NoSQL](assets/4_9.png)

Enter the following configuration:

```
Workload Type:     Development / Testing
Resource Group:    foundry
Account Name:      cosmosdb-workshop-lab
Availability Zone: Disable
Location:          West US
Capacity mode:     Serverless
```

![CosmosDB configuration](assets/4_10.png)

- Click **Review + create**.

![Review and create](assets/4_11.png)

- Click **Create**.

> ⏳ Wait a few minutes for Azure to create the resource.

![Resource creation in progress](assets/4_12.png)

---

**2. Create Container**

- Select **Data Explorer** from the menu bar.

![Data Explorer](assets/4_13.png)

- Select **New Container**.

![New Container](assets/4_14.png)

Enter the following container details:

```
Database Id:   agent-memory
Container Id:  memories
Partition Key: KBId
```

- Click **OK**.
- Verify the container and database are created successfully.

![Container and database created](assets/4_15.png)

---

**3. Upload Knowledge Base Data**

- Select the container **memories** and choose **Items**.

![Select memories container](assets/4_16.png)

- Choose **Upload Item** in the top bar.

![Upload Item](assets/4_17.png)

- Upload the file `knowledge_base.json` and click **Upload**.

![Upload knowledge_base.json](assets/4_18.png)

---

**4. Import CosmosDB to AI Search Index**

- Navigate back to `foundry-search-service-001` that you created earlier.

![Foundry Search Service overview](assets/4_19.png)

- Select **Import Data** in the top bar.

![Import Data](assets/4_20.png)

- Select **Azure Cosmos DB** as the data source and enter the following details:

```
Subscription:      <Your subscription>
Cosmos DB Account: cosmosdb-workshop-lab
Database:          agent-memory
Collection:        memories
Query:             <leave empty>
```

![CosmosDB import configuration](assets/4_21.png)

- Click **Next** through all remaining steps, then click **Create** to create the index.

![Create index](assets/4_22.png)

> ⏳ Wait for the resource to be created. An index with a generated ID will appear. It may take some time to index the data — initially you will see **0 documents** as shown below.

![Index created with 0 documents](assets/4_23.png)

- Refresh the page to check if documents have been indexed successfully.

![Index with documents indexed](assets/4_24_1.png)

---

## KnowledgeAgent Integration

### Step-by-Step Guide

**1. Return to Foundry IQ**

- Return to **Foundry IQ** in the Foundry portal.

![Foundry IQ portal](assets/4_25.png)

---

**2. Create a Knowledge Base**

- Click the **Create a knowledge base** button.

![Create a knowledge base](assets/4_26.png)

- Select the **Azure AI Search Index** tab and click **Connect**.

![Azure AI Search Index tab](assets/4_27.png)

---

**3. Configure Knowledge Base — Source**

Enter the following details:

```
Name:              <You can leave it as the default random name>
Description:       This document contains investigation guidelines and an incident report template
Select search index: <Select the index ID created in the previous step>
```

![Knowledge base source configuration](assets/4_28.png)

---

**4. Configure Knowledge Base — Settings**

Enter the following details:

```
Name:                      <You can leave it as the default random name>
Description:               This document contains investigation guidelines and an incident report template
Chat completion model:     gpt-4.1
Retrieval reasoning effort: Minimal
Output mode:               Extractive data
```

- Click the **Save knowledge base** button.

![Save knowledge base](assets/4_29.png)

---

### ✅ Verification Checklist

- [ ] CosmosDB account and container created successfully
- [ ] `knowledge_base.json` uploaded to the **memories** container
- [ ] AI Search index created and documents indexed
- [ ] Knowledge Base connected to Foundry IQ
- [ ] Knowledge Base saved successfully

---
## Next Steps

We built a knowledge base for our agent. Let's move on to how to build an actual agent:

➡️ **[05. Agent Development](./5-agent.md)**: Create AI agents with various capabilities.

---

[← Previous: 03. Models and Deployment](./3-model.md) | [Home](./README.md) | [Next: 05. Agent Development →](./5-agent.md)