# Multi-Agent Systems & Graph Architectures: CrewAI and GraphRAG

This repository serves as a structured log of concepts, architectural breakdowns, and implementation strategies learned regarding CrewAI, multi-agent workflows, and GraphRAG.

---

## Executive Summary

The primary objective was to transition from basic single-agent prompts to building enterprise-ready, autonomous multi-agent systems and leveraging Knowledge Graphs for hallucination-free retrieval.

---

## 1. CrewAI Core Pillars & Concepts

CrewAI structures multi-agent applications around three fundamental abstractions:

* **Agents:** Autonomous execution units defined by specific roles, goals, and backstories (personas).
* **Tasks:** Executable instructions assigned to agents, specifying the task description and the expected output structure.
* **Crews:** The orchestration layer that bundles agents and tasks together to run execution pipelines.

### Process Execution Models
* **Sequential Process (`Process.sequential`):** Tasks execute in a linear chain where the output of Task N becomes the context for Task N+1.
* **Hierarchical Process (`Process.hierarchical`):** Introduces an automated or custom Manager Agent that delegates tasks to specialized worker agents, evaluates outputs, and triggers revisions if quality criteria are not met.

### Tool Binding & Integration
* Tools can be built-in (e.g., search tools, file readers) or custom-built using the `@tool` decorator.
* Proper type hinting and detailed docstrings are required so the LLM can dynamically decide when to invoke a tool.

---

## 2. Event-Driven Workflows with CrewAI Flows

CrewAI Flows extend basic Crews to support stateful, complex application pipelines.

* **State Management:** Uses structured models (such as Pydantic `BaseModel`) to persist data across different steps.
* **Flow Decorators:**
  * `@start()`: Marks the initiation point of the flow.
  * `@listen()`: Executes a function or micro-crew upon the completion of a targeted step.
  * `@router()`: Handles conditional branching to direct execution paths dynamically.
* **Micro-Crews:** Allows breaking monolithic agent setups into small, dedicated Crews that run only when triggered by specific events.

---

## 3. Architectural Comparison: CrewAI vs. LangGraph

Selecting between CrewAI and LangGraph depends on the required control mechanisms:

| Feature / Metric | CrewAI | LangGraph |
| :--- | :--- | :--- |
| **Abstraction Level** | High-level (fast setup and high readability) | Low-level (granular control over nodes and edges) |
| **Primary Focus** | Role-playing autonomous team delegation | State Graphs with cyclic loops and deterministic control |
| **State Retention** | Flow State & persistent Memory | Advanced Graph Checkpointing and state persistence |
| **Human-in-the-Loop** | Handled via task delegation and flows | Native execution pause, state editing, and resume |

**Decision Framework:** Use **CrewAI** for rapid development, autonomous role delegation, and collaborative agent tasks. Use **LangGraph** when explicit execution loops, exact conditional transitions, and low-level state persistence are critical requirements.

---

## 4. Knowledge Graphs and GraphRAG

### Knowledge Graphs (KG)
Unlike traditional relational databases or unstructured text files, Knowledge Graphs store data as interconnected entities and relationships using triples:
`Subject` -> `Predicate` -> `Object`

This structure allows AI systems to perform multi-hop reasoning and trace deep relationships across complex domain data.

### Standard Vector RAG vs. GraphRAG
* **Vector RAG:** Uses vector similarity to retrieve text chunks. It often misses inter-document relationships and context spanning across separate files.
* **GraphRAG:** Combines Knowledge Graph entity structures with Vector Search. It queries nodes and edges to provide structured context to the LLM, significantly reducing hallucinations and improving factual precision.

---

## 5. Learning Resources & References

* **Official Documentation:**
  * CrewAI Docs: https://docs.crewai.com
  * Microsoft GraphRAG: https://microsoft.github.io/graphrag/
* **Video Tutorials & Guides:**
  * CrewAI Deep Dive & Flows Tutorial: [Insert Link Here]
  * GraphRAG & Neo4j Integration Walkthrough: [Insert Link Here]

---

## Setup & Local Testing

To run sample implementations:

```bash
# Clone repository
git clone [https://github.com/YOUR_USERNAME/CrewAI-and-GraphRAG-Learning.git](https://github.com/YOUR_USERNAME/CrewAI-and-GraphRAG-Learning.git)

# Install dependencies
pip install crewai neo4j pydantic
