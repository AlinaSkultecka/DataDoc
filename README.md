## DataDoc – A Research Agent for Scientific Literature

This project focused on building a **real-world research agent** from scratch, step by step.  
The goal was not just to query an LLM, but to design a **transparent, controllable system** that can retrieve, filter, and synthesize information from **multiple external data sources**.

Feeling stuck during development was a natural part of the process. Even experienced developers need to rerun code, debug pipelines, and revisit concepts when working with complex agent-based systems. This project emphasized learning by **building and iterating**.

---

## Core Objective

The purpose of **DataDoc** is to generate **research-oriented answers and reports** by combining:

- Academic literature (PMC / PubMed Central)
- Vector-based semantic search (RAG)
- Web search (Google via SerpAPI)

This allows the system to use **recent, proprietary, or external data** that is not part of the LLM’s training data.

---

## Knowledge Base Construction (RAG Pipeline)

The Retrieval-Augmented Generation (RAG) system was built in several stages:

1. **Search PMC** for relevant scientific articles
2. **Download metadata and abstracts**
3. **Download full-text PDFs**
4. **Parse and split documents into smaller text chunks**
5. **Embed chunks into numeric vectors** using an embedding model
6. **Store embeddings in Pinecone**, a high-performance vector database

This enables fast and accurate semantic similarity searches over scientific texts.

---

## Tools Implemented

Several LangChain tools were created to give the agent functionality:

- **Fetch PMC Abstract Tool**  
  Retrieves full abstracts from PubMed Central using NCBI E-utilities (XML-based, robust parsing)

- **Web Search Tool (SerpAPI)**  
  Performs Google searches to retrieve up-to-date or non-academic information

- **RAG Search Tool**  
  Searches the entire Pinecone knowledge base using semantic similarity

- **RAG Search Filter Tool (PMCID)**  
  Searches *within a single scientific paper*, ensuring answers remain consistent with one source

- **Final Answer Tool**  
  Compiles results from multiple tools into a structured, readable response  
  
<img width="1042" height="466" alt="Graph" src="https://github.com/user-attachments/assets/7c849b45-db34-486d-a9dc-5ee0e9e26bc2" />

---

## Agent Architecture (LangGraph)

The agent was implemented using **LangGraph**, allowing:

- Explicit definition of **agent state**
- Clear **nodes** (tools/actions)
- **Edges and conditional edges** controlling execution flow

An **Oracle LLM** decides:
- Which tools to run
- In what order
- Under constraints (e.g. at least one tool must run, tools cannot be reused excessively)

This creates a **deterministic and debuggable agent workflow**, rather than a black-box chain.

---

## Why LangGraph?

LangGraph provides several advantages:

- Full transparency into tool usage and prompts
- Strong control over execution flow
- Easy debugging and inspection of intermediate steps
- High flexibility for customization

Compared to more opaque agent approaches, this makes DataDoc easier to understand, extend, and trust—especially for research use cases.

---

## Results and Takeaways

The research agent successfully:
- Retrieved relevant information from **PMC articles and the web**
- Filtered results at both **database level** and **paper level**
- Produced coherent, source-grounded answers with minimal tuning

The project demonstrates the **practical potential of agent-based RAG systems** for scientific research and knowledge exploration.

---

## Broader Context

While LangChain and LangGraph are leading frameworks in this space, other tools such as **Haystack** and **LlamaIndex** are also evolving rapidly and are worth exploring in future iterations.

---

## Final Note

DataDoc shows how modern AI applications go beyond simple prompt–response systems.  
By combining **retrieval, embeddings, vector databases, tools, and agent logic**, it is possible to build powerful, transparent research assistants tailored to real-world scientific workflows.
